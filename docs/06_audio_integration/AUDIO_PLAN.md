# Audio Plan

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` — định hướng âm thanh `TBD`, nguồn audio `UNASSIGNED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [06_audio_integration/DEPARTMENT](DEPARTMENT.md) · [CONTENT_PIPELINE](CONTENT_PIPELINE.md) · [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md)

---

## 1. Định hướng âm thanh — `TBD`

Phụ thuộc Game Vision (OQ-001), tông giọng thế giới (OQ-012) và Art Direction (OQ-014). Sẽ gồm: phong cách nhạc, nhạc cụ/âm sắc chủ đạo, mức độ "game-y" hay hiện thực của SFX, vai trò của im lặng.

## 2. Danh mục yêu cầu audio (khung)

| Nhóm | Ví dụ loại (`EXAMPLE — NOT APPROVED`) | Cần từ | Mức ưu tiên |
|---|---|---|---|
| SFX nhân vật | Bước chân, tấn công, trúng đòn, chết, kỹ năng | M5 (placeholder từ M2 nếu cần) | Cao — phản hồi combat |
| SFX kẻ địch | Telegraph đòn đánh, trúng đòn, chết | M5 | Cao — người chơi cần nghe cảnh báo |
| SFX UI | Chọn, xác nhận, hủy, mở menu, nhận quest | M5 | Trung bình |
| SFX môi trường | Ambience theo khu vực, tương tác vật thể | M5 | Trung bình |
| Nhạc | Khám phá, chiến đấu, boss, thị trấn/an toàn, menu | M5 (tối thiểu) | Trung bình |
| Voice | Có hay không | `TBD` | — |

Danh sách cụ thể được lập theo từng Feature Spec (mục "Audio feedback") để không sót.

## 3. Ánh xạ event → audio

Âm thanh được kích hoạt bởi **event gameplay** (MODULE_BOUNDARIES), không gọi trực tiếp từ logic gameplay. Contract: DC-AUDIO-EVENTS.

| Event | Audio cue | Ghi chú |
|---|---|---|
| *(ví dụ cấu trúc)* `AttackHit` | `sfx_combat_hit_<material>` | `EXAMPLE — NOT APPROVED` |

## 4. Thông số kỹ thuật — `PROPOSED`

| Thông số | Đề xuất | Ghi chú |
|---|---|---|
| Định dạng bàn giao | WAV (PCM, không nén) | Unity tự nén khi build |
| Sample rate | 44.1 kHz hoặc 48 kHz — chọn một cho toàn dự án | `TBD` |
| Nén trong Unity | SFX ngắn: nạp vào bộ nhớ; nhạc dài: streaming | Cân nhắc bộ nhớ Android |
| Đặt tên | `sfx_<group>_<subject>_<action>_<variant>`, `mus_<context>_<name>` | Đồng bộ với ASSET_SPEC §6 |
| Âm lượng | Chuẩn hóa mức âm lượng giữa các file; có nhóm âm lượng Master/Music/SFX | Mức cụ thể `TBD` |

## 5. Nguồn audio — `UNASSIGNED`

[OQ-026](../00_governance/OPEN_QUESTIONS.md). Các phương án để GD cân nhắc (Claude không khuyến nghị cụ thể khi chưa có ngân sách):

| Phương án | Ưu | Nhược / cần kiểm tra |
|---|---|---|
| Thư viện SFX/nhạc có license thương mại | Nhanh, chất lượng ổn định | Chi phí; điều khoản license; bản sắc thấp |
| Người làm audio (freelance/đối tác) | Bản sắc, chất lượng | Chi phí, quản lý |
| Công cụ AI tạo audio | Nhanh, rẻ | **Chưa xác minh** chất lượng và điều khoản thương mại; cần thử nghiệm và review trước khi dùng |
| Kết hợp | Cân bằng | Cần quy tắc nhất quán |

Bất kể nguồn nào: mọi file audio phải có provenance và license được ghi lại trước khi tích hợp.

## 6. Placeholder audio

Cho M2–M3 có thể dùng placeholder có license rõ ràng hoặc không có âm thanh. Placeholder được ghi vào danh sách placeholder (giống ASSET_MANIFEST §3) và phải thay trước M5.
