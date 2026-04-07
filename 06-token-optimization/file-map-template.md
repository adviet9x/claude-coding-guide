# Template: FILE_MAP.md

> Copy template này, điền thông tin dự án. Claude dùng file này để tìm code nhanh.

---

## Template

```markdown
# FILE_MAP.md — [Tên Dự Án]
> Cập nhật: [ngày]. Tổng: [X] files, [Y] LOC.

## Entry Points
| File | Purpose |
|------|---------|
| [entry1] | [mô tả] |
| [entry2] | [mô tả] |

## Core Logic
| File | Lines | Purpose | Dependencies |
|------|-------|---------|-------------|
| [file] | [N] | [mô tả] | [imports gì] |

## API / Routes
| File | Lines | Endpoints |
|------|-------|-----------|
| [file] | [N] | GET/POST /api/... |

## Services / Business Logic
| File | Lines | Purpose |
|------|-------|---------|
| [file] | [N] | [mô tả] |

## Database / Models
| File | Lines | Tables/Collections |
|------|-------|--------------------|
| [file] | [N] | [tên bảng] |

## Config
| File | Lines | Contains |
|------|-------|----------|
| [file] | [N] | [mô tả] |

## Tests
| File | Tests | Covers |
|------|-------|--------|
| [file] | [N] | [module nào] |

## Protected Files (DO NOT MODIFY)
- [file] — [lý do]

## Recently Changed
| File | Date | Change |
|------|------|--------|
| [file] | [date] | [mô tả] |
```

---

## Ví Dụ Thực Tế

```markdown
# FILE_MAP.md — TopicForge
> Cập nhật: 2026-04-07. Tổng: 67 files, 18,844 LOC.

## Entry Points
| File | Purpose |
|------|---------|
| main.py (300) | CLI orchestrator |
| admin/app.py (120) | Flask web admin |

## Core Logic
| File | Lines | Purpose |
|------|-------|---------|
| agents/agent_pipeline.py | 823 | Pipeline v2 — 7-step orchestrator |
| agents/pipeline_config.py | 110 | Pipeline constants & presets |
| agents_legacy.py | 4000 | Legacy pipeline — DO NOT MODIFY |

## Admin Routes
| File | Endpoints |
|------|-----------|
| admin/routes/pipeline.py | POST /run, GET /status |
| admin/routes/keywords.py | CRUD /keywords |
| admin/routes/prompts.py | CRUD /prompts |
| admin/routes/sites.py | CRUD /sites |
| admin/routes/costs.py | GET /costs |
| admin/routes/dashboard.py | GET / |

## CLI Modules
| File | Lines | Purpose |
|------|-------|---------|
| cli/state.py | 40 | Shared state |
| cli/bootstrap.py | 80 | Init & setup |
| cli/pipeline_runner.py | 90 | Run pipeline |
| cli/keyword_tracker.py | 60 | Track keywords |

## Config
| File | Contains |
|------|----------|
| settings.py (85) | All config constants |
| .env | Secrets (gitignored) |

## Tests
| File | Tests |
|------|-------|
| tests/ (total) | 152 tests, all pass |

## Protected Files
- agents_legacy.py — backward compat, 4000 LOC
- admin/db.py — shared DB connection

## Recently Changed
| File | Date | Change |
|------|------|--------|
| agents/agent_pipeline.py | 2026-04-07 | 1074→823 (extracted config) |
| agents/pipeline_config.py | 2026-04-07 | NEW (extracted constants) |
| main.py | 2026-04-05 | 870→300 (extracted to cli/) |
```

---

## Tips

- Cập nhật FILE_MAP sau mỗi refactor lớn
- Ưu tiên files Claude thường cần đọc
- Giữ < 150 dòng (nếu dự án lớn, chỉ list core files)
- Có thể lưu trong `docs/` hoặc repo memory
