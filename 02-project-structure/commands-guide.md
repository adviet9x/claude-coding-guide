# Tạo Commands — Lệnh Tái Sử Dụng

> Commands là các prompt/workflow có thể gọi lặp lại bằng tên ngắn.
> Giống "macro" cho Claude — gõ 1 lệnh, chạy workflow phức tạp.

---

## 1. Commands Là Gì?

```
.claude/commands/
├── deploy.md          # /deploy → chạy quy trình deploy
├── fix-issue.md       # /fix-issue → phân tích & sửa lỗi
├── review.md          # /review → code review
├── new-endpoint.md    # /new-endpoint → scaffold API
└── status.md          # /status → báo cáo progress
```

- User gõ `/command-name` → Claude thực thi workflow
- Tiết kiệm thời gian cho các task lặp lại
- Đảm bảo consistency — cùng quy trình mỗi lần

---

## 2. Cách Viết Command

### Format cơ bản
```markdown
# Command: [tên]

## Description
[Mô tả ngắn]

## Arguments
- `$1` — [Mô tả argument 1]
- `$2` — [Mô tả argument 2]

## Instructions
[Workflow step-by-step cho Claude thực hiện]
```

---

## 3. Các Command Phổ Biến

### a. Deploy
```markdown
# Command: deploy

## Description
Deploy ứng dụng lên production

## Instructions
1. Chạy tất cả tests: `npm test`
2. Nếu tests fail → DỪNG và báo lỗi
3. Build production: `npm run build`
4. Kiểm tra build output
5. Push to main branch
6. Tag release version
7. Báo cáo kết quả
```

### b. Fix Issue
```markdown
# Command: fix-issue

## Description  
Phân tích và sửa một issue/bug

## Arguments
- `$1` — Mô tả lỗi hoặc issue number

## Instructions
1. Đọc mô tả lỗi: $1
2. Tìm file liên quan (grep_search, semantic_search)
3. Đọc code liên quan
4. Xác định root cause
5. Đề xuất giải pháp (chờ user duyệt)
6. Implement fix
7. Viết regression test
8. Chạy toàn bộ test suite
9. Báo cáo kết quả
```

### c. Code Review
```markdown
# Command: review

## Description
Review code theo checklist chuẩn

## Arguments
- `$1` — File hoặc folder cần review

## Instructions
Đọc code trong $1 và đánh giá theo:

### Correctness
- [ ] Logic đúng
- [ ] Edge cases handled
- [ ] Error handling đầy đủ

### Security
- [ ] Input validated
- [ ] No hardcoded secrets
- [ ] SQL injection safe

### Performance
- [ ] No N+1 queries
- [ ] Proper indexing
- [ ] No memory leaks

### Maintainability
- [ ] Code readable
- [ ] Functions < 30 lines
- [ ] Naming clear

### Output
Trả lời dạng bảng:
| Category | Score | Issues |
|----------|-------|--------|
```

### d. New Endpoint
```markdown
# Command: new-endpoint

## Description
Scaffold một API endpoint mới hoàn chỉnh

## Arguments
- `$1` — HTTP method (GET/POST/PUT/DELETE)
- `$2` — Route path (/api/v1/...)

## Instructions
1. Tạo route handler trong `src/routes/`
2. Tạo controller trong `src/controllers/`
3. Tạo service trong `src/services/`
4. Thêm Zod validation schema
5. Thêm error handling
6. Register route
7. Tạo unit test
8. Cập nhật API documentation
```

### e. Status Report
```markdown
# Command: status

## Description
Báo cáo trạng thái dự án hiện tại

## Instructions
1. Đọc CLAUDE.md → lấy current sprint
2. Đếm test cases: pass/fail
3. Kiểm tra git status (uncommitted changes)
4. Đọc TODO/FIXME trong codebase
5. Trả lời format:

## Project Status
- **Sprint**: [tên sprint]
- **Tests**: X/Y pass
- **Open TODOs**: N items
- **Uncommitted**: [files]
- **Recent changes**: [list]
```

### f. Quick Audit
```markdown
# Command: audit

## Description
Audit nhanh codebase

## Instructions
1. **Security scan**
   - Tìm hardcoded secrets (grep API_KEY, password, secret)
   - Kiểm tra .env trong git
   
2. **Code quality**
   - File nào > 500 dòng? → cần tách
   - Hàm nào > 50 dòng? → cần refactor
   
3. **Dependencies**
   - `npm audit` hoặc `pip audit`
   
4. **Test coverage**
   - Có test cho tất cả services?
   - Coverage report

5. Báo cáo kết quả dạng bảng
```

---

## 4. Sử Dụng Commands

### Trong Claude Code CLI
```bash
# Gọi command
/deploy
/fix-issue "Login fails with 500 error"
/review src/services/
/new-endpoint POST /api/v1/orders
/status
```

### Trong VS Code Copilot Chat
```
Chạy command deploy
Chạy command fix-issue: "Login fails with 500 error"
```

---

## 5. Tips Viết Command Tốt

### ✅ Nên
- **Atomic**: mỗi command làm 1 việc
- **Có arguments**: linh hoạt, tái sử dụng
- **Step-by-step**: Claude follow được
- **Có exit conditions**: khi nào DỪNG
- **Có output format**: biết trả lời gì

### ❌ Không nên
- Quá phức tạp (> 20 steps)
- Không có mô tả rõ
- Không handle lỗi
- Trùng lặp với command khác

---

## 6. Command vs Skill

| | Command | Skill |
|-|---------|-------|
| Kích hoạt | User gõ `/command` | Tự động match |
| Scope | Task cụ thể | Domain cụ thể |
| Reusable | Gọi lặp lại | Áp dụng khi phù hợp |
| Ví dụ | `/deploy` | Deploy Skill |
| Phù hợp | Task lặp lại | Workflow phức tạp |
