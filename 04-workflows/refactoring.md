# Workflow: Refactoring Code

> Quy trình refactor an toàn — cải thiện code mà không break tính năng.

---

## Nguyên Tắc Vàng

```
✅ "Make it work → Make it right → Make it fast"
✅ Refactor khi tests đã green
✅ Mỗi bước nhỏ → test → tiếp
❌ KHÔNG đổi behavior trong khi refactor
❌ KHÔNG refactor + thêm feature cùng lúc
```

---

## Quy Trình

```
1. ĐÁNH GIÁ → Code nào cần refactor? Tại sao?
2. BACKUP → Chạy tests, confirm tất cả green
3. LÊN KẾ HOẠCH → Liệt kê thay đổi cụ thể
4. THỰC HIỆN → Từng bước nhỏ
5. VERIFY → Chạy tests sau mỗi bước
6. REVIEW → Kiểm tra backward compat
```

---

## Prompt Mẫu

### Đánh giá
```
File [path] có [X] dòng. Phân tích:
- Có cần refactor không?
- Vấn đề chính là gì?
- Đề xuất cải thiện (chưa code)
```

### Thực hiện
```
Refactor [file/module].
Yêu cầu:
1. Giữ nguyên public API / interface
2. Tất cả import hiện tại vẫn hoạt động
3. Chạy test sau mỗi thay đổi
4. Nếu test fail → rollback bước đó
```

### Tách file
```
File [path] quá dài ([X] dòng).
Tách thành:
- [file1] — chứa [constants/config]
- [file2] — chứa [helpers]
- [file_gốc] — import từ file mới
Backward compat: exports cũ vẫn hoạt động.
```

---

## Các Loại Refactoring Phổ Biến

| Loại | Khi nào | Prompt gợi ý |
|------|---------|--------------|
| Extract function | Hàm > 30 dòng | "Tách hàm X thành các hàm nhỏ" |
| Extract file | File > 500 dòng | "Tách constants ra file riêng" |
| Rename | Tên không rõ nghĩa | "Rename X → Y trong toàn codebase" |
| Remove duplication | Code lặp lại | "Tìm code duplication, extract shared" |
| Simplify conditionals | If/else phức tạp | "Simplify logic trong hàm X" |
| Replace magic numbers | Số cứng trong code | "Extract constants cho magic numbers" |

---

## Safety Checklist

Trước khi refactor:
- [ ] Tất cả tests GREEN
- [ ] Biết rõ ai consumer/caller của code
- [ ] Có plan backward compat
- [ ] Đã list cụ thể thay đổi

Sau khi refactor:
- [ ] Tất cả tests vẫn GREEN
- [ ] Import cũ vẫn hoạt động
- [ ] Không có file orphan (import bị broken)
- [ ] Code ngắn hơn hoặc clear hơn

---

## Xem Thêm
- [Viết Tests](testing.md) — đảm bảo tests vẫn pass sau refactor
- [Code Review](code-review.md) — review lại code sau refactor
