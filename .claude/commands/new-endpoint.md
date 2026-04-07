---
name: new-endpoint
description: Tạo Flask API endpoint mới với đầy đủ route + test
arguments:
  - name: resource
    description: Tên resource (ví dụ "topical-maps", "articles")
    required: true
  - name: methods
    description: HTTP methods cần tạo (ví dụ "CRUD" hoặc "GET,POST")
    required: false
---

# New Endpoint Command

## Quy trình
1. Tạo route file: `admin/routes/{resource}.py`
2. Tạo Blueprint với url_prefix `/api/v1/{resource}`
3. Implement methods theo `$ARGUMENTS.methods` (default: CRUD)
4. Register blueprint trong `admin/app.py`
5. Tạo test file: `tests/test_routes_{resource}.py`
6. Chạy tests: `python -m pytest tests/test_routes_{resource}.py -v`

## Template Route
```python
from flask import Blueprint, request, jsonify
from bson import ObjectId
from admin.db import get_db
from admin.auth import login_required

bp = Blueprint('{resource}', __name__, url_prefix='/api/v1/{resource}')

@bp.route('', methods=['GET'])
@login_required
def list_{resource}():
    db = get_db()
    page = request.args.get('page', 1, type=int)
    limit = request.args.get('limit', 20, type=int)
    items = list(db.{collection}.find().skip((page-1)*limit).limit(limit))
    total = db.{collection}.count_documents({})
    return jsonify(success=True, data=items, pagination={
        'page': page, 'limit': limit, 'total': total
    }), 200
```

## Checklist
- [ ] Blueprint registered in `app.py`
- [ ] `@login_required` on all routes
- [ ] Input validation
- [ ] ObjectId validation
- [ ] Error responses consistent
- [ ] Tests for all methods
