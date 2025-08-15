# GitHub Actions CI/CD - Hướng dẫn sử dụng

Dự án này đã được cấu hình với GitHub Actions để tự động hóa quy trình CI/CD và có thể xem trực tiếp trên GitHub.

## Các Workflow GitHub Actions

### 1. CI/CD Pipeline (`.github/workflows/ci-cd.yml`)
**Trigger**: Push lên `main` hoặc `develop` branch, hoặc tạo Pull Request

**Jobs**:
- **Test**: Linting, type checking
- **Build Android**: Tạo APK/AAB file
- **Build iOS**: Tạo IPA file  
- **Deploy Preview**: Deploy lên Expo (chỉ khi push lên `develop`)

**Xem logs**: GitHub repository → Actions tab → "React Native CI/CD"

### 2. Production Deployment (`.github/workflows/production-deploy.yml`)
**Trigger**: Tạo tag `v*` (ví dụ: `v1.0.0`)

**Jobs**:
- **Build Production**: Build cho Android và iOS
- **Submit to Stores**: Submit lên Google Play và Apple App Store
- **Deploy to Expo**: Deploy production update

**Xem logs**: GitHub repository → Actions tab → "Production Deployment"

## Cách xem CI/CD trên GitHub

### 1. Truy cập Actions tab
- Vào GitHub repository của bạn
- Click tab **"Actions"** ở trên cùng
- Bạn sẽ thấy tất cả workflow runs

### 2. Xem chi tiết workflow
- Click vào workflow run để xem chi tiết
- Xem logs từng step
- Download build artifacts (APK, IPA files)

### 3. Xem real-time progress
- Khi push code, workflow sẽ tự động chạy
- Bạn có thể xem progress real-time
- Nhận notification khi hoàn thành

## Cấu hình cần thiết

### 1. Expo Token
Để GitHub Actions có thể sử dụng EAS, cần tạo Expo token:

```bash
# Tạo token
npx eas-cli@latest login
npx eas-cli@latest whoami
```

Sau đó thêm token vào GitHub Secrets:
1. Vào repository → Settings → Secrets and variables → Actions
2. Tạo secret `EXPO_TOKEN` với token vừa tạo

### 2. App Store Credentials (cho production)
- **Google Play**: Service account key
- **Apple App Store**: App Store Connect API key

## Cách sử dụng

### Development Workflow
```bash
# Push lên develop branch
git checkout develop
git add .
git commit -m "Add new feature"
git push origin develop
```
→ Tự động trigger CI/CD pipeline

### Production Release
```bash
# Tạo tag để release
git tag v1.0.0
git push origin v1.0.0
```
→ Tự động trigger production deployment

### Manual Trigger
- Vào Actions tab
- Click "Run workflow"
- Chọn workflow và branch

## So sánh: EAS Workflows vs GitHub Actions

| Tính năng | EAS Workflows | GitHub Actions |
|-----------|---------------|----------------|
| **Xem logs** | expo.dev | GitHub repository |
| **Tốc độ** | Tối ưu cho mobile | Tổng quát |
| **Setup** | Đơn giản | Linh hoạt hơn |
| **Cost** | Miễn phí (có giới hạn) | Miễn phí (có giới hạn) |
| **Integration** | Expo ecosystem | GitHub ecosystem |

## Troubleshooting

### Lỗi thường gặp
1. **EXPO_TOKEN not found**: Kiểm tra GitHub Secrets
2. **Build fails**: Xem logs chi tiết trong Actions tab
3. **Permission denied**: Kiểm tra repository permissions

### Debug
- Xem logs chi tiết trong Actions tab
- Kiểm tra workflow syntax
- Verify environment variables

## Tài liệu tham khảo
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [EAS CLI Documentation](https://docs.expo.dev/eas/)
- [React Native CI/CD Best Practices](https://reactnative.dev/docs/ci-cd)
