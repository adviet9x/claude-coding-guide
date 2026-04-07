# Tạo Rules — Quy Tắc Bắt Buộc

> Rules là các file `.md` trong `.claude/rules/` mà Claude **luôn tuân thủ**.
> Khác với CLAUDE.md (context), rules là **lệnh bắt buộc**.

---

## 1. Rules Là Gì?

```
.claude/rules/
├── code-style.md          # Cách format code
├── naming-conventions.md  # Đặt tên biến, file, DB
├── security.md            # Quy tắc bảo mật
├── api-conventions.md     # Thiết kế API
├── error-handling.md      # Xử lý lỗi
├── database.md            # Quy tắc database
├── testing.md             # Quy tắc test
└── git-workflow.md        # Git branching & commits
```

- Claude đọc **tất cả** rule files khi bắt đầu session
- Rules được apply **tự động** — không cần nhắc lại
- Rules **ghi đè** hành vi mặc định của Claude

---

## 2. Cách Viết Rule File

### Format chuẩn
```markdown
# [Tên Rule]

## Nguyên tắc chung
- [Bullet point ngắn gọn]
- [Bullet point ngắn gọn]

## [Category 1]
\`\`\`js
// ✅ Good
const userName = 'John';

// ❌ Bad  
const n = 'John';
\`\`\`

## [Category 2]
| Trường hợp | Quy tắc |
|------------|---------|
| Variables | camelCase |
| Classes | PascalCase |
| Constants | UPPER_SNAKE |
```

### Nguyên tắc viết
1. **Dùng ✅ / ❌** để phân biệt đúng/sai
2. **Cho code ví dụ** — Claude học từ ví dụ tốt hơn mô tả
3. **Ngắn gọn** — mỗi rule file < 200 dòng
4. **Actionable** — nói Claude phải LÀM gì, không chỉ NÊN gì

---

## 3. Các Rule File Phổ Biến

### a. code-style.md
```markdown
# Code Style

## Formatting
- Indent: 2 spaces (JS/TS) | 4 spaces (Python)  
- Max line: 100 chars
- Single quotes (JS) | Double quotes (Python f-strings)
- Trailing commas in multi-line

## Naming
| Loại | Convention | Ví dụ |
|------|-----------|-------|
| Variables / Functions | camelCase | getUserById |
| Classes | PascalCase | UserService |
| Constants | UPPER_SNAKE | MAX_RETRIES |
| Files | kebab-case | user-service.js |
| DB tables | snake_case | user_profiles |

## Imports Order
1. Built-in modules
2. External packages  
3. Internal modules
```

### b. security.md
```markdown
# Security — CRITICAL

## NEVER
- Hardcode secrets, API keys, passwords
- Commit .env files
- Log passwords, tokens, PII
- Use eval() with user input
- Concatenate SQL strings

## ALWAYS
- Use environment variables for secrets
- Validate all user input (Zod/Pydantic)
- Use parameterized queries
- Hash passwords (bcrypt, 12 rounds)
- Set rate limiting on auth endpoints
```

### c. error-handling.md
```markdown
# Error Handling

## Rules
- Never swallow errors silently
- Use custom AppError class
- Async handlers wrapped in try/catch
- Return consistent error format

## Error Response Format
\`\`\`json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human readable message"
  }
}
\`\`\`
```

### d. api-conventions.md
```markdown
# API Conventions

## URL: kebab-case, plural nouns
GET /api/v1/users
POST /api/v1/users
GET /api/v1/users/:id

## Status Codes
| Code | When |
|------|------|
| 200 | Success GET/PUT/PATCH |
| 201 | Success POST |
| 400 | Invalid input |
| 401 | Not authenticated |
| 404 | Not found |
| 500 | Server error |
```

---

## 4. Rule Cho Từng Ngôn Ngữ

### Python Projects
```markdown
# Python Rules

- Type hints cho tất cả function params và return
- Dùng f-strings, không .format() hay %
- Dùng pathlib thay os.path
- Dùng dataclass hoặc pydantic cho data models
- Dùng pytest, không unittest
- Docstring: Google style
```

### JavaScript/TypeScript Projects
```markdown
# JS/TS Rules

- TypeScript bắt buộc — không dùng plain JS
- Strict mode: true
- Async/await — không callback, không .then()
- Dùng const mặc định, let khi cần, KHÔNG var
- Arrow functions cho callbacks
- Named exports (không default export)
```

---

## 5. Rule Cho Dự Án Cụ Thể

### Dự án có legacy code
```markdown
# Legacy Rules

## Protected Files — KHÔNG ĐƯỢC SỬA
- agents_legacy.py (4000 LOC, backward compat)
- migrations/001_initial.sql

## Extension Only
- agents/__init__.py — chỉ thêm, không sửa exports cũ
- settings.py — chỉ thêm biến mới, không đổi tên cũ
```

### Dự án monorepo
```markdown
# Monorepo Rules

## Package Boundaries
- packages/api — KHÔNG import từ packages/web
- packages/shared — hàm dùng chung
- Mỗi package có package.json riêng
```

---

## 6. Kiểm Tra Rules Hoạt Động

Test bằng cách yêu cầu Claude làm gì đó vi phạm rule:

```
# Nếu có rule "KHÔNG dùng var"
Tạo 1 biến dùng var
# → Claude nên dùng const/let thay vì var
```

```
# Nếu có rule naming convention
Tạo hàm lấy user theo ID
# → Claude nên đặt tên getUserById (camelCase), không get_user_by_id
```

---

## 7. Bảo Trì Rules

| Khi nào | Hành động |
|---------|----------|
| Claude vi phạm style | Thêm/cập nhật rule tương ứng |
| Đổi convention | Cập nhật rule file |
| Rule quá dài | Tách thành 2 files |
| Rule mâu thuẫn | Review và sửa |
| Adoption mới (TypeScript, Prisma...) | Thêm rule mới |

> 💡 **Tip**: Khi Claude lặp lại 1 sai lầm > 2 lần → tạo rule cho nó.
