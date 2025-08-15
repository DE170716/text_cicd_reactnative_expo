# Hướng dẫn thiết lập GitHub Actions

## 🔧 **Bước 1: Tạo Expo Token**

Để GitHub Actions có thể sử dụng EAS, bạn cần tạo Expo token:

### Cách 1: Sử dụng EAS CLI
```bash
# Đăng nhập vào Expo
npx eas-cli@latest login

# Tạo token
npx eas-cli@latest token:create
```

### Cách 2: Từ Expo Dashboard
1. Vào https://expo.dev/accounts/quanghuy12345/settings/access-tokens
2. Click "Create token"
3. Đặt tên token (ví dụ: "GitHub Actions")
4. Copy token

## 🔧 **Bước 2: Thêm Token vào GitHub Secrets**

1. Vào GitHub repository của bạn
2. Vào **Settings** → **Secrets and variables** → **Actions**
3. Click **"New repository secret"**
4. Đặt tên: `EXPO_TOKEN`
5. Paste token vào Value
6. Click **"Add secret"**

## 🔧 **Bước 3: Push code để test**

```bash
# Commit thay đổi
git add .
git commit -m "Fix app.json configuration for CI/CD"

# Push lên GitHub
git push origin main
```

## 🔧 **Bước 4: Kiểm tra GitHub Actions**

1. Vào GitHub repository
2. Click tab **"Actions"**
3. Bạn sẽ thấy workflow "React Native CI/CD" đang chạy
4. Click vào workflow để xem logs

## 🔧 **Bước 5: Test Production Deployment**

```bash
# Tạo tag để trigger production deployment
git tag v1.0.0
git push origin v1.0.0
```

## 📊 **Kết quả mong đợi**

### EAS Workflows (Đã sửa)
- ✅ Build Android thành công
- ✅ Build iOS thành công
- ✅ Xem logs tại: https://expo.dev/accounts/quanghuy12345/projects/my-app/workflows

### GitHub Actions (Sau khi setup)
- ✅ Test job thành công
- ✅ Build Android thành công  
- ✅ Build iOS thành công
- ✅ Xem logs tại: GitHub repository → Actions tab

## 🚨 **Lỗi đã sửa**

### ❌ **Trước khi sửa**
```json
"ios": {
  "supportsTablet": true
},
"android": {
  "adaptiveIcon": {
    "foregroundImage": "./assets/images/adaptive-icon.png",
    "backgroundColor": "#ffffff"
  },
  "edgeToEdgeEnabled": true
}
```

### ✅ **Sau khi sửa**
```json
"ios": {
  "supportsTablet": true,
  "bundleIdentifier": "com.quanghuy12345.myapp"
},
"android": {
  "adaptiveIcon": {
    "foregroundImage": "./assets/images/adaptive-icon.png",
    "backgroundColor": "#ffffff"
  },
  "edgeToEdgeEnabled": true,
  "package": "com.quanghuy12345.myapp"
}
```

## 📝 **Lưu ý quan trọng**

1. **Bundle Identifier**: Phải unique trên toàn thế giới
2. **Package Name**: Phải unique trên Google Play Store
3. **Token Security**: Không chia sẻ token với ai
4. **GitHub Secrets**: Token được mã hóa và bảo mật

## 🔗 **Links hữu ích**

- [EAS Token Documentation](https://docs.expo.dev/eas/update/using-updates/)
- [GitHub Secrets Documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
- [Expo App Configuration](https://docs.expo.dev/versions/latest/config/app/)
