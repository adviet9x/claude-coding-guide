---
name: fix-issue
description: Phân tích và fix một bug/issue
arguments:
  - name: issue
    description: Mô tả bug hoặc issue number
    required: true
---

# Fix Issue Command

## Quy trình
1. Đọc mô tả issue: `$ARGUMENTS.issue`
2. Tìm file liên quan bằng `grep_search` và `semantic_search`
3. Reproduce lỗi bằng test hiện có hoặc viết test mới
4. Phân tích nguyên nhân gốc
5. Fix lỗi
6. Viết regression test
7. Chạy toàn bộ test suite: `python -m pytest tests/ -v`
8. Tóm tắt thay đổi

## Rules
- KHÔNG fix triệu chứng — fix nguyên nhân gốc
- LUÔN viết regression test
- KHÔNG break tests hiện tại
- Commit message: `fix(<scope>): <description>`
