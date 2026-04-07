# Viết Prompt Hiệu Quả

> Prompt tốt = output tốt. Hướng dẫn viết prompt để Claude code chính xác.

---

## 1. Công Thức Prompt Chuẩn

```
[CONTEXT] + [TASK] + [CONSTRAINTS] + [OUTPUT FORMAT]
```

| Thành phần | Mô tả | Ví dụ |
|-----------|--------|-------|
| Context | Bối cảnh, file liên quan | "Trong file user-service.js" |
| Task | Yêu cầu cụ thể | "Thêm method deleteUser" |
| Constraints | Ràng buộc, giới hạn | "Soft delete, giữ backward compat" |
| Output Format | Định dạng mong muốn | "Trả lời code only" |

---

## 2. Prompt Levels

### Level 1: Câu ngắn (task đơn giản)
```
Sửa lỗi typo trong file README.md
```

### Level 2: Câu chi tiết (task rõ ràng)
```
Thêm endpoint GET /api/users/:id vào admin/routes/users.py.
Return JSON format: {"success": true, "data": {...}}.
Thêm validation cho id (phải là valid ObjectId).
```

### Level 3: Prompt có context (task phức tạp)
```
Trong agents/agent_pipeline.py, hàm run_pipeline() đang quá dài (280 dòng).
Tách các config constants (DEFAULT_SETTINGS, RUN_MODE_PRESETS) ra file riêng.
Giữ backward compat — tất cả import cũ phải vẫn hoạt động.
Sau khi xong, chạy pytest để verify 152/152 tests pass.
```

### Level 4: Prompt chi tiết (task rủi ro cao)
```
Refactor agents.py (4000 LOC) thành agents/ package.

## Yêu cầu:
1. KHÔNG đổi tên hàm public
2. KHÔNG thay đổi behavior  
3. agents/__init__.py re-export tất cả hàm cũ
4. Từng bước nhỏ, chạy test sau mỗi bước
5. Nếu test fail → rollback bước đó

## File cần giữ nguyên:
- agents.py → rename thành agents_legacy.py
- Mọi import `from agents import X` phải vẫn hoạt động

## Sau khi xong:
- Chạy pytest -v
- Liệt kê thay đổi
- Confirm backward compat
```

---

## 3. Patterns Hiệu Quả

### a. "Đọc trước, làm sau"
```
Đọc file [tên file] trước. Sau đó [yêu cầu].
```
→ Claude hiểu context trước khi hành động.

### b. "Theo pattern hiện tại"
```
Tạo [thứ gì] theo đúng pattern của [file/module mẫu hiện có].
```
→ Claude copy style từ code sẵn có.

### c. "Verify sau khi xong"
```
[Yêu cầu]. Sau đó chạy tests để verify.
```
→ Tự động kiểm tra kết quả.

### d. "Step-by-step"
```
Thực hiện theo thứ tự:
1. [Bước 1]
2. [Bước 2]  
3. [Bước 3]
Dừng lại và báo cáo sau mỗi bước.
```
→ Kiểm soát tiến trình.

### e. "Không break gì cả"
```
[Yêu cầu]. Đảm bảo:
- Không break import hiện tại
- Không thay đổi public API
- Tất cả test vẫn pass
```

---

## 4. Prompt Cho Từng Loại Task

### Tạo mới
```
Tạo file [path] với [mô tả chức năng].
Follow pattern của [file mẫu].
Include: [danh sách yêu cầu]
```

### Sửa lỗi  
```
File [path] bị lỗi: [mô tả lỗi]
Error message: [paste error]
Fix lỗi này. Giải thích root cause.
```

### Refactoring
```
File [path] cần refactor:
- Vấn đề: [mô tả]
- Mong muốn: [kết quả]
- Ràng buộc: [giới hạn]
Chạy test trước và sau khi refactor.
```

### Review
```
Review file [path]. Kiểm tra:
1. Security issues
2. Performance bottlenecks
3. Code style violations
4. Missing error handling
Trả lời dạng bảng có severity.
```

### Phân tích
```
Phân tích [folder/file/module]:
- Có bao nhiêu dòng code?
- Functions nào dài nhất?
- Có code duplication?
- Đề xuất cải thiện (nếu có)
Trả lời trước, chưa sửa gì.
```

---

## 5. Từ Khóa Mạnh

| Từ khóa | Tác dụng |
|---------|---------|
| `KHÔNG` / `NEVER` | Cấm hành động |
| `BẮT BUỘC` / `MUST` | Yêu cầu bắt buộc |
| `Giữ nguyên` / `KEEP` | Không thay đổi |
| `Trước khi` / `Before` | Thứ tự ưu tiên |
| `Nếu ... thì dừng lại` | Điều kiện dừng |
| `Chỉ` / `Only` | Giới hạn scope |
| `Theo pattern của` | Copy style |
| `Trả lời ngắn gọn` | Giảm output length |
| `Code only` | Chỉ trả code |

---

## 6. Prompt Tiếng Việt vs Tiếng Anh

Claude hiểu cả hai. Chọn theo:

| Tiêu chí | Tiếng Việt | Tiếng Anh |
|----------|-----------|-----------|
| Giao tiếp nhanh | ✅ Tự nhiên | Chậm hơn |
| Thuật ngữ kỹ thuật | Dùng xen Anh | ✅ Chính xác |
| Code comments | Không phù hợp | ✅ Chuẩn |
| CLAUDE.md / Rules | Tùy team | ✅ Phổ biến |

### Khuyến nghị
- **Prompt giao tiếp**: Tiếng Việt
- **Rules, CLAUDE.md**: Tiếng Anh (pha Việt được)
- **Code output**: Tiếng Anh (comments, variable names)
- **Mô tả technical**: Giữ thuật ngữ Anh nguyên (`endpoint`, `middleware`, `controller`)
