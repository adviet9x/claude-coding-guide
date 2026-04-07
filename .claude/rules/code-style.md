# Code Style — Python

## Formatting
- **PEP 8** — tuân thủ 100%
- Indent: **4 spaces** (không dùng tab)
- Max line length: **100 ký tự**
- Dùng **single quotes** cho strings thông thường
- Dùng **f-strings** cho interpolation

## Naming
```python
# Variables, functions: snake_case
user_profile = {}
def get_user_by_id(user_id): ...

# Classes: PascalCase
class UserService: ...
class TopicalMapBuilder: ...

# Constants: UPPER_SNAKE_CASE
MAX_RETRY_COUNT = 3
API_BASE_URL = 'https://api.example.com'

# Files: snake_case.py
# user_service.py, auth_middleware.py

# Private: prefix underscore
def _validate_input(data): ...
_internal_cache = {}
```

## Functions
```python
# ✅ Docstring cho public functions
def process_article(article_id, options=None):
    """Process article through AI pipeline."""
    ...

# ✅ Type hints cho tham số quan trọng
def find_user(email: str) -> dict | None: ...

# ❌ Hàm > 30 dòng → tách ra
# ❌ > 3 tham số → dùng dict hoặc dataclass
```

## Imports
```python
# Thứ tự: 1. stdlib  2. third-party  3. local
import os
from datetime import datetime

from flask import Blueprint, request, jsonify
from bson import ObjectId

from admin.db import get_db
from services.ai_client import call_ai
```

## Comments
```python
# ✅ Giải thích WHY, không phải WHAT
# Retry 3 lần vì Claude API hay timeout khi peak hours
MAX_RETRIES = 3

# ❌ Comment thừa
# Gán x = 5
x = 5
```
