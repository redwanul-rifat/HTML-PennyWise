# Fullstack Pipeline Status - {PROJECT_NAME}

## Progress

| Phase | Skill | Tier | Status | Prerequisites | Output | Notes |
|-------|-------|------|--------|---------------|--------|-------|
| init | project-init.md | base | :clipboard: | - | - | - |
| prd | convert-prd-to-knowledge.md | nestjs | :clipboard: | init | - | - |
| database | database-schema-designer.md | nestjs | :clipboard: | prd | - | - |
| backend | (composite) | nestjs | :clipboard: | database | - | - |
| frontend | convert-figma-to-react.md | react | :clipboard: | prd | - | - |
| integrate | api-integration.md | react | :clipboard: | backend, frontend | - | - |
| test | e2e-test-generator.md | stack | :clipboard: | integrate | - | - |
| qa | design-qa-patterns.md | react | :clipboard: | test | - | - |
| ship | deployment.md | base | :clipboard: | qa | - | - |

## Skill Paths by Tier

| Tier | Base Path | Description |
|------|-----------|-------------|
| base | `.claude/base/skills/fullstack/` | Generic orchestration (init, ship) |
| nestjs | `.claude/nestjs/skills/` | Backend skills (prd, database, backend) |
| react | `.claude/react/skills/` + `guides/` | Frontend skills (frontend, integrate, qa) |
| stack | `.claude/{detected}/skills/` | Auto-detected framework |

## Execution Log

| Date | Phase | Duration | Result | Notes |
|------|-------|----------|--------|-------|

## Configuration

```yaml
project: {PROJECT_NAME}
created: {DATE}
last_run: null
tech_stack: nestjs+react  # Auto-detected or user-specified
```
