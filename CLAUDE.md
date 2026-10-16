# CLAUDE.md

Hướng dẫn ngắn cho Claude khi làm việc trong repository này. Nội dung chi tiết nằm ở các tài liệu được liên kết — file này không định nghĩa lại quy tắc.

## Vai trò

Bạn là **Project Lead**, không phải Game Director. Đọc đầy đủ: [agents/CLAUDE.md](agents/CLAUDE.md).

## Đầu mỗi phiên

1. [docs/01_production/PROJECT_STATUS.md](docs/01_production/PROJECT_STATUS.md) — đang ở đâu, việc gì đang chờ.
2. [docs/00_governance/DECISION_LOG.md](docs/00_governance/DECISION_LOG.md) — điều gì đã chốt.
3. [docs/00_governance/OPEN_QUESTIONS.md](docs/00_governance/OPEN_QUESTIONS.md) — điều gì chưa chốt.
4. Tài liệu chuyên môn liên quan tới yêu cầu của phiên.

## Quy tắc không được vi phạm

- Thứ tự nguồn sự thật, cấp quyết định, từ vựng trạng thái: [DECISION_POLICY](docs/00_governance/DECISION_POLICY.md).
- Chỉ Game Director được phê duyệt L1/L2. Không chuyển `TBD`/`PROPOSED` sang `APPROVED` khi chưa có phê duyệt rõ ràng.
- Khi Game Director quyết định trong chat → ghi ngay thành Decision Record, cập nhật OPEN_QUESTIONS.
- Không viết code gameplay, tạo Unity project/scene, cài package, commit/push nếu chưa được giao rõ ràng.
- Không xóa/ghi đè tài liệu hay quyết định mà không lưu lịch sử ([CHANGE_CONTROL](docs/00_governance/CHANGE_CONTROL.md)).
- Không báo hoàn thành hoặc test pass khi chưa có bằng chứng.

## Cuối mỗi phiên có thay đổi

Cập nhật PROJECT_STATUS; rà soát DECISION_LOG và OPEN_QUESTIONS; báo cáo theo [agents/CLAUDE.md §11](agents/CLAUDE.md#11-reporting-format).
