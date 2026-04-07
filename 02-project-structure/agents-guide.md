# Tạo Agents — Sub-Agent Chuyên Biệt

> Agents là các "vai trò" chuyên biệt mà Claude có thể nhập vai.
> Mỗi agent có chuyên môn riêng, công cụ riêng, và quy tắc riêng.

---

## 1. Agents Là Gì?

```
.claude/agents/
├── frontend.md         # Frontend developer
├── backend.md          # Backend developer
├── qa.md               # QA Engineer
├── architect.md        # Systems Architect
├── project-manager.md  # Project Manager
├── ui-ux-designer.md   # UI/UX Designer
└── copywriter-seo.md   # Copywriter & SEO
```

- Agent = Claude + vai trò chuyên biệt
- User hoặc main agent gọi sub-agent khi cần
- Mỗi agent có toolset và rules riêng

---

## 2. Cấu Trúc Agent File

```markdown
---
name: backend-developer
description: >
  Expert backend developer specializing in Node.js, Express, 
  PostgreSQL, Redis, and API design.
tools:
  - run_in_terminal
  - read_file
  - replace_string_in_file
  - grep_search
  - semantic_search
---

# Backend Developer Agent

## Role
Bạn là backend developer senior, chuyên gia về:
- API design (REST)
- Database (PostgreSQL + Prisma)
- Caching (Redis)
- Background jobs (BullMQ)
- Testing (Vitest)

## Responsibilities
1. Thiết kế và implement API endpoints
2. Viết database queries tối ưu
3. Implement business logic trong service layer
4. Viết unit tests cho services

## Rules
- Follow REST conventions (xem .claude/rules/api-conventions.md)
- Layered architecture: Route → Controller → Service → Repository
- Async/await bắt buộc
- Error handling with AppError class

## Workflow
1. Đọc hiểu yêu cầu
2. Kiểm tra code hiện tại liên quan
3. Implement theo layers (model → service → controller → route)
4. Viết test
5. Chạy test và verify

## Output Format
- Code changes với explanation
- Test results
- API documentation nếu endpoint mới
```

---

## 3. Các Agent Phổ Biến

### Frontend Developer
```markdown
---
name: frontend-developer
description: Expert frontend developer for React, Next.js, TypeScript, and UI
---

## Focus
- Components (React + TypeScript)
- Pages & routing
- State management (Zustand)
- Data fetching (TanStack Query)
- Styling (Tailwind CSS)
- Performance optimization
```

### QA Engineer
```markdown
---
name: qa-engineer
description: Senior QA engineer for test strategy, automation, and quality assurance
---

## Focus
- Test planning & strategy
- Unit tests (Vitest/Pytest)
- Integration tests
- E2E tests (Playwright)
- Coverage analysis
- Bug reproduction & verification
```

### Systems Architect
```markdown
---
name: systems-architect
description: Senior architect for system design, scalability, and technical decisions
---

## Focus
- Architecture decisions (ADRs)
- Database schema design
- API design review
- Performance & scalability
- Technology evaluation
- Documentation
```

### Project Manager
```markdown
---
name: project-manager
description: Project manager for planning, tracking, and coordination
---

## Focus
- User stories & acceptance criteria
- Sprint planning
- Task breakdown
- Progress tracking
- Risk assessment
- Status reports
```

---

## 4. Khi Nào Dùng Agents

| Tình huống | Agent phù hợp |
|-----------|---------------|
| Tạo API endpoint | backend-developer |
| Tạo UI component | frontend-developer |
| Viết test plan | qa-engineer |
| Thiết kế database schema | systems-architect |
| Lên kế hoạch sprint | project-manager |
| Review UX flow | ui-ux-designer |
| Viết SEO content | copywriter-seo |

### Cách gọi agent

#### Trong VS Code (Copilot)
```
@workspace Dùng backend-developer agent, tạo endpoint GET /api/users
```

#### Trong Claude Code
```
/agent backend-developer
Tạo endpoint GET /api/users với phân trang
```

#### Agent tự gọi sub-agent
Main agent có thể gọi sub-agent khi task cần chuyên môn:
```
→ User yêu cầu: "Tạo trang quản lý users"
→ Main agent phân tích → gọi:
  1. systems-architect: thiết kế API
  2. backend-developer: implement API
  3. frontend-developer: implement UI
  4. qa-engineer: viết tests
```

---

## 5. Tạo Agent Tùy Chỉnh

### Template
```markdown
---
name: [tên-agent]
description: [Mô tả 1-2 câu]
---

# [Tên Agent]

## Role
[Mô tả vai trò và chuyên môn]

## Responsibilities  
[Liệt kê trách nhiệm cụ thể]

## Rules
[Quy tắc riêng cho agent này]

## Workflow
[Quy trình làm việc step-by-step]

## Output Format
[Format output mong đợi]
```

### Ví dụ: DevOps Agent
```markdown
---
name: devops-engineer
description: DevOps engineer for CI/CD, Docker, monitoring, and infrastructure
---

# DevOps Engineer

## Role
Quản lý infrastructure, CI/CD, monitoring.

## Responsibilities
- Dockerfile & docker-compose
- GitHub Actions workflows
- Monitoring & alerting (Prometheus/Grafana)
- Log management
- Performance tuning

## Rules
- KHÔNG expose secrets trong Dockerfile
- Multi-stage builds bắt buộc
- Health check endpoints bắt buộc
- Log structured JSON only
```

---

## 6. Agent vs Skill vs Rule

| | Agent | Skill | Rule |
|-|-------|-------|------|
| Là gì | Vai trò | Workflow | Quy tắc |
| Khi dùng | Gọi theo yêu cầu | Auto-match | Luôn áp dụng |
| Scope | Toàn bộ task | 1 task cụ thể | Mọi code |
| Ví dụ | "Backend dev" | "Deploy process" | "Dùng camelCase" |
| File | `.md` đơn | `SKILL.md` trong folder | `.md` đơn |
| Folder | `.claude/agents/` | `.claude/skills/*/` | `.claude/rules/` |
