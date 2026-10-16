# Backlog

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director (ưu tiên L1) · **Status:** `ACTIVE` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [MILESTONES](MILESTONES.md) · [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md) · [DEFINITION_OF_READY_DONE](../00_governance/DEFINITION_OF_READY_DONE.md)

Trạng thái task: [DECISION_POLICY §5.4](../00_governance/DECISION_POLICY.md#54-trạng-thái-task). Task ID: `M<n>-<DEPT>-NNN`.
Task nhỏ ghi trực tiếp ở đây; task lớn có file riêng `tasks/<TASK-ID>.md` theo [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md).

---

## M0 — Governance Foundation

| Task ID | Objective | Owner | Status | Bằng chứng |
|---|---|---|---|---|
| M0-PRD-001 | Kiểm tra thư mục làm việc, xác định file cần bảo vệ | Claude | `DONE` | Thư mục rỗng, không phải git repo (2026-10-15) |
| M0-PRD-002 | Tạo governance foundation (`docs/00_governance/`) | Claude | `IN_REVIEW` | 9 file — chờ GD nghiệm thu |
| M0-PRD-003 | Tạo agent role files (`agents/`) và hướng dẫn gốc | Claude | `IN_REVIEW` | 6 file + README, CLAUDE.md, AGENTS.md |
| M0-PRD-004 | Tạo 7 department charter và tài liệu chuyên môn | Claude | `IN_REVIEW` | `docs/01_…07_` |
| M0-PRD-005 | Tạo roadmap, milestone framework, risk register | Claude | `IN_REVIEW` | `docs/01_production/` |
| M0-PRD-006 | Tạo 5 template | Claude | `IN_REVIEW` | `docs/templates/` |
| M0-PRD-007 | Kiểm tra link, trạng thái, phân quyền, tính nhất quán | Claude | `IN_REVIEW` | Báo cáo hoàn thành M0 |
| M0-PRD-008 | Game Director nghiệm thu M0 | Game Director | `BACKLOG` | Acceptance Record ACC-001 |

---

## M1 — Game Vision & Design Discovery (kế hoạch)

Các task dưới đây **chưa READY**. Chúng chỉ được chuyển `READY` sau khi M0 được nghiệm thu và đủ DoR.

| Task ID | Objective | Owner | Phụ thuộc | Status |
|---|---|---|---|---|
| M1-PRD-001 | ★ Xác minh năng lực Codex: môi trường có Unity không, chạy được batchmode test/build không, build Android được không | Codex (Claude soạn task) | D-0012, OQ-006 (cần phiên bản Unity để thử) | `BACKLOG` |
| M1-PRD-002 | Thiết lập version control theo quyết định OQ-009 | Codex hoặc GD | OQ-009 | `BLOCKED` |
| M1-PRD-003 | Lập kế hoạch M2 và phân rã task | Claude | M1 exit decisions | `BACKLOG` |
| M1-GD-001 | Game Vision brief: khung câu hỏi + phương án để GD và advisor thảo luận | Claude | — | `BACKLOG` |
| M1-GD-002 | Phân tích so sánh góc nhìn camera | Claude (tư vấn: ChatGPT, Gemini, Codex) | M1-GD-001 | `BACKLOG` |
| M1-GD-003 | Đề xuất các phương án core gameplay loop | Claude | OQ-001 | `BLOCKED` |
| M1-GD-004 | Đề xuất các phương án Combat Direction cho prototype | Claude | OQ-002, OQ-003 | `BLOCKED` |
| M1-GD-005 | Đề xuất mô hình di chuyển | Claude | OQ-002 | `BLOCKED` |
| M1-NAR-001 | Khung workshop thế giới/tông giọng (câu hỏi định hướng, không viết canon) | Claude | OQ-001 | `BACKLOG` |
| M1-ART-001 | ★ Art research + moodboard cho ≥3 hướng Art Direction | Antigravity | D-0012, M0 accepted | `BACKLOG` |
| M1-ART-002 | ★ Thử năng lực: nhân vật thử nghiệm trung tính qua nhiều tư thế, 1 chu kỳ đi bộ — **chỉ để đánh giá công cụ**, không phải asset dự án | Antigravity | D-0012 | `BACKLOG` |
| M1-ENG-001 | Technical options brief: Unity version, render pipeline, input, VCS, vị trí project | Claude (Codex góp ý khả thi) | — | `BACKLOG` |
| M1-ENG-002 | Spec kiến trúc phạm vi prototype M2 | Claude | OQ-002, OQ-005, OQ-006–OQ-010 | `BLOCKED` |
| M1-QA-001 | Checklist đánh giá cảm giác điều khiển/chiến đấu cho playtest M2 | Claude | OQ-005 | `BLOCKED` |

★ = thuộc đề xuất [D-0012](../00_governance/DECISION_LOG.md#d-0012--điều-chỉnh-nhỏ-cho-kế-hoạch-milestone) (`PROPOSED`). Nếu GD bác bỏ D-0012, các task này chuyển `CANCELLED`.

---

## M2–M7

Chưa phân rã. Sẽ được lập khi milestone trước đó gần hoàn tất và các quyết định phụ thuộc đã có — tránh lập task dựa trên giả định chưa được duyệt.
