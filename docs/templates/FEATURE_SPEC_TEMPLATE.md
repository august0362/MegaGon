# Feature Specification Template

> **Document Owner:** Claude · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [WORKFLOW Step 3](../00_governance/WORKFLOW.md#1-quy-trình-thực-hiện-một-tính-năng-feature-workflow) · [DEFINITION_OF_READY_DONE §1.2](../00_governance/DEFINITION_OF_READY_DONE.md#12-feature-spec-sẵn-sàng-để-chia-task) · [ACCEPTANCE_CRITERIA](../07_qa_release/ACCEPTANCE_CRITERIA.md)

Lưu tại `docs/<bộ phận sở hữu>/specs/FS-NNN-<slug>.md`. Trường ★ bắt buộc.

---

```markdown
# FS-NNN — <Tên feature> ★

- **Status:** PROPOSED / UNDER_REVIEW / APPROVED / SUPERSEDED ★
- **Level:** L0 / L1 ★ · **Approver:** ★
- **Based on decisions:** D-NNNN, … ★
- **Owner (spec):** Claude · **Implementers:** Codex / Antigravity
- **Milestone:** M<n>
- **Version / Last Updated:**

## 1. Mục tiêu ★
Feature giải quyết điều gì cho người chơi / cho dự án.

## 2. Functional Requirements ★
| ID | Yêu cầu | Ưu tiên (Must/Should/Could) |
|---|---|---|
| FR-1 | | |

## 3. Non-functional Requirements ★
Hiệu năng, bộ nhớ, độ trễ input, khả năng mở rộng dữ liệu, khả năng test.

## 4. Platform Considerations (PC + Android) ★
Input, UI, hiệu năng, vòng đời app — khác biệt giữa hai nền tảng và cách xử lý.

## 5. Dependencies ★
Feature/module/quyết định/asset cần có trước.

## 6. Data Contracts ★
Contract sử dụng hoặc tạo mới (DC-…), trạng thái.

## 7. Tuning Parameters
| Tham số | Đơn vị | Mặc định đề xuất | Dải hợp lệ | Trạng thái |

## 8. Save/Load Impact
Trạng thái nào cần lưu; ảnh hưởng schema.

## 9. Art / Audio Requirements
Animation, VFX, UI art, audio cue cần cho feature (liên kết Art Brief).

## 10. Acceptance Criteria ★
AC theo định dạng ACCEPTANCE_CRITERIA §2.

## 11. Test Requirements ★
Unit / integration / manual / playtest — gắn với AC.

## 12. Scope Exclusions ★
Những gì feature **không** làm trong phiên bản này.

## 13. Open Questions
OQ liên quan còn `TBD` và giả định tạm thời (nếu GD cho phép).

## 14. Change Log
```
