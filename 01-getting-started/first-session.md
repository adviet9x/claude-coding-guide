# Phiên Làm Việc Đầu Tiên

> Hướng dẫn step-by-step cho phiên code đầu tiên với Claude.

---

## 1. Mở Dự Án

```bash
# VS Code
code /path/to/project

# Claude Code CLI
cd /path/to/project
claude
```

## 2. Cho Claude Hiểu Dự Án (Prompt Đầu Tiên)

### Dự án mới (chưa có code)
```
Tôi muốn tạo 1 dự án [mô tả]. Stack: [tech stack].
Hãy tạo cấu trúc dự án ban đầu.
```

### Dự án đã có code
```
Hãy đọc CLAUDE.md và phân tích cấu trúc dự án.
Liệt kê các file chính và mục đích của chúng.
```

### Dự án lớn (chưa có CLAUDE.md)
```
Dự án này chưa có tài liệu. Hãy:
1. Scan cấu trúc thư mục
2. Đọc entry point (main.py / index.js / ...)
3. Tóm tắt kiến trúc
4. Tạo CLAUDE.md cho dự án
```

---

## 3. Quy Trình Làm Việc Chuẩn

```
┌─────────────────────────────────────────┐
│  1. MÔ TẢ yêu cầu rõ ràng              │
│  2. Claude PHÂN TÍCH & lên kế hoạch     │
│  3. Claude THỰC HIỆN (code/edit/test)   │
│  4. BẠN REVIEW kết quả                  │
│  5. LẶP LẠI nếu cần điều chỉnh         │
└─────────────────────────────────────────┘
```

### Ví dụ session thực tế

```
👤 Bạn: "Thêm endpoint GET /api/users với phân trang"

🤖 Claude:
  → Đọc routes/ folder
  → Đọc model User
  → Tạo route handler
  → Thêm validation
  → Chạy test
  → Báo cáo kết quả

👤 Bạn: "OK. Thêm filter theo role nữa"

🤖 Claude:
  → Sửa endpoint vừa tạo
  → Thêm query param ?role=admin
  → Cập nhật test
```

---

## 4. Các Lệnh Hữu Ích

### Phân tích code
```
Giải thích file [tên file] làm gì
Liệt kê tất cả API endpoints
Tìm tất cả nơi sử dụng hàm [tên hàm]
```

### Tạo code mới
```
Tạo service [tên] với các method: [liệt kê]
Thêm route [mô tả] theo pattern hiện tại
Tạo model [tên] với các trường: [liệt kê]
```

### Sửa lỗi
```
File [tên file] bị lỗi [mô tả lỗi]. Fix
Chạy test và sửa tất cả lỗi
Tại sao endpoint [route] trả về 500?
```

### Refactoring
```
Refactor hàm [tên] — quá dài, tách nhỏ
File [tên] 1000 dòng, tối ưu đi
Tách [module] thành package riêng
```

---

## 5. Tips Cho Phiên Đầu Tiên

### ✅ Nên
- Bắt đầu với yêu cầu nhỏ, rõ ràng
- Cho Claude đọc code trước khi sửa
- Review kết quả sau mỗi thay đổi
- Chạy test sau mỗi thay đổi
- Lưu memory cho những gì quan trọng

### ❌ Không nên
- Yêu cầu quá nhiều thứ cùng lúc
- Để Claude đoán mò — nói rõ ý muốn
- Bỏ qua review — luôn kiểm tra output
- Sợ nói "sai rồi, sửa lại"

---

## 6. Khi Gặp Vấn Đề

| Vấn đề | Giải pháp |
|--------|-----------|
| Claude không hiểu dự án | Tạo/cập nhật CLAUDE.md |
| Claude sửa sai file | Thêm rule "KHÔNG sửa file X" |
| Claude quên context | Dùng memory system |
| Output quá dài | Yêu cầu "ngắn gọn" hoặc "chỉ code" |
| Claude không follow style | Tạo rule code-style.md |

---

## 7. Kết Thúc Phiên

Trước khi đóng:
1. **Kiểm tra** tất cả code đã save
2. **Chạy test** để đảm bảo nothing broken
3. **Lưu memory** nếu có gì quan trọng cần nhớ
4. **Commit** thay đổi với message rõ ràng

```
Tóm tắt những gì đã thay đổi trong phiên này.
Lưu vào session memory nếu còn việc dở dang.
```
