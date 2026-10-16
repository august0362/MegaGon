# Level Design

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` (khung) · nội dung `TBD` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [GAME_DESIGN §4](GAME_DESIGN.md#4-góc-nhìn-camera--tbd) · [WORLD_BIBLE](../03_narrative/WORLD_BIBLE.md) · [ASSET_SPEC](../04_art/ASSET_SPEC.md) · [UNITY_ARCHITECTURE_PROPOSAL](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md)

Level design phụ thuộc trực tiếp vào góc nhìn camera ([OQ-002](../00_governance/OPEN_QUESTIONS.md)) và mô hình di chuyển ([OQ-004](../00_governance/OPEN_QUESTIONS.md)). Tài liệu này chỉ định nghĩa **khung tổ chức và quy trình**; không có bản đồ nào được duyệt.

---

## 1. Đơn vị tổ chức thế giới — `PROPOSED`

| Cấp | Tên | Mô tả |
|---|---|---|
| 1 | **Region** | Vùng lớn có bản sắc riêng (thẩm mỹ, kẻ địch, câu chuyện) |
| 2 | **Area** | Một khu vực chơi liên tục — thường tương ứng một scene Unity hoặc một phần scene |
| 3 | **Zone** | Phần nhỏ trong Area có mục đích rõ (chiến đấu, khám phá, câu đố, nghỉ) |
| 4 | **Point of Interest** | NPC, rương, lối đi bí mật, điểm lưu… |

Số Region/Area: `TBD` ([OQ-024](../00_governance/OPEN_QUESTIONS.md)). Cách ánh xạ Area ↔ scene: xem [UNITY_ARCHITECTURE_PROPOSAL §5](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md#5-scene-management).

## 2. Level metrics — `TBD`

Phải chốt sau khi có camera, kích thước nhân vật và mô hình di chuyển:

| Metric | Phụ thuộc | Trạng thái |
|---|---|---|
| Kích thước tile / đơn vị lưới (pixels per unit) | Art Direction, ASSET_SPEC | `TBD` |
| Chiều cao/rộng nhân vật tính theo tile | ASSET_SPEC | `TBD` |
| Tầm nhìn camera (bao nhiêu tile hiển thị) | Camera, tỉ lệ màn hình PC/Android | `TBD` |
| Khoảng cách nhảy/dash (nếu có) | OQ-004 | `TBD` |
| Độ rộng lối đi tối thiểu | Movement, combat | `TBD` |

Tầm nhìn camera phải được kiểm tra ở cả tỉ lệ màn hình PC và Android (màn hình điện thoại dài hơn 16:9 là phổ biến).

## 3. Quy trình thiết kế một Area — `PROPOSED`

1. **Area Brief** — mục đích, vị trí trong tiến trình câu chuyện, kẻ địch, phần thưởng, thời lượng dự kiến.
2. **Paper layout** — sơ đồ khối (ảnh hoặc ASCII).
3. **Greybox** — Codex dựng bằng placeholder trong Unity theo layout.
4. **Playtest greybox** — GD đánh giá nhịp độ, độ khó, khả năng định hướng.
5. **Art pass** — chỉ sau khi greybox được chấp nhận và Art Direction `APPROVED`.
6. **Polish & validation** — kiểm tra va chạm, hiệu năng Android, điểm kẹt.

## 4. Mẫu Area Brief

```markdown
### Area: <AREA_ID> — <tên tạm>
- Region:
- Mục đích trong trải nghiệm:
- Liên kết narrative (story events, quest):
- Kẻ địch / thử thách:
- Phần thưởng / mở khóa:
- Lối vào / lối ra:
- Thời lượng chơi dự kiến:
- Platform notes (camera trên màn hình dài, vùng UI cảm ứng che khuất):
- Trạng thái: PROPOSED / APPROVED
```

## 5. Yêu cầu cho Vertical Slice (M5)

Một chuỗi Area đủ cho: mở đầu → thử thách → boss → kết thúc. Nội dung cụ thể `TBD` cho tới khi có thế giới và cốt truyện được duyệt.
