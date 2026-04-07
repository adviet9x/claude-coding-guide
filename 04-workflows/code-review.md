# Workflow: Code Review

> Dùng Claude để review code — tìm bugs, security issues, và cải thiện chất lượng.

---

## Prompt Review

### Review nhanh (1 file)
```
Review file [path]. Focus: bugs và security.
Trả lời dạng bảng ngắn gọn.
```

### Review chi tiết
```
Review [file/folder] theo checklist:
1. Correctness — logic đúng?
2. Security — input validation, secrets, injection?
3. Performance — N+1, missing index, memory?
4. Error handling — try/catch, edge cases?
5. Code quality — naming, duplication, complexity?
6. Tests — coverage đủ?

Format:
| # | Issue | Severity | File:Line | Suggestion |
```

### Review trước merge
```
Review tất cả thay đổi trong session này.
Kiểm tra:
- Backward compatibility
- Missing tests
- Security concerns
- Naming consistency
OK hay cần sửa gì?
```

---

## Checklist Review

### Security
- [ ] Input validated trước khi dùng
- [ ] Không hardcode secrets
- [ ] SQL injection safe (parameterized queries)
- [ ] XSS prevention (sanitize output)
- [ ] Auth/authorization checked

### Performance  
- [ ] Không có N+1 queries
- [ ] Proper indexing
- [ ] Pagination cho list queries
- [ ] Caching cho data đọc nhiều
- [ ] Không memory leak

### Code Quality
- [ ] Functions < 30 dòng
- [ ] Files < 500 dòng
- [ ] Naming rõ ràng, consistent
- [ ] Error handling đầy đủ
- [ ] Không code duplication

### Tests
- [ ] Unit tests cho business logic
- [ ] Edge cases covered
- [ ] Error cases tested
- [ ] All tests pass

---

## Severity Levels

| Level | Ý nghĩa | Hành động |
|-------|---------|----------|
| 🔴 Critical | Security hole, data loss risk | Fix ngay |
| 🟠 High | Bug, logic sai | Fix trước merge |
| 🟡 Medium | Code smell, maintainability | Nên fix |
| 🟢 Low | Style, optimization | Tùy chọn |
