# Definition of Ready & Definition of Done

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [WORKFLOW](WORKFLOW.md) · [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md) · [ACCEPTANCE_CRITERIA](../07_qa_release/ACCEPTANCE_CRITERIA.md) · [TEST_STRATEGY](../07_qa_release/TEST_STRATEGY.md)

---

## 1. Definition of Ready

### 1.1. Task giao cho Codex hoặc Antigravity

Task chỉ được chuyển `READY` khi có đủ:

- [ ] **Objective** — mục tiêu một câu, đo được.
- [ ] **Scope** — trong phạm vi và **ngoài phạm vi**.
- [ ] **Owner** — đúng một agent thực thi.
- [ ] **Input References** — link tới spec/decision/contract/art brief ở trạng thái `APPROVED` (hoặc ghi rõ phần nào là placeholder được phép).
- [ ] **Dependencies** — task/quyết định phải xong trước; tất cả đã xong hoặc được ghi rõ cách xử lý.
- [ ] **Output Contract** — định dạng, vị trí, tên file/module đầu ra.
- [ ] **Acceptance Criteria** — kiểm chứng được, theo [ACCEPTANCE_CRITERIA](../07_qa_release/ACCEPTANCE_CRITERIA.md).
- [ ] **Validation Method** — cách kiểm chứng (test tự động, kiểm tra thủ công, visual review…).
- [ ] **Completion Evidence** — bằng chứng cần nộp.
- [ ] **Platform Scope** — PC, Android hoặc cả hai.

**Thiếu thông tin quan trọng → không được tự suy diễn thành yêu cầu chính thức.** Ghi phần thiếu là `TBD`, tạo/ liên kết OQ, giữ task ở `BACKLOG` hoặc `BLOCKED`.

### 1.2. Feature Spec sẵn sàng để chia task

- [ ] Decision Record nền tảng `APPROVED`.
- [ ] Đủ các mục bắt buộc trong [FEATURE_SPEC_TEMPLATE](../templates/FEATURE_SPEC_TEMPLATE.md).
- [ ] Không còn `TBD` ở phần cần cho task sắp giao (các `TBD` còn lại được ghi rõ là ngoài phạm vi).
- [ ] Spec `APPROVED` theo đúng Level.

### 1.3. Art task

Ngoài §1.1, bắt buộc có Art Brief ([ART_BRIEF_TEMPLATE](../04_art/ART_BRIEF_TEMPLATE.md)) và chỉ rõ bước pipeline (sketch / concept / final) — **task final asset chỉ READY khi concept đã `APPROVED`**.

---

## 2. Definition of Done

### 2.1. Task kỹ thuật (Codex)

- [ ] Implementation tồn tại trong repository/branch đã chỉ định.
- [ ] Mọi acceptance criterion đã được kiểm chứng, hoặc được ghi "chưa kiểm chứng" kèm lý do và được Claude chấp nhận.
- [ ] Test liên quan **đã chạy** (có output) — hoặc hạn chế (không chạy được) được báo cáo rõ.
- [ ] Không còn lỗi blocking đã biết trong phạm vi task.
- [ ] Không thay đổi ngoài phạm vi; không thêm dependency chưa duyệt.
- [ ] Tài liệu cần thiết đã cập nhật.
- [ ] Handoff report đã nộp, Claude review `ACCEPTED`.

### 2.2. Task mỹ thuật (Antigravity)

- [ ] Concept cần thiết đã `APPROVED` (Art Review Record).
- [ ] Asset xuất đúng định dạng yêu cầu ([ASSET_SPEC](../04_art/ASSET_SPEC.md)).
- [ ] Đúng tên file, kích thước, pivot, tiêu chuẩn kỹ thuật.
- [ ] Đã qua visual review.
- [ ] Có thể được Codex tích hợp, hoặc đã tích hợp thành công theo phạm vi task.
- [ ] Đã ghi vào [ASSET_MANIFEST](../04_art/ASSET_MANIFEST.md) kèm nguồn gốc (provenance).
- [ ] Handoff report đã nộp, Claude review `ACCEPTED`.

### 2.3. Task tài liệu

- [ ] File tồn tại, không rỗng, có metadata.
- [ ] Link tương đối hoạt động.
- [ ] Không mâu thuẫn với tài liệu có thứ hạng cao hơn.
- [ ] Trạng thái nội dung (`APPROVED`/`PROPOSED`/`TBD`/`EXAMPLE`) được đánh dấu đúng.

### 2.4. Feature

- [ ] Mọi task thuộc feature `DONE`.
- [ ] Integration và regression test liên quan đã chạy.
- [ ] Đã kiểm tra trên các nền tảng trong phạm vi spec.
- [ ] GD nghiệm thu nếu feature là L1 (Acceptance Record).

### 2.5. Milestone

- [ ] Mọi exit gate trong [MILESTONES](../01_production/MILESTONES.md) được thỏa mãn và có bằng chứng.
- [ ] Known issues được ghi và phân loại.
- [ ] DECISION_LOG, OPEN_QUESTIONS, PROJECT_STATUS cập nhật.
- [ ] **Game Director phê duyệt** → milestone `ACCEPTED`.

---

## 3. Bằng chứng được chấp nhận

| Loại | Ví dụ hợp lệ | Không hợp lệ |
|---|---|---|
| Test tự động | Output test runner (số test, pass/fail), file kết quả | "Đã viết test", "test chắc sẽ pass" |
| Build | Log build thành công, đường dẫn file build, kích thước | "Build được" không kèm log |
| Gameplay | Video/GIF ngắn, ảnh chụp màn hình, các bước tái hiện | Mô tả chung chung |
| Asset | File thật trong repository, ảnh preview, thông số kỹ thuật | Link ảnh không lưu vào dự án |
| Thiết bị Android | Model máy, phiên bản Android, FPS quan sát được, ảnh/video | "Chạy tốt trên Android" |
| Phê duyệt | Trích dẫn + ngày trong Decision/Acceptance Record | "GD có vẻ đồng ý" |

---

## 4. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo | Claude |
