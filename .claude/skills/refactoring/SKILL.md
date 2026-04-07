# Skill: Refactoring

## Khi nào dùng
- Tách file > 300 dòng thành modules nhỏ
- Extract functions/classes ra file riêng
- Giảm code duplication
- Cải thiện cấu trúc mà KHÔNG thay đổi behavior

## Quy trình

### Bước 1: Snapshot tests
```bash
python -m pytest tests/ -v --tb=short > /tmp/before.txt
```
Ghi nhận số tests pass trước khi refactor.

### Bước 2: Phân tích
- Đếm dòng code: file nào > 300 dòng?
- Tìm code duplication: pattern lặp lại ở đâu?
- Tìm functions > 30 dòng: cần tách?
- Tìm circular imports: cần restructure?

### Bước 3: Thực hiện refactor
Mỗi bước nhỏ:
1. Tạo file mới (nếu cần extract)
2. Move code sang file mới
3. Update imports ở tất cả files sử dụng
4. Chạy tests → phải pass 100%
5. Commit

### Bước 4: Verify
```bash
python -m pytest tests/ -v --tb=short > /tmp/after.txt
# So sánh: số tests phải bằng hoặc nhiều hơn
```

## Rules
- **KHÔNG** thay đổi behavior — chỉ restructure
- **KHÔNG** thêm features mới trong khi refactor
- Commit sau MỖI bước nhỏ (1 extract = 1 commit)
- Nếu test fail → revert ngay, debug trước khi tiếp

## Ví dụ thực tế (TopicForge)
```
# agents.py (870 dòng) → tách thành:
# agents/agent_pipeline.py (823 dòng → tiếp tục tách)
# agents/pipeline_config.py (110 dòng)

# main.py (870 dòng) → tách thành:
# cli/run.py, cli/test.py, cli/seed.py, ... (9 modules)
# main.py (300 dòng — chỉ imports + dispatch)
```
