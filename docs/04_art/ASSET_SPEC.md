# Asset Specification

> **Document Owner:** Claude (Technical Art spec) · **Approver:** Game Director (các thông số L1) · **Status:** `UNDER_REVIEW` — thông số chính `TBD` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ART_DIRECTION_EXPLORATION](ART_DIRECTION_EXPLORATION.md) · [ASSET_MANIFEST](ASSET_MANIFEST.md) · [CONTENT_PIPELINE](../06_audio_integration/CONTENT_PIPELINE.md)

Tiêu chuẩn kỹ thuật cho mọi visual asset. Phần lớn thông số phụ thuộc Art Direction (OQ-014) và camera (OQ-002), nên đang `TBD`; các **quy tắc kiểm soát** dưới đây có hiệu lực ngay khi tài liệu được duyệt.

---

## 1. Tính nhất quán

- Mọi asset tuân theo Style Guide (sẽ có sau khi Art Direction `APPROVED`).
- Một nhân vật có **một character sheet chuẩn** (turnaround/các hướng, bảng màu); mọi sprite và animation phải khớp sheet này.
- Bảng màu (palette) cố định cho mỗi nhân vật/region; ngoại lệ phải ghi trong brief.
- Visual review kiểm tra: tỉ lệ, palette, độ dày nét, hướng ánh sáng, mức chi tiết so với asset đã duyệt.

## 2. Tỉ lệ nhân vật — `TBD`

| Thông số | Giá trị | Trạng thái |
|---|---|---|
| Chiều cao nhân vật chuẩn (pixel / unit) | — | `TBD` |
| Tỉ lệ đầu–thân (ví dụ chibi vs thực tế) | — | `TBD` |
| Kích thước tương đối NPC / kẻ địch thường / boss | — | `TBD` |

Cần một **bảng tỉ lệ (scale lineup)** được duyệt trong M4 trước khi sản xuất hàng loạt.

## 3. Sprite dimensions và PPU — `TBD`

| Thông số | Giá trị | Trạng thái |
|---|---|---|
| Pixels Per Unit (PPU) toàn dự án | — | `TBD` |
| Kích thước khung sprite nhân vật | — | `TBD` |
| Kích thước tile | — | `TBD` |
| Độ phân giải tham chiếu (reference resolution) | — | `TBD` |
| Giới hạn kích thước texture/atlas (Android) | — | `TBD` |

Quy tắc (`PROPOSED`): một PPU duy nhất cho toàn dự án; mọi frame của cùng một animation có cùng kích thước khung.

## 4. Pivot — `PROPOSED`

| Loại asset | Pivot đề xuất | Lý do |
|---|---|---|
| Nhân vật, kẻ địch (đứng trên mặt đất) | Bottom-center (điểm chạm đất) | Đặt vị trí và sorting theo chân nhân vật nhất quán |
| Projectile, VFX | Center | Xoay/quét quanh tâm |
| Prop đặt trên mặt đất | Bottom-center | Như nhân vật |
| Tile | Theo grid của Tilemap | Theo chuẩn Unity Tilemap |
| UI | Theo layout UI | Do UI programmer quyết định |

Pivot phải **cố định qua mọi frame** của một animation (nếu không nhân vật sẽ "rung").

## 5. Animation frame requirements

Phương pháp animation `TBD` ([OQ-015](../00_governance/OPEN_QUESTIONS.md)). Danh sách animation tối thiểu phụ thuộc combat (OQ-005) và camera (OQ-002).

**Bộ animation tham chiếu** — `EXAMPLE — NOT APPROVED`, chỉ để ước lượng khối lượng:

| Animation | Lặp | Ghi chú |
|---|---|---|
| Idle | Có | |
| Walk / Run | Có | |
| Attack (mỗi đòn) | Không | Cần đánh dấu frame active cho hitbox |
| Hurt | Không | |
| Death | Không | |
| Skill / Dash / Jump | Tùy thiết kế | Phụ thuộc OQ-004, OQ-017 |

Quy tắc (`PROPOSED`):
- Mỗi animation khai báo: số frame, frame rate hoặc thời lượng từng frame, lặp hay không, frame sự kiện (active hitbox, âm thanh bước chân).
- Số hướng (1, 2 lật gương, 4, 8) xác định sau OQ-002 — đây là yếu tố chi phí lớn nhất.
- Frame từ công cụ AI phải được kiểm tra: cùng kích thước, cùng pivot, nhân vật không đổi chi tiết giữa các frame.

