# Viết CLAUDE.md Hiệu Quả

> CLAUDE.md là file **quan trọng nhất** — Claude đọc đầu tiên để hiểu dự án.
> File này quyết định 80% chất lượng output của Claude.

---

## 1. CLAUDE.md Ở Đâu?

```
project-root/
├── CLAUDE.md              ← Root level (bắt buộc)
├── .claude/
│   ├── CLAUDE.md          ← Scope .claude/ (tùy chọn)
│   └── CLAUDE.local.md    ← Local overrides (gitignore)
├── src/
│   └── CLAUDE.md          ← Scope src/ (tùy chọn)
└── tests/
    └── CLAUDE.md          ← Scope tests/ (tùy chọn)
```

### Thứ tự ưu tiên
1. Claude đọc `CLAUDE.md` ở root **trước**
2. Khi làm việc trong folder con → đọc thêm `CLAUDE.md` của folder đó
3. `CLAUDE.local.md` cho cấu hình cá nhân (gitignore)

---

## 2. Cấu Trúc CLAUDE.md Chuẩn

```markdown
# CLAUDE.md — [Tên Dự Án]

## Project Identity
- **Name**: Tên dự án
- **Stack**: Ngôn ngữ + Framework + DB
- **Purpose**: 1-2 câu mô tả mục đích

## Critical Rules
1. KHÔNG [hành động cấm 1]
2. KHÔNG [hành động cấm 2]
3. LUÔN [hành động bắt buộc]

## Architecture
[Sơ đồ ASCII kiến trúc]

## Directory Structure
[Cây thư mục chính — KHÔNG liệt kê quá chi tiết]

## How to Run
[Lệnh cụ thể]

## How to Test
[Lệnh cụ thể]

## Key Patterns
[Các pattern quan trọng trong codebase]

## Current Sprint / Focus
[Đang làm gì — giúp Claude ưu tiên đúng]
```

---

## 3. Nguyên Tắc Viết

### ✅ Nên

| Nguyên tắc | Ví dụ |
|-----------|-------|
| Ngắn gọn, súc tích | "Stack: Python 3.12 + Flask + MongoDB" |
| Dùng bullet points | Không viết đoạn văn dài |
| Nêu rõ ràng buộc | "KHÔNG sửa agents_legacy.py" |
| Cho ví dụ code | Cho 1 đoạn code mẫu pattern |
| Cập nhật thường xuyên | Sau mỗi sprint, cập nhật |

### ❌ Không nên

| Anti-pattern | Tại sao |
|-------------|---------|
| Viết quá dài (>500 dòng) | Claude phải đọc hết → tốn token |
| Copy paste toàn bộ code | Dùng link đến file thay vì copy |
| Mô tả chung chung | "Code phải tốt" → vô nghĩa |
| Không cập nhật | Thông tin cũ → Claude làm sai |
| Lặp lại rules | Rules đã có trong `.claude/rules/` |

---

## 4. Sections Quan Trọng Nhất

### Critical Rules (BẮT BUỘC)
```markdown
## Critical Rules
1. **KHÔNG sửa** `legacy_module.py` — backward compat
2. **KHÔNG thay đổi** schema của collection `users` 
3. **Mọi API endpoint** phải có validation (Zod/Pydantic)
4. **Mọi database call** phải trong try/catch
5. **Port**: 5050 (dev), 8080 (prod)
```

> ⚡ Dùng **in đậm** và **CAPS** cho từ khóa quan trọng — Claude nhận ra ngay.

### Architecture (KHUYÊN DÙNG)
```markdown
## Architecture
\`\`\`
Request → Routes → Controllers → Services → Repositories → DB
\`\`\`

- **Routes**: URL mapping, không logic
- **Services**: Business logic
- **Repositories**: Database queries
```

### Current Focus (CẬP NHẬT THƯỜNG XUYÊN)
```markdown
## Current Focus
- Sprint 3: Agent 6 multi-site publisher
- Đang fix: Pipeline timeout cho bài dài
- Sắp làm: Agent 7 internal linker
```

---

## 5. Ví Dụ Thực Tế

### Dự án nhỏ (< 20 files)
```markdown
# CLAUDE.md — My Todo API

## Stack: Node.js 20 + Express + PostgreSQL + Prisma
## Port: 3000
## DB: PostgreSQL (prisma migrate dev)

## Rules
- TypeScript only
- Async/await, no callbacks
- Zod validation on all inputs

## Run: npm run dev
## Test: npm test
```

### Dự án lớn (> 50 files)
→ Xem [CLAUDE.md Template](../07-templates/CLAUDE-md-template.md)

---

## 6. CLAUDE.md Trong Subfolder

```markdown
# CLAUDE.md — tests/

## Test Conventions
- File pattern: `test_*.py`
- Framework: pytest
- Fixtures: conftest.py
- KHÔNG mock database — dùng test DB

## Run
pytest tests/ -v
pytest tests/unit/ -v --tb=short
```

Đặt `CLAUDE.md` trong subfolder khi:
- Folder đó có quy tắc riêng
- Claude thường xuyên làm việc trong folder đó
- Muốn cung cấp context cụ thể cho folder

---

## 7. Bảo Trì CLAUDE.md

| Khi nào cập nhật | Cập nhật gì |
|------------------|-------------|
| Thêm dependency mới | Stack section |
| Đổi kiến trúc | Architecture section |
| Sprint mới | Current Focus section |
| Thêm quy tắc | Critical Rules section |
| Refactor lớn | Directory Structure |

### Lệnh nhờ Claude cập nhật
```
Cập nhật CLAUDE.md - thêm section về [tính năng mới].
Giữ ngắn gọn, format giống hiện tại.
```
