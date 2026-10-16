# Decision Policy

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md) · [DECISION_LOG](DECISION_LOG.md) · [OPEN_QUESTIONS](OPEN_QUESTIONS.md) · [CHANGE_CONTROL](CHANGE_CONTROL.md) · [DECISION_RECORD_TEMPLATE](../templates/DECISION_RECORD_TEMPLATE.md)

Tài liệu này là **nguồn duy nhất** cho: thứ tự ưu tiên thông tin, cấp quyết định, quy tắc phê duyệt và toàn bộ từ vựng trạng thái của dự án. Tài liệu khác chỉ tham chiếu, không định nghĩa lại.

---

## 1. Single Source of Truth

Khi thông tin mâu thuẫn, ưu tiên theo thứ tự (1 cao nhất):

1. Quyết định đã được Game Director phê duyệt rõ ràng.
2. Decision Records có trạng thái `APPROVED` trong [DECISION_LOG](DECISION_LOG.md).
3. Các đặc tả (Feature Spec) đã được duyệt.
4. Các module/data contract đã được duyệt.
5. Các kế hoạch triển khai đang có hiệu lực (task, milestone plan).
6. Các đề xuất và bản nháp (`PROPOSED`, `TBD`, `EXAMPLE — NOT APPROVED`).

**Quy tắc về chat history:** Lịch sử chat với bất kỳ AI nào **không phải** nguồn sự thật. Một quyết định chỉ tồn tại khi đã được ghi vào DECISION_LOG. Nếu Game Director phê duyệt trong chat, Claude phải ghi lại thành Decision Record (kèm ngày và trích dẫn nội dung phê duyệt) trước khi dùng nó làm căn cứ.

### 1.1. Quy tắc duy trì nghiêm ngặt DECISION_LOG và OPEN_QUESTIONS

Hai tài liệu này là công cụ kiểm soát chính của Game Director. Bắt buộc:

1. Mọi quyết định L1/L2 phải có một Decision Record trong [DECISION_LOG](DECISION_LOG.md) — không có ngoại lệ.
2. Mọi vấn đề chưa quyết định mà ảnh hưởng tới thiết kế, phạm vi hoặc kiến trúc phải có một mục trong [OPEN_QUESTIONS](OPEN_QUESTIONS.md).
3. Khi một OQ được giải quyết: ghi Decision ID vào OQ, chuyển OQ sang mục "Đã giải quyết" — **không xóa**.
4. Không sửa nội dung một Decision Record `APPROVED`. Muốn thay đổi → tạo record mới với trạng thái `SUPERSEDED` cho record cũ (xem [CHANGE_CONTROL](CHANGE_CONTROL.md)).
5. ID không bao giờ được tái sử dụng.
6. Claude rà soát hai tài liệu này **vào cuối mỗi phiên làm việc có thay đổi quyết định** và tại mỗi milestone gate.

---

## 2. Cấp quyết định

| Level | Tên | Ai quyết | Ví dụ |
|---|---|---|---|
| **L0** | Operational Decision | Claude. Codex/Antigravity được quyết định chi tiết thực thi **bên trong phạm vi task đã giao**. | Chia task, thứ tự task không đổi mục tiêu, tổ chức tài liệu, quy trình review nội bộ, theo dõi milestone, điều phối dependency, tên biến/hàm, cấu trúc class nội bộ một module |
| **L1** | Design or Architecture Decision | Game Director phê duyệt, dựa trên đề xuất có cấu trúc | Gameplay cốt lõi, cơ chế chiến đấu quan trọng, kiến trúc nền tảng, dữ liệu ảnh hưởng nhiều module, concept asset quan trọng, cốt truyện chính, thay đổi phạm vi milestone lớn, thay đổi công nghệ chính, thêm package/dependency |
| **L2** | Project Direction Decision | Chỉ Game Director | Thể loại, tầm nhìn, phong cách game (bao gồm **Art Direction**), góc nhìn camera, bối cảnh thế giới và tông giọng, mục tiêu sản phẩm, quy mô phát triển lớn, thay đổi phạm vi chiến lược, mọi quyết định ảnh hưởng bản sắc sản phẩm |

Ghi chú: Master Prompt liệt kê Art Direction ở cả nhóm L1 và nhóm "phong cách game" của L2. Dự án áp dụng cấp cao hơn (L2) theo quy tắc dưới đây.

**Khi không chắc thuộc cấp nào → coi như cấp cao hơn.**

Bảng phân quyền chi tiết theo từng lĩnh vực: [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md).

### 2.1. Định dạng đề xuất cho L1/L2

Mọi đề xuất trình Game Director phải có tối thiểu:

1. **Vấn đề** — cần quyết định điều gì, vì sao bây giờ.
2. **Các phương án** — tối thiểu 2 nếu có phương án thực tế.
3. **Ưu và nhược điểm** của từng phương án.
4. **Chi phí và tác động** — hệ thống, tài liệu, milestone, nền tảng (PC/Android) bị ảnh hưởng.
5. **Khuyến nghị** — của Claude, kèm lý do; ghi rõ nếu ChatGPT/Gemini có ý kiến khác.
6. **Quyết định cần phê duyệt** — câu hỏi đóng, cụ thể.

Dùng [DECISION_RECORD_TEMPLATE](../templates/DECISION_RECORD_TEMPLATE.md).

---

## 3. Quy tắc phê duyệt

