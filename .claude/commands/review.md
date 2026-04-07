---
name: review
description: Review code quality, security, và conventions
arguments:
  - name: target
    description: File hoặc folder cần review
    required: true
---

# Code Review Command

## Quy trình
1. Đọc file/folder: `$ARGUMENTS.target`
2. Kiểm tra theo checklist:
   - Security: input validation, auth, secrets
   - Code quality: naming, length, DRY
   - Error handling: try/except, status codes
   - Testing: coverage, edge cases
3. Output review report

## Output Format
```markdown
## Review: [target]

### ✅ Tốt
- ...

### ⚠️ Cần sửa
- **[File:Line]**: [Vấn đề] → [Fix]

### 💡 Gợi ý
- ...

### Verdict: ✅ / ⚠️ / ❌
```
