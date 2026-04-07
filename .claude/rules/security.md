# Security Rules

## CRITICAL — Không bao giờ vi phạm
- **Không** hardcode secrets, API keys, passwords trong source code
- **Không** commit `.env` vào git
- **Không** log sensitive data (passwords, tokens, PII)
- **Không** dùng `eval()` hoặc `exec()` với user input
- **Luôn** validate và sanitize tất cả user input

## Environment Variables
```python
# ✅ Dùng env vars cho secrets
import os
db_password = os.environ.get('DB_PASSWORD')
api_key = os.environ.get('ANTHROPIC_API_KEY')

# ❌ Không hardcode
api_key = 'sk-ant-xxxxx'
```

## Input Validation
```python
# ✅ Validate dữ liệu đầu vào
from bson import ObjectId

def get_site(site_id):
    if not ObjectId.is_valid(site_id):
        return jsonify(success=False, error='Invalid ID'), 400
    site = db.sites.find_one({'_id': ObjectId(site_id)})
    ...

# ✅ Sanitize HTML
import bleach
clean_content = bleach.clean(user_input, tags=['p', 'b', 'i', 'a'])
```

## Authentication
```python
# ✅ Hash passwords với bcrypt
from werkzeug.security import generate_password_hash, check_password_hash
hashed = generate_password_hash(password)

# ✅ Session-based auth cho Flask admin
@login_required
def admin_dashboard(): ...
```

## MongoDB Injection Prevention
```python
# ✅ Dùng PyMongo parameterized queries
db.users.find_one({'email': email})

# ❌ KHÔNG string concatenation
db.command(f"find users where email = '{email}'")

# ✅ Validate type trước khi query
if not isinstance(email, str):
    raise ValueError('Invalid email type')
```

## HTTP Security
```python
# Flask security headers
from flask_talisman import Talisman
Talisman(app)

# CORS
from flask_cors import CORS
CORS(app, origins=os.environ.get('ALLOWED_ORIGINS', '').split(','))
```
