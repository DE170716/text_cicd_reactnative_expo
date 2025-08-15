# Troubleshooting CI/CD Issues

## 🚨 **Lỗi thường gặp và cách sửa**

### 1. **Lỗi: "android.package" is required**

**Nguyên nhân**: Thiếu cấu hình package name trong `app.json`

**Cách sửa**:
```json
{
  "expo": {
    "android": {
      "package": "com.quanghuy12345.myapp"
    }
  }
}
```

### 2. **Lỗi: "ios.bundleIdentifier" is required**

**Nguyên nhân**: Thiếu cấu hình bundle identifier trong `app.json`

**Cách sửa**:
```json
{
  "expo": {
    "ios": {
      "bundleIdentifier": "com.quanghuy12345.myapp"
    }
  }
}
```

### 3. **EAS vẫn báo lỗi cũ sau khi sửa**

**Nguyên nhân**: EAS đang sử dụng cache cũ

**Cách sửa**:
1. Cập nhật workflow để chỉ định profile rõ ràng
2. Chạy lại workflow
3. Kiểm tra logs mới nhất

### 4. **GitHub Actions không trigger**

**Nguyên nhân**: Thiếu Expo token hoặc cấu hình sai

**Cách sửa**:
1. Tạo Expo token: `npx eas-cli@latest token:create`
2. Thêm token vào GitHub Secrets với tên `EXPO_TOKEN`
3. Push code để trigger workflow

## 🔧 **Các bước kiểm tra**

### Kiểm tra cấu hình app.json
```bash
# Kiểm tra file app.json có đúng không
cat app.json
```

### Kiểm tra EAS workflow
```bash
# Chạy test workflow
npx eas-cli@latest workflow:run test-build.yml
```

### Kiểm tra GitHub Actions
```bash
# Push code để trigger
git add .
git commit -m "Test CI/CD"
git push origin main
```

## 📊 **Trạng thái hiện tại**

### ✅ **Đã sửa**
- ✅ Thêm `android.package` vào app.json
- ✅ Thêm `ios.bundleIdentifier` vào app.json
- ✅ Cập nhật EAS workflow với profile production
- ✅ Tạo test workflow để kiểm tra

### ⏳ **Cần làm**
- ⏳ Setup GitHub Actions với Expo token
- ⏳ Test cả 2 hệ thống hoạt động

## 🎯 **Kết quả mong đợi**

### EAS Workflows
- ✅ Build Android thành công
- ✅ Build iOS thành công
- ✅ Xem logs tại: https://expo.dev/accounts/quanghuy12345/projects/my-app/workflows

### GitHub Actions
- ✅ Test job thành công
- ✅ Build jobs thành công
- ✅ Xem logs tại: GitHub repository → Actions tab

## 📝 **Lưu ý quan trọng**

1. **Bundle Identifier**: Phải unique trên toàn thế giới
2. **Package Name**: Phải unique trên Google Play Store
3. **Cache**: EAS có thể cache cấu hình cũ
4. **Token**: GitHub Actions cần Expo token để hoạt động

## 🔗 **Links hữu ích**

- [EAS Build Documentation](https://docs.expo.dev/eas/build/)
- [Expo App Configuration](https://docs.expo.dev/versions/latest/config/app/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
