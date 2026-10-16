# Department 07 — QA & Release

> **Document Owner:** Claude (giám sát) · **Executor:** Codex (QA cơ bản) · **Approver:** Game Director (nghiệm thu) · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [TEST_STRATEGY](TEST_STRATEGY.md) · [ACCEPTANCE_CRITERIA](ACCEPTANCE_CRITERIA.md) · [RELEASE_CHECKLIST](RELEASE_CHECKLIST.md) · [DEFINITION_OF_READY_DONE](../00_governance/DEFINITION_OF_READY_DONE.md)

## 1. Mission

Đảm bảo không có tuyên bố chất lượng nào thiếu bằng chứng, và mọi bản build tới tay Game Director hoặc người chơi đã được kiểm tra đúng mức.

## 2. Scope

**Trong phạm vi:** test strategy, acceptance criteria, unit/integration/regression test, gameplay test cơ bản, narrative progression test, visual review, build validation PC/Android, performance checks, release checklist.
**Ngoài phạm vi:** quyết định thiết kế khi test phát hiện vấn đề trải nghiệm (chuyển 02/GD).

## 3. Roles

| Vai trò | Đảm nhận | Ghi chú |
|---|---|---|
| QA Lead | Claude | Chiến lược, đánh giá bằng chứng, quyết định pass/fail kỹ thuật |
| Test Engineer | Codex | Viết và chạy test tự động |
| Gameplay Tester | Codex (kịch bản cơ bản) · **GD** (cảm giác, trải nghiệm) | AI không thay thế được đánh giá cảm giác chơi |
| Narrative QA | Codex (test progression tự động) · Claude (continuity) | |
| Visual QA | Antigravity | Review asset trong game |
| Performance Tester | Codex (profiling) · GD hoặc người được chỉ định (thiết bị thật) | Phụ thuộc OQ-011 |
| Build Engineer | Codex | Build PC/Android, log |
| Release Manager | Claude (checklist) · **GD** (go/no-go) | |

## 4. Responsibilities

- Duy trì TEST_STRATEGY, ACCEPTANCE_CRITERIA, RELEASE_CHECKLIST.
- Codex viết/chạy test, build, báo cáo kèm output.
- Claude đánh giá bằng chứng, xác định phần chưa kiểm chứng, yêu cầu sửa lỗi.
- GD nghiệm thu trải nghiệm cuối cùng.
- Quản lý bug: phân loại, ưu tiên, theo dõi.

## 5. Deliverables

Test suites, test reports, bug reports, build reports, performance reports, Acceptance Records, release checklist hoàn tất.

## 6. Input Requirements

Feature Spec với acceptance criteria; task records; build; cấu hình thử nghiệm đã duyệt (OQ-011).

## 7. Output Contracts

- Test report: lệnh/công cụ đã chạy, số test, pass/fail, output, môi trường (Unity version, nền tảng).
- Bug report: theo mẫu trong [TEST_STRATEGY §6](TEST_STRATEGY.md#6-bug-report).
- Acceptance Record: theo [ACCEPTANCE_CRITERIA §5](ACCEPTANCE_CRITERIA.md#5-acceptance-log).

## 8. Dependencies

Phụ thuộc mọi bộ phận (đối tượng test), 05 (khả năng test của code), OQ-011 (thiết bị), OQ-022 (CI). Bị phụ thuộc: 01 (milestone gate), GD (nghiệm thu).

## 9. Workflows

Theo Step 7–8 của [WORKFLOW](../00_governance/WORKFLOW.md#1-quy-trình-thực-hiện-một-tính-năng-feature-workflow): Codex test → Claude đối chiếu yêu cầu → Antigravity visual review → GD nghiệm thu. Bug: phát hiện → BUG-NNN → phân loại (Claude) → sửa (Codex) → verify → đóng.

## 10. Quality Gates

- **Không tuyên bố tính năng đã qua kiểm thử nếu chưa có bằng chứng.**
- Không đóng bug khi chưa verify.
- Không release khi còn bug Blocker/Critical (trừ miễn trừ của GD, có ghi nhận).
- Build Android phải được kiểm tra trên thiết bị thật trước milestone yêu cầu Android.

## 11. Approval Authority

Claude: pass/fail kỹ thuật, phân loại bug (L0). GD: nghiệm thu trải nghiệm, miễn trừ bug blocking, go/no-go phát hành.

## 12. Assigned Agents

**Codex** (thực thi QA cơ bản), **Claude** (giám sát), **Antigravity** (visual QA), **Game Director** (nghiệm thu).

## 13. Documentation Ownership

Claude: TEST_STRATEGY, ACCEPTANCE_CRITERIA, RELEASE_CHECKLIST. Codex: test reports, build reports.

## 14. Escalation Rules

- Không chạy được test/build trong môi trường hiện có → Codex báo Claude ngay (R-005).
- Bug Blocker/Critical gần milestone gate → Claude báo GD kèm phương án (sửa, hoãn, miễn trừ).
- Kết quả playtest mâu thuẫn spec → chuyển 02, có thể CR.
