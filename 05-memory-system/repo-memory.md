# Repo Memory — Ghi Nhớ Dự Án

> Tồn tại vĩnh viễn, áp dụng cho 1 dự án cụ thể.
> Path: `/memories/repo/`

---

## Dùng Cho

- Conventions riêng của dự án
- File map (bản đồ file quan trọng)
- Build/run/test commands
- Sprint progress
- Key decisions đã đưa ra
- Known issues / workarounds

---

## Ví Dụ Thực Tế

### `/memories/repo/project-basics.md`
```markdown
## TopicForge — Quick Facts
- Stack: Python 3.12 + Flask + MongoDB
- Port: 5050
- DB: topicforge (MongoDB)
- Test: pytest tests/ -v (152 tests)
- Entry: main.py (CLI) + admin/app.py (Web)

## Key Decisions
- agents.py → agents_legacy.py (backward compat)
- Pipeline v2: agents/agent_pipeline.py (823 lines)
- Config extracted: agents/pipeline_config.py
```

### `/memories/repo/file-map.md`
```markdown
## Core Files
| File | Lines | Purpose |
|------|-------|---------|
| main.py | 300 | CLI orchestrator |
| settings.py | 85 | Config constants |
| agents/agent_pipeline.py | 823 | Pipeline v2 |
| agents/pipeline_config.py | 110 | Pipeline constants |
| admin/app.py | 120 | Flask admin app |
| admin/routes/ | 16 files | Route handlers |

## Test Files
| File | Tests | Covers |
|------|-------|--------|
| tests/test_pipeline.py | 45 | Pipeline v2 |
| tests/test_routes.py | 60 | Admin routes |
```

### `/memories/repo/conventions.md`
```markdown
## Naming
- Routes: admin/routes/{feature}.py
- Templates: admin/templates/{feature}/*.html
- Tests: tests/test_{feature}.py

## Patterns
- Route blueprint: bp = Blueprint('{name}', __name__)
- DB access: from admin.db import get_db; db = get_db()
- Config: from settings import SETTING_NAME
```

---

## Quản Lý Repo Memory

### Khi nào tạo
- Đầu dự án mới → tạo project-basics.md
- Sau refactor lớn → cập nhật file-map.md
- Sau decision quan trọng → thêm vào decisions
- Phát hiện convention → ghi vào conventions.md

### Nguyên tắc
- Tổ chức theo topic (1 file/topic)
- Cập nhật khi codebase thay đổi lớn
- Ưu tiên facts cụ thể hơn mô tả chung
- File map giúp Claude tìm file nhanh → tiết kiệm token

### Prompt tạo repo memory
```
Phân tích dự án này và tạo repo memory:
1. project-basics.md — stack, commands, key files
2. file-map.md — bản đồ files quan trọng
3. conventions.md — patterns và naming conventions
```
