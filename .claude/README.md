# Claude AI Configuration — Reference Template

> Bộ `.claude/` mẫu tối ưu cho dự án Python/Flask/MongoDB.
> Copy folder này vào root dự án, chỉnh sửa cho phù hợp.

## Tại sao dùng bộ này?

Khi dùng Claude AI hỗ trợ code, bộ `.claude/` cấu hình tốt sẽ giúp:
- Claude **hiểu đúng** tech stack và conventions của dự án
- **Tiết kiệm token** — rules ngắn gọn, chỉ chứa thông tin cần thiết
- **Output chính xác** — agents/skills khớp với workflow thực tế

Bộ mẫu này được thiết kế theo nguyên tắc:
- Rules viết cho **đúng stack** (Python/Flask/MongoDB)
- Mỗi file **< 80 dòng** — tối ưu token
- Agents phân vai rõ ràng, không trùng lặp

### Thống kê

| Thành phần | Số lượng | Dung lượng |
|-----------|---------|-----------|
| Rules | 8 files | ~480 dòng |
| Agents | 5 files | ~350 dòng |
| Commands | 4 files | ~130 dòng |
| Skills | 3 skills | ~180 dòng |
| **Tổng** | **20 files** | **~1,200 dòng (~10K tokens)** |

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
