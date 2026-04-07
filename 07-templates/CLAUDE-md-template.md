# Template: CLAUDE.md

> Copy template này để tạo CLAUDE.md cho dự án mới.
> Thay `[...]` bằng thông tin thực tế.

---

## Template Cơ Bản (Dự án nhỏ)

```markdown
# CLAUDE.md — [Tên Dự Án]

## Project: [Tên] — [Mô tả 1 câu]
## Stack: [Ngôn ngữ] + [Framework] + [Database]
## Port: [port] | DB: [tên DB]

## Run
\`\`\`bash
[lệnh chạy dev]
[lệnh chạy test]
\`\`\`

## Critical Rules
1. [Quy tắc quan trọng nhất]
2. [Quy tắc thứ hai]
3. [Quy tắc thứ ba]

## Structure
\`\`\`
[project]/
├── [folder1]/    # [mô tả]
├── [folder2]/    # [mô tả]
└── [entry point] # Entry point (main.py, app.py, ...)
\`\`\`
```

---

## Template Đầy Đủ (Dự án lớn)

```markdown
# CLAUDE.md — [Tên Dự Án]

## Project Identity
- **Name**: [Tên dự án]
- **Purpose**: [Mô tả 1-2 câu]
- **Stack**: [Ngôn ngữ] + [Framework] + [Database] + [Cache]
- **Port**: [Dev port] | **DB**: [DB name]

## Critical Rules
1. **KHÔNG** sửa file [protected files]
2. **KHÔNG** thay đổi schema collection [tên]
3. **LUÔN** validate input trước khi xử lý
4. **LUÔN** chạy tests sau mỗi thay đổi
5. Mọi [entity] mới → tạo trong [folder]

## Architecture
\`\`\`
[Sơ đồ ASCII kiến trúc]
Request → Routes → Services → Database
\`\`\`

## Directory Structure
\`\`\`
[tên-project]/
├── src/              # Source code
│   ├── routes/       # API route handlers
│   ├── services/     # Business logic
│   ├── models/       # Database models
│   └── utils/        # Helpers
├── tests/            # Test files
├── docs/             # Documentation
└── [entry point]     # Main entry
\`\`\`

## How to Run
\`\`\`bash
# Development
[lệnh chạy dev]

# Tests
[lệnh chạy tests]

# Build
[lệnh build]
\`\`\`

## Key Patterns
- **Routes**: [pattern mô tả]
- **Services**: [pattern mô tả]  
- **Database**: [ORM/query pattern]
- **Error handling**: [pattern]

## Dependencies
- [dep1]: [mục đích]
- [dep2]: [mục đích]

## Environment Variables
→ xem `.env.example`

## Current Focus
- Sprint [N]: [tên sprint]
- Đang làm: [task hiện tại]
- Sắp làm: [task tiếp theo]

## Docs
- `docs/FILE_MAP.md` — Bản đồ file
- `docs/ARCHITECTURE.md` — Chi tiết kiến trúc
```

---

## Tips

- Dự án nhỏ (< 20 files) → dùng template cơ bản
- Dự án lớn (> 50 files) → dùng template đầy đủ
- **Giữ < 200 dòng** — tóm tắt, link đến docs/ nếu cần chi tiết
- Cập nhật "Current Focus" mỗi sprint
