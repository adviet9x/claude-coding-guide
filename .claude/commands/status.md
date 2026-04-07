---
name: status
description: Kiểm tra trạng thái project (tests, errors, structure)
---

# Project Status Command

## Quy trình
1. Chạy test suite:
   ```bash
   python -m pytest tests/ -v --tb=short 2>&1 | tail -20
   ```
2. Kiểm tra lỗi syntax:
   ```bash
   python -m py_compile admin/app.py
   ```
3. Đếm files và lines:
   ```bash
   find . -name "*.py" -not -path "./__pycache__/*" | wc -l
   find . -name "*.py" -not -path "./__pycache__/*" -exec cat {} + | wc -l
   ```
4. Kiểm tra MongoDB connection:
   ```bash
   python -c "from admin.db import get_db; print(get_db().list_collection_names())"
   ```
5. Báo cáo kết quả:
   - Số tests pass/fail
   - Số files Python / tổng dòng code
   - Collections trong MongoDB
   - Vấn đề phát hiện (nếu có)
