# Release Checklist

> **Document Owner:** Claude (Release Manager) · **Approver:** Game Director (go/no-go) · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [TEST_STRATEGY](TEST_STRATEGY.md) · [MILESTONES](../01_production/MILESTONES.md) · [TECH_DECISIONS TD-09](../05_engineering/TECH_DECISIONS.md#td-09--cấu-hình-build-android)

Dùng cho mọi build giao cho người ngoài nhóm (playtest, demo M7). Với build nội bộ milestone, dùng các mục §1–§3. Sao chép checklist này vào báo cáo release của từng lần phát hành và đánh dấu từng mục; mục không áp dụng ghi `N/A` kèm lý do.

---

## 1. Chất lượng

- [ ] Toàn bộ test tự động đã chạy; report đính kèm.
- [ ] Regression checklist thủ công hoàn tất.
- [ ] Không còn bug Blocker/Critical đã biết — hoặc có miễn trừ của GD được ghi lại.
- [ ] Known issues được liệt kê.
- [ ] Save/load: tạo mới, tải lại, tương thích save của build trước (nếu có cam kết).

## 2. Build PC

- [ ] Build thành công; log lưu lại.
- [ ] Khởi động trên cấu hình PC thử nghiệm đã duyệt.
- [ ] Điều khiển bàn phím/chuột (và gamepad nếu được duyệt) hoạt động.
- [ ] Các độ phân giải và chế độ cửa sổ/toàn màn hình.
- [ ] Đạt performance budget.

## 3. Build Android

- [ ] Build thành công (IL2CPP/ARM64 theo TD-09); log lưu lại.
- [ ] Cài và chạy trên thiết bị Android thử nghiệm đã duyệt.
- [ ] Điều khiển cảm ứng; safe area; các tỉ lệ màn hình.
- [ ] Vòng đời: xuống nền, khôi phục, khóa màn hình, kill app — không mất tiến độ.
- [ ] Đạt performance budget (FPS, bộ nhớ, nhiệt độ quan sát).
- [ ] Ký bằng keystore đúng (với bản phát hành); keystore được lưu an toàn bởi GD.

## 4. Nội dung và pháp lý

- [ ] Mọi asset trong build có trong ASSET_MANIFEST với provenance và license.
- [ ] Mọi audio có license rõ.
- [ ] Không có placeholder ngoài danh sách được GD cho phép.
- [ ] Originality review hoàn tất cho asset quan trọng (P12).
- [ ] Font hiển thị đầy đủ ký tự các ngôn ngữ được hỗ trợ.
- [ ] Credits/attribution theo yêu cầu license.

## 5. Phát hành (khi phát hành công khai — M7+)

- [ ] Tên game, icon, package name chốt (OQ-029).
- [ ] Kênh phát hành và yêu cầu cửa hàng được kiểm tra (OQ-027) — bao gồm target API level hiện hành của Google Play.
- [ ] Release notes.
- [ ] Bản build và mã nguồn tương ứng được đánh dấu phiên bản (tag) trong VCS.

## 6. Quyết định

- [ ] Claude tổng hợp báo cáo release.
- [ ] **Game Director quyết định Go / No-go** — ghi Acceptance Record.