1. Chỉ ghi `APPROVED` khi có **phê duyệt rõ ràng** từ **đúng người có thẩm quyền** theo Level.
2. **Im lặng, không phản đối, hoặc "để sau" không phải là phê duyệt.**
3. **Sự đồng thuận giữa ChatGPT, Gemini và Claude không phải là phê duyệt.**
4. Phê duyệt có điều kiện ("duyệt nhưng…") được ghi đúng điều kiện; phần chưa duyệt giữ trạng thái cũ.
5. Phê duyệt một phần → tách Decision Record hoặc ghi rõ phạm vi được duyệt.
6. Bằng chứng phê duyệt ghi trong trường **Approval Evidence** của Decision Record: ngày, kênh (chat/tài liệu), câu trích dẫn ngắn.
7. Quyết định L0 do Claude tự ghi `APPROVED` với Decision Owner = Claude; Game Director có thể bác bỏ bất cứ lúc nào.

---

## 4. Xử lý mâu thuẫn giữa tài liệu

Khi phát hiện mâu thuẫn, agent **không được tự đoán** mà phải:

1. Chỉ ra chính xác: file, mục, nội dung mâu thuẫn.
2. Xác định nguồn nào có thứ hạng cao hơn theo §1.
3. Liệt kê hệ thống/tài liệu/task bị ảnh hưởng.
4. Đề xuất phương án xử lý.
5. Nếu cách xử lý vượt quyền hạn của mình → chuyển cấp (agent → Claude → Game Director).
6. Trong lúc chờ: dừng phần việc bị ảnh hưởng, tiếp tục phần không bị ảnh hưởng.

---

## 5. Từ vựng trạng thái

### 5.1. Trạng thái quyết định và nội dung (Decision / Item Status)

| Status | Nghĩa |
|---|---|
| `TBD` | Chưa có phương án hoặc chưa phân tích |
| `PROPOSED` | Đã có đề xuất, chưa trình hoặc đang chờ trình |
| `UNDER_REVIEW` | Đã trình người có thẩm quyền, đang chờ quyết định |
| `APPROVED` | Đã được phê duyệt rõ ràng bởi đúng người có thẩm quyền |
| `REJECTED` | Đã bị bác bỏ (giữ lại để tham khảo) |
| `SUPERSEDED` | Đã được thay thế bằng một quyết định mới (ghi ID thay thế) |

### 5.2. Nhãn nội dung trong tài liệu

| Nhãn | Dùng khi |
|---|---|
| `APPROVED` | Nội dung đã được phê duyệt — phải có Decision ID đi kèm |
| `PROPOSED` | Đề xuất của một agent, chưa được duyệt |
| `TBD` | Chưa quyết định |
| `EXAMPLE — NOT APPROVED` | Ví dụ minh họa; **không bao giờ** được dùng làm yêu cầu triển khai |
| `UNASSIGNED` | Vai trò/nhiệm vụ chưa có người/agent đảm nhận |

### 5.3. Trạng thái tài liệu (Document Status)

| Status | Nghĩa |
|---|---|
| `DRAFT` | Đang viết, chưa trình |
| `UNDER_REVIEW` | Đã trình Game Director nghiệm thu |
| `APPROVED` | Cấu trúc và quy tắc của tài liệu đã được duyệt |
| `ACTIVE` | Tài liệu sống (log, backlog, status, manifest) — cập nhật liên tục |
| `SUPERSEDED` | Đã được thay thế |

Document Status phản ánh **cấu trúc và quy tắc** của tài liệu. Từng mục nội dung bên trong có trạng thái riêng theo §5.1/§5.2. Ví dụ: `WORLD_BIBLE.md` có thể `APPROVED` về cấu trúc nhưng toàn bộ nội dung thế giới vẫn `TBD`.

### 5.4. Trạng thái task

`BACKLOG` → `READY` (đạt DoR) → `IN_PROGRESS` → `IN_REVIEW` (đã nộp bằng chứng) → `DONE` (đạt DoD, được chấp nhận).
Ngoài luồng: `BLOCKED` (ghi rõ blocker), `CANCELLED` (ghi lý do).

### 5.5. Trạng thái milestone

`NOT_STARTED` → `IN_PROGRESS` → `GATE_REVIEW` (exit gate đã nộp, chờ phê duyệt) → `ACCEPTED`.
Ngoài luồng: `ON_HOLD`.

---

## 6. Quy ước ID

| Loại | Định dạng | Ví dụ | Nơi lưu |
|---|---|---|---|
| Decision | `D-NNNN` | D-0012 | [DECISION_LOG](DECISION_LOG.md) |
| Open Question | `OQ-NNN` | OQ-002 | [OPEN_QUESTIONS](OPEN_QUESTIONS.md) |
| Change Request | `CR-NNN` | CR-001 | [CHANGE_CONTROL](CHANGE_CONTROL.md#7-change-request-log) |
| Risk | `R-NNN` | R-003 | [RISK_REGISTER](../01_production/RISK_REGISTER.md) |
| Task | `M<n>-<DEPT>-NNN` (DEPT: PRD, GD, NAR, ART, ENG, AUD, QA) | M2-ENG-004 | [BACKLOG](../01_production/BACKLOG.md) |
| Feature Spec | `FS-NNN` | FS-001 | `docs/<bộ phận>/specs/` (tạo khi có spec đầu tiên) |
| Art Brief / Art Review | `AB-NNN` / `AR-NNN` | AR-004 | `docs/04_art/briefs/`, `docs/04_art/reviews/` |
| Test Case / Bug | `TC-<MODULE>-NNN` / `BUG-NNN` | TC-COMBAT-012 | [TEST_STRATEGY](../07_qa_release/TEST_STRATEGY.md) |
| Acceptance Record | `ACC-NNN` | ACC-001 | [ACCEPTANCE_CRITERIA](../07_qa_release/ACCEPTANCE_CRITERIA.md#5-acceptance-log) |

ID không bao giờ được tái sử dụng, kể cả khi mục bị hủy.

---

## 7. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo | Claude |
