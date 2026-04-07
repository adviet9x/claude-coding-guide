# Tạo Skills — Kỹ Năng Chuyên Biệt

> Skills là các workflow phức tạp mà Claude thực hiện khi gặp task phù hợp.
> Khác với Rules (luôn áp dụng), Skills chỉ kích hoạt khi cần.

---

## 1. Skills Là Gì?

```
.claude/skills/
├── deploy/
│   └── SKILL.md           # Quy trình deploy
├── security-review/
│   └── SKILL.md           # Audit bảo mật
├── database-migration/
│   └── SKILL.md           # Tạo migration
└── api-scaffold/
    └── SKILL.md           # Scaffold API endpoint mới
```

- Mỗi skill = **1 folder** chứa `SKILL.md`
- Claude đọc SKILL.md khi task matching với skill description
- Skill chứa **workflow step-by-step** chi tiết

---

## 2. Cấu Trúc SKILL.md

```markdown
---
name: deploy
description: Automate deployment process including build, test, and release
applyTo: "**" 
---

# Deploy Skill

## Trigger
Kích hoạt khi user yêu cầu: deploy, release, build production

## Pre-conditions
- [ ] All tests pass
- [ ] No uncommitted changes
- [ ] CHANGELOG.md updated

## Steps

### Step 1: Validate
1. Run `npm test`
2. Check for uncommitted changes
3. Verify version in package.json

### Step 2: Build
1. Run `npm run build`
2. Check build output

### Step 3: Deploy
1. Push to main branch
2. Tag version: `git tag v{version}`
3. Push tags

## Post-conditions
- [ ] Deployment verified
- [ ] Monitoring checked
```

---

## 3. YAML Frontmatter

```yaml
---
name: skill-name                    # Tên ngắn gọn
description: >
  Mô tả skill. Claude dùng mô tả này 
  để quyết định có dùng skill không.
applyTo: "**"                       # Glob pattern — file nào kích hoạt
                                    # "**" = mọi file
                                    # "src/**/*.py" = chỉ Python trong src/
                                    # "tests/**" = chỉ trong tests/
---
```

---

## 4. Các Skill Phổ Biến

### a. API Scaffold
```markdown
---
name: api-scaffold
description: Scaffold a new REST API endpoint with route, controller, service, and test
applyTo: "src/**"
---

# API Scaffold Skill

## Khi nào dùng
User yêu cầu tạo API endpoint mới.

## Steps
1. **Tạo Route** — `src/routes/{resource}.js`
2. **Tạo Controller** — `src/controllers/{resource}-controller.js`  
3. **Tạo Service** — `src/services/{resource}-service.js`
4. **Tạo Test** — `tests/unit/services/{resource}-service.test.js`
5. **Register route** — thêm vào `src/routes/index.js`
6. **Validation** — thêm Zod schema

## Template cho mỗi file
[đặt code template ở đây]
```

### b. Database Migration
```markdown
---
name: database-migration
description: Create and run database migration safely
applyTo: "prisma/**"
---

# Database Migration Skill

## Steps
1. Sửa `prisma/schema.prisma`
2. Chạy `npx prisma migrate dev --name {description}`
3. Kiểm tra migration file generated
4. Update seed data nếu cần
5. Chạy test để verify
```

### c. Security Review
```markdown
---
name: security-review
description: Perform security audit of codebase
applyTo: "**"
---

# Security Review Skill

## Checklist
1. Scan for hardcoded secrets (API keys, passwords)
2. Check input validation on all endpoints
3. Verify authentication middleware
4. Check SQL injection vectors
5. Review CORS configuration
6. Check rate limiting
7. Audit npm dependencies: `npm audit`

## Output Format
| Finding | Severity | File | Line | Fix |
|---------|----------|------|------|-----|
```

### d. Refactoring Guide
```markdown
---
name: refactoring
description: Safely refactor code following test-first approach
applyTo: "src/**"
---

# Refactoring Skill

## Workflow
1. **Đọc hiểu** — đọc toàn bộ file cần refactor
2. **Chạy test** — đảm bảo test pass trước khi sửa
3. **Lên kế hoạch** — liệt kê thay đổi cụ thể
4. **Thực hiện** — sửa từng phần nhỏ
5. **Chạy test lại** — sau mỗi thay đổi
6. **Verify** — kiểm tra backward compat

## Rules
- KHÔNG đổi public API/interface
- KHÔNG sửa quá 1 concern per commit
- LUÔN giữ test pass tại mỗi bước
```

---

## 5. Viết Skill Tốt

### ✅ Nên
- Mô tả rõ **khi nào** kích hoạt
- Liệt kê **pre-conditions** (điều kiện cần)
- Steps **cụ thể**, có thể thực thi
- Có **post-conditions** (kiểm tra kết quả)
- Cho **ví dụ** input/output

### ❌ Không nên
- Quá chung chung ("code tốt hơn")
- Quá dài (> 300 dòng)
- Trùng lặp với rules
- Không có trigger rõ ràng

---

## 6. Skill vs Rule

| | Rule | Skill |
|-|------|-------|
| Khi nào áp dụng | **Luôn luôn** | Chỉ khi match |
| Nội dung | Quy tắc, convention | Workflow, process |
| Ví dụ | "Dùng camelCase" | "Cách deploy" |
| Độ dài | Ngắn (< 200 dòng) | Dài hơn (< 300 dòng) |
| Folder | `.claude/rules/` | `.claude/skills/*/` |
