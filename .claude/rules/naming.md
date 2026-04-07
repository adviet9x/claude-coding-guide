# Naming Conventions

## Python Code
| Loại | Convention | Ví dụ |
|------|-----------|-------|
| File | snake_case.py | `agent_pipeline.py`, `wp_client.py` |
| Function | snake_case | `get_user_by_id()`, `run_pipeline()` |
| Class | PascalCase | `BaseAgent`, `TopicalMapBuilder` |
| Constant | UPPER_SNAKE | `MAX_RETRIES`, `DEFAULT_PORT` |
| Private | _prefix | `_validate()`, `_cache` |

## MongoDB
```python
# Collections: snake_case, plural
'sites', 'keywords', 'topical_maps', 'run_history'

# Fields: snake_case
'site_id', 'created_at', 'is_active', 'seo_score'

# Indexes: idx_{collection}_{field}
'idx_articles_site_id', 'idx_keywords_status'
```

## Flask Routes
```python
# Blueprint: snake_case
bp = Blueprint('topical_map', __name__)

# URLs: kebab-case, plural, versioned
'/api/v1/topical-maps'
'/api/v1/topical-maps/<map_id>/subtopics'
'/api/v1/sites/<site_id>/articles'
```

## Cache Keys (Redis/Dict)
```python
# Pattern: {app}:{version}:{entity}:{id}:{variant}
'topicforge:v1:user:123:profile'
'topicforge:v1:site:456:config'
```

## Prompt Files
```
# Folder: mục đích
prompts/topical_authority/agent1_build_map.txt
prompts/game_h5/generate_article.txt
```

## Git Branches
```
feature/topical-map-builder
fix/login-redirect-bug
hotfix/critical-security-patch
```
