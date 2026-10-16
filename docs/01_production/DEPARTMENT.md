# Department 01 — Production & Management

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ROADMAP](ROADMAP.md) · [MILESTONES](MILESTONES.md) · [BACKLOG](BACKLOG.md) · [PROJECT_STATUS](PROJECT_STATUS.md) · [RISK_REGISTER](RISK_REGISTER.md) · [agents/CLAUDE.md](../../agents/CLAUDE.md)

## 1. Mission

Giữ cho dự án có hướng đi rõ ràng, phạm vi được kiểm soát, quyết định được ghi lại và tiến độ được báo cáo trung thực.

## 2. Scope

**Trong phạm vi:** charter, roadmap, milestone, backlog, task, risk, decision log, open questions, change control, project status, quản lý phạm vi và nguồn lực, tính nhất quán tài liệu.
**Ngoài phạm vi:** nội dung sáng tạo (thuộc 02/03/04), quyết định kiến trúc (thuộc 05, duyệt bởi GD), thực thi code/art.

## 3. Roles

| Vai trò | Đảm nhận | Trọng tâm |
|---|---|---|
| Project Lead | Claude | Điều phối tổng thể, đặc tả, đề xuất L1/L2 |
| Producer | Claude (hỗ trợ: GD quyết định nguồn lực) | Phạm vi, nguồn lực, đánh đổi phạm vi–chất lượng |
| Project Manager | Claude | Milestone, dependency, tiến độ |
| Task Coordinator | Claude | Task record, handoff package, theo dõi trạng thái task |
| Documentation Manager | Claude | Cấu trúc tài liệu, link, trạng thái, lịch sử thay đổi |
| Risk Manager | Claude | Risk register, cảnh báo sớm |

## 4. Responsibilities

- Duy trì [PROJECT_CHARTER](../00_governance/PROJECT_CHARTER.md), [ROADMAP](ROADMAP.md), [MILESTONES](MILESTONES.md).
- Quản lý [BACKLOG](BACKLOG.md): tạo task đạt DoR, theo dõi trạng thái.
- Duy trì nghiêm ngặt [DECISION_LOG](../00_governance/DECISION_LOG.md) và [OPEN_QUESTIONS](../00_governance/OPEN_QUESTIONS.md).
- Vận hành [CHANGE_CONTROL](../00_governance/CHANGE_CONTROL.md).
- Cập nhật [PROJECT_STATUS](PROJECT_STATUS.md) và [RISK_REGISTER](RISK_REGISTER.md).
- Tổ chức milestone gate review, chuẩn bị bằng chứng để GD nghiệm thu.

## 5. Deliverables

Charter, roadmap, milestone plan, backlog, task records, decision records, OQ register, CR log, project status, risk register, milestone gate report.

## 6. Input Requirements

Quyết định của GD; phân tích của ChatGPT/Gemini (khi GD cung cấp); handoff report từ Codex/Antigravity; báo cáo của các bộ phận.

## 7. Output Contracts

- Task record theo [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md), đạt [DoR](../00_governance/DEFINITION_OF_READY_DONE.md#1-definition-of-ready).
- Decision Record theo [DECISION_RECORD_TEMPLATE](../templates/DECISION_RECORD_TEMPLATE.md).
- Milestone plan theo [MILESTONE_TEMPLATE](../templates/MILESTONE_TEMPLATE.md).
- PROJECT_STATUS luôn phản ánh trạng thái **có bằng chứng**.

## 8. Dependencies

Phụ thuộc vào GD (quyết định), mọi bộ phận (báo cáo). Mọi bộ phận phụ thuộc vào 01 để có task và thứ tự ưu tiên.

## 9. Workflows

- Feature workflow 9 bước và handoff: [WORKFLOW](../00_governance/WORKFLOW.md).
- Vòng đời quyết định: OQ → Decision Record → APPROVED/REJECTED ([DECISION_POLICY](../00_governance/DECISION_POLICY.md)).
- Milestone gate: Claude tổng hợp bằng chứng theo exit gate → trạng thái `GATE_REVIEW` → GD quyết định → `ACCEPTED` hoặc danh sách việc còn lại.

## 10. Quality Gates

- Không task nào chuyển `READY` khi chưa đạt DoR.
- Không task nào chuyển `DONE` khi chưa có bằng chứng và review `ACCEPTED`.
- Không milestone nào `ACCEPTED` khi chưa có phê duyệt của GD.
- Mỗi gate review: kiểm tra link, trạng thái, mâu thuẫn tài liệu.

## 11. Approval Authority

L0 (task, thứ tự, tài liệu, quy trình nội bộ): Claude. Phạm vi milestone lớn, exit gate, nguồn lực, timeline: Game Director ([AUTHORITY_MATRIX](../00_governance/AUTHORITY_MATRIX.md)).

## 12. Assigned Agents

Primary Executor: **Claude**. Game Director: phê duyệt. ChatGPT/Gemini: tư vấn khi GD yêu cầu.

## 13. Documentation Ownership

Claude sở hữu toàn bộ `docs/00_governance/` và `docs/01_production/`, `docs/templates/`, `agents/`, file gốc `README.md`, `CLAUDE.md`, `AGENTS.md`. Thay đổi quy tắc trong governance cần GD duyệt (sau khi M0 được nghiệm thu).

## 14. Escalation Rules

Claude chuyển lên GD khi: blocker ảnh hưởng exit gate, rủi ro mức High mới, yêu cầu thay đổi phạm vi, mâu thuẫn tài liệu không tự giải quyết được, hoặc GD cần quyết định để mở khóa task. Định dạng: [WORKFLOW §4](../00_governance/WORKFLOW.md#4-escalation).
