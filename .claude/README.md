# Claude AI Configuration — Reference Template

> Bộ `.claude/` mẫu tối ưu, rút từ kinh nghiệm thực tế dự án TopicForge.
> Copy folder này vào root dự án, chỉnh sửa cho phù hợp.

## Tại sao bộ này tốt hơn?

Bộ `.claude/` gốc của TopicForge có **vấn đề nghiêm trọng**:
- 13 rule files viết cho **JS/TS** nhưng project là **Python/Flask/MongoDB**
- `tech-stack.md` dài 370 dòng — quá tốn token
- Agents mô tả team Node.js — không khớp thực tế
- Commands dùng `npm` — project không có `package.json`

Bộ mẫu này đã fix tất cả:

| Tiêu chí | Bộ cũ (gốc) | Bộ mới (mẫu) |
|----------|-------------|--------------|
| Rules | 13 files, 1,680 dòng | 8 files, ~480 dòng |
| Agents | 7 files, 1,101 dòng | 5 files, ~350 dòng |
| Commands | 3 files, 103 dòng | 4 files, ~130 dòng |
| Skills | 2 files, 112 dòng | 3 skills, ~180 dòng |
| **Tổng** | **~3,086 dòng** | **~1,200 dòng** |
| Token/session | ~25K tokens | **~10K tokens** |
| Khớp với project | ❌ Sai stack | ✅ Đúng 100% |

## Cách sử dụng

```bash
# Copy vào dự án
cp -r docs/claude-coding-guide/.claude/ .claude/

# Chỉnh sửa CLAUDE.md cho dự án của bạn
# Chỉnh sửa rules/ cho conventions của bạn
# Xóa agents/skills không cần
```

## Cấu trúc

```
.claude/
├── CLAUDE.md              # Instructions tổng quan (47 dòng)
├── settings.json          # Config (15 dòng)
├── rules/                 # 8 rules (~60 dòng/file)
│   ├── code-style.md
│   ├── naming.md
│   ├── security.md
│   ├── api-conventions.md
│   ├── error-handling.md
│   ├── database.md
│   ├── testing.md
│   └── git-workflow.md
├── skills/                # 3 skills
│   ├── refactoring/SKILL.md
│   ├── new-feature/SKILL.md
│   └── debug/SKILL.md
├── agents/                # 5 agents (~70 dòng/file)
│   ├── backend.md
│   ├── frontend.md
│   ├── qa.md
│   ├── architect.md
│   └── reviewer.md
└── commands/              # 4 commands (~30 dòng/file)
    ├── fix-issue.md
    ├── review.md
    ├── status.md
    └── new-endpoint.md
```
