# Combat Design

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` (cấu trúc) · nội dung `TBD` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [GAME_DESIGN](GAME_DESIGN.md) · [SYSTEMS_OVERVIEW](SYSTEMS_OVERVIEW.md) · [D-0004](../00_governance/DECISION_LOG.md#d-0004--phong-cách-chiến-đấu-real-time-action) · [OQ-005](../00_governance/OPEN_QUESTIONS.md)

**Đã duyệt:** chiến đấu Real-time Action (D-0004). **Mọi chi tiết khác là `TBD`.** Combat Direction là một trong ba quyết định ưu tiên của M1; nó phụ thuộc góc nhìn camera (OQ-002).

---

## 1. Các trục thiết kế cần quyết định

| # | Trục | Phương án tham khảo | Phụ thuộc | Trạng thái |
|---|---|---|---|---|
| 1 | Mô hình tấn công | Combo đòn thường; đòn đơn có thời gian hồi; chủ yếu kỹ năng | OQ-003 | `TBD` |
| 2 | Nhắm mục tiêu | Theo hướng nhân vật; theo con trỏ chuột (PC); auto-target/soft lock-on; lock-on cứng | OQ-002, OQ-008 | `TBD` |
| 3 | Hit detection | Hitbox/hurtbox theo frame animation; vùng va chạm đơn giản theo thời gian; projectile | OQ-015 | `TBD` |
| 4 | Phòng thủ / né | Dash/né có i-frames; đỡ đòn; parry; không có | OQ-004 | `TBD` |
| 5 | Phản hồi đòn đánh (game feel) | Hitstop, knockback, rung camera, flash, số sát thương | — | `TBD` |
| 6 | Kỹ năng | Xem [§5](#5-kỹ-năng-skills--tbd) | OQ-017 | `TBD` |
| 7 | Tài nguyên chiến đấu | Máu; năng lượng/mana; stamina; cooldown | OQ-017, OQ-018 | `TBD` |
| 8 | Độ khó và nhịp | Ít kẻ địch mạnh vs đông kẻ địch yếu | OQ-001 | `TBD` |

## 2. Ràng buộc nền tảng cho combat

- **Android:** combat phải chơi được bằng cảm ứng mà không cần độ chính xác như chuột. Số nút ảo đồng thời cần được giới hạn (con số cụ thể `TBD`, kiểm chứng qua playtest M2).
- **PC:** không mặc định người chơi dùng gamepad (OQ-008).
- Độ trễ từ input tới phản hồi trên màn hình là tiêu chí playtest bắt buộc trên cả hai nền tảng.

## 3. Mô hình trạng thái chiến đấu (khung kiến trúc)

Mô tả ở mức khái niệm — **không** phải danh sách trạng thái đã duyệt:

```
Idle ⇄ Move → Attack(windup → active → recovery) → Idle
          ↘ Defend/Evade (nếu có) ↗
Any → Hurt → (Idle | Dead)
```

Quy tắc khung (`PROPOSED`):
- Mỗi đòn đánh chia pha *windup / active / recovery* để có thể chỉnh cảm giác qua dữ liệu.
- Hitbox chỉ hoạt động trong pha *active*.
- Thời lượng các pha là tham số tuning, không hardcode.

## 4. Kẻ địch và boss — `TBD`

| Hạng mục | Cần quyết định |
|---|---|
| Phân loại kẻ địch | Vai trò (cận chiến, tầm xa, hỗ trợ…), số loại cho prototype và vertical slice |
| Hành vi AI | Mức phức tạp: state machine đơn giản (patrol → chase → attack) là đủ cho M2 (`PROPOSED`) |
| Telegraph | Cách báo hiệu đòn đánh để người chơi phản ứng |
| Boss | Số phase, cơ chế đặc biệt — chỉ cần cho M5 |

> `EXAMPLE — NOT APPROVED`: một kẻ địch cận chiến cơ bản cho prototype có thể có các trạng thái *Patrol → Chase → Telegraph → Attack → Cooldown*. Không phải yêu cầu.

## 5. Kỹ năng (Skills) — `TBD`

[OQ-017](../00_governance/OPEN_QUESTIONS.md). Cần quyết định: cách nhận kỹ năng, số kỹ năng có thể trang bị cùng lúc, tài nguyên sử dụng, nâng cấp, gắn với lớp nhân vật hay không (OQ-016).

Nguyên tắc dữ liệu (`PROPOSED`): mọi kỹ năng được định nghĩa bằng dữ liệu (P5) — xem [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md). **Không có số kỹ năng, hệ phái hay chỉ số sát thương nào được duyệt.**

## 6. Tham số tuning (khung)

Khi Combat Direction được duyệt, spec phải liệt kê tham số theo mẫu:

| Tham số | Đơn vị | Mặc định đề xuất | Dải hợp lệ | Trạng thái |
|---|---|---|---|---|
| *(ví dụ cấu trúc)* attack_windup | giây | — | — | `TBD` |

## 7. Tiêu chí đánh giá cảm giác chiến đấu (cho playtest M2)

Khung câu hỏi (`PROPOSED`), chi tiết hóa trong M1-QA-001:
1. Người chơi có hiểu vì sao mình trúng đòn hoặc đánh trúng không?
2. Input có cảm giác phản hồi ngay không (PC và Android)?
3. Đòn đánh có "lực" không (feedback thị giác/âm thanh)?
4. Điều khiển cảm ứng có gây mệt hoặc che màn hình quá nhiều không?
