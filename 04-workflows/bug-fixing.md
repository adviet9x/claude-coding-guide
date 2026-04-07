# Workflow: Sửa Lỗi & Debug

> Quy trình chuẩn để tìm và sửa bug hiệu quả với Claude.

---

## Quy Trình

```
1. MÔ TẢ lỗi chính xác
2. Claude TÌM root cause
3. Claude ĐỀ XUẤT fix
4. IMPLEMENT fix
5. VIẾT regression test
6. VERIFY tất cả tests pass
```

---

## 1. Mô Tả Lỗi Hiệu Quả

### Template
```
## Bug Report
- **Behavior sai**: [mô tả]
- **Expected**: [behavior đúng]
- **Steps to reproduce**: [các bước]
- **Error message**: [paste error/stack trace]
- **File liên quan**: [nếu biết]
```

### Ví dụ
```
GET /api/users?page=0 trả về 500.
Expected: trả về page 1 hoặc lỗi 400.
Error: TypeError: Cannot read property 'skip' of undefined
File: admin/routes/users.py hoặc services/user-service.py
```

---

## 2. Prompt Debug

### Khi có error message
```
Lỗi này xuất hiện khi [action]:

[paste error message + stack trace]

Tìm root cause và fix.
```

### Khi không có error message
```
Bug: [mô tả behavior sai]
Expected: [behavior đúng]
Actual: [behavior sai]

Trace qua code liên quan, tìm nguyên nhân.
```

### Khi lỗi intermittent
```
Bug intermittent: [mô tả]
Xảy ra khoảng [tần suất].
Kiểm tra:
- Race conditions?
- Memory/resource limits?
- External service timeout?
```

---

## 3. Sau Khi Fix

```
Viết regression test cho bug vừa fix.
Test phải:
- Reproduce lỗi cũ (nếu không fix thì phải fail)
- Verify fix đúng
- Không break tests khác
```

---

## 4. Debug Tips

| Tình huống | Prompt |
|-----------|--------|
| Biết file lỗi | "File X, dòng Y: lỗi Z. Fix." |
| Không biết file | "Lỗi [message]. Tìm file gây lỗi." |
| Logic sai | "Hàm X trả về sai giá trị khi input [Y]. Debug." |
| Performance | "Endpoint X chậm (>2s). Tìm bottleneck." |
| Lỗi chỉ Production | "Lỗi chỉ xảy ra ở production. Kiểm tra env vars, config." |
