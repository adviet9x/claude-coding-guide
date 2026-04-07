# Workflow: Deployment

> Dùng Claude để chuẩn bị và thực hiện deployment an toàn.

---

## Pre-deployment Checklist

```
Chuẩn bị deploy. Kiểm tra:
1. Tất cả tests pass
2. Không có uncommitted changes
3. CHANGELOG.md đã cập nhật
4. Environment variables đầy đủ
5. Database migrations sẵn sàng
Báo cáo kết quả.
```

---

## Deployment Steps

### 1. Validate
```
Chạy kiểm tra pre-deploy:
- npm test (hoặc pytest)
- npm run build (hoặc build command)
- npm audit (dependency security)
```

### 2. Database
```
Kiểm tra database migrations:
- Có migrations pending không?
- Migration có backward compat không?
- Có cần seed data không?
```

### 3. Deploy
```
# Tùy platform
git push origin main          # Auto-deploy (Vercel, Railway)
docker build && docker push   # Container deploy
./scripts/deploy.sh           # Custom script
```

### 4. Verify
```
Sau khi deploy:
1. Health check endpoint: GET /health
2. Smoke test: các endpoint chính
3. Check logs: có errors không?
4. Monitor metrics: response time, error rate
```

---

## Rollback Plan

```
Nếu deploy gặp lỗi:
1. Revert deployment
2. Rollback database migration (nếu có)
3. Verify rollback thành công
4. Investigate root cause
```

---

## Tips

- Yêu cầu Claude **tạo deploy script** thay vì deploy trực tiếp
- Claude có thể tạo **GitHub Actions workflow** cho CI/CD tự động
- Luôn deploy **staging** trước **production**
- Không để Claude deploy trực tiếp lên production — cần approval
