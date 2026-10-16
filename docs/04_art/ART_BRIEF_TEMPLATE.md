# Art Brief Template

> **Document Owner:** Claude · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [04_art/DEPARTMENT §9](DEPARTMENT.md#9-workflows) · [ASSET_SPEC](ASSET_SPEC.md) · [ART_REVIEW_TEMPLATE](../templates/ART_REVIEW_TEMPLATE.md)

Claude tạo Art Brief trước mọi art task. Lưu tại `docs/04_art/briefs/AB-NNN-<slug>.md`. Brief thiếu mục bắt buộc (★) → task chưa đạt DoR.

---

```markdown
# AB-NNN — <Tên asset / nhóm asset>

- **Task ID:** M<n>-ART-NNN ★
- **Giai đoạn yêu cầu:** Research / Moodboard / Sketch / Concept / Final ★
- **Loại asset:** Character / Enemy / Boss / Environment / Prop / UI / VFX / Icon ★
- **Mức độ quan trọng:** Quan trọng (bắt buộc concept approval) / Phụ ★
- **Trạng thái brief:** PROPOSED / APPROVED

## 1. Mục đích ★
Asset này phục vụ điều gì trong game? Người chơi cần hiểu gì khi nhìn thấy nó?

## 2. Bối cảnh ★
- Art Direction / Style Guide áp dụng: (link, hoặc "đang khám phá — hướng X")
- Narrative: (link CHARACTER_REGISTER / WORLD_BIBLE nếu có)
- Gameplay: (vai trò combat, kích thước hitbox, hành vi — link COMBAT_DESIGN)

## 3. Yêu cầu hình ảnh
- Từ khóa tính cách/cảm xúc:
- Hình khối, màu sắc chủ đạo (nếu đã có style guide):
- Bắt buộc có:
- Tránh:

## 4. Tham khảo
- Tham khảo được dùng (ghi nguồn) và **điều cần học từ đó** (ví dụ "độ rõ silhouette"), không phải "làm giống".

## 5. Yêu cầu kỹ thuật ★ (cho Final)
- Kích thước / PPU / pivot: theo ASSET_SPEC §3–4 (hoặc ghi ngoại lệ)
- Số hướng:
- Danh sách animation và số frame: theo ASSET_SPEC §5
- Định dạng xuất, tên file: theo ASSET_SPEC §6–7

## 6. Nền tảng
- Kiểm tra độ đọc được ở kích thước hiển thị trên điện thoại: có / không cần

## 7. Đầu ra mong đợi ★
- Số lượng sketch/variant, file, vị trí bàn giao

## 8. Tiêu chí chấp nhận ★
- …

## 9. Ngoài phạm vi
- …
```
