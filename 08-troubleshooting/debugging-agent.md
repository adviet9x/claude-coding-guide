# Debug Khi Claude Không Tuân Thủ Rules

> Khi Claude bỏ qua rules hoặc instructions, dùng checklist này để debug.

---

## 1. Checklist Debug

### File có được load không?
```
# Kiểm tra Claude có đọc rules
"Liệt kê tất cả rules trong .claude/rules/"
"Đọc file .claude/rules/code-style.md"
```

### Rule có rõ ràng không?
```
# ❌ Quá chung chung — Claude không biết làm gì
"Code phải sạch"

# ✅ Cụ thể — Claude biết chính xác
"Variables: camelCase. Constants: UPPER_SNAKE. Files: kebab-case."
```

### Rule có mâu thuẫn không?
```
# ❌ Mâu thuẫn giữa 2 rules
Rule A: "Dùng snake_case cho mọi thứ"
Rule B: "Dùng camelCase cho biến JS"

# ✅ Rõ scope
Rule A: "snake_case cho Python code"
Rule B: "camelCase cho JavaScript code"
```

---

## 2. Tại Sao Claude Bỏ Qua Rules?

| Nguyên nhân | Giải pháp |
|------------|----------|
| Rule quá chung | Viết cụ thể hơn, cho ví dụ |
| Rule bị ghi đè bởi prompt | Prompt user > rules trong some cases |
| Rule file không được load | Kiểm tra path, settings.json |
| Context window hết | Rules cuối bị cắt, rút gọn rules |
| Rule mâu thuẫn | Review và sửa conflicts |
| Rule quá nhiều (>20 files) | Gộp rules, giữ < 10 files |

---

## 3. Cách Enforce Rules Mạnh Hơn

### Đưa vào CLAUDE.md (Critical Rules)
```markdown
## Critical Rules — PHẢI TUÂN THỦ
1. **KHÔNG BAO GIỜ** sửa agents_legacy.py
2. **BẮT BUỘC** chạy test sau mỗi thay đổi
```
→ CLAUDE.md được đọc mọi lúc, ưu tiên cao.

### Nhắc lại trong prompt
```
"Thêm endpoint X. REMEMBER: follow api-conventions.md"
```

### Dùng từ khóa mạnh
```
NEVER / KHÔNG BAO GIỜ
ALWAYS / LUÔN LUÔN
MUST / BẮT BUỘC
CRITICAL / QUAN TRỌNG
```

---

## 4. Test Rules

```
# Tạo task cố tình trigger rule
"Tạo biến tên x"  
→ Nếu rule naming active: Claude nên đặt tên rõ nghĩa

"Hardcode API key trong code"
→ Nếu rule security active: Claude nên dùng env var

"Sửa agents_legacy.py"
→ Nếu rule protected files active: Claude nên từ chối
```

---

## 5. Escalation

Nếu đã thử tất cả mà Claude vẫn không follow:

1. **Simplify rules** — Quá nhiều rules = Claude confused
2. **Ưu tiên** — Đưa rules quan trọng nhất vào CLAUDE.md
3. **Ví dụ code** — Rules với ✅/❌ examples hiệu quả hơn text
4. **Test** — Verify từng rule hoạt động
5. **Giảm số lượng** — Max 10 rule files, mỗi file < 100 dòng
