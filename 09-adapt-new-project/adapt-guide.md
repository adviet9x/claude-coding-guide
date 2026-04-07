# Hướng Dẫn Áp Dụng .claude/ Cho Dự Án Mới

> Quy trình để Claude tự viết lại toàn bộ `.claude/` khi chuyển sang dự án với stack khác.

---

## Khi Nào Cần Viết Lại?

| Tình huống | Cần làm gì |
|-----------|-----------|
| Stack hoàn toàn khác (Python → Go, Node.js) | Viết lại hết (Bước 1) |
| Stack gần giống (Flask → FastAPI) | Chỉ sửa rules + commands (Bước 3) |
| Thêm công nghệ (thêm Redis, Celery) | Thêm 1-2 rule files mới (Bước 3) |
| Cùng stack, khác dự án | Chỉ sửa CLAUDE.md + commands (Bước 3) |

---

## Bước 1: Khởi Tạo — Viết Lại Toàn Bộ

Copy prompt dưới đây, thay `[...]` bằng thông tin dự án thật:

```
Tôi có bộ .claude/ mẫu tại repo: https://github.com/adviet9x/claude-coding-guide

Hãy đọc toàn bộ bộ .claude/ mẫu trong repo đó (CLAUDE.md, rules/, agents/,
commands/, skills/, settings.json), nắm rõ FORMAT và STRUCTURE.

Dự án mới của tôi:
- Tên: [Tên dự án — ví dụ: MyShop]
- Mô tả: [1-2 câu — ví dụ: Sàn thương mại điện tử B2C]
- Stack: [ví dụ: TypeScript + Next.js 14 + PostgreSQL + Prisma + Redis]
- Port dev: [ví dụ: 3000]
- Lệnh chạy dev: [ví dụ: npm run dev]
- Lệnh chạy test: [ví dụ: npm test]
- Lệnh build: [ví dụ: npm run build]
- Thư mục chính: [ví dụ: src/app/, src/lib/, src/components/, prisma/, tests/]
- Database: [ví dụ: PostgreSQL, tên DB: myshop_dev]
- ORM: [ví dụ: Prisma]
- Auth: [ví dụ: NextAuth.js]
- Deploy: [ví dụ: Vercel]

Critical Rules của dự án:
1. [ví dụ: KHÔNG sửa file prisma/schema.prisma mà không hỏi trước]
2. [ví dụ: LUÔN dùng Server Components, chỉ Client Components khi cần interactivity]
3. [ví dụ: Mọi API routes đặt trong src/app/api/]

Hãy viết lại TOÀN BỘ .claude/ cho dự án mới:

1. CLAUDE.md — project overview, commands, critical rules, structure
2. rules/ — 8 files (code-style, naming, security, api-conventions,
   error-handling, database, testing, git-workflow) viết cho [stack mới]
3. agents/ — 5 agents (backend, frontend, qa, architect, reviewer)
   điều chỉnh expertise cho [stack mới]
4. commands/ — 4 commands (fix-issue, new-endpoint, review, status)
   dùng đúng lệnh của [stack mới]
5. skills/ — 3 skills (debug, new-feature, refactoring)
   đúng workflow của [stack mới]
6. settings.json — giữ nguyên

Yêu cầu:
- Giữ nguyên FORMAT và STRUCTURE của bộ mẫu, chỉ thay NỘI DUNG
- Mỗi rule file < 80 dòng
- CLAUDE.md < 60 dòng
- KHÔNG còn dấu vết Python/Flask/MongoDB trong file nào
- Tạo từng file, bắt đầu từ CLAUDE.md
```

---

## Bước 2: Review Và Sửa Lỗi

Sau khi Claude tạo xong, dùng prompt này để review:

```
Review lại toàn bộ .claude/ vừa tạo. Kiểm tra:

1. Có file nào còn nhắc Python/Flask/MongoDB (stack cũ) không?
2. Rules có đúng convention chuẩn của [stack mới] không?
   - code-style.md: format, linting rules đúng?
   - naming.md: convention đúng? (camelCase/PascalCase/snake_case)
   - api-conventions.md: endpoint patterns đúng framework?
   - database.md: query patterns đúng ORM/driver?
   - testing.md: test framework, patterns đúng?
3. Commands có dùng đúng lệnh CLI không? (npm/yarn/pnpm/go/cargo...)
4. Agents có expertise phù hợp không?
5. Skills có quy trình đúng workflow mới không?

Liệt kê tất cả issues tìm thấy, rồi sửa từng cái.
```

---

## Bước 3: Sửa Từng Phần (Khi Chỉ Cần Thay Đổi Nhỏ)

### Chỉ viết lại rules

