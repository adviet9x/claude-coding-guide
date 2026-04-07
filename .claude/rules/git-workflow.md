# Git Workflow

## Branch Strategy
```
main        — Production-ready code
develop     — Integration branch
feature/*   — New features
fix/*       — Bug fixes
hotfix/*    — Urgent production fixes
```

## Branch Naming
```
feature/topical-map-builder
feature/agent7-internal-linker
fix/login-redirect-bug
hotfix/critical-security-patch
```

## Commit Format (Conventional Commits)
```
<type>(<scope>): <short description>

feat(agents): add topical map builder agent
fix(routes): correct pagination offset calculation
test(sites): add integration tests for site CRUD
refactor(pipeline): extract config to pipeline_config.py
chore: upgrade Flask to 3.1.0
docs(api): add route documentation
```

## Commit Types
| Type | Khi dùng |
|------|---------|
| `feat` | Tính năng mới |
| `fix` | Sửa bug |
| `test` | Thêm/sửa tests |
| `refactor` | Restructure code, không thay đổi logic |
| `docs` | Chỉ thay đổi docs |
| `chore` | Build, deps, config |

## Rules
- Commit nhỏ, focused — mỗi commit là 1 thay đổi logic
- **Không** commit: `.env`, `__pycache__/`, `data/`, secrets
- Chạy `pytest` trước khi commit
- PR title theo conventional commit format
- Minimum 1 reviewer approval
