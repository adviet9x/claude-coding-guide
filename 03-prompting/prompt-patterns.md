# Các Pattern Prompt Phổ Biến

> Tập hợp các prompt pattern đã kiểm chứng, copy-paste và dùng ngay.

---

## 1. Exploration Patterns

### Hiểu dự án mới
```
Scan dự án này và trả lời:
1. Tech stack (ngôn ngữ, framework, DB)
2. Entry points
3. Cấu trúc thư mục chính
4. Cách chạy (dev, test, build)
Tóm tắt trong 20 dòng.
```

### Hiểu 1 file
```
Đọc file [path] và giải thích:
- File này làm gì?
- Các hàm public và input/output
- Dependencies (import gì)
- Ai gọi file này?
```

### Tìm code liên quan
```
Tìm tất cả nơi sử dụng hàm [tên_hàm].
Liệt kê: file, dòng, context.
```

### Đếm và thống kê
```
Đếm:
- Tổng số file [.py / .js / .ts]
- Tổng số dòng code
- File nào dài nhất?
- Hàm nào dài nhất?
```

---

## 2. Creation Patterns

### Tạo file mới theo pattern
```
Tạo file [path] theo đúng pattern của [file_mẫu].
Chức năng: [mô tả].
```

### Tạo CRUD endpoints
```
Tạo CRUD endpoints cho resource [tên]:
- GET /api/[resources] (list + phân trang)
- GET /api/[resources]/:id
- POST /api/[resources]
- PATCH /api/[resources]/:id
- DELETE /api/[resources]/:id
Follow conventions trong api-conventions.md.
```

### Tạo test
```
Viết unit tests cho [file/class/function].
Cover các cases:
- Happy path
- Edge cases
- Error handling
Framework: [pytest / vitest / jest]
```

### Tạo database model
```
Tạo model [tên] với các trường:
- [field1]: [type] (required)
- [field2]: [type] (optional)
- [field3]: [type] (default: [value])
Thêm indexes cho [fields thường query].
```

---

## 3. Modification Patterns

### Sửa lỗi chính xác
```
File [path], dòng [X]: lỗi [mô tả].
Error: [paste error message]
Fix lỗi này, giải thích root cause.
```

### Thêm tính năng vào file có sẵn
```
Trong file [path], thêm:
- [Tính năng mới]
KHÔNG sửa: [phần cần giữ nguyên]
Chạy test sau khi xong.
```

### Sửa nhiều file
```
Task: [mô tả task]
Files cần sửa:
1. [file1] — [sửa gì]
2. [file2] — [sửa gì]
3. [file3] — [sửa gì]
Thực hiện theo thứ tự, test sau mỗi file.
```

---

## 4. Refactoring Patterns

### Tách file lớn
```
File [path] có [X] dòng, quá dài.
Tách thành:
- [module1] — chứa [gì]
- [module2] — chứa [gì]
Giữ backward compat: import cũ phải vẫn hoạt động.
```

### Tách hàm lớn
```
Hàm [tên] trong [file] có [X] dòng, quá phức tạp.
Tách thành các hàm nhỏ.
Giữ nguyên input/output của hàm gốc.
```

### Rename / Move
```
Rename [old_name] → [new_name] trong toàn bộ codebase.
Bao gồm: imports, references, tests, docs.
```

---

## 5. Analysis Patterns

### Code review
```
Review [file/folder]:
1. Security issues
2. Performance problems
3. Code quality
4. Missing tests
Trả lời dạng bảng: | Issue | Severity | Location |
```

### So sánh
```
So sánh [A] với [B]:
- Ưu điểm / nhược điểm
- Performance
- Maintainability
Khuyến nghị dùng cái nào.
```

### Lên kế hoạch
```
Tôi muốn [mục tiêu lớn].
Hãy:
1. Phân tích hiện trạng
2. Lên kế hoạch chi tiết (chia sprint)
3. Ước lượng effort mỗi task
4. Liệt kê rủi ro
Trả lời trước, CHƯA code.
```

---

## 6. Debug Patterns

### Trace lỗi
```
Lỗi: [paste error message + stack trace]
Tìm root cause. Trace từ entry point đến lỗi.
```

### Reproduce lỗi
```
Bug: [mô tả behavior sai]
Expected: [behavior đúng]
Actual: [behavior sai]
Tìm và fix bug. Viết regression test.
```

### Performance debug
```
[Endpoint/function] chạy chậm (> [X]ms).
Phân tích:
- N+1 queries?
- Missing index?
- Loop không hiệu quả?
- Memory leak?
Đề xuất fix.
```

---

## 7. Documentation Patterns

### Tạo README
```
Tạo README.md cho dự án này.
Bao gồm: overview, tech stack, setup, run, test.
Ngắn gọn, developer-focused.
```

### Tạo API docs
```
Tạo API documentation cho tất cả endpoints trong [folder].
Format: Markdown table với Method, Path, Description, Auth.
```

### Cập nhật CHANGELOG
```
Tóm tắt thay đổi trong session này.
Thêm vào CHANGELOG.md format:
## [Date]
### Added
### Changed
### Fixed
```

---

## 8. Multi-Step Patterns

### Pipeline pattern
```
Thực hiện theo pipeline:
Step 1: [action] → báo kết quả
Step 2: [action based on step 1] → báo kết quả
Step 3: [final action]
Dừng lại để tôi review sau mỗi step.
```

### Mỗi task với yêu cầu riêng biệt
```
Sprint plan:
1. ✅ [Done] — Tạo model User
2. 🔄 [Current] — Tạo UserService
3. ⬜ [Next] — Tạo user routes
4. ⬜ [Next] — Viết tests
Tiếp tục từ task 2.
```
