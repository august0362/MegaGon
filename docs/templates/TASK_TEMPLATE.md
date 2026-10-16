# Task Template

> **Document Owner:** Claude · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [WORKFLOW §2](../00_governance/WORKFLOW.md#2-handoff-protocol) · [DEFINITION_OF_READY_DONE](../00_governance/DEFINITION_OF_READY_DONE.md) · [BACKLOG](../01_production/BACKLOG.md)

Task record phải **tự đủ ngữ cảnh**: agent nhận việc chỉ cần đọc task và các tài liệu được liên kết. Lưu tại `docs/01_production/tasks/<TASK-ID>.md` (task lớn) hoặc trực tiếp trong BACKLOG (task nhỏ). Mọi trường ★ bắt buộc để đạt DoR.

---

```markdown
# <TASK-ID> — <Tiêu đề> ★

- **Owner:** Codex / Antigravity / Claude ★
- **Status:** BACKLOG / READY / IN_PROGRESS / IN_REVIEW / DONE / BLOCKED / CANCELLED ★
- **Milestone:** M<n> · **Priority:**
- **Created by / Date:** Claude ·

## Objective ★
Một câu, đo được.

## Input References ★
- Spec: FS-NNN · Decision: D-NNNN · Contract: DC-… · Art Brief: AB-NNN
- Tài liệu khác:

## Scope ★
**Trong phạm vi:**
-
**Ngoài phạm vi:**
-
**File/thư mục được phép thay đổi:**
-

## Dependencies ★
- Task / quyết định phải xong trước:

## Deliverables / Output Contract ★
- Đầu ra, định dạng, vị trí:

## Acceptance Criteria ★
- AC-1:
- AC-2:

## Validation Method ★
- Cách kiểm chứng từng AC (test tự động, manual, visual review…)

## Platform Scope ★
- PC / Android / Both

## Completion Evidence ★
- Bằng chứng cần nộp (test output, build log, ảnh/video, file asset…)

## Notes / Constraints
- Ví dụ: không thêm package; dùng placeholder art; không sửa scene X.

## Review (Claude điền)
- Kết luận: ACCEPTED / CHANGES_REQUESTED / ESCALATED · Ngày · Ghi chú
- Report: reports/<TASK-ID>-report.md
```
