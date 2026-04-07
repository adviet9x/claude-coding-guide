# Skill: New Feature

## Khi nào dùng
- Thêm tính năng mới (route, agent, service)
- Tạo collection MongoDB mới
- Thêm UI page/component mới

## Quy trình

### Bước 1: Hiểu yêu cầu
- Feature này thuộc layer nào? (route / service / agent)
- Cần thêm collection MongoDB mới không?
- Cần thêm route / template mới không?
- Ảnh hưởng đến code hiện tại không?

### Bước 2: Tạo file structure
```
# Ví dụ: thêm Topical Map feature
agents/agent1_topical_map.py     # Agent logic
admin/routes/topical_map.py      # Flask routes
admin/templates/topical-map/     # Jinja2 templates
prompts/topical_authority/       # AI prompts
tests/test_topical_map.py        # Tests
```

### Bước 3: Implement bottom-up
1. **Database**: Tạo collection schema, indexes
2. **Service/Agent**: Business logic
3. **Route**: Flask blueprint + API endpoints
4. **Template**: UI (nếu cần)
5. **Tests**: Unit + integration tests
6. **Register**: Thêm blueprint vào `admin/app.py`

### Bước 4: Register blueprint
```python
# admin/app.py
from admin.routes.topical_map import bp as topical_map_bp
app.register_blueprint(topical_map_bp)
```

### Bước 5: Verify
```bash
python -m pytest tests/ -v  # All tests pass
python -m admin.app          # App starts without errors
```

## Checklist
- [ ] Route có `@login_required` (nếu cần auth)?
- [ ] Input validation cho tất cả user input?
- [ ] Error handling cho external calls?
- [ ] Tests cover happy path + error cases?
- [ ] Blueprint registered trong `app.py`?
- [ ] Template extends `base.html`?
