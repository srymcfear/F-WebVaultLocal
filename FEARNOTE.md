# FEAR·VAULT — Session Log

## 2026-07-25

### Created
- Standalone vault page tại `G:\FEAR_PAGE\FEAR-Vault\index.html`
- File HTML đơn, mở browser là chạy, không cần server/build

### Cơ chế
- **Mã hoá**: AES-256-GCM + PBKDF2 (100k iterations) — port từ FEAR-Local
- **Storage**: localStorage — không cần backend
- **Kiến trúc**: single HTML file, all-in-one (CSS + JS inline)

### Tính năng
- Lock screen — mật khẩu chính
- Tạo vault lần đầu + Recovery Key
- Khôi phục vault bằng Recovery Key
- CRUD entries (thêm/sửa/xoá)
- Search + category filter
- Password generator
- Copy/show/hide password
- Export/Import vault (v2 envelope, AES-GCM + HMAC)
- Đổi mật khẩu chính
- Tự động khoá sau 5 phút

### Style
- Terminal-style từ `Demo/test.html` (purple/black, JetBrains Mono + Orbitron)
- Lock screen với scan-line effect + glow

### File structure
```
FEAR-Vault/
  index.html   (≈500 dòng, standalone)
  FEARNOTE.md
```

### Chạy
Mở `index.html` trong browser — không cần gì thêm.