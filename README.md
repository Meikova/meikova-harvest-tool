# Meikova Harvest Tool

<div align="center">

<img src="docs/assets/logo.png" alt="Meikova Harvest Logo" width="160px">

[![Release](https://img.shields.io/github/v/release/Meikova/meikova-harvest-tool?style=flat-square&color=059669)](https://github.com/Meikova/meikova-harvest-tool/releases)
[![Platforms](https://img.shields.io/badge/Platforms-Windows%20%7C%20macOS%20%7C%20Linux-2563eb?style=flat-square)](https://github.com/Meikova/meikova-harvest-tool)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-Automated%20Release-7c3aed?style=flat-square)](https://github.com/Meikova/meikova-harvest-tool/actions)
[![License](https://img.shields.io/badge/License-MIT-16a34a?style=flat-square)](LICENSE)

**Kho lưu trữ phân phối phát hành tự động, binary đa nền tảng và kênh cập nhật OTA cho hệ sinh thái Meikova Harvest.**

[Tải Bản Cài Đặt Mới Nhất](https://github.com/Meikova/meikova-harvest-tool/releases/latest) | [Mã Nguồn Meikova Harvest](https://github.com/Meikova/meikova-harvest) | [Báo Lỗi](https://github.com/Meikova/meikova-harvest-tool/issues)

</div>

---

## 1. Tổng quan kho phân phối

Meikova Harvest Tool đóng vai trò là hạ tầng phân phối công khai (Release Distribution & Auto-Update Channel) cho dự án [Meikova Harvest](https://github.com/Meikova/meikova-harvest):

- **Kênh cập nhật OTA**: Lưu trữ và phục vụ cấu hình `update.json` để ứng dụng Electron tự động đối soát phiên bản và nâng cấp không gián đoạn.
- **Phân phối bản dựng CI/CD**: Tiếp nhận các gói cài đặt đã được đóng gói và mã hóa nhị phân từ quy trình GitHub Actions.
- **Tính toàn vẹn tệp**: Cung cấp mã băm SHA-256 kiểm tra trước khi cài đặt.

---

## 2. Danh mục gói phát hành đa nền tảng

Tất cả các bản dựng đều được biên dịch tự động trên môi trường ảo sạch:

| Hệ điều hành | Định dạng | Mục tiêu phát hành |
| :--- | :--- | :--- |
| Windows | `.exe` (Installer & Portable) | Windows 10, 11 (x64) |
| macOS | `.dmg`, `.zip` | Apple Silicon (arm64) và Intel (x64) |
| Linux | `.AppImage`, `.deb`, `.tar.gz` | Ubuntu, Debian, Fedora, Arch (x64) |

Tải bản phát hành mới nhất tại: [GitHub Releases](https://github.com/Meikova/meikova-harvest-tool/releases/latest)

---

## 3. Cấu trúc kênh cập nhật (update.json)

Ứng dụng client truy vấn endpoint `update.json` định kỳ để kiểm tra phiên bản mới:

```json
{
  "version": "2.0.3",
  "url": "https://github.com/Meikova/meikova-harvest-tool/releases/download/v2.0.3/MeikovaHarvest-Setup-2.0.3.exe",
  "platforms": {
    "win32": "https://github.com/Meikova/meikova-harvest-tool/releases/download/v2.0.3/MeikovaHarvest-Setup-2.0.3.exe",
    "darwin_arm64": "https://github.com/Meikova/meikova-harvest-tool/releases/download/v2.0.3/MeikovaHarvest-2.0.3-arm64.dmg",
    "darwin_x64": "https://github.com/Meikova/meikova-harvest-tool/releases/download/v2.0.3/MeikovaHarvest-2.0.3-x64.dmg",
    "linux_x64": "https://github.com/Meikova/meikova-harvest-tool/releases/download/v2.0.3/MeikovaHarvest-2.0.3-x64.AppImage"
  },
  "changelog": "Phiên bản phát hành tự động qua quy trình CI/CD. Chi tiết xem tại mục Releases trên GitHub."
}
```

---

## 4. Quy trình phát hành tự động (CI/CD Matrix)

```
[Mã nguồn Meikova Harvest]
        │
        ├── Push Git Tag (v*.*.*)
        ▼
[GitHub Actions Runner Matrix]
        ├── windows-latest  ──> PyInstaller + Electron Builder ──> Setup.exe & Portable.exe
        ├── macos-latest    ──> PyInstaller + Electron Builder ──> .dmg (arm64 / x64)
        └── ubuntu-latest   ──> PyInstaller + Electron Builder ──> .AppImage & .deb
        │
        ▼
[Meikova Harvest Tool Release Channel]
        ├── GitHub Releases (Binaries + SHA256SUMS)
        └── Cập nhật update.json phục vụ Auto-Updater
```

---

## 5. Giấy phép bản quyền (License)

Dự án được phân phối theo giấy phép mã nguồn mở **MIT License**.

---

## 6. Hệ sinh thái Meikova

- [Meikova Harvest](https://github.com/Meikova/meikova-harvest) - Hệ sinh thái trích xuất và tải đa phương tiện đa nền tảng.
- [Meikova Loop](https://github.com/Meikova/meikova-loop) - DJ mashup và infinite soundscape engine chạy trên web, desktop và mobile.
- [Meikova Relay](https://github.com/Meikova/meikova-relay) - Điều khiển máy tính từ xa độ trễ thấp, outbound-only.
- [Meikova Auth](https://github.com/Meikova/meikova-auth) - Cổng xác thực tập trung, Universal SSO Ed25519 và quản lý danh tính đa nền tảng.
- [Meikova Balance](https://github.com/Meikova/meikova-balance) - Quản lý tài chính cá nhân, chia hóa đơn nhóm và trợ lý AI đa tầng.
- [Meikova Campus](https://github.com/Meikova/meikova-campus) - Nền tảng thương mại khóa học, phân quyền Google Drive tự động và LMS trực tuyến.
- [Meikova Exchange](https://github.com/Meikova/meikova-exchange) - Sàn giao dịch B2B cho dự án phần mềm, mã nguồn và tài sản số.
- [Meikova Traverse](https://github.com/Meikova/meikova-traverse) - Trình duyệt tệp tin cục bộ, SFTP, WebDAV và quản lý lưu trữ đa nền tảng.
- [Meikova Shield](https://github.com/Meikova/meikova-shield) - Hệ thống phòng thủ an ninh mạng và phát hiện web defacement bằng học máy lai ghép.
- [Meikova Vision](https://github.com/Meikova/meikova-vision) - Bộ công cụ xử lý ảnh RAW, ghép đa phơi sáng HDR và tone mapping chuyên nghiệp.
- [Meikova Flow](https://github.com/Meikova/meikova-flow) - Động cơ trích xuất, biến đổi, nạp dữ liệu (ETL) và tự động hóa luồng báo cáo.
