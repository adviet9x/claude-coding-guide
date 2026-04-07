# Quản Lý Context & Token

> Claude có giới hạn context window. Quản lý tốt = output chính xác + tiết kiệm tiền.

---

## 1. Context Window Là Gì?

```
┌──────────────────────────────────────────┐
│           Context Window (~200K tokens)  │
│                                          │
│  System Prompt     ████ (~10%)           │
│  CLAUDE.md         ██ (~5%)              │
│  Rules             ████ (~10%)           │
│  Conversation      ████████████ (~40%)   │
│  File contents     ██████████ (~30%)     │
│  Tool outputs      ██ (~5%)             │
│                                          │
│  ← Token budget = có hạn →              │
└──────────────────────────────────────────┘
```

- Mỗi từ ≈ 1.3 tokens (tiếng Anh), 2-3 tokens (tiếng Việt)
- Mỗi dòng code ≈ 10-20 tokens
- File 1000 dòng ≈ 15,000 tokens
- **Hết context → Claude quên thông tin cũ**

---

## 2. Cách Claude Đọc Dự Án

```
Bước 1: Đọc CLAUDE.md (root) → hiểu tổng quan
Bước 2: Đọc .claude/rules/*.md → nắm quy tắc
Bước 3: Đọc file user yêu cầu → hiểu code
Bước 4: Search thêm file liên quan → gathering context
Bước 5: Thực thi yêu cầu
```

### Điều Claude KHÔNG tự đọc
- ❌ Tất cả file trong dự án (quá tốn token)
- ❌ node_modules, __pycache__, build outputs
- ❌ File binary (images, PDFs)
- ❌ File > 10MB

→ **Bạn phải chỉ dẫn** Claude đọc file nào khi cần.

---

## 3. Chiến Lược Tiết Kiệm Token

### a. Giữ CLAUDE.md ngắn gọn
```markdown
# ❌ Quá dài (500+ dòng)
[Copy paste toàn bộ code mẫu, lịch sử dự án, meeting notes...]

# ✅ Ngắn gọn (100-200 dòng)
[Tóm tắt, link đến file chi tiết thay vì copy]
```

### b. Tạo FILE_MAP.md
```markdown
# File Map — thay cho scan toàn bộ dự án

| File | Lines | Purpose |
|------|-------|---------|
| main.py | 300 | CLI entry |
| settings.py | 85 | Config |
| agents/agent_pipeline.py | 823 | Pipeline v2 |
| admin/app.py | 120 | Flask app |
```
→ Claude tìm file nhanh mà không cần list_dir + read_file nhiều lần.

### c. Dùng `docs/` thay vì giải thích lại
```
# ❌ Mỗi session phải giải thích lại kiến trúc
"Dự án này có kiến trúc 3 layer, route gọi service,
service gọi repository..."

# ✅ Viết 1 lần trong docs/, Claude tự đọc
"Đọc docs/ARCHITECTURE.md để hiểu kiến trúc"
```

### d. Prompt ngắn, chính xác
```
# ❌ Prompt dài (150 tokens)
"Tôi muốn bạn giúp tôi tạo một API endpoint mới 
cho việc lấy danh sách users, endpoint này cần có 
phân trang, tôi muốn dùng query parameters page 
và limit, và response format phải theo chuẩn..."

# ✅ Prompt ngắn (40 tokens)
"Tạo GET /api/users với phân trang (?page, ?limit).
Response format theo api-conventions.md"
```

### e. Yêu cầu output ngắn
```
Trả lời ngắn gọn, chỉ code
Không giải thích, chỉ sửa
Tóm tắt 3 dòng
```

---

## 4. Khi Context Bị Hết

### Dấu hiệu
- Claude quên thay đổi đã làm trước đó
- Claude hỏi lại thứ đã nói
- Output bắt đầu lặp lại hoặc sai

### Giải pháp

#### a. Bắt đầu conversation mới
```
# Đầu conversation mới, cho context nhanh:
Đọc CLAUDE.md và docs/FILE_MAP.md.
Tôi đang làm tiếp [mô tả task].
File liên quan: [liệt kê file].
```

#### b. Dùng Memory System
```
# Lưu progress trước khi hết context
Lưu tiến trình hiện tại vào session memory:
- Đã xong: [danh sách]
- Đang làm: [task]
- Còn lại: [danh sách]
```

#### c. Chia nhỏ task
```
# Thay vì 1 task lớn
"Refactor toàn bộ codebase"

# Chia thành nhiều conversation
Session 1: "Refactor module A"
Session 2: "Refactor module B"  
Session 3: "Integration test"
```

---

## 5. Files Nào Tốn Nhiều Token?

| File type | Token/dòng | Ví dụ |
|-----------|-----------|-------|
| Code (Python/JS) | ~15 | 1000 dòng ≈ 15K tokens |
| Markdown | ~8 | 1000 dòng ≈ 8K tokens |
| JSON/YAML | ~12 | Configs, schemas |
| HTML | ~20 | Templates phức tạp |
| Logs/Output | ~10 | Terminal output |

### Ước tính token
```
Quy tắc nhanh:
- 1 file nhỏ (< 100 dòng): ~1.5K tokens
- 1 file trung bình (100-500 dòng): ~5K tokens  
- 1 file lớn (500-1000 dòng): ~12K tokens
- Mỗi message user: ~50-200 tokens
- Mỗi message Claude: ~200-2000 tokens
```

---

## 6. Tối Ưu Cho Dự Án Lớn

### Dự án < 20 files
→ Claude scan tất cả được. Không cần tối ưu nhiều.

### Dự án 20-100 files
→ Cần FILE_MAP.md + CLAUDE.md tốt.

### Dự án > 100 files
→ Cần:
- FILE_MAP.md chi tiết
- CLAUDE.md ngắn gọn
- Repo memory cho conventions
- Chia task theo module
- Dùng sub-agents cho từng domain

### Template cho dự án lớn
```markdown
# CLAUDE.md — Large Project

## Quick Reference
- Entry: src/index.ts
- Config: src/config/
- API: src/api/ (42 endpoints)
- DB: PostgreSQL + Prisma (28 models)
- Tests: tests/ (340 tests)

## File Map → docs/FILE_MAP.md
## Architecture → docs/ARCHITECTURE.md
## API Docs → /api-docs (Swagger)

## Current Sprint: Sprint 5 — Payment Integration
```
