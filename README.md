# 🛡️ FEAR-VAULT · CYBER HUD PASSWORD MANAGER

![License](https://img.shields.io/badge/Security-AES--256--GCM-00f0ff?style=for-the-badge)
![Encryption](https://img.shields.io/badge/KDF-PBKDF2--100k-ef4444?style=for-the-badge)
![Architecture](https://img.shields.io/badge/Architecture-Zero--Knowledge-10b981?style=for-the-badge)
![UI Theme](https://img.shields.io/badge/UI-Cyberpunk_HUD-38bdf8?style=for-the-badge)

**FEAR-Vault** là ứng dụng quản lý mật khẩu cá nhân thế hệ mới với giao diện **Cyberpunk HUD Matrix** đẳng cấp, áp dụng mô hình kiến trúc **Zero-Knowledge 100% Client-Side**. Toàn bộ dữ liệu được mã hóa quân sự trực tiếp trên trình duyệt của bạn trước khi lưu trữ.

---

## 🌟 TÍNH NĂNG NỔI BẬT

- 🔒 **Zero-Knowledge Client-Side Encryption**: Mật khẩu chính (Master Password) không bao giờ rời khỏi thiết bị của bạn. Không gửi bất kỳ dữ liệu nào về Server hay bên thứ 3.
- 🎨 **Giao Diện Cyber HUD Matrix 3D**: Trải nghiệm giao diện tương lai với ma trận số tuôn trôi, hiệu ứng cảm biến quét vân tay vi mạch 3D (**Biometric Circuit Fingerprint Scanner**), con dấu xoay 360° và các ô nhập OTP gợn sóng (Wave Ripple) theo con trỏ chuột.
- 🛡️ **Xác Thực 2 Bước 2FA (RFC 6238 TOTP)**: Hỗ trợ tạo mã QR và tích hợp ứng dụng Google Authenticator, Authy, Microsoft Authenticator.
- 🔑 **Khôi Phục Bằng Recovery Key**: Cấp mã Recovery Key định dạng `FEAR-XXXX-XXXX` cho phép khôi phục lại kho mật khẩu khi quên Mật khẩu chính.
- 🎲 **Bộ Tạo Mật Khẩu Mạnh CSPRNG**: Tạo mật khẩu ngẫu nhiên an toàn cao sử dụng thuật toán xáo trộn Fisher-Yates + `crypto.getRandomValues()`.
- 📁 **Xuất / Nhập Dữ Liệu An Toàn (HMAC Envelope v2)**: Cho phép Export/Import file JSON mã hóa AES-256-GCM có chữ ký HMAC-SHA256 xác thực tính toàn vẹn.
- ⏱️ **Tự Động Khóa (Auto-Lock & Clipboard Clear)**: Tự động khóa kho sau 5 phút không hoạt động và tự động xóa bộ nhớ đệm sao chép (Clipboard) sau 30 giây.
- 🚫 **Lọc Ký Tự Thông Minh & Cảnh Báo**: Tự động chặn các ký tự không hợp lệ (Tiếng Việt có dấu, khoảng trắng) và hiển thị thông báo cảnh báo trực quan.

---

## 🔐 KIẾN TRÚC BẢO MẬT & MÃ HÓA

FEAR-Vault sử dụng các tiêu chuẩn mã hóa bảo mật cao nhất hiện nay:

```
[ Master Password ] ──( Salt 16-byte )──► [ PBKDF2 SHA-256: 100,000 Iterations ]
                                                       │
                                                       ▼
                                            [ AES-256-GCM Key (256-bit) ]
                                                       │
                                   ( IV 12-byte ) ─────┼─────► [ Encrypted Ciphertext ]
                                                       │
                                                       ▼
                                            [ Browser LocalStorage ]
```

### 1. Thuật toán mã hóa & băm
* **Mật Khẩu Chính (Master Password)**: Được băm qua hàm **PBKDF2 (SHA-256)** với **100,000 vòng lặp (100,000 iterations)** kết hợp **Salt ngẫu nhiên 16-byte**. Không lưu mật khẩu thô dưới bất kỳ hình thức nào.
* **Dữ Liệu Mật Khẩu (Vault Items)**: Đóng gói dạng JSON và mã hóa đối xứng **AES-256-GCM (Galois/Counter Mode)** với **IV ngẫu nhiên 12-byte** cho mỗi mục.
* **Mã Xác Thực 2FA (TOTP Secret)**: Được mã hóa riêng bằng AES-256-GCM trước khi lưu.
* **File Export**: Sử dụng cấu trúc Envelope v2 tích hợp chữ ký mã hóa **HMAC-SHA256** chống sửa đổi file.

### 2. Quy tắc ký tự Mật khẩu chính
Nhằm đảm bảo tính tương thích và bảo mật cao nhất, ô nhập Mật khẩu chính hỗ trợ:
- **Chữ cái Tiếng Anh**: `A - Z` và `a - z`
- **Chữ số**: `0 - 9`
- **Ký tự đặc biệt cho phép**: `@`, `!`, `#`, `&`, `-`

---

## 💻 HƯỚNG DẪN SỬ DỤNG

### 1. Chạy trực tiếp trên máy
1. Tải file mã nguồn hoặc clone repository về máy.
2. Mở trực tiếp file [`index.html`](file:///G:/FEAR_PAGE/FEAR-Vault/index.html) bằng bất kỳ trình duyệt web nào (Chrome, Edge, Firefox, Brave, Safari).
3. Không cần cài đặt `Node.js` hay `npm`.

### 2. Deploy miễn phí lên Cloudflare Pages (`*.pages.dev`)

🚀 **Kéo thả trực tiếp (Không cần cài đặt gì, có link `.pages.dev` sau 10 giây!)**
Nếu bạn không muốn liên kết GitHub, bạn chỉ cần kéo thả file `index.html` trực tiếp lên Cloudflare:

1. Truy cập trang chủ Cloudflare: [dash.cloudflare.com](https://dash.cloudflare.com) và đăng ký/đăng nhập 1 tài khoản miễn phí.
2. Ở menu bên trái, bấm vào **Workers & Pages**.
3. Chọn tab **Pages** $\rightarrow$ bấm nút **Create a project**.
4. Chọn mục **Upload assets** (Kéo thả file).
5. Nhập **Project name** (Tên dự án của bạn, ví dụ: `fear-vault`). Tên này sẽ tạo thành link `https://fear-vault.pages.dev`.
6. Kéo thư mục chứa file `index.html` thả vào ô vuông trên màn hình.
7. Bấm **Save and Deploy**.

✨ **Hoàn thành!** Bạn sẽ nhận được ngay đường link dạng `https://fear-vault.pages.dev` hoạt động 24/7!

---

## 📜 GIẤY PHÉP (LICENSE)

Dự án được phát hành dưới giấy phép MIT License. Bạn có thể tự do sử dụng, chỉnh sửa và triển khai cá nhân.

---
*Built with ❤️ for Security & Performance — FEAR-Vault Cyber HUD Edition.*
