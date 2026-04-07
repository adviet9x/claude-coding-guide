# Hệ Thống Memory — Tổng Quan

> Memory giúp Claude **nhớ** thông tin qua các sessions.
> Không có memory = mỗi session Claude là "người mới", không biết gì về bạn.

---

## 1. 3 Cấp Độ Memory

```
┌───────────────────────────────────────┐
│  /memories/                          │
│  USER MEMORY — Nhớ vĩnh viễn        │
│  Across all projects & sessions      │
│  VD: Preferences, patterns           │
├───────────────────────────────────────┤
│  /memories/repo/                     │
│  REPO MEMORY — Nhớ theo dự án       │
│  Tồn tại xuyên sessions             │
│  VD: Conventions, build commands     │
├───────────────────────────────────────┤
│  /memories/session/                  │
│  SESSION MEMORY — Nhớ tạm           │
│  Chỉ trong conversation hiện tại    │
│  VD: Task progress, temp notes      │
└───────────────────────────────────────┘
```

| Scope | Tồn tại | Chia sẻ | Dùng cho |
|-------|---------|---------|---------|
| User | Vĩnh viễn | Tất cả dự án | Preferences, patterns |
| Repo | Vĩnh viễn | Dự án cụ thể | Conventions, file map |
| Session | 1 conversation | Không | Task progress |

---

## 2. Khi Nào Dùng Memory

### Nên lưu
- ✅ Quy ước dự án (port, DB name, build command)
- ✅ Bug đã gặp và cách fix
- ✅ User preferences (ngôn ngữ, style)
- ✅ Task progress (phiên dài)
- ✅ Decisions đã thống nhất

### Không nên lưu
- ❌ Code chi tiết (đã có trong file)
- ❌ Thông tin nhạy cảm (passwords, API keys)
- ❌ Thông tin tạm thời, dùng 1 lần
- ❌ Quá nhiều chi tiết (memory có giới hạn)

---

## 3. Cách Claude Dùng Memory

```
Session bắt đầu:
1. Đọc User Memory (auto-loaded, 200 dòng đầu)
2. Liệt kê Session Memory files (chưa đọc)
3. Liệt kê Repo Memory files (chưa đọc)
4. Đọc memory files khi cần

Trong session:
- Tham khảo memory khi thực hiện tasks
- Tạo/cập nhật memory khi có thông tin mới

Session kết thúc:
- Session memory bị xóa
- User + Repo memory giữ nguyên
```

---

## 4. Commands Memory

### Xem memory
```
Xem user memory
Xem repo memory
Xem session memory
```

### Lưu memory
```
Lưu vào user memory: [thông tin]
Lưu vào repo memory: [thông tin dự án]
Lưu progress vào session memory
```

### Cập nhật
```
Cập nhật repo memory file [tên]: thêm [thông tin]
Xóa session memory file [tên]
```

---

## 5. Tóm Tắt Nhanh

```
User Memory   → "Tôi thích gì" (preferences)
Repo Memory   → "Dự án này thế nào" (conventions)
Session Memory → "Đang làm gì" (progress)
```

> Chi tiết từng loại → xem các file tiếp theo trong folder này.
