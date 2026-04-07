# Template: SKILL.md

> Dùng template này để tạo skills trong `.claude/skills/[skill-name]/SKILL.md`.

---

## Template

```markdown
---
name: [skill-name]
description: >
  [Mô tả 1-2 câu — Claude dùng mô tả này 
  để quyết định có kích hoạt skill không]
applyTo: "[glob pattern]"
---

# [Skill Name]

## Trigger
Kích hoạt khi user yêu cầu: [liệt kê keywords/phrases]

## Pre-conditions
- [ ] [Điều kiện 1 cần đạt trước khi bắt đầu]
- [ ] [Điều kiện 2]

## Steps

### Step 1: [Tên bước]
1. [Hành động cụ thể]
2. [Hành động cụ thể]

### Step 2: [Tên bước]
1. [Hành động cụ thể]
2. [Hành động cụ thể]

### Step 3: [Tên bước]
1. [Hành động cụ thể]
2. [Hành động cụ thể]

## Post-conditions
- [ ] [Kiểm tra kết quả 1]
- [ ] [Kiểm tra kết quả 2]

## Error Handling
- Nếu [lỗi X] → [hành động]
- Nếu [lỗi Y] → [hành động]

## Example
Input: [ví dụ input]
Output: [ví dụ output]
```

---

## applyTo Patterns

| Pattern | Áp dụng cho |
|---------|------------|
| `"**"` | Tất cả files |
| `"src/**"` | Files trong src/ |
| `"**/*.py"` | Tất cả Python files |
| `"tests/**"` | Files trong tests/ |
| `"*.md"` | Markdown files ở root |
| `"src/api/**"` | API code only |

---

## Tips
- Description phải rõ ràng — Claude match skill bằng description
- Steps phải cụ thể — Claude thực thi step-by-step
- Có error handling — khi nào dừng, khi nào retry
- Giữ < 200 dòng
