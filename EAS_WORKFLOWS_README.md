# EAS Workflows - Hướng dẫn sử dụng

Dự án này đã được cấu hình với EAS Workflows để tự động hóa quy trình CI/CD cho React Native app.

## Các Workflow có sẵn

### 1. Development Builds (`.eas/workflows/development-builds.yml`)
- **Mục đích**: Tạo development builds để test app
- **Chạy thủ công**: `npx eas-cli@latest workflow:run development-builds.yml`
- **Kết quả**: APK/IPA files cho development testing

### 2. Preview Builds (`.eas/workflows/preview-builds.yml`)
- **Mục đích**: Tạo preview builds để test trước khi release
- **Chạy thủ công**: `npx eas-cli@latest workflow:run preview-builds.yml`
- **Kết quả**: APK/IPA files cho preview testing

### 3. Production Builds (`.eas/workflows/create-production-builds.yml`)
- **Mục đích**: Tạo production builds cho release
- **Chạy thủ công**: `npx eas-cli@latest workflow:run create-production-builds.yml`
- **Kết quả**: APK/IPA files cho production release

### 4. CI/CD Pipeline (`.eas/workflows/ci-cd-pipeline.yml`)
- **Mục đích**: Tự động build khi push code lên main branch
- **Trigger**: Tự động khi push lên `main` branch
- **Kết quả**: Development và preview builds tự động

### 5. Submit to Stores (`.eas/workflows/submit-to-stores.yml`)
- **Mục đích**: Submit app lên Google Play Store và Apple App Store
- **Chạy thủ công**: `npx eas-cli@latest workflow:run submit-to-stores.yml`
- **Lưu ý**: Cần cấu hình app store credentials trước

### 6. Release Pipeline (`.eas/workflows/release-pipeline.yml`)
- **Mục đích**: Quy trình release hoàn chỉnh (build + submit)
- **Trigger**: Tự động khi push tag `v*` lên main branch
- **Kết quả**: Build production và submit lên stores

## Cách sử dụng

### Chạy workflow thủ công
```bash
# Chạy development builds
npx eas-cli@latest workflow:run development-builds.yml

# Chạy production builds
npx eas-cli@latest workflow:run create-production-builds.yml

# Submit lên stores
npx eas-cli@latest workflow:run submit-to-stores.yml
```

### Trigger tự động từ GitHub
1. Kết nối GitHub repository với EAS project
2. Push code lên `main` branch để trigger CI/CD pipeline
3. Tạo tag `v1.0.0` để trigger release pipeline

### Xem logs và kết quả
- Truy cập: https://expo.dev/accounts/quanghuy12345/projects/my-app/workflows
- Xem logs chi tiết của từng workflow run

## Cấu hình cần thiết

### 1. App Store Credentials
Để submit lên stores, cần cấu hình:
- Google Play Store: Service account key
- Apple App Store: App Store Connect API key

### 2. Environment Variables
Có thể thêm environment variables vào workflow:
```yaml
jobs:
  build_android:
    type: build
    params:
      platform: android
    env:
      MY_API_KEY: ${{ secrets.MY_API_KEY }}
```

### 3. Custom Build Profiles
Có thể tạo custom build profiles trong `eas.json`:
```json
{
  "build": {
    "custom": {
      "android": {
        "buildType": "apk"
      }
    }
  }
}
```

## Troubleshooting

### Lỗi thường gặp
1. **Build fails**: Kiểm tra dependencies và native code
2. **Submit fails**: Kiểm tra app store credentials
3. **Workflow not triggered**: Kiểm tra GitHub integration

### Debug
- Xem logs chi tiết trên Expo dashboard
- Kiểm tra `eas.json` configuration
- Verify app store credentials

## Tài liệu tham khảo
- [EAS Workflows Documentation](https://docs.expo.dev/eas/workflows/get-started/)
- [EAS Build Documentation](https://docs.expo.dev/eas/build/)
- [EAS Submit Documentation](https://docs.expo.dev/eas/submit/)
