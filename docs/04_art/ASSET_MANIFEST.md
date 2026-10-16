# Asset Manifest

> **Document Owner:** Claude (xác minh) · **Cập nhật bởi:** Antigravity (khi bàn giao), Codex (khi tích hợp) · **Status:** `ACTIVE` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ASSET_SPEC](ASSET_SPEC.md) · [CONTENT_PIPELINE](../06_audio_integration/CONTENT_PIPELINE.md)

Sổ đăng ký mọi visual asset của dự án. **Asset không có trong manifest thì không được dùng trong build** (trừ placeholder được task cho phép, ghi ở mục 3). Hiện **chưa có asset nào**.

---

## 1. Trạng thái asset

`CONCEPT` → `CONCEPT_APPROVED` → `IN_PRODUCTION` → `DELIVERED` → `VALIDATED` → `INTEGRATED` → `ACCEPTED`
Ngoài luồng: `REJECTED`, `DEPRECATED` (giữ lịch sử, không xóa).

## 2. Production assets

| Asset ID / File | Loại | Liên kết (CHR/AREA…) | Version | Status | Brief | Review | Công cụ & mức chỉnh sửa | Nguồn tham khảo / License | Originality check | Ngày |
|---|---|---|---|---|---|---|---|---|---|---|
| — | — | — | — | — | — | — | — | — | — | — |

## 3. Placeholder assets

Placeholder dùng cho prototype (M2, M3). Phải được thay thế trước khi milestone liên quan yêu cầu final art.

| File | Dùng ở | Nguồn / License | Thay bằng | Status |
|---|---|---|---|---|
| — | — | — | — | — |

Quy tắc: placeholder từ bên ngoài chỉ dùng khi license cho phép; ưu tiên hình khối đơn giản do Codex tạo trong Unity.

## 4. Lịch sử thay đổi

| Ngày | Asset | Thay đổi | Người cập nhật |
|---|---|---|---|
| 2026-10-15 | — | Khởi tạo manifest rỗng | Claude |
