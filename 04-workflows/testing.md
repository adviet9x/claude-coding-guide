# Workflow: Viết Tests

> Dùng Claude để viết tests nhanh và toàn diện.

---

## Loại Tests

```
         [E2E Tests]         ← Ít, chậm, test full flow
       [Integration Tests]   ← Vừa, test giữa các module
     [Unit Tests]            ← Nhiều, nhanh, test logic đơn lẻ
```

---

## Prompt Mẫu

### Viết unit tests
```
Viết unit tests cho [file/class/function].
Framework: [pytest / vitest / jest]
Cover:
- Happy path
- Edge cases (empty, null, boundary)
- Error cases (invalid input, not found)
```

### Viết integration tests
```
Viết integration test cho endpoint [METHOD /path].
Test:
- Success case (200/201)
- Validation error (400/422)
- Not found (404)
- Unauthorized (401)
```

### Viết regression test
```
Bug vừa fix: [mô tả].
Viết test đảm bảo bug không tái phát.
Test phải fail nếu revert fix.
```

### Check coverage
```
Kiểm tra test coverage cho [module].
File nào chưa có test?
Function nào chưa được cover?
```

---

## Test Naming

```python
# Python (pytest)
def test_find_user_by_id_returns_user_when_exists():
def test_find_user_by_id_raises_404_when_not_found():
def test_create_user_fails_with_duplicate_email():

# JavaScript (vitest/jest)
it('should return user when id exists')
it('should throw 404 when user not found')
it('should reject duplicate email')
```

Pattern: `test_[action]_[expected_result]_when_[condition]`

---

## Tips

- Yêu cầu Claude viết test **trước** code (TDD) cho logic phức tạp
- Nói rõ framework: `pytest` / `vitest` / `jest`
- Yêu cầu mock external dependencies
- Luôn chạy tests sau khi viết: `pytest` / `npm test`

---

## Xem Thêm
- [Bug Fixing](bug-fixing.md) — viết regression test khi fix bug
- [Tính Năng Mới](new-feature.md) — quy trình tạo feature có test
