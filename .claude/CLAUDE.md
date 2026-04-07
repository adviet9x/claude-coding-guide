# CLAUDE.md — Project Context

## Project Overview
- **Name**: TopicForge — Topical Authority SEO Automation Engine
- **Stack**: Python 3.10+ / Flask / MongoDB / Bootstrap 5 / Claude API
- **Purpose**: Multi-site SEO platform with 8 AI agents for content pipeline
- **Admin UI**: Flask + Jinja2 + Bootstrap 5, port 5050

## Architecture
```
Flask Admin (port 5050) → Agent Pipeline → AI Client → WordPress
                        → MongoDB (topicforge DB)
```

## Key Directories
- `admin/` — Flask app, routes, templates
- `agents/` — Modular AI agents (agent1–agent8)
- `services/` — Shared services (ai_client, wp_client, serpapi)
- `cli/` — CLI commands (run, test, seed, etc.)
- `prompts/` — AI prompt templates (.txt files)
- `tests/` — pytest test suite (152+ tests)
- `data/` — Cached keyword data

## Commands
```bash
python -m pytest tests/ -v          # Run all tests
python -m pytest tests/ -x          # Stop on first failure
python main.py run <keyword>        # Run pipeline for keyword
python -m admin.app                 # Start admin server
```

## Critical Rules
1. **Never break existing 152+ tests** — run pytest before committing
2. **Python only** — no Node.js, no npm, no TypeScript
3. **Flask + Jinja2** for UI — no React/Next.js migration
4. **MongoDB** via PyMongo — no SQL, no ORM
5. **All AI calls** through `services/ai_client.py`
6. **All WP calls** through `services/wp_client.py`
7. Follow rules in `.claude/rules/` at all times

## Memory Usage
- **Đầu session**: đọc `/memories/repo/` để nắm context dự án (project-basics, file-map, conventions)
- **Phát hiện pattern/bug mới**: lưu vào `/memories/` (user) hoặc `/memories/repo/` (project-specific)
- **Task dài (>10 messages)**: lưu progress vào `/memories/session/current-task.md`
- **Sau refactor lớn**: cập nhật `/memories/repo/file-map.md`
- **Tham khảo** `/memories/repo/file-map.md` để tìm file nhanh thay vì search lại
- **Không lưu**: secrets, code dài, thông tin tạm dùng 1 lần

## .env Variables
```
MONGO_URI, MONGO_DB, ANTHROPIC_API_KEY, WP_URL, WP_USER, WP_APP_PASSWORD
SERPAPI_KEY, ADMIN_USERNAME, ADMIN_PASSWORD, SECRET_KEY, PORT
```
