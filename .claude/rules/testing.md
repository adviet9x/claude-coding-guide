# Testing — pytest

## Cấu trúc
```
tests/
├── conftest.py              # Shared fixtures
├── test_routes_sites.py     # Route tests
├── test_routes_keywords.py
├── test_services_ai.py      # Service tests
├── test_agents_writer.py    # Agent tests
└── test_utils.py            # Utility tests
```

## Conventions
- File: `test_{module}.py`
- Function: `test_{action}_{expected_result}()`
- Dùng fixtures cho setup/teardown
- Mock external services (AI, WP, SerpAPI)

## Fixture Pattern
```python
# tests/conftest.py
import pytest
from admin.app import create_app
from admin.db import get_db

@pytest.fixture
def app():
    app = create_app({'TESTING': True, 'MONGO_DB': 'topicforge_test'})
    yield app

@pytest.fixture
def client(app):
    return app.test_client()

@pytest.fixture
def db(app):
    with app.app_context():
        database = get_db()
        yield database
        # Cleanup
        for col in database.list_collection_names():
            database[col].drop()
```

## Test Examples
```python
# ✅ Route test
def test_list_sites_returns_200(client, db):
    db.sites.insert_one({'name': 'Test Site', 'url': 'https://test.com'})
    response = client.get('/api/v1/sites')
    assert response.status_code == 200
    assert response.json['success'] is True
    assert len(response.json['data']) == 1

# ✅ Error case
def test_get_site_invalid_id_returns_400(client):
    response = client.get('/api/v1/sites/invalid-id')
    assert response.status_code == 400

# ✅ Mock external service
from unittest.mock import patch

def test_agent_calls_ai(db):
    with patch('services.ai_client.call_ai') as mock_ai:
        mock_ai.return_value = 'Generated content'
        result = run_agent(keyword='test')
        mock_ai.assert_called_once()
        assert 'Generated content' in result
```

## Commands
```bash
python -m pytest tests/ -v              # All tests
python -m pytest tests/ -x              # Stop on first fail
python -m pytest tests/ -k "test_site"  # Filter by name
python -m pytest tests/ --cov=admin     # Coverage report
```
