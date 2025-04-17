# ZigiSoft - README Chuẩn Hóa Cài Đặt Ứng Dụng

Tài liệu này là hướng dẫn chính thức cho tất cả các ứng dụng thuộc hệ sinh thái **ZigiSoft**, nhằm đảm bảo launcher có thể nhận diện, kiểm tra và cập nhật ứng dụng chính xác.

---

## 1. Khai báo thông tin phiên bản trong project

Trong file `.csproj`, phải có:

```xml
<PropertyGroup>
  <Version>1.0.0</Version>
  <FileVersion>1.0.0.0</FileVersion>
  <AssemblyVersion>1.0.0.0</AssemblyVersion>
</PropertyGroup>
```

> ⚠️ KHÔNG để trống, nếu không launcher sẽ không lấy được version.

---

## 2. Ghi registry khi cài đặt (Setup Project)

### Bước 1: Vào `Registry Editor` trong Setup Project

- Tạo key:
  ```
  HKEY_LOCAL_MACHINE\SOFTWARE\ZigiSoft\[AppId]
  ```
- AppId là định danh duy nhất: `zigimail`, `zigibook`, `zigiedu`, ...

### Bước 2: Thêm các giá trị:

| Tên         | Kiểu     | Giá trị             |
|-------------|----------|---------------------|
| `InstallDir`| `REG_SZ` | `[TARGETDIR]`       |
| `Version`   | `REG_SZ` | `[ProductVersion]`  |

> 📌 Lưu trong HKLM để launcher đọc toàn máy.

---

## 3. Tên file `.exe` và thư mục cài đặt

- Tên file `.exe` chính phải trùng với `ExeName` trong DTO
- Mỗi app phải nằm trong thư mục riêng

### Ví dụ:

✅ `C:\Program Files\ZigiSoft\ZigiMail\ZigiMail.exe`

❌ `C:\ZigiSoft\AllApps\ZigiMail.exe`

---

## 4. Tên file setup

Chuẩn tên file setup:

```bash
[AppName].Setup.[Version].exe
```

Ví dụ: `ZigiMail.Setup.1.2.3.exe`

---

## 5. (Tùy chọn) File `version.txt` hoặc `appinfo.json`

Giúp launcher có thể đọc thông tin nhanh nếu cần:

### version.txt
```
1.2.3
```

### appinfo.json
```json
{
  "id": "zigibook",
  "version": "1.2.3",
  "buildDate": "2025-04-17"
}
```

---

## 6. Launcher sẽ đọc những gì?

- Đường dẫn từ `InstallDir` (registry)
- Tên file từ `ExeName` (DTO)
- Phiên bản từ `.exe` hoặc `version.txt`

=> Từ đó xác định:
- App đã cài chưa?
- Đang dùng version nào?
- Có cần cập nhật không?

---

## ✅ Checklist bắt buộc

- [x] Khai báo đầy đủ `<Version>`, `<FileVersion>`, `<AssemblyVersion>` trong `.csproj`
- [x] Đặt tên file `.exe` trùng khớp với `ExeName` khai báo trong launcher
- [x] Dùng Setup Project ghi thông tin vào registry:
  - `InstallDir` = `[TARGETDIR]`
  - `Version` = `[ProductVersion]`
- [x] Tên file setup theo định dạng: `[AppName].Setup.[Version].exe`
- [x] Cài đặt vào thư mục riêng biệt cho từng ứng dụng
- [ ] (Tuỳ chọn) Có `version.txt` hoặc `appinfo.json` trong thư mục cài để launcher có thể đọc nhanh thông tin

---

> 🧠 Đây là chuẩn bắt buộc cho mọi ứng dụng thuộc ZigiSoft.

Vui lòng đảm bảo app của bạn tuân thủ tài liệu này để launcher hoạt động trơn tru.