## 6. Naming conventions — `PROPOSED`

Định dạng: `<category>_<subject>_<variant>_<action>_<direction>_<index>.<ext>` — chữ thường, tiếng Anh, không dấu, nối bằng `_`, bỏ trường không dùng.

| Category | Ví dụ |
|---|---|
| `chr` — nhân vật | `chr_hero_default_walk_right_00.png` *(EXAMPLE)* |
| `enm` — kẻ địch, `boss` — boss | `enm_slime_green_attack_left_03.png` *(EXAMPLE)* |
| `env` — môi trường, `tile` — tileset | `tile_forest_ground_01.png` *(EXAMPLE)* |
| `prop` — vật thể | `prop_chest_wood_open.png` *(EXAMPLE)* |
| `ui`, `icon`, `vfx` | `icon_item_potion_red.png` *(EXAMPLE)* |

Sprite sheet: `<…>_sheet.png` kèm file mô tả frame nếu công cụ xuất ra. Tên subject khớp ID trong [CHARACTER_REGISTER](../03_narrative/CHARACTER_REGISTER.md) khi có.

## 7. Export formats — `PROPOSED`

| Loại | Định dạng bàn giao | Ghi chú |
|---|---|---|
| Sprite, tile, UI, icon | PNG 32-bit có alpha, nền trong suốt | Không dùng JPG cho sprite |
| File nguồn | Định dạng gốc của công cụ (ví dụ .psd, .aseprite, .kra) nếu có | Lưu trong thư mục source, không trong Unity `Assets/` nếu không cần |
| Concept, moodboard | PNG/JPG | Không vào build |

Không đặt màu nền giả trong suốt (ô caro) vào ảnh — kiểm tra kênh alpha thật.

## 8. Asset versioning

- Phiên bản ghi trong [ASSET_MANIFEST](ASSET_MANIFEST.md) (`v1`, `v2`…), **không** ghi vào tên file dùng trong Unity (để không làm vỡ tham chiếu).
- Thay asset đã tích hợp → giữ nguyên tên file và GUID Unity (ghi đè file), ghi phiên bản mới + lý do trong manifest.
- File nguồn và concept cũ được giữ lại (lưu trữ), không xóa.
- Khi có version control: file nhị phân quản lý bằng Git LFS (OQ-009).

## 9. Copyright và originality

- **Nguyên tắc P12:** không sao chép nhân vật, logo, sprite, bản đồ, UI đặc trưng của game khác (bao gồm Ngọc Rồng Online, Ninja School) hay của bất kỳ tác phẩm có bản quyền nào.
- Không dùng prompt yêu cầu "theo phong cách của <nghệ sĩ còn hoạt động / game cụ thể>".
- Tham khảo chỉ để học nguyên lý (bố cục, silhouette, độ đọc), ghi nguồn trong brief.
- **Hình ảnh AI tạo không mặc nhiên dùng được trực tiếp.** Mỗi asset AI phải: qua technical validation, qua originality review (so với tham khảo đã dùng), ghi công cụ và mức chỉnh sửa trong manifest.
- Điều khoản sử dụng thương mại của từng công cụ AI phải được kiểm tra trước khi asset từ công cụ đó được dùng trong bản phát hành — trách nhiệm theo dõi: Claude; quyết định: GD.
- Font, texture, asset từ bên thứ ba: chỉ dùng khi license cho phép sử dụng thương mại; ghi license trong manifest.

## 10. Asset acceptance — checklist Technical Validation

| # | Kiểm tra | Bắt buộc |
|---|---|---|
| 1 | Có concept `APPROVED` (nếu là asset quan trọng) | ✓ |
| 2 | Tên file đúng §6 | ✓ |
| 3 | Định dạng, alpha thật đúng §7 | ✓ |
| 4 | Kích thước khung, PPU đúng §3 | ✓ |
| 5 | Pivot đúng và ổn định qua mọi frame §4 | ✓ |
| 6 | Đủ animation và frame theo brief §5 | ✓ |
| 7 | Nhất quán với character sheet / style guide §1 | ✓ |
| 8 | Đọc được ở kích thước hiển thị trên điện thoại | ✓ |
| 9 | Provenance và originality ghi trong manifest §9 | ✓ |
| 10 | Kích thước file/texture trong giới hạn | Khi giới hạn được chốt |
