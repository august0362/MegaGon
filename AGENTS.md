# AGENTS.md

Hướng dẫn chung cho mọi AI agent làm việc trong repository này (Codex, Antigravity và các agent khác). File này chỉ dẫn đường — quy tắc chi tiết nằm ở tài liệu được liên kết.

## 1. Xác định vai trò của bạn

| Agent | File vai trò |
|---|---|
| Codex | [agents/CODEX.md](agents/CODEX.md) |
| Antigravity | [agents/ANTIGRAVITY.md](agents/ANTIGRAVITY.md) |
| Claude | [CLAUDE.md](CLAUDE.md) → [agents/CLAUDE.md](agents/CLAUDE.md) |
| ChatGPT / Gemini | [agents/CHATGPT.md](agents/CHATGPT.md) / [agents/GEMINI.md](agents/GEMINI.md) |

Tổng quan và mô hình giao tiếp: [docs/00_governance/AGENT_ROLES.md](docs/00_governance/AGENT_ROLES.md).

## 2. Chỉ làm việc khi có task

Codex và Antigravity chỉ thực hiện công việc có **task record** đạt Definition of Ready ([DEFINITION_OF_READY_DONE](docs/00_governance/DEFINITION_OF_READY_DONE.md)). Task nằm trong [BACKLOG](docs/01_production/BACKLOG.md) hoặc `docs/01_production/tasks/`.

## 3. Quy tắc chung

- Game Director là người quyết định cuối cùng. Agent không tự phê duyệt.
- Chưa có trong [DECISION_LOG](docs/00_governance/DECISION_LOG.md) thì chưa phải quyết định. Mục `TBD`/`PROPOSED`/`EXAMPLE — NOT APPROVED` không phải yêu cầu.
- Chỉ sửa file trong phạm vi task. Không cài dependency, không commit/push/merge khi chưa được phép, không chạy lệnh phá hủy dữ liệu.
- Thiếu thông tin hoặc thấy mâu thuẫn → dừng phần đó và báo lại, không tự đoán.
- Mọi bàn giao kèm handoff report và bằng chứng thật ([WORKFLOW §2](docs/00_governance/WORKFLOW.md#2-handoff-protocol)).
- Tôn trọng nguyên tắc nguyên bản (P12): không sao chép nội dung của game khác.

## 4. Quy ước

ID, trạng thái: [DECISION_POLICY §5–6](docs/00_governance/DECISION_POLICY.md#5-từ-vựng-trạng-thái). Code và module: [MODULE_BOUNDARIES](docs/05_engineering/MODULE_BOUNDARIES.md). Asset: [ASSET_SPEC](docs/04_art/ASSET_SPEC.md).
