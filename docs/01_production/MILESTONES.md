# Milestones

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ROADMAP](ROADMAP.md) · [BACKLOG](BACKLOG.md) · [DEFINITION_OF_READY_DONE §2.5](../00_governance/DEFINITION_OF_READY_DONE.md#25-milestone) · [MILESTONE_TEMPLATE](../templates/MILESTONE_TEMPLATE.md)

**Cách đọc:** "Exit Gate" là điều kiện do Game Director đặt ([D-0010](../00_governance/DECISION_LOG.md#d-0010--khung-milestone-m0m7-chỉ-thực-thi-m0), `APPROVED`). "Acceptance Criteria" là các tiêu chí kiểm chứng chi tiết do Claude đề xuất để làm rõ Exit Gate — trạng thái `PROPOSED` cho tới khi GD duyệt. Mục đánh dấu ★ thuộc điều chỉnh [D-0012](../00_governance/DECISION_LOG.md#d-0012--điều-chỉnh-nhỏ-cho-kế-hoạch-milestone) (`PROPOSED`).

Mọi milestone: **Approver = Game Director**. Không có deadline.

---

## M0 — Project Governance Foundation

- **Status:** `GATE_REVIEW`
- **Mục tiêu:** Tổ chức 7 bộ phận, phân vai agent, quy tắc quyết định, cấu trúc tài liệu, workflow, decision log, backlog foundation.
- **Entry:** Master Prompt v1.0 (đã có).
- **Exit Gate:** Tất cả tài liệu quản trị bắt buộc được tạo và nhất quán.
- **Acceptance Criteria (`PROPOSED`):**
  1. Mọi file trong cây tài liệu bắt buộc tồn tại và có nội dung dùng được (không rỗng, không chỉ tiêu đề).
  2. Mọi link tương đối giữa các tài liệu hoạt động.
  3. Không mục `TBD` nào bị ghi thành `APPROVED`; mọi mục `APPROVED` có Decision ID.
  4. Vai trò: Claude ≠ Game Director; ChatGPT/Gemini không có quyền phê duyệt; Codex không đổi Game Design; Antigravity theo Sketch → Approval → Production; audio production `UNASSIGNED`.
  5. Game Director đọc và chấp nhận (hoặc yêu cầu sửa) bộ tài liệu.
- **Bằng chứng:** báo cáo kiểm tra tính nhất quán của Claude; danh sách file.

## M1 — Game Vision & Design Discovery

- **Status:** `NOT_STARTED`
- **Dependencies:** M0 `ACCEPTED`.
- **Deliverables:** Game vision proposal; core gameplay loop proposal; combat design alternatives; narrative design framework; art direction exploration plan; initial technical architecture options. ★ Xác minh năng lực agent. ★ Art research + moodboard.
- **Exit Gate:** Các quyết định cốt lõi cần thiết cho prototype được Game Director duyệt.
- **Acceptance Criteria (`PROPOSED`):**
  1. OQ-001 → OQ-011 (nhóm A trong [OPEN_QUESTIONS](../00_governance/OPEN_QUESTIONS.md)) có Decision Record `APPROVED`, hoặc được GD cho phép hoãn kèm giả định tạm thời ghi rõ.
  2. Có Feature Spec `APPROVED` cho phạm vi prototype M2 (movement, combat cơ bản, enemy cơ bản, camera, input).
  3. M2 được phân rã thành task đạt DoR.
  4. ★ Có báo cáo xác minh năng lực Codex (Unity batchmode test/build) và Antigravity (nhất quán nhân vật, sprite frame) — kết quả thực tế, kể cả khi thất bại.
  5. ★ Có moodboard cho tối thiểu 3 hướng Art Direction.
- **Ngoài phạm vi:** code gameplay, final art, nội dung cốt truyện canon.

## M2 — Core Gameplay Prototype

- **Status:** `NOT_STARTED`
- **Dependencies:** M1 `ACCEPTED`; OQ-002, OQ-004, OQ-005, OQ-006–OQ-010 đã duyệt.
- **Deliverables:** Unity prototype; basic player movement; basic combat; basic enemy behavior; basic camera; input testing. Placeholder art. ★ Android smoke build.
- **Exit Gate:** Có bản chơi thử để đánh giá cảm giác điều khiển và chiến đấu.
- **Acceptance Criteria (`PROPOSED`):**
  1. Build PC chạy được; GD điều khiển nhân vật, tấn công và đánh bại ít nhất một loại kẻ địch cơ bản.
  2. Các tham số cảm giác (tốc độ, gia tốc, thời gian đòn đánh…) chỉnh được qua dữ liệu mà không cần sửa code.
  3. Unit test cho logic tách khỏi MonoBehaviour (ví dụ tính sát thương, state transition) chạy và có báo cáo.
  4. ★ Build Android cài được trên ít nhất một thiết bị thật; điều khiển cảm ứng tối thiểu dùng được; ghi nhận FPS quan sát.
  5. GD hoàn thành playtest và ghi phản hồi theo checklist cảm giác ([ACCEPTANCE_CRITERIA](../07_qa_release/ACCEPTANCE_CRITERIA.md)).
- **Ngoài phạm vi:** final art, narrative, save/load, UI hoàn chỉnh.

## M3 — Narrative & World Foundation

- **Status:** `NOT_STARTED`
- **Dependencies:** M2 `ACCEPTED`; OQ-019, OQ-020, OQ-021 đã duyệt; data contract narrative `APPROVED`.
- **Deliverables:** Story runtime; quest system foundation; dialogue system foundation; tương tác NPC; basic narrative progression; save/load proof of concept.
- **Exit Gate:** Có thể chơi một chuỗi nhiệm vụ đơn giản và lưu đúng tiến độ.
- **Acceptance Criteria (`PROPOSED`):**
  1. Một chuỗi nhiệm vụ thử nghiệm (nội dung `EXAMPLE — NOT APPROVED`) gồm nói chuyện NPC → hoàn thành mục tiêu → nhận kết quả, được định nghĩa hoàn toàn bằng dữ liệu.
  2. Lưu giữa chừng, thoát game, tải lại → quest state, story state, dialogue state, world state khớp trước khi lưu (test tự động + kiểm tra thủ công).
  3. Save data có số phiên bản schema.
  4. Narrative runtime không phụ thuộc trực tiếp vào nội dung cụ thể (thay dữ liệu không cần sửa code).
- **Ngoài phạm vi:** cốt truyện canon, cutscene hoàn chỉnh.

## M4 — Art Production Pipeline

- **Status:** `NOT_STARTED`
- **Dependencies:** OQ-014 Art Direction `APPROVED`; OQ-002 camera `APPROVED`; ASSET_SPEC kích thước/pivot `APPROVED`. Có thể chạy song song một phần với M2/M3 khi phụ thuộc đã giải quyết.
- **Deliverables:** Approved Art Direction; character concept; sprite workflow; animation workflow; environment asset workflow; asset integration standards.
- **Exit Gate:** Có bộ asset mẫu được duyệt và tích hợp thành công.
- **Acceptance Criteria (`PROPOSED`):**
  1. Style guide `APPROVED`.
  2. Ít nhất một nhân vật đi qua toàn bộ pipeline: brief → sketch → concept `APPROVED` → sprite + bộ animation tối thiểu → technical validation → tích hợp trong Unity → visual acceptance.
  3. Ít nhất một bộ asset môi trường mẫu đi qua toàn bộ pipeline.
  4. Hiển thị đúng trên PC và Android (tỉ lệ, độ sắc nét, pivot).
  5. Mọi asset có mục trong ASSET_MANIFEST với provenance.

## M5 — Vertical Slice

- **Status:** `NOT_STARTED`
- **Dependencies:** M3 và M4 `ACCEPTED`; các OQ nhóm B liên quan đã duyệt; nguồn audio tối thiểu đã xác định (OQ-026).
- **Deliverables:** Một trải nghiệm phiêu lưu quy mô nhỏ: gameplay, NPC, quest, combat, boss encounter, story progression, UI, art, audio tối thiểu, save/load.
- **Exit Gate:** Người chơi có thể hoàn thành một đoạn phiêu lưu có mở đầu, thử thách và kết thúc.
- **Acceptance Criteria (`PROPOSED`):**
  1. Nội dung slice (khu vực, NPC, quest, boss) dùng nội dung canon `APPROVED`.
  2. Playthrough từ đầu tới cuối không có lỗi blocking, trên PC; kiểm tra cơ bản trên Android.
  3. Mọi asset hiển thị là final hoặc được GD cho phép là placeholder.
  4. GD playtest và chấp nhận.

## M6 — Cross-platform & Quality Validation

- **Status:** `NOT_STARTED`
- **Dependencies:** M5 `ACCEPTED`; OQ-011 cấu hình thử nghiệm `APPROVED`.
- **Deliverables:** PC controls; Android touch controls; UI scaling; performance checks; build validation; regression testing; save/load validation.
- **Exit Gate:** Bản game hoạt động trên những cấu hình PC và Android thử nghiệm được phê duyệt.
- **Acceptance Criteria (`PROPOSED`):**
  1. Đạt performance budget đã duyệt trên từng cấu hình thử nghiệm.
  2. UI dùng được ở các tỉ lệ màn hình mục tiêu và safe area.
  3. Toàn bộ regression suite chạy và có báo cáo.
  4. Save/load đúng khi app Android bị đưa xuống nền và khôi phục.

## M7 — Playable Demo

- **Status:** `NOT_STARTED`
- **Dependencies:** M6 `ACCEPTED`; OQ-027, OQ-029 nếu demo được phát hành công khai.
- **Deliverables:** Gameplay polish, bug fixing, visual polish, basic audio, content validation, demo build, user playtesting, release documentation.
- **Exit Gate:** Game Director nghiệm thu bản demo.
- **Acceptance Criteria (`PROPOSED`):**
  1. [RELEASE_CHECKLIST](../07_qa_release/RELEASE_CHECKLIST.md) hoàn tất cho các nền tảng phát hành.
  2. Không còn bug mức Blocker/Critical đã biết (hoặc được GD miễn trừ có ghi nhận).
  3. Có báo cáo user playtesting.
  4. GD ký Acceptance Record.
