# API Conventions — Flask REST

## URL Structure
- Kebab-case: `/api/v1/topical-maps`
- Plural nouns: `/api/v1/sites`, `/api/v1/articles`
- Nested: `/api/v1/sites/<site_id>/articles`

## HTTP Methods & Status Codes
| Method | Dùng khi | Status |
|--------|---------|--------|
| GET | Đọc resource | 200 |
| POST | Tạo mới | 201 |
| PUT/PATCH | Cập nhật | 200 |
| DELETE | Xóa | 204 |

## Response Format
```python
# ✅ Success
return jsonify(success=True, data=result), 200

# ✅ Error
return jsonify(success=False, error={
    'code': 'VALIDATION_ERROR',
    'message': 'Email is required'
}), 422

# ✅ Paginated list
return jsonify(
    success=True,
    data=items,
    pagination={'page': page, 'limit': limit, 'total': total}
), 200
```

## Route Pattern
```python
from flask import Blueprint, request, jsonify
from admin.db import get_db

bp = Blueprint('sites', __name__, url_prefix='/api/v1/sites')

@bp.route('', methods=['GET'])
@login_required
def list_sites():
    """GET /api/v1/sites — List all sites with pagination."""
    db = get_db()
    page = request.args.get('page', 1, type=int)
    limit = request.args.get('limit', 20, type=int)
    skip = (page - 1) * limit

    sites = list(db.sites.find().skip(skip).limit(limit))
    total = db.sites.count_documents({})

    return jsonify(
        success=True,
        data=sites,
        pagination={'page': page, 'limit': limit, 'total': total}
    ), 200

@bp.route('/<site_id>', methods=['GET'])
@login_required
def get_site(site_id):
    """GET /api/v1/sites/:id — Get single site."""
    if not ObjectId.is_valid(site_id):
        return jsonify(success=False, error='Invalid ID'), 400
    site = get_db().sites.find_one({'_id': ObjectId(site_id)})
    if not site:
        return jsonify(success=False, error='Not found'), 404
    return jsonify(success=True, data=site), 200
```
