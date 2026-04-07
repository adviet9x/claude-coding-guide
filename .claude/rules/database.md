# Database — MongoDB/PyMongo

## Connection
```python
# admin/db.py — Singleton pattern
from pymongo import MongoClient
import os

_client = None

def get_db():
    global _client
    if _client is None:
        _client = MongoClient(os.environ.get('MONGO_URI', 'mongodb://localhost:27017'))
    return _client[os.environ.get('MONGO_DB', 'topicforge')]
```

## Query Best Practices
```python
db = get_db()

# ✅ Chỉ lấy fields cần thiết (projection)
user = db.users.find_one({'_id': uid}, {'email': 1, 'name': 1})

# ❌ Lấy hết (tốn bộ nhớ)
user = db.users.find_one({'_id': uid})

# ✅ Pagination
sites = list(db.sites.find()
    .sort('created_at', -1)
    .skip((page - 1) * limit)
    .limit(limit))

# ✅ Count riêng cho pagination
total = db.sites.count_documents({})
```

## Indexes
```python
# Tạo indexes khi khởi tạo app
db.articles.create_index('site_id')
db.articles.create_index([('status', 1), ('created_at', -1)])
db.users.create_index('email', unique=True)
```

## Transactions (Replica Set required)
```python
# ✅ Dùng session cho atomic operations
with client.start_session() as session:
    with session.start_transaction():
        db.orders.insert_one(order_data, session=session)
        db.inventory.update_one(
            {'_id': product_id},
            {'$inc': {'stock': -1}},
            session=session
        )
```

## ObjectId Handling
```python
from bson import ObjectId
import json

# ✅ Validate trước khi query
if not ObjectId.is_valid(site_id):
    return jsonify(error='Invalid ID'), 400

# ✅ Serialize cho JSON response
class MongoJSONEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, ObjectId):
            return str(obj)
        if isinstance(obj, datetime):
            return obj.isoformat()
        return super().default(obj)
```

## Naming
- Collections: **snake_case**, plural: `topical_maps`, `run_history`
- Fields: **snake_case**: `created_at`, `site_id`, `is_active`
- Indexes: `idx_{collection}_{field}`
