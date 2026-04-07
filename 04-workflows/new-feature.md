# Workflow: Xây Dựng Tính Năng Mới

> Quy trình chuẩn từ yêu cầu → code → test → merge khi thêm feature mới.

---

## Quy Trình Tổng Quan

```
1. PHÂN TÍCH → Hiểu yêu cầu, scope
2. THIẾT KẾ → Lên kế hoạch, chọn approach
3. IMPLEMENT → Code theo plan
4. TEST → Viết và chạy tests
5. REVIEW → Kiểm tra chất lượng
6. MERGE → Tích hợp vào codebase
```

---

## Step 1: Phân Tích

```
Tôi muốn thêm tính năng [mô tả].

Hãy phân tích:
1. Scope — ảnh hưởng những file/module nào?
2. Dependencies — cần thêm lib gì không?
3. Risk — có gì có thể break không?
4. Approach — đề xuất cách implement

Trả lời trước, CHƯA code.
```

### Output mẫu từ Claude
```
## Phân tích: [Tên tính năng]

### Scope
- Files mới: 2 (service, route)
- Files sửa: 1 (app.py — register route)
- Tests mới: 1

### Dependencies: Không cần thêm

### Risk: Thấp — không ảnh hưởng code hiện tại

### Approach
1. Tạo model [...]
2. Tạo service [...]
3. Tạo route [...]
4. Register trong app
```

---

## Step 2: Thiết Kế

```
OK approach đó hợp lý. Thiết kế chi tiết hơn:
- Data model / schema
- API endpoints (method, path, request/response)
- Business rules
```

---

## Step 3: Implement

```
Bắt đầu implement theo plan trên.
Thực hiện từng bước, chạy test sau mỗi bước.
```

### Tips
- Yêu cầu Claude tạo từ **bottom up**: Model → Service → Controller → Route
- Mỗi bước nên là 1 file hoặc 1 thay đổi nhỏ
- Claude sẽ tự chạy test nếu bạn yêu cầu

---

## Step 4: Test

```
Viết test cho tính năng vừa tạo:
- Unit tests cho service methods
- Integration test cho endpoint
Chạy toàn bộ test suite để verify nothing broken.
```

---

## Step 5: Review

```
Review lại tất cả code vừa tạo:
1. Code quality
2. Security
3. Error handling
4. Edge cases
5. Naming conventions
```

---

## Step 6: Commit

```
Tóm tắt thay đổi cho commit message.
Format: conventional commits.
```

---

## Ví Dụ Thực Tế

### Prompt chuỗi cho feature "User Profile"

```
# Message 1
Thêm tính năng User Profile. Phân tích scope.

# Message 2  
OK. Tạo model UserProfile.

# Message 3
Tạo UserProfileService với: getProfile, updateProfile.

# Message 4
Tạo routes: GET/PATCH /api/users/:id/profile.

# Message 5
Viết unit tests cho UserProfileService.

# Message 6
Chạy tất cả tests. Tóm tắt thay đổi.
```

→ 6 messages, feature hoàn chỉnh, mỗi step có kiểm tra.
