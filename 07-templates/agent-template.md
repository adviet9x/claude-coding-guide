# Template: Agent File

> Dùng template này để tạo agent definitions trong `.claude/agents/`.

---

## Template

```markdown
---
name: [agent-name]
description: >
  [Mô tả 1-2 câu về chuyên môn và vai trò của agent]
tools:
  - read_file
  - replace_string_in_file
  - run_in_terminal
  - grep_search
  - semantic_search
---

# [Agent Name]

## Role
[Mô tả vai trò và chuyên môn chi tiết, 2-3 câu]

## Expertise
- [Chuyên môn 1]
- [Chuyên môn 2]
- [Chuyên môn 3]

## Responsibilities
1. [Trách nhiệm chính 1]
2. [Trách nhiệm chính 2]
3. [Trách nhiệm chính 3]

## Rules
- [Quy tắc riêng cho agent này]
- [Quy tắc 2]
- Follow [rule-file].md

## Workflow
1. [Bước 1] — [mô tả]
2. [Bước 2] — [mô tả]
3. [Bước 3] — [mô tả]
4. [Bước 4 — verify/test]

## Output Format
[Mô tả format output mong đợi]

## When NOT to Use
- [Trường hợp không phù hợp]
```

---

## Commonly Needed Agents

### Backend Developer
```yaml
name: backend-developer
description: APIs, services, database queries, background jobs
```

### Frontend Developer
```yaml
name: frontend-developer
description: React components, pages, state management, UI
```

### QA Engineer
```yaml
name: qa-engineer
description: Test plans, automated tests, coverage analysis
```

### Systems Architect
```yaml
name: systems-architect
description: System design, architecture decisions, scalability
```

### DevOps Engineer
```yaml
name: devops-engineer
description: CI/CD, Docker, monitoring, infrastructure
```

---

## Tips
- Tools list = công cụ agent được phép dùng
- Rules = quy tắc riêng + reference đến shared rules
- Workflow = quy trình chuẩn cho mọi task
- Giữ < 100 dòng per agent
