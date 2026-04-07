# Skill: Debug

## Khi nào dùng
- Test fail không rõ nguyên nhân
- Route trả về 500 error
- Agent pipeline crash giữa chừng
- Data không đúng format trong MongoDB

## Quy trình

### Bước 1: Thu thập thông tin
```bash
# Xem error message đầy đủ
python -m pytest tests/test_failing.py -v --tb=long

# Xem log output
python -m pytest tests/test_failing.py -v -s  # -s để hiện print/log
```

### Bước 2: Reproduce
- Chạy test cụ thể bị fail
- Nếu lỗi ở route: test bằng `client.get/post()` trong pytest
- Nếu lỗi ở agent: isolate agent call với mock data

### Bước 3: Phân tích nguyên nhân
```python
# Kiểm tra data trong MongoDB
db = get_db()
print(db.sites.find_one({'_id': ObjectId(site_id)}))

# Kiểm tra response
response = client.get('/api/v1/sites')
print(response.status_code, response.json)
```

### Bước 4: Fix
- Fix nguyên nhân gốc, KHÔNG fix triệu chứng
- Thêm regression test cho bug vừa fix
- Chạy toàn bộ test suite: `python -m pytest tests/ -v`

### Bước 5: Verify
```bash
# Test cụ thể pass
python -m pytest tests/test_failing.py::test_specific -v

# Toàn bộ suite vẫn pass
python -m pytest tests/ -v
```

## Common Issues (TopicForge)

### ObjectId serialization
```python
# ❌ TypeError: ObjectId is not JSON serializable
# ✅ Fix: convert to string
site['_id'] = str(site['_id'])
```

### Flask test client context
```python
# ❌ RuntimeError: Working outside of application context
# ✅ Fix: dùng app.app_context()
with app.app_context():
    db = get_db()
```

### Mock không hoạt động
```python
# ❌ Mock path sai
with patch('agents.ai_client.call_ai'):  # Sai!

# ✅ Mock tại nơi import
with patch('agents.agent3_writer.call_ai'):  # Đúng!
```
