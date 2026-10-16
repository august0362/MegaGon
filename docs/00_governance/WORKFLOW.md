# Master Workflow

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [AGENT_ROLES](AGENT_ROLES.md) · [DEFINITION_OF_READY_DONE](DEFINITION_OF_READY_DONE.md) · [CHANGE_CONTROL](CHANGE_CONTROL.md) · [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md) · [FEATURE_SPEC_TEMPLATE](../templates/FEATURE_SPEC_TEMPLATE.md)

---

## 1. Quy trình thực hiện một tính năng (Feature Workflow)

| Step | Tên | Người thực hiện | Đầu vào | Đầu ra | Cổng chuyển bước |
|---|---|---|---|---|---|
| 1 | **Idea** | Game Director | Ý tưởng, mục tiêu | Mô tả ý tưởng (chat hoặc tài liệu) | Claude ghi nhận thành OQ hoặc yêu cầu |
| 2 | **Strategic Analysis** *(tùy chọn)* | ChatGPT, Gemini phân tích; GD quyết định | OQ, bối cảnh từ repository | Phân tích, phương án, phản biện | GD chọn phương án → Decision Record `APPROVED` |
| 3 | **Specification** | Claude | Decision `APPROVED` | Feature Spec: functional/non-functional requirements, dependencies, data contracts, acceptance criteria, test requirements, scope exclusions | Spec `APPROVED` (L1: GD duyệt; L0: Claude) |
| 4 | **Task Decomposition** | Claude | Spec đã duyệt | Task records đạt [DoR](DEFINITION_OF_READY_DONE.md#1-definition-of-ready) | Task `READY` |
| 5 | **Implementation** | Codex (code) · Antigravity (art) | Task record | Code / asset + handoff report | Bằng chứng nộp đủ |
| 6 | **Integration** | Codex | Code, asset, dữ liệu đã nộp | Build tích hợp | Build chạy được |
| 7 | **Verification** | Codex (test kỹ thuật) · Claude (đối chiếu yêu cầu) · Antigravity (visual review) | Build + bằng chứng | Kết quả kiểm thử, danh sách điểm chưa kiểm chứng | Đạt [DoD](DEFINITION_OF_READY_DONE.md#2-definition-of-done) |
| 8 | **Acceptance** | Game Director (với sản phẩm quan trọng) | Build + báo cáo của Claude | Acceptance Record `ACC-NNN` | Chấp nhận / trả về |
| 9 | **Documentation** | Claude | Kết quả các bước | Cập nhật project status, backlog, milestone, decision log, known issues | — |

**Song song hóa (Step 5):** Codex và Antigravity chỉ làm song song khi data contract và asset contract liên quan đã `APPROVED` (nguyên tắc P6).

### 1.1. Luồng trả về khi không đạt

| Phát hiện tại | Nguyên nhân | Quay về |
|---|---|---|
| Step 5–7 | Lỗi triển khai | Step 5 (cùng task, ghi BUG-NNN) |
| Step 5–7 | Spec thiếu/mâu thuẫn/bất khả thi | Step 3 (Claude sửa spec; nếu đổi quyết định L1 → CR) |
| Step 8 | Đúng spec nhưng trải nghiệm không đạt | Step 2 hoặc 3 tùy mức độ (qua [CHANGE_CONTROL](CHANGE_CONTROL.md)) |
| Bất kỳ | Phát hiện xung đột với quyết định `APPROVED` | Dừng phần bị ảnh hưởng → [DECISION_POLICY §4](DECISION_POLICY.md#4-xử-lý-mâu-thuẫn-giữa-tài-liệu) |

### 1.2. Fast track cho task nhỏ

Task L0 (sửa lỗi trong phạm vi, tooling nội bộ, cập nhật tài liệu) được bỏ Step 1–3 và Step 8, nhưng **vẫn phải** có task record, tiêu chí nghiệm thu và bằng chứng.

---

## 2. Handoff Protocol

### 2.1. Claude → Codex / Antigravity (giao việc)

Một **handoff package** gồm:

1. Task record theo [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md) — đạt DoR.
2. Đường dẫn tới mọi tài liệu đầu vào (spec, contract, art brief, decision).
3. Danh sách file/thư mục được phép thay đổi.
4. Danh sách những gì **ngoài phạm vi**.
5. Cách nộp bằng chứng.

Lưu task: task nhỏ ghi trực tiếp trong [BACKLOG](../01_production/BACKLOG.md); task lớn tạo file `docs/01_production/tasks/<TASK-ID>.md` (thư mục tạo khi có task đầu tiên cần file riêng).

### 2.2. Codex / Antigravity → Claude (bàn giao)

Mỗi lần bàn giao phải có **handoff report** theo định dạng trong file vai trò của agent ([CODEX §11](../../agents/CODEX.md#11-reporting-format), [ANTIGRAVITY §11](../../agents/ANTIGRAVITY.md#11-reporting-format)). Lưu tại `docs/01_production/reports/<TASK-ID>-report.md`.

Báo cáo **phải tách bạch**: đã làm và đã kiểm chứng / đã làm nhưng chưa kiểm chứng / chưa làm / vấn đề phát hiện.

### 2.3. ChatGPT / Gemini → Game Director (tư vấn)

Phân tích tư vấn được Game Director mang về repository khi muốn dùng làm căn cứ. Claude tóm tắt vào Decision Record (mục Options/Trade-offs), ghi rõ nguồn ("Theo phân tích của ChatGPT ngày …").

### 2.4. Khi ChatGPT và Gemini bất đồng

Claude trình bày hai quan điểm song song trong Decision Record, chỉ ra điểm bất đồng cốt lõi và giả định khác nhau, đưa ra khuyến nghị riêng. **GD quyết định.** Không được lấy "đa số AI" làm căn cứ.

---

## 3. Verification — Claude review checklist

Khi nhận handoff report, Claude kiểm tra:

- [ ] Task ID và tham chiếu spec/decision đúng.
- [ ] Mọi acceptance criterion có bằng chứng tương ứng hoặc được ghi "chưa kiểm chứng" kèm lý do.
- [ ] Test đã chạy thật (có output/log), không chỉ "đã viết test".
- [ ] Không có file nào bị thay đổi ngoài phạm vi cho phép.
- [ ] Không có dependency/package mới chưa được duyệt.
- [ ] PC và Android: đã kiểm tra, hoặc ghi rõ nền tảng nào chưa kiểm tra.
- [ ] Tài liệu liên quan đã cập nhật.

Kết luận review: `ACCEPTED` / `CHANGES_REQUESTED` / `ESCALATED` — ghi vào task record.

---

## 4. Escalation

Chuỗi chuyển cấp: **Codex / Antigravity → Claude → Game Director**. ChatGPT/Gemini báo trực tiếp cho Game Director.

| Tình huống | Hành động |
|---|---|
| Thiếu thông tin để thực hiện task | Dừng phần thiếu, báo Claude; không tự bịa yêu cầu |
| Phát hiện spec bất khả thi về kỹ thuật | Báo Claude kèm phân tích tác động; không tự đổi thiết kế |
| Cần package/dependency mới | Đề xuất qua Claude → L1 |
| Mâu thuẫn tài liệu | Theo [DECISION_POLICY §4](DECISION_POLICY.md#4-xử-lý-mâu-thuẫn-giữa-tài-liệu) |
| Vấn đề vượt L0 | Claude lập đề xuất L1/L2 → GD |
| Blocker kéo dài ảnh hưởng milestone | Claude cập nhật [RISK_REGISTER](../01_production/RISK_REGISTER.md) và báo GD |

Nội dung một escalation: vấn đề · nơi phát hiện · tác động · phương án · khuyến nghị · điều cần quyết định.

---

## 5. Giao thức phiên làm việc (mọi agent thực thi)

**Đầu phiên:** đọc [PROJECT_STATUS](../01_production/PROJECT_STATUS.md) → đọc task được giao → đọc tài liệu đầu vào của task → kiểm tra [OPEN_QUESTIONS](OPEN_QUESTIONS.md) liên quan.

**Cuối phiên:** nộp handoff report (Codex/Antigravity) hoặc cập nhật status/backlog/decision log (Claude). Không kết thúc phiên với thay đổi chưa được ghi lại.

---

## 6. Git, Branch, Pull Request — `PROPOSED`

> Áp dụng sau khi [OQ-009](OPEN_QUESTIONS.md) (version control) được duyệt. Hiện thư mục dự án **chưa** là git repository.

| Hạng mục | Đề xuất |
|---|---|
| Hệ thống | Git + Git LFS cho file nhị phân (PNG, PSD, audio, font…) |
| Nhánh chính | `main` — luôn ở trạng thái mở được trong Unity và build được; không push trực tiếp |
| Nhánh làm việc | `feature/<TASK-ID>-<slug>`, `fix/<BUG-ID>-<slug>`, `art/<TASK-ID>-<slug>`, `docs/<slug>` |
| Commit message | `<TASK-ID>: <mô tả ngắn>` — ví dụ `M2-ENG-003: add player movement controller` |
| Pull Request | Mỗi PR gắn đúng một task. Mô tả PR = handoff report rút gọn (thay đổi, test đã chạy kèm kết quả, phần chưa kiểm chứng, ảnh hưởng PC/Android) |
| Review | Claude review theo [§3](#3-verification--claude-review-checklist). Merge vào `main` chỉ khi Claude `ACCEPTED` **và** GD cho phép merge (mặc định giai đoạn đầu) |
| Unity | Asset Serialization = Force Text; Visible Meta Files; `.gitignore` chuẩn Unity (loại `Library/`, `Temp/`, `Logs/`, `UserSettings/`, `Build/`) |
| Xung đột scene/prefab | Mỗi scene/prefab dùng chung có một owner tại một thời điểm (ghi trong task). Ưu tiên tách prefab nhỏ để giảm xung đột |
| Lịch sử | Không rewrite lịch sử `main`; không force-push nhánh dùng chung |

Agent không được commit, push, merge khi chưa được Game Director cho phép trong phiên đó hoặc trong quy tắc đã duyệt.

---

## 7. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo | Claude |
