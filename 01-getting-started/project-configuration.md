# Cấu Hình Dự Án Cho Claude

> Hướng dẫn tạo cấu trúc `.claude/` và `CLAUDE.md` để Claude hiểu dự án nhanh nhất.

---

## 1. Tạo CLAUDE.md (Root)

File quan trọng nhất — Claude đọc **đầu tiên** khi mở dự án.

```bash
# Tạo ở root dự án
touch CLAUDE.md
```

### Nội dung tối thiểu

```markdown
# CLAUDE.md — [Tên Dự Án]

## Project Overview
- **Tên**: [Tên dự án]
- **Stack**: [Python/Node.js/...] + [Framework] + [Database]
- **Mục đích**: [1-2 câu mô tả]

## Critical Rules
1. [Quy tắc quan trọng nhất]
2. [Quy tắc thứ hai]

## Directory Structure
[Cây thư mục chính]

## How to Run
[Lệnh chạy dự án]

## How to Test
[Lệnh chạy test]
```

> 💡 Chi tiết hơn → xem [CLAUDE.md Template](../07-templates/CLAUDE-md-template.md)

---

## 2. Tạo Folder `.claude/`

```bash
mkdir -p .claude/rules .claude/skills .claude/agents .claude/commands
```

### Cấu trúc đầy đủ
```
.claude/
├── CLAUDE.md              # Instructions cho scope này
├── settings.json          # Cấu hình Claude
├── settings.local.json    # Cấu hình local (gitignore)
├── rules/                 # Quy tắc bắt buộc
│   ├── code-style.md      # Style guide
│   ├── naming.md          # Quy tắc đặt tên
│   ├── security.md        # Bảo mật
│   └── ...
├── skills/                # Kỹ năng chuyên biệt
│   └── deploy/
│       └── SKILL.md
├── agents/                # Sub-agents
│   ├── frontend.md
│   ├── backend.md
│   └── ...
└── commands/              # Lệnh tái sử dụng
    ├── deploy.md
    └── fix-issue.md
```

---

## 3. Tạo settings.json

```json
// .claude/settings.json
{
  "model": "claude-sonnet-4",
  "maxTokens": 8192,
  "temperature": 0,
  "rules": [
    "rules/*.md"
  ],
  "skills": [
    "skills/*/SKILL.md"
  ]
}
```

---

## 4. Tạo Rules Cơ Bản

Mỗi dự án nên có ít nhất 3 rule files:

### a. Code Style
```bash
# .claude/rules/code-style.md
```
```markdown
# Code Style

- Indent: 2 spaces (JS/TS) hoặc 4 spaces (Python)
- Max line length: 100 chars
- Naming: camelCase (JS), snake_case (Python)
- Luôn dùng async/await
```

### b. Project Rules
```markdown
# Project Rules

- KHÔNG sửa file legacy: [tên file]
- KHÔNG thay đổi database schema trực tiếp
- Mọi thay đổi phải có test
- Dùng [ORM name] cho database queries
```

### c. Security
```markdown
# Security

- KHÔNG hardcode secrets
- KHÔNG log passwords hoặc tokens
- Validate tất cả user input
- Dùng parameterized queries
```

---

## 5. File .gitignore Cho Claude

Thêm vào `.gitignore`:
```gitignore
# Claude local files
.claude/settings.local.json
.claude/CLAUDE.local.md
```

**KHÔNG gitignore** các file sau (cần share với team):
- `.claude/rules/*`
- `.claude/skills/*`
- `.claude/agents/*`
- `.claude/commands/*`
- `.claude/CLAUDE.md`
- `.claude/settings.json`
- `CLAUDE.md` (root)

---

## 6. Tạo docs/ Cho AI

```bash
mkdir -p docs
```

### docs/PROJECT.md
```markdown
# [Tên dự án] — AI Context

## Tech Stack
| Layer | Technology |
|-------|-----------|
| Language | Python 3.12 |
| Framework | Flask |
| Database | MongoDB |

## Entry Points
- `main.py` — CLI entry
- `admin/app.py` — Web admin

## Key Patterns
- Service layer: `services/`
- Route handlers: `admin/routes/`
```

### docs/FILE_MAP.md
```markdown
# File Map

## Core Files
| File | Lines | Purpose |
|------|-------|---------|
| main.py | 300 | CLI orchestrator |
| settings.py | 85 | Configuration |
| agents/agent_pipeline.py | 823 | Pipeline v2 |
```

> 💡 FILE_MAP giúp Claude tìm file nhanh mà không scan toàn bộ dự án → tiết kiệm token.

---

## 7. Checklist Hoàn Thành

- [ ] `CLAUDE.md` ở root — mô tả dự án
- [ ] `.claude/rules/` — ít nhất 3 rules
- [ ] `.claude/settings.json` — cấu hình cơ bản
- [ ] `docs/PROJECT.md` — context cho AI
- [ ] `docs/FILE_MAP.md` — bản đồ file
- [ ] `.gitignore` — đã thêm local files
- [ ] Test: Claude có thể hiểu và thao tác dự án
