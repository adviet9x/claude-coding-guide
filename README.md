# 📘 Hướng Dẫn Code Với Claude AI

> Tài liệu toàn diện để làm việc hiệu quả với Claude AI trong mọi dự án code.
> Áp dụng cho VS Code + GitHub Copilot (Claude), Claude Code, và các IDE tích hợp Claude.

---

## 📂 Mục Lục

### 1. [Bắt Đầu](01-getting-started/)
- [Cài đặt môi trường](01-getting-started/setup-environment.md)
- [Cấu hình dự án cho Claude](01-getting-started/project-configuration.md)
- [Phiên làm việc đầu tiên](01-getting-started/first-session.md)

### 2. [Cấu Trúc Dự Án](02-project-structure/)
- [Viết CLAUDE.md hiệu quả](02-project-structure/claude-md-guide.md)
- [Tạo Rules (quy tắc bắt buộc)](02-project-structure/rules-guide.md)
- [Tạo Skills (kỹ năng chuyên biệt)](02-project-structure/skills-guide.md)
- [Tạo Agents (sub-agent chuyên biệt)](02-project-structure/agents-guide.md)
- [Tạo Commands (lệnh tái sử dụng)](02-project-structure/commands-guide.md)

### 3. [Kỹ Thuật Prompting](03-prompting/)
- [Viết prompt hiệu quả](03-prompting/effective-prompts.md)
- [Quản lý context & token](03-prompting/context-management.md)
- [Các pattern prompt phổ biến](03-prompting/prompt-patterns.md)
- [Anti-patterns — Những gì KHÔNG nên làm](03-prompting/anti-patterns.md)

### 4. [Quy Trình Làm Việc](04-workflows/)
- [Xây dựng tính năng mới](04-workflows/new-feature.md)
- [Sửa lỗi & debug](04-workflows/bug-fixing.md)
- [Refactoring code](04-workflows/refactoring.md)
- [Code review](04-workflows/code-review.md)
- [Viết test](04-workflows/testing.md)
- [Deployment](04-workflows/deployment.md)

### 5. [Hệ Thống Memory](05-memory-system/)
- [Tổng quan memory](05-memory-system/memory-overview.md)
- [User Memory — ghi nhớ cá nhân](05-memory-system/user-memory.md)
- [Repo Memory — ghi nhớ dự án](05-memory-system/repo-memory.md)
- [Session Memory — ghi nhớ phiên](05-memory-system/session-memory.md)
- [Chiến lược tối ưu memory](05-memory-system/memory-strategies.md)

### 6. [Tối Ưu Token](06-token-optimization/)
- [Hiểu về token](06-token-optimization/token-basics.md)
- [Giảm tiêu thụ token](06-token-optimization/reducing-token-usage.md)
- [Viết tài liệu tối ưu cho AI](06-token-optimization/documentation-for-ai.md)
- [Template FILE_MAP.md](06-token-optimization/file-map-template.md)

### 7. [Templates](07-templates/)
- [CLAUDE.md template](07-templates/CLAUDE-md-template.md)
- [Rule template](07-templates/rule-template.md)
- [SKILL.md template](07-templates/skill-template.md)
- [Agent template](07-templates/agent-template.md)
- [Project docs template](07-templates/project-docs-template.md)

### 8. [Xử Lý Sự Cố](08-troubleshooting/)
- [Lỗi thường gặp](08-troubleshooting/common-issues.md)
- [Debug khi Claude không tuân thủ](08-troubleshooting/debugging-agent.md)
- [FAQ — Câu hỏi thường gặp](08-troubleshooting/faq.md)

---

## 🎯 Ai nên đọc?

| Đối tượng | Bắt đầu từ |
|-----------|------------|
| Mới dùng Claude | Chương 1 → 2 → 3 |
| Đã dùng, muốn tối ưu | Chương 3 → 5 → 6 |
| Muốn setup dự án mới | Chương 2 → 7 (templates) |
| Gặp vấn đề | Chương 8 |

## ⚡ Quick Start

```bash
# 1. Tạo cấu trúc .claude/ cho dự án
mkdir -p .claude/rules .claude/skills .claude/agents .claude/commands

# 2. Tạo CLAUDE.md ở root
# → Xem template tại 07-templates/CLAUDE-md-template.md

# 3. Tạo rules cơ bản
# → Xem hướng dẫn tại 02-project-structure/rules-guide.md

# 4. Bắt đầu code với Claude!
```
