# Error Handling — Python/Flask

## Nguyên tắc
- **Không** nuốt lỗi im lặng — luôn log hoặc raise
- Dùng custom exception class cho operational errors
- Return response nhất quán cho API errors
- Phân biệt: operational error (expected) vs programmer error (bug)

## Custom Error Class
```python
# services/errors.py
class AppError(Exception):
    def __init__(self, message, status_code=500, code='INTERNAL_ERROR'):
        super().__init__(message)
        self.message = message
        self.status_code = status_code
        self.code = code
```

## Throwing Errors
```python
from services.errors import AppError

def get_site(site_id):
    site = db.sites.find_one({'_id': ObjectId(site_id)})
    if not site:
        raise AppError('Site not found', 404, 'SITE_NOT_FOUND')
    return site
```

## Global Error Handler
```python
# admin/app.py
@app.errorhandler(AppError)
def handle_app_error(error):
    return jsonify(
        success=False,
        error={'code': error.code, 'message': error.message}
    ), error.status_code

@app.errorhandler(Exception)
def handle_unexpected_error(error):
    app.logger.error(f'Unexpected error: {error}', exc_info=True)
    return jsonify(
        success=False,
        error={'code': 'INTERNAL_ERROR', 'message': 'An unexpected error occurred'}
    ), 500
```

## Try/Catch Pattern
```python
# ✅ Wrap external calls
try:
    result = call_ai(prompt, model='claude-sonnet')
except Exception as e:
    logger.error(f'AI call failed: {e}')
    raise AppError('AI service unavailable', 503, 'AI_ERROR')

# ❌ Catch quá rộng không log
try:
    do_something()
except:
    pass
```
