# Anti-Patterns — Những Gì KHÔNG Nên Làm

> Các sai lầm phổ biến khi làm việc với Claude. Tránh để tiết kiệm thời gian và token.

---

## 1. Prompt Anti-Patterns

### ❌ Quá mơ hồ
```
# ❌ Bad
"Cải thiện code"
"Làm cho tốt hơn"
"Fix mấy cái lỗi"

# ✅ Good
"Refactor hàm processOrder() trong orders-service.js — tách thành 3 hàm nhỏ"
"Fix lỗi 500 khi gọi GET /api/users?page=0"
```

### ❌ Quá nhiều task cùng lúc
```
# ❌ Bad — Claude sẽ bỏ sót hoặc làm nửa vời
"Tạo user management system: model, routes, controllers,
services, tests, UI, database migration, API docs,
validation, error handling, logging, caching"

# ✅ Good — Chia nhỏ
"Tạo User model với fields: email, name, role, createdAt"
# (đợi xong) →
"Tạo UserService với CRUD methods"
# (đợi xong) →
"Tạo user routes và controllers"
```

### ❌ Giả định Claude nhớ
```
# ❌ Bad — Claude có thể quên trong conversation dài
"Sửa cái file lúc nãy"
"Tiếp tục task hôm qua"

# ✅ Good — Nhắc lại context
"Sửa file agents/agent_pipeline.py — hàm _step_write()"
"Tiếp tục task refactor pipeline. Đã xong step 1-3. Làm step 4."
```

### ❌ Copy paste quá nhiều code
```
# ❌ Bad — Tốn token, Claude đã đọc file được
"Đây là code hiện tại:
[paste 500 dòng code]
Sửa lỗi ở dòng 230"

# ✅ Good — Chỉ cần chỉ file
"File agents/agent_pipeline.py, dòng 230: lỗi KeyError. Fix."
```

### ❌ Hỏi rồi không dùng
```
# ❌ Bad — Tốn token vô ích
"Giải thích file X" → (đọc xong rồi ignore)
"Liệt kê tất cả endpoints" → (không dùng info đó)

# ✅ Good — Chỉ hỏi khi cần
"Đọc file X và sửa lỗi [cụ thể]"
```

---

## 2. Workflow Anti-Patterns

### ❌ Không review output
```
# ❌ Bad — Tin tưởng mù quáng
"Sửa lỗi" → accept mà không đọc
"Refactor" → merge mà không test

# ✅ Good
"Sửa lỗi" → đọc code → chạy test → confirm
```

### ❌ Không chạy test
```
# ❌ Bad
Sửa 10 files → không test → deploy → bug

# ✅ Good
Sửa 1 file → test → sửa file tiếp → test → ... → all green
```

### ❌ Sửa trực tiếp file quan trọng
```
# ❌ Bad
"Sửa database schema trực tiếp"
"Sửa file config production"

# ✅ Good
"Tạo migration file để thay đổi schema"
"Sửa file config development/staging, KHÔNG sửa production"
```

### ❌ Session quá dài
```
# ❌ Bad — Context hết, Claude bắt đầu "ảo"
1 session liên tục 50+ messages → Claude quên đầu conversation

# ✅ Good — Chia session
Session 1: Task A (10-15 messages) → save memory → kết thúc
Session 2: Task B (10-15 messages) → save memory → kết thúc
```

---

## 3. Configuration Anti-Patterns

### ❌ CLAUDE.md quá dài
```
# ❌ Bad — 500+ dòng, copy paste mọi thứ
→ Tốn token mỗi message
→ Claude overhead xử lý

# ✅ Good — 100-200 dòng
→ Tóm tắt, link đến docs/ khi cần detail  
```

### ❌ Rules mâu thuẫn nhau
```
# ❌ Bad
# Rule 1: "Dùng camelCase cho mọi thứ"
# Rule 2: "Database columns dùng snake_case"

# ✅ Good — Rõ ràng scope
# Rule 1: "camelCase cho JS variables và functions"
# Rule 2: "snake_case cho database columns"
```

### ❌ Không có rules cho dự án
```
# ❌ Bad
Dự án không có .claude/rules/ → Claude dùng default behavior
→ Mỗi session style khác nhau
→ Naming không nhất quán

# ✅ Good
Tạo ít nhất 3 rule files: code-style, naming, security
```

### ❌ Giữ rules cũ không cập nhật
```
# ❌ Bad
Rule: "Dùng Sequelize ORM"  
Thực tế: Đã migrate sang Prisma 6 tháng trước

# ✅ Good
Cập nhật rules sau mỗi thay đổi lớn
```

---

## 4. Token Waste Anti-Patterns

### ❌ Hỏi Claude giải thích những gì biết rồi
```
# ❌ Bad — Tốn 500+ tokens
"Giải thích async/await là gì?"

# ✅ Good — Hỏi cụ thể về dự án
"Tại sao hàm X dùng callback thay vì async/await?"
```

### ❌ Yêu cầu format thừa
```
# ❌ Bad
"Tạo file X. Cho tôi markdown đẹp, có bullet points,
headers, code blocks, giải thích từng dòng..."

# ✅ Good
"Tạo file X. Code only."
```

### ❌ Lặp lại yêu cầu
```
# ❌ Bad — Gõ lại mọi thứ
Message 1: "Tạo UserService với findById, create, update, delete"
Message 5: "Tạo UserService với findById, create, update, delete kèm validation"

# ✅ Good — Reference 
Message 5: "Thêm validation vào UserService vừa tạo"
```

---

## 5. Security Anti-Patterns

### ❌ Paste secrets vào chat
```
# ❌ NEVER
"Database URL là mongodb://admin:password123@localhost:27017"
"API key: sk-xxx-xxx-xxx"

# ✅ Good
"Database URL nằm trong biến môi trường MONGO_URI"
```

### ❌ Để Claude tạo .env với giá trị thật
```
# ❌ Bad
"Tạo .env file với API keys"

# ✅ Good
"Tạo .env.example với placeholder values"
```

---

## 6. Checklist Tránh Anti-Patterns

Trước mỗi session, tự hỏi:

- [ ] Yêu cầu có **cụ thể** không?
- [ ] Có chia task **đủ nhỏ** không?
- [ ] Có **context** cần thiết cho Claude không?
- [ ] Dự án có **CLAUDE.md** và **rules** chưa?
- [ ] Có plan **review** và **test** output không?
- [ ] Có **paste secrets** trong prompt không?
- [ ] Session có **quá dài** không (> 30 messages)?
