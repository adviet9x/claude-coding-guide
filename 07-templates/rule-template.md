# Template: Rule File

> Dùng template này để tạo rule files trong `.claude/rules/`.

---

## Template

```markdown
# [Tên Rule]

> [Mô tả 1 câu — khi nào rule này áp dụng]

## Nguyên Tắc
- [Bullet point 1]
- [Bullet point 2]
- [Bullet point 3]

## Quy Tắc Chi Tiết

### [Category 1]
\`\`\`[lang]
// ✅ Good
[ví dụ code đúng]

// ❌ Bad
[ví dụ code sai]
\`\`\`

### [Category 2]
| Trường hợp | Quy tắc |
|-----------|---------|
| [case 1] | [rule] |
| [case 2] | [rule] |

## Exceptions
- [Trường hợp ngoại lệ nếu có]
```

---

## Checklist Rule Tốt

- [ ] Tiêu đề rõ ràng, mô tả scope
- [ ] Có ✅ / ❌ examples
- [ ] Code ví dụ cho patterns phức tạp
- [ ] Ngắn gọn (< 150 dòng)
- [ ] Actionable — nói rõ PHẢI LÀM gì
- [ ] Không trùng với rule khác
