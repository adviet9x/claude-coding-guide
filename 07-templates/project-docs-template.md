# Template: Project Documentation

> Templates cho docs/ folder — tạo tài liệu AI-friendly cho dự án.

---

## 1. docs/PROJECT.md

```markdown
# [Tên Dự Án] — Project Overview

## Identity
| Key | Value |
|-----|-------|
| Name | [Tên] |
| Purpose | [1 câu] |
| Stack | [Lang] + [Framework] + [DB] |
| Port | [dev port] |
| Status | [active/maintenance] |

## Run Commands
\`\`\`bash
[lệnh chạy dev]
[lệnh chạy test]
[lệnh build]
\`\`\`

## Entry Points
| File | Purpose |
|------|---------|
| [file1] | [mô tả] |
| [file2] | [mô tả] |

## Key Dependencies
| Package | Version | Purpose |
|---------|---------|---------|
| [pkg1] | [ver] | [why] |
| [pkg2] | [ver] | [why] |
```

---

## 2. docs/ARCHITECTURE.md

```markdown
# Architecture — [Tên Dự Án]

## High-Level Flow
\`\`\`
[Sơ đồ ASCII]
User → Frontend → API → Service → DB
\`\`\`

## Layers
| Layer | Folder | Purpose |
|-------|--------|---------|
| Routes | src/routes/ | URL mapping, validation |
| Services | src/services/ | Business logic |
| Models | src/models/ | Data schemas |
| Utils | src/utils/ | Shared helpers |

## Data Flow
\`\`\`
[Request lifecycle]
1. Request → Middleware (auth, validation)
2. → Route handler
3. → Service layer (business logic)
4. → Database query
5. → Response formatting
\`\`\`

## Database Schema
\`\`\`
[ERD hoặc mô tả collections/tables chính]
users: id, email, name, role
orders: id, user_id, total, status
\`\`\`

## External Services
| Service | Purpose | Config |
|---------|---------|--------|
| [service1] | [why] | [env var] |
```

---

## 3. docs/DECISIONS.md

```markdown
# Technical Decisions

## [Date] — [Tên quyết định]
- **Context**: [Tại sao cần quyết định]
- **Decision**: [Quyết định gì]
- **Alternatives**: [Đã xem xét gì khác]
- **Consequence**: [Hệ quả]

## [Date] — [Tên quyết định 2]
- **Context**: [...]
- **Decision**: [...]
```

---

## 4. docs/CHANGELOG.md

```markdown
# Changelog

## [Date]
### Added
- [Tính năng mới]

### Changed
- [Thay đổi code]
- [file] ([old] → [new] lines): [mô tả]

### Fixed
- [Bug fix]

### Removed
- [Xóa gì]
```

---

## Tips

- Tất cả files **< 150 dòng**
- Dùng **tables** thay paragraphs
- **Cập nhật** sau mỗi thay đổi lớn
- Claude đọc docs/ khi cần context → tiết kiệm token
- Không duplicate info từ CLAUDE.md
