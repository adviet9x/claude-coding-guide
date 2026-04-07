# Session Memory — Ghi Nhớ Phiên

> Chỉ tồn tại trong 1 conversation. Bị xóa khi kết thúc.
> Path: `/memories/session/`

---

## Dùng Cho

- Task progress (đang làm đến đâu)
- Temporary notes trong phiên dài
- Plan/checklist cho multi-step task
- Working context khi phải chuyển topic

---

## Ví Dụ

### Lưu progress
```
Lưu session memory:
- Task: Refactor agent_pipeline.py
- Đã xong: tách config, env helpers
- Đang làm: cleanup imports
- Còn lại: run tests, verify backward compat
```

### Lưu plan
```
Lưu session memory — Sprint plan:
1. ✅ Tạo pipeline_config.py
2. ✅ Import config vào agent_pipeline.py
3. 🔄 Tách env override logic
4. ⬜ Cleanup inline imports
5. ⬜ Chạy tests
6. ⬜ Verify backward compat
```

---

## Khi Nào Dùng

| Tình huống | Dùng session memory |
|-----------|-------------------|
| Task < 5 messages | ❌ Không cần |
| Task 5-15 messages | ⚠️ Tùy complexity |
| Task > 15 messages | ✅ Nên dùng |
| Multi-step refactor | ✅ Bắt buộc |
| Debug session dài | ✅ Ghi notes |

---

## Tips

- Session memory **không auto-loaded** — Claude phải đọc khi cần
- Đừng lưu quá nhiều — chỉ lưu khi phiên dài
- Cuối session dài → lưu summary để session tiếp đọc nhanh
- Nếu task cần nhiều sessions → lưu info quan trọng vào **repo memory** thay vì session
