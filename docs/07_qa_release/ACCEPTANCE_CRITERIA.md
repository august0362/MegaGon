# Acceptance Criteria

> **Document Owner:** Claude (QA Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [TEST_STRATEGY](TEST_STRATEGY.md) · [MILESTONES](../01_production/MILESTONES.md) · [DEFINITION_OF_READY_DONE](../00_governance/DEFINITION_OF_READY_DONE.md) · [FEATURE_SPEC_TEMPLATE](../templates/FEATURE_SPEC_TEMPLATE.md)

Quy định **cách viết** và **cách ghi nhận** tiêu chí nghiệm thu. Exit gate và tiêu chí của từng milestone nằm ở [MILESTONES](../01_production/MILESTONES.md); tiêu chí của từng feature nằm trong Feature Spec.

---

## 1. Ba cấp tiêu chí

| Cấp | Nơi viết | Ai kiểm chứng | Ai chấp nhận |
|---|---|---|---|
| Task | Task record | Codex / Antigravity | Claude |
| Feature | Feature Spec | Codex + Claude (+ Antigravity cho visual) | Claude (L0) / GD (L1) |
| Milestone | MILESTONES | Claude tổng hợp bằng chứng | GD |

## 2. Cách viết một acceptance criterion

Mỗi AC phải: **cụ thể, kiểm chứng được, có phương pháp kiểm chứng, có nền tảng áp dụng.**

Định dạng ưu tiên — Given / When / Then:

```
AC-<n>: Given <bối cảnh>, When <hành động>, Then <kết quả quan sát được>.
Verify: <unit test | integration test | manual | playtest | visual review>
Platform: PC | Android | Both
```

> `EXAMPLE — NOT APPROVED`:
> AC-1: Given nhân vật đứng yên trên mặt đất, When người chơi nhấn action Attack, Then animation tấn công bắt đầu trong khung hình kế tiếp và hitbox chỉ hoạt động trong pha active.
> Verify: PlayMode test + manual. Platform: Both.

**Không hợp lệ:** "Combat phải vui", "chạy mượt", "trông đẹp" — các mục cảm nhận được chuyển thành câu hỏi playtest cho GD (§3).

## 3. Tiêu chí trải nghiệm (playtest checklist)

Những gì không đo được tự động được đánh giá bằng checklist playtest do GD trả lời. Mỗi câu có thang trả lời (ví dụ Đạt / Gần đạt / Không đạt) và chỗ ghi nhận xét. Checklist cụ thể cho M2 được soạn trong M1-QA-001, dựa trên [COMBAT_DESIGN §7](../02_game_design/COMBAT_DESIGN.md#7-tiêu-chí-đánh-giá-cảm-giác-chiến-đấu-cho-playtest-m2).

## 4. Quy tắc

- AC được chốt **trước** khi task chuyển `READY` (DoR).
- Thay đổi AC của spec đã duyệt → CHANGE_CONTROL.
- AC "chưa kiểm chứng" phải có lý do và được người chấp nhận đồng ý rõ ràng; không được ngầm bỏ qua.

## 5. Acceptance Log

Ghi nhận mọi lần nghiệm thu của Game Director (feature L1, milestone, asset quan trọng, release).

| ACC ID | Đối tượng | Kết quả | Điều kiện / ghi chú | Bằng chứng | Người nghiệm thu | Ngày |
|---|---|---|---|---|---|---|
| ACC-001 | M0 — Governance Foundation | *Chờ* | — | Báo cáo hoàn thành M0 | Game Director | — |
