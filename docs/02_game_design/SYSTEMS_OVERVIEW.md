# Systems Overview

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [GAME_DESIGN](GAME_DESIGN.md) · [COMBAT_DESIGN](COMBAT_DESIGN.md) · [MODULE_BOUNDARIES](../05_engineering/MODULE_BOUNDARIES.md) · [STORY_ARCHITECTURE](../03_narrative/STORY_ARCHITECTURE.md)

Danh sách hệ thống gameplay dự kiến, trạng thái thiết kế và milestone cần đến. Việc một hệ thống **có mặt trong danh sách không có nghĩa là đã được duyệt sẽ có trong game** — trừ khi ghi `APPROVED`.

---

## 1. Danh mục hệ thống

| Hệ thống | Mô tả | Trạng thái thiết kế | Cần cho | OQ |
|---|---|---|---|---|
| Character Movement | Điều khiển và di chuyển nhân vật | `TBD` | M2 | OQ-004 |
| Camera | Theo dõi nhân vật, giới hạn khu vực | `TBD` | M2 | OQ-002 |
| Combat | Tấn công, hit/hurt, sát thương, chết | Real-time Action `APPROVED`; chi tiết `TBD` | M2 | OQ-005 |
| Enemy AI | Hành vi kẻ địch | `TBD` | M2 (cơ bản), M5 (boss) | OQ-005 |
| Skills | Kỹ năng chủ động/bị động | `TBD` | M5 | OQ-017 |
| Character System | Một nhân vật / lớp nhân vật / party | `TBD` | M5 | OQ-016 |
| Stats & Progression | Chỉ số, cấp độ, mở khóa | `TBD` | M5 | OQ-018 |
| Inventory | Lưu trữ vật phẩm | `TBD` — chưa xác định có hay không | M5 | OQ-023 |
| Equipment | Trang bị ảnh hưởng chỉ số/ngoại hình | `TBD` — chưa xác định có hay không | M5 | OQ-023 |
| Economy | Tiền tệ, mua bán | `TBD` — chưa xác định có hay không | Sau M5 | OQ-025 |
| Exploration & Interaction | Tương tác vật thể, NPC, chuyển khu vực | `TBD` | M3 | OQ-002 |
| Quest | Nhiệm vụ | Khung kiến trúc `PROPOSED` | M3 | [QUEST_DIALOGUE_DESIGN](../03_narrative/QUEST_DIALOGUE_DESIGN.md) |
| Dialogue | Hội thoại | Khung kiến trúc `PROPOSED` | M3 | OQ-020 |
| Save/Load | Lưu tiến độ | Yêu cầu khung `PROPOSED`; chế độ lưu `TBD` | M3 | OQ-019 |
| UI/HUD | Máu, kỹ năng, menu, điều khiển cảm ứng | `TBD` | M2 (tối thiểu), M5 | OQ-008 |
| Audio feedback | Âm thanh phản hồi sự kiện | `TBD` | M5 | OQ-026 |

## 2. Phụ thuộc giữa các hệ thống

```
Movement ─► Combat ─► Enemy AI
   │          │
   │          └─► Skills ─► Stats & Progression ◄─ Equipment ◄─ Inventory
   │                                ▲
Exploration/Interaction ─► Dialogue ─► Quest ─┘ (phần thưởng)
                                     │
               Save/Load ◄── mọi hệ thống có trạng thái bền vững
UI ─► đọc trạng thái của mọi hệ thống (không sở hữu logic gameplay)
```

Ý nghĩa: không thiết kế Progression trước khi có Combat và Character System; không thiết kế Equipment trước khi có Stats. Quy tắc phụ thuộc phía code: [MODULE_BOUNDARIES](../05_engineering/MODULE_BOUNDARIES.md).

## 3. Thứ tự thiết kế đề xuất — `PROPOSED`

1. M1: Movement, Camera, Combat cơ bản, Enemy AI cơ bản, UI tối thiểu (đủ cho prototype).
2. Trước M3: Exploration/Interaction, Dialogue, Quest, Save/Load.
3. Trước M5: Character System, Skills, Stats & Progression, Inventory/Equipment (nếu được duyệt), Boss.
4. Sau M5: Economy và hệ thống mở rộng (nếu được duyệt).

## 4. Quy tắc chung cho mọi hệ thống

- Dữ liệu cấu hình tách khỏi logic (P5).
- Trạng thái cần lưu được khai báo rõ trong spec (phục vụ Save/Load).
- Mỗi hệ thống có mục Platform Considerations.
- Số liệu chưa duyệt ghi `PROPOSED` hoặc `EXAMPLE — NOT APPROVED`.