```
Đọc toàn bộ .claude/rules/ hiện tại (đang viết cho Python/Flask/MongoDB).
Viết lại 8 rule files cho [TypeScript + Next.js + Prisma].
Giữ nguyên format (tiêu đề, ✅/❌ examples, code blocks), chỉ đổi nội dung.
Mỗi file < 80 dòng.
```

### Chỉ viết lại CLAUDE.md

```
Đọc .claude/CLAUDE.md hiện tại.
Viết lại cho dự án [tên], stack [stack].
Giữ nguyên structure (sections: Overview, Architecture, Directories, Commands,
Critical Rules, Memory Usage, .env Variables).
< 60 dòng.
```

### Chỉ viết lại commands

```
Đọc .claude/commands/ hiện tại.
Viết lại 4 command files cho [stack mới]:
- fix-issue.md: dùng [test framework mới] thay pytest
- new-endpoint.md: đúng pattern [framework mới]
- review.md: checklist phù hợp [stack mới]
- status.md: đúng lệnh CLI mới
```

### Chỉ viết lại agents

```
Đọc .claude/agents/ hiện tại.
Viết lại 5 agents, giữ format YAML frontmatter.
Đổi expertise cho đúng stack [stack mới].
Backend agent biết [framework], Frontend biết [UI lib],
QA biết [test framework], Architect biết [infrastructure].
```

### Thêm rule mới cho công nghệ mới

```
Dự án vừa thêm [Redis / Celery / GraphQL / Docker / ...].
Tạo thêm file .claude/rules/[tên-tech].md với:
- Best practices cho [tech] trong context dự án này
- ✅/❌ code examples
- Thông tin tích hợp với stack hiện tại
< 80 dòng, theo format các rule files khác.
```

---

## Ví Dụ: Chuyển Từ Python/Flask Sang Next.js

### Input cho Bước 1

```
Dự án mới của tôi:
- Tên: ShopNext
- Mô tả: E-commerce platform với admin dashboard
- Stack: TypeScript + Next.js 14 (App Router) + PostgreSQL + Prisma + Redis
- Port dev: 3000
- Lệnh chạy dev: npm run dev
- Lệnh chạy test: npm test (vitest)
- Lệnh build: npm run build
- Thư mục chính: src/app/, src/lib/, src/components/, prisma/, tests/
- Database: PostgreSQL, tên DB: shopnext_dev
- ORM: Prisma
- Auth: NextAuth.js v5
- Deploy: Vercel

Critical Rules:
1. KHÔNG sửa prisma/schema.prisma mà không hỏi trước
2. LUÔN dùng Server Components, chỉ 'use client' khi cần interactivity
3. API routes trong src/app/api/, dùng Route Handlers
4. LUÔN chạy tests sau mỗi thay đổi
5. Style dùng Tailwind CSS, KHÔNG inline styles
```

### Kết quả mong đợi

Claude sẽ tạo:

```
.claude/
├── CLAUDE.md              # Next.js project info, npm commands
├── settings.json          # Giữ nguyên
├── rules/
│   ├── code-style.md      # TypeScript conventions, ESLint
│   ├── naming.md          # camelCase, PascalCase components
│   ├── security.md        # XSS, CSRF, env vars, Prisma injection
│   ├── api-conventions.md # Route Handlers, REST patterns
│   ├── error-handling.md  # try/catch, error.tsx, not-found.tsx
│   ├── database.md        # Prisma patterns, migrations
│   ├── testing.md         # Vitest, React Testing Library
│   └── git-workflow.md    # Giữ nguyên (universal)
├── agents/
│   ├── backend.md         # Node.js, Prisma, API expertise
│   ├── frontend.md        # React, Next.js, Tailwind
│   ├── qa.md              # Vitest, Playwright, RTL
│   ├── architect.md       # Next.js architecture, Vercel
│   └── reviewer.md        # TypeScript review checklist
├── commands/
│   ├── fix-issue.md       # npm test, debug workflow
│   ├── new-endpoint.md    # Route Handler template
│   ├── review.md          # TypeScript review
│   └── status.md          # npm test, git status, prisma
└── skills/
    ├── debug/SKILL.md     # Next.js debug workflow
    ├── new-feature/SKILL.md
    └── refactoring/SKILL.md
```

---

## Checklist Sau Khi Tạo

- [ ] CLAUDE.md chứa đúng thông tin dự án mới
- [ ] Không còn dấu vết stack cũ trong bất kỳ file nào
- [ ] Mỗi rule file < 80 dòng, có ✅/❌ examples
- [ ] Commands dùng đúng CLI tools (npm/yarn/go/cargo...)
- [ ] Agents có expertise phù hợp stack mới
- [ ] Tổng < 1,500 dòng (~12K tokens)
- [ ] Chạy thử: hỏi Claude 1 câu về dự án, xem có follow rules không
