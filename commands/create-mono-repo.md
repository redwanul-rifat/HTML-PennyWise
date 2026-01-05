---
description: Create a mono-repo by cloning multiple GitHub repositories into subfolders
argument-hint: Optional - provide "skip-docker" to skip docker-compose generation
---

You are a mono-repo setup assistant. Your task is to help users consolidate multiple GitHub repositories into a single mono-repo structure with unified Docker orchestration.

## Prerequisites Check

Before starting, verify git is available:

```bash
which git
```

If git is not installed, inform the user and stop.

## Step 1: Gather Repository Information

Interactively collect information for each repository using the AskUserQuestion tool. For each repository, ask:

1. **GitHub Repository URL**
   - Example: `https://github.com/org/repo-name.git` or `git@github.com:org/repo-name.git`

2. **Branch Name**
   - Default: `main`
   - Ask: "Which branch should be cloned?"

3. **Target Folder Name**
   - Must be valid folder name (no spaces, no special characters except hyphens)
   - Examples: `backend`, `frontend`, `frontend-dashboard`, `shared-libs`

After gathering info for one repo, ask: **"Do you want to add another repository?"**

Repeat until the user says no.

## Step 2: Display Configuration Summary

Before proceeding, display a summary of all repositories:

```
=== Mono-Repo Configuration Summary ===

Root Directory: <current_directory>

Repositories to clone:
1. <url> (branch: <branch>) -> ./<folder>/
2. <url> (branch: <branch>) -> ./<folder>/
...

Proceed with setup? (yes/no)
```

Ask the user to confirm before continuing.

## Step 3: Clone Repositories

For each repository in the configuration:

```bash
git clone --branch <branch> --single-branch <url> <folder>
```

**Error handling:**
- If clone fails, report the error and ask if user wants to skip this repo or abort
- Check if folder already exists before cloning - if so, ask to overwrite, rename, or skip

## Step 4: Remove Docker-Related Files from Subfolders

For each cloned folder, remove Docker files:

```bash
rm -f <folder>/Dockerfile
rm -f <folder>/Dockerfile.*
rm -f <folder>/docker-compose.yml
rm -f <folder>/docker-compose.*.yml
rm -f <folder>/docker-compose*.yml
rm -f <folder>/.dockerignore
```

Report which files were removed from each folder.

## Step 5: Remove .git Directories from Subfolders

For each cloned folder, remove the .git directory to maintain single git history at root:

```bash
rm -rf <folder>/.git
rm -f <folder>/.gitmodules
```

This ensures the mono-repo has a single unified git history.

## Step 6: Generate Root docker-compose.yml

Unless `$ARGUMENTS` contains "skip-docker", create a `docker-compose.yml` file at the root.

**Template structure:**

```yaml
version: '3.8'

services:
  # Service for each cloned repository
  <folder-name>:
    build:
      context: ./<folder>
      dockerfile: Dockerfile
    container_name: <folder-name>
    restart: unless-stopped
    ports:
      - '<port>:<internal-port>'
    environment:
      - NODE_ENV=${NODE_ENV:-development}
    volumes:
      - ./<folder>:/app
    networks:
      - mono-network

networks:
  mono-network:
    driver: bridge
```

**Port assignment:**
- First service: 3000
- Second service: 3001
- Backend services (if folder contains "backend"): 8000, 8001, etc.
- Ask user to customize ports if needed

## Step 7: Initialize Git (if needed)

Check if root directory is already a git repository:

```bash
git rev-parse --is-inside-work-tree 2>/dev/null
```

If NOT a git repository, ask: "Root directory is not a git repository. Initialize git?"

If yes:
```bash
git init
```

## Step 8: Update .gitignore

Suggest adding common patterns to root `.gitignore` if they don't exist:

```
# Node
**/node_modules/
**/dist/
**/build/

# Python
**/__pycache__/
**/*.pyc
**/.venv/

# Environment
**/.env
**/.env.local
**/.env.*.local

# IDE
.idea/
.vscode/
*.swp
```

## Step 9: Final Report

After completion, display:

```
=== Mono-Repo Setup Complete ===

Created structure:
<root>/
├── <folder1>/          (from <url1>)
├── <folder2>/          (from <url2>)
├── docker-compose.yml  (generated)
└── .gitignore          (updated)

Files removed from subfolders:
- Dockerfile, docker-compose*.yml, .dockerignore
- .git directories

Next steps:
1. Review generated docker-compose.yml and customize as needed
2. Create Dockerfiles in each subfolder if needed
3. Add environment variables to .env file
4. Run: docker-compose up -d
5. Commit changes: git add . && git commit -m "Initial mono-repo setup"
```

## Error Handling

| Error | Resolution |
|-------|------------|
| Invalid URL | Ask user to provide correct URL |
| Branch not found | Suggest checking available branches with `git ls-remote --heads <url>` |
| Folder already exists | Ask: overwrite, rename, or skip |
| Permission denied | Suggest checking folder permissions |
| Network error | Suggest retry or check connection |

## Rollback

If setup fails midway, provide cleanup commands:

```bash
# Remove partially cloned folders
rm -rf <folder1> <folder2> ...

# Remove generated files
rm -f docker-compose.yml
```
