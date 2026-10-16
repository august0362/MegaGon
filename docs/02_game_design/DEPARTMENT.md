# Department 02 — Game Design

> **Document Owner:** Claude (đặc tả) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [GAME_DESIGN](GAME_DESIGN.md) · [COMBAT_DESIGN](COMBAT_DESIGN.md) · [SYSTEMS_OVERVIEW](SYSTEMS_OVERVIEW.md) · [LEVEL_DESIGN](LEVEL_DESIGN.md)

## 1. Mission

Thiết kế trải nghiệm chơi — di chuyển, chiến đấu, khám phá, phát triển nhân vật — thành các quy tắc rõ ràng, kiểm chứng được và triển khai được trên cả PC lẫn Android.

## 2. Scope

**Trong phạm vi:** core gameplay loop, quy tắc di chuyển, real-time combat, kỹ năng, progression, equipment/inventory, khám phá, enemy/boss, level design, cân bằng.
**Ngoài phạm vi:** nội dung câu chuyện (03), hình ảnh (04), cách cài đặt kỹ thuật (05).

## 3. Roles

| Vai trò | Đảm nhận hiện tại | Trọng tâm |
|---|---|---|
| Game Designer | Claude (đặc tả) — GD quyết định | Vision → quy tắc, core loop |
| Character Mechanics Designer | Claude | Di chuyển, điều khiển, cảm giác |
| Combat Designer | Claude | Tấn công, phòng thủ, hit/hurt, nhịp chiến đấu |
| Skill Designer | Claude | Kỹ năng, tài nguyên, cooldown |
| System Designer | Claude | Inventory, equipment, economy, tương tác hệ thống |
| Progression Designer | Claude | Chỉ số, cấp độ, mở khóa |
| Level Designer | Claude (khung) — nội dung theo camera đã chốt | Bố cục, metrics, nhịp độ khu vực |
| Enemy & Boss Designer | Claude | Hành vi, pattern, độ khó |
| Balance Designer | Claude (đề xuất dải) · Codex (tuning trong dải) | Số liệu, đường cong độ khó |

ChatGPT và Gemini có thể đóng vai trò phản biện cho bất kỳ vai trò nào khi GD yêu cầu.

## 4. Responsibilities

- Chuyển quyết định thiết kế đã duyệt thành Feature Spec.
- Phân tích phương án cho các OQ thiết kế (OQ-001 → OQ-005, OQ-016 → OQ-018, OQ-023).
- Xác định tham số tuning, dải giá trị và cách chỉnh qua dữ liệu.
- Viết acceptance criteria về cảm giác chơi (feel) và quy tắc.
- Đảm bảo mọi thiết kế có mục Platform Considerations (PC + Android).

## 5. Deliverables

GAME_DESIGN, COMBAT_DESIGN, SYSTEMS_OVERVIEW, LEVEL_DESIGN; Feature Specs `FS-NNN` trong `docs/02_game_design/specs/`; bảng tham số tuning; checklist playtest.

## 6. Input Requirements

Decision Records `APPROVED` (vision, camera, combat direction); phản hồi playtest của GD; ràng buộc kỹ thuật từ 05; ràng buộc art (kích thước nhân vật, animation) từ 04.

## 7. Output Contracts

- Feature Spec theo [FEATURE_SPEC_TEMPLATE](../templates/FEATURE_SPEC_TEMPLATE.md).
- Mọi số liệu trong spec có nhãn trạng thái; số liệu chưa duyệt là `PROPOSED` hoặc `EXAMPLE — NOT APPROVED`.
- Tham số tuning khai báo kèm: tên, đơn vị, giá trị mặc định đề xuất, dải hợp lệ — để Codex hiện thực hóa thành dữ liệu cấu hình.

## 8. Dependencies

- Phụ thuộc: GD (quyết định), 03 (narrative cho quest/khám phá), 04 (kích thước và animation ảnh hưởng hitbox, timing), 05 (khả thi kỹ thuật).
- Bị phụ thuộc: 05 (triển khai), 07 (tiêu chí test), 04 (yêu cầu animation từ combat).

## 9. Workflows

1. OQ → Claude lập phương án (có thể kèm phân tích ChatGPT/Gemini) → GD quyết định → Decision Record.
2. Decision → Feature Spec → GD duyệt (L1) → task cho Codex.
3. Prototype → playtest của GD → điều chỉnh tuning (L0 trong dải) hoặc CR (ngoài dải/đổi cơ chế).

## 10. Quality Gates

- Không spec nào dựa trên OQ còn `TBD` mà không ghi rõ giả định tạm thời được GD cho phép.
- Mọi cơ chế có cách kiểm chứng (test tự động hoặc kịch bản playtest).
- Mọi spec có Platform Considerations.
- Không có số liệu bịa đặt được trình bày như yêu cầu chính thức.

## 11. Approval Authority

Game Director phê duyệt core loop, cơ chế, hệ thống, cân bằng ngoài dải (L1/L2). Claude quyết định tuning trong dải đã duyệt (L0).

## 12. Assigned Agents

Đặc tả: **Claude**. Triển khai: **Codex**. Phê duyệt: **Game Director**. Tư vấn: ChatGPT, Gemini.

## 13. Documentation Ownership

Claude sở hữu toàn bộ `docs/02_game_design/`. Codex không sửa tài liệu thiết kế; đề xuất thay đổi qua handoff report.

## 14. Escalation Rules

- Codex phát hiện cơ chế bất khả thi hoặc quá đắt → báo Claude → Claude chỉnh spec (L0) hoặc lập CR (L1).
- Playtest cho thấy cơ chế cốt lõi không đạt → Claude trình GD phương án thay thế.
- Mâu thuẫn với narrative hoặc art → Claude điều phối; nếu ảnh hưởng quyết định đã duyệt → GD.
