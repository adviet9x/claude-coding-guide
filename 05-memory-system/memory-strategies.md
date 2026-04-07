# Chiến Lược Tối Ưu Memory

> Tổ chức memory hiệu quả = Claude hoạt động tốt hơn + tiết kiệm token.

---

## 1. Cấu Trúc Memory Lý Tưởng

```
/memories/
├── language_preference.md     # 5 dòng — ngôn ngữ giao tiếp
├── coding_patterns.md         # 20 dòng — patterns đã học
├── debugging.md               # 15 dòng — debug tips
│
├── repo/
│   ├── project-basics.md      # 20 dòng — overview dự án
│   ├── file-map.md            # 30 dòng — bản đồ file
│   └── conventions.md         # 20 dòng — coding conventions
│
└── session/
    └── current-task.md        # Progress hiện tại
```

**Tổng user memory: < 100 dòng** (tiết kiệm token mỗi session)

---

## 2. Nguyên Tắc Tối Ưu

### Keep it small
```
# ❌ Bad — 50 dòng cho 1 entry
## Bug fix: MongoDB connection
Hôm qua tôi gặp lỗi kết nối MongoDB...
[kể dài dòng 50 dòng]

# ✅ Good — 1 dòng
- MongoDB Windows: restart service "MongoDB" nếu connection refused
```

### Keep it organized
```
# ❌ Bad — 1 file for everything
/memories/notes.md (200 dòng, đủ thứ lẫn lộn)

# ✅ Good — chia theo topic
/memories/debugging.md (15 dòng)
/memories/patterns.md (20 dòng)
/memories/preferences.md (10 dòng)
```

### Keep it current
```
# ❌ Bad — thông tin cũ
- Dùng Sequelize ORM (thực tế đã chuyển Prisma)

# ✅ Good — cập nhật khi thay đổi
- ORM: Prisma (migrated from Sequelize, Sprint 3)
```

---

## 3. Memory Lifecycle

```
Phiên 1: Phát hiện pattern → Lưu user memory
Phiên 2: Claude đọc memory → Áp dụng pattern → Nhanh hơn
Phiên 5: Pattern outdated → Cập nhật memory
Phiên 10: Memory cleanup → Xóa entries không cần
```

### Maintenance schedule
| Tần suất | Hành động |
|----------|----------|
| Mỗi phiên | Review session memory |
| Mỗi tuần | Review repo memory |
| Mỗi tháng | Review + cleanup user memory |

---

## 4. Prompt Quản Lý Memory

### Setup memory cho dự án mới
```
Phân tích dự án và tạo repo memory:
- project-basics.md: stack, commands, key facts
- file-map.md: files quan trọng nhất
- conventions.md: patterns trong codebase
Mỗi file < 30 dòng.
```

### Cleanup memory
```
Xem tất cả memory files.
Liệt kê entries cũ/không chính xác.
Đề xuất cleanup (chưa xóa).
```

### Export insights
```
Từ session này, có gì cần lưu vào memory?
- Pattern mới phát hiện → user memory
- Info dự án → repo memory
```

---

## 5. Anti-Patterns Memory

| ❌ Không nên | ✅ Nên |
|-------------|-------|
| Lưu mọi thứ | Lưu insights, patterns |
| 1 file khổng lồ | Chia nhỏ theo topic |
| Không bao giờ cleanup | Cleanup hàng tháng |
| Lưu code snippet dài | Lưu file path + purpose |
| Lưu sensitive data | KHÔNG lưu secrets |
| Duplicate info từ CLAUDE.md | Chỉ lưu bổ sung |
