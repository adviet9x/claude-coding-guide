# Lỗi Thường Gặp

> Các vấn đề phổ biến khi làm việc với Claude và cách giải quyết.

---

## 1. Claude Không Hiểu Dự Án

### Triệu chứng
- Claude hỏi "dự án này dùng gì?"
- Output không đúng tech stack
- Tạo code sai framework

### Nguyên nhân
- Thiếu `CLAUDE.md`
- CLAUDE.md quá chung chung

### Fix
```
1. Tạo CLAUDE.md ở root với đầy đủ thông tin
2. Tạo .claude/rules/ với code style cụ thể
3. Tạo docs/FILE_MAP.md để Claude biết file nào ở đâu
```

---

## 2. Claude Sửa Sai File / Phần Sai

### Triệu chứng
- Sửa file không liên quan
- Sửa phần code không cần sửa
- Overwrite code quan trọng

### Fix
```
# Thêm vào CLAUDE.md
## Protected Files — KHÔNG SỬA
- [file cần bảo vệ]

# Prompt rõ ràng hơn
"Chỉ sửa hàm X trong file Y. KHÔNG sửa gì khác."
```

---

## 3. Claude Quên Context Trước Đó

### Triệu chứng
- Hỏi lại thứ đã nói
- Quên thay đổi đã thực hiện
- Output mâu thuẫn với trước

### Nguyên nhân
- Conversation quá dài → hết context window

### Fix
```
1. Lưu progress vào session memory
2. Bắt đầu session mới
3. Đầu session mới: "Đọc session memory và tiếp tục"
```

---

## 4. Claude Tạo Code Sai Style

### Triệu chứng
- CamelCase thay vì snake_case (hoặc ngược lại)
- Import order sai
- Không dùng async/await

### Fix
```
1. Tạo .claude/rules/code-style.md với ví dụ cụ thể ✅/❌
2. Nếu vẫn sai → thêm vào CLAUDE.md Critical Rules
3. Dùng prompt: "Follow code-style.md ruleset"
```

---

## 5. Claude Output Quá Dài

### Triệu chứng
- Giải thích dài dòng khi chỉ cần code
- Comments quá nhiều
- Response 2000+ tokens cho task đơn giản

### Fix
```
# Thêm vào prompt
"Code only, không giải thích"
"Trả lời ngắn gọn, < 10 dòng"
"Chỉ code, không comment"
```

---

## 6. Tests Fail Sau Khi Claude Sửa Code

### Triệu chứng
- Tests pass trước, fail sau khi Claude edit
- Import errors, missing functions

### Fix
```
# Prompt pattern
"Chạy tests TRƯỚC KHI sửa.
Sửa code.
Chạy tests SAU KHI sửa.
Nếu fail → rollback."
```

---

## 7. Claude Không Tìm Thấy File

### Triệu chứng
- "Không tìm thấy file X"
- Tìm sai đường dẫn

### Fix
```
# Cho đường dẫn chính xác
"File ở admin/routes/pipeline.py" ← đúng
"File pipeline.py" ← Claude có thể tìm sai

# Tạo FILE_MAP.md
Claude tra cứu file map thay vì scan
```

---

## 8. Claude Không Chạy Được Lệnh

### Triệu chứng
- Command not found
- Permission denied
- Wrong working directory

### Fix
```
# Cho biết environment
"Python ở C:\Python314\python.exe"
"Dùng PowerShell, không bash"
"cd đến [thư mục] trước"
```

---

## Quick Reference

| Vấn đề | Fix nhanh |
|--------|----------|
| Không hiểu dự án | Tạo/cập nhật CLAUDE.md |
| Sửa sai file | Thêm Protected Files rule |
| Quên context | Lưu memory, session mới |
| Sai style | Tạo code-style.md rule |
| Output dài | "Code only" |
| Test fail | "Chạy test trước/sau mỗi sửa" |
| Không tìm file | Cho path chính xác, FILE_MAP |
| Lệnh lỗi | Cho biết OS, path, env |

---

## Xem Thêm
- [Debug Agent](debugging-agent.md) — khi Claude không follow rules
- [FAQ](faq.md) — câu hỏi thường gặp
- [Memory System](../05-memory-system/memory-overview.md) — cách dùng memory để giữ context
- [Bug Fixing Workflow](../04-workflows/bug-fixing.md) — quy trình fix bug với Claude
