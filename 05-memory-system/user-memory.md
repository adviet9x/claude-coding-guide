# User Memory — Ghi Nhớ Cá Nhân

> Tồn tại vĩnh viễn, áp dụng cho tất cả dự án và conversation.
> Path: `/memories/`

---

## Dùng Cho

- Ngôn ngữ giao tiếp ưa thích
- Coding style preferences
- Patterns đã học
- Common mistakes và cách tránh
- Tool/workflow preferences

---

## Ví Dụ Thực Tế

### `/memories/language_preference.md`
```markdown
## Giao tiếp
- Luôn trả lời bằng tiếng Việt
```

### `/memories/coding_patterns.md`
```markdown
## Patterns đã kiểm chứng
- Refactor file lớn: tách config ra trước, test, rồi tách logic
- Khi tách file: luôn giữ backward compat exports
- Chạy test SAU MỖI bước refactor, không đợi cuối

## Mistakes hay gặp
- Import circular: tách shared types ra file riêng
- Test patch path: patch tại nơi import, không nơi define
```

### `/memories/debugging.md`
```markdown
## Debug tips
- MongoDB Windows: service name "MongoDB"
- Python 3.14 trên máy: C:\Python314\python.exe
- Flask port default: 5050
```

---

## Quản Lý User Memory

### Nguyên tắc
- **Ngắn gọn** — mỗi entry 1-2 dòng
- **Có tổ chức** — chia theo topic, mỗi topic 1 file
- **Cập nhật** — xóa thông tin cũ/sai
- **Không nhạy cảm** — không lưu passwords, API keys

### Khi nào tạo
- Claude lặp lại sai lầm > 2 lần → ghi lại pattern đúng
- Bạn có preference mà phải nhắc mỗi session → lưu memory
- Phát hiện pattern hữu ích → ghi lại

### Giới hạn
- 200 dòng đầu được auto-loaded vào context
- Quá nhiều memory = tốn token mỗi session
- Chỉ lưu insights, không lưu chi tiết code
