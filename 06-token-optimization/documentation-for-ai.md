# Viết Tài Liệu Tối Ưu Cho AI

> Tài liệu viết cho CON NGƯỜI khác với tài liệu viết cho AI.
> AI cần: ngắn gọn, có cấu trúc, dễ parse, factual.

---

## 1. Nguyên Tắc

| Con người thích | AI cần |
|----------------|--------|
| Đoạn văn giải thích dài | Bullet points ngắn |
| Câu chuyện, context | Facts, data |
| Hình ảnh, diagrams | ASCII art, tables |
| Links đến tài liệu ngoài | Inline content |
| Indent sâu, nested | Flat structure |

---

## 2. Format Tối Ưu

### Tables > Paragraphs
```markdown
# ❌ Cho AI đọc
Dự án dùng Python 3.12 với Flask framework. Database là MongoDB,
chạy trên port 27017. Admin panel chạy trên port 5050.
Test framework là pytest với 152 test cases.

# ✅ Cho AI đọc
| Key | Value |
|-----|-------|
| Language | Python 3.12 |
| Framework | Flask |
| DB | MongoDB :27017 |
| Port | 5050 |
| Tests | pytest (152 tests) |
```

### Bullet points > Paragraphs
```markdown
# ❌
Khi tạo route mới, bạn cần tạo một blueprint, sau đó
register nó trong app.py. Route handler nhận request,
validate input, gọi service layer...

# ✅
## Route Pattern
1. Tạo Blueprint trong `admin/routes/{name}.py`
2. Register trong `admin/app.py`
3. Handler: validate → service call → response
```

### Code blocks > Description
```markdown
# ❌
Để chạy tests, mở terminal, navigate đến thư mục dự án,
rồi gõ lệnh pytest với flag -v...

# ✅
\`\`\`bash
cd topicforge
pytest tests/ -v
\`\`\`
```

---

## 3. Cấu Trúc docs/ Cho AI

```
docs/
├── PROJECT.md           # Tổng quan (AI đọc đầu tiên)
├── FILE_MAP.md          # Bản đồ file (tìm nhanh)
├── ARCHITECTURE.md      # Kiến trúc (hiểu flow)
├── DECISIONS.md         # Quyết định kỹ thuật (tại sao)
└── CHANGELOG.md         # Lịch sử thay đổi (tracking)
```

### PROJECT.md (< 100 dòng)
```markdown
# [Tên] — AI Context

## Stack: Python 3.12 + Flask + MongoDB
## Port: 5050 | DB: topicforge

## Entry Points
- CLI: main.py
- Web: admin/app.py

## Run
\`\`\`bash
python admin/app.py      # Web admin
python main.py            # CLI pipeline
pytest tests/ -v          # Tests
\`\`\`

## Key Files
→ xem FILE_MAP.md
```

### FILE_MAP.md (< 150 dòng)
```markdown
# File Map

## Core (read these first)
| File | Lines | What |
|------|-------|------|
| main.py | 300 | CLI entry, thin wrapper |
| settings.py | 85 | All config constants |

## Agents
| File | Lines | What |
|------|-------|------|
| agents/agent_pipeline.py | 823 | Pipeline v2 orchestrator |
| agents/pipeline_config.py | 110 | Pipeline constants |
| agents_legacy.py | 4000 | Legacy — DO NOT MODIFY |

## Admin
| File | Lines | What |
|------|-------|------|
| admin/app.py | 120 | Flask app factory |
| admin/routes/*.py | 16 files | Route handlers |
```

---

## 4. Viết CHANGELOG Cho AI

```markdown
# CHANGELOG

## 2026-04-07
### Changed
- agent_pipeline.py: 1074 → 823 lines (extracted config)
- NEW: agents/pipeline_config.py (110 lines)

## 2026-04-05
### Changed  
- main.py: 870 → 300 lines (extracted to cli/)
- NEW: cli/ package (9 modules)

## 2026-04-03
### Added
- Prompt edit UI (admin/routes/prompts.py)
- File caching for prompt folders
```

---

## 5. Checklist Tài Liệu AI-Friendly

- [ ] Dùng **tables** thay paragraphs khi có thể
- [ ] Dùng **bullet points** thay đoạn văn
- [ ] **Code blocks** cho commands và patterns
- [ ] Mỗi file **< 150 dòng**
- [ ] **Không narrative** — facts only
- [ ] **Cập nhật** khi codebase thay đổi
- [ ] **No broken links** — inline content preferred
