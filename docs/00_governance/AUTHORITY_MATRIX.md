# Authority Matrix & RACI

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [DECISION_POLICY](DECISION_POLICY.md) · [AGENT_ROLES](AGENT_ROLES.md) · [WORKFLOW](WORKFLOW.md)

Định nghĩa Level L0/L1/L2 nằm ở [DECISION_POLICY §2](DECISION_POLICY.md#2-cấp-quyết-định). Tài liệu này áp các Level đó vào từng lĩnh vực cụ thể.

Viết tắt: **GD** = Game Director · **CG** = ChatGPT · **GM** = Gemini · **CL** = Claude · **CX** = Codex · **AG** = Antigravity.

---

## 1. Authority Matrix

| Lĩnh vực quyết định | Level | Đề xuất | Tư vấn | **Quyết định** | Thực thi |
|---|---|---|---|---|---|
| Thể loại, tầm nhìn, game pillars | L2 | GD (CL cấu trúc hóa) | CG, GM | **GD** | CL ghi nhận |
| Tên game, bản sắc thương hiệu | L2 | GD | CG, GM, CL | **GD** | CL ghi nhận |
| Góc nhìn camera | L2 | CL (phân tích phương án) | CG, GM, CX (khả thi) | **GD** | CL đặc tả |
| Art Direction | L2 | AG (biến thể), CL (tổng hợp) | CG, GM | **GD** | AG |
| Bối cảnh thế giới, tông giọng | L2 | GD / CL (khung) | CG, GM | **GD** | CL ghi nhận |
| Phạm vi chiến lược, quy mô, business model | L2 | CL (phân tích) | CG, GM | **GD** | CL |
| Thời gian phát hành, ngân sách | L2 | — | CG, GM, CL | **GD** | CL lập kế hoạch |
| Go/No-go phát hành, nghiệm thu demo | L2 | CL (báo cáo) | CX (QA) | **GD** | CL, CX |
| Core gameplay loop | L1 | CL | CG, GM | **GD** | CL đặc tả → CX |
| Cơ chế di chuyển, chiến đấu cốt lõi | L1 | CL | CG, GM, CX | **GD** | CX |
| Hệ thống kỹ năng, chỉ số, progression, inventory | L1 | CL | CG, GM | **GD** | CX |
| Cốt truyện chính, chương, nhân vật chính | L1 | GD / CL (bản nháp `PROPOSED`) | CG, GM | **GD** | CL ghi canon → CX runtime |
| Nội dung phụ (side quest, hội thoại phụ) trong canon đã duyệt | L1 (duyệt theo lô) | CL / CG / GM | CL (continuity) | **GD** | CX nhập dữ liệu |
| Concept nhân vật chính, boss, quái quan trọng, môi trường chính | L1 | AG | CL, CG, GM | **GD** | AG |
| Asset phụ theo style guide đã duyệt (prop, tile, biến thể) | L0 + nghiệm thu theo lô | AG | CL | **CL** (kỹ thuật) · **GD** (nghiệm thu lô tại milestone) | AG → CX |
| Kiến trúc nền tảng (module, scene strategy, save format) | L1 | CL | CX, CG, GM | **GD** | CX |
| Unity version, render pipeline, input system | L1 | CL | CX, CG, GM | **GD** | CX |
| Thêm package / thư viện bên thứ ba | L1 | CX hoặc CL | CL | **GD** | CX |
| Data contract dùng chung nhiều module | L1 | CL | CX | **GD** | CX |
| Data contract nội bộ một module | L0 | CX | CL | **CL** | CX |
| Chi tiết triển khai trong phạm vi task | L0 (task-level) | — | — | **CX / AG** (báo cáo trong handoff) | CX / AG |
| Tuning tham số trong dải đã duyệt | L0 | CX / CL | — | **CL** | CX |
| Tuning vượt dải đã duyệt | L1 | CL | — | **GD** | CX |
| Thay đổi phạm vi milestone nhỏ (không đổi exit gate) | L0 | CL | — | **CL** (thông báo GD) | CL |
| Thay đổi phạm vi milestone lớn / exit gate | L1 | CL | CG, GM | **GD** | CL |
| Nghiệm thu milestone | L1/L2 | CL (bằng chứng) | — | **GD** | — |
| Chia task, thứ tự task, tổ chức tài liệu, review nội bộ | L0 | CL | — | **CL** | CL |
| Phân loại bug, độ ưu tiên | L0 | CX / CL | — | **CL** | CX |
| Miễn trừ bug blocking cho release | L1 | CL | CX | **GD** | — |

**ChatGPT và Gemini không có quyết định nào trong cột "Quyết định".**

---

## 2. RACI Matrix

**R** = Responsible (làm) · **A** = Accountable (chịu trách nhiệm cuối, duy nhất mỗi dòng) · **C** = Consulted · **I** = Informed

| Deliverable | GD | CG | GM | CL | CX | AG |
|---|---|---|---|---|---|---|
| Game Vision & pillars | A | C | C | R | I | I |
| Decision Records | A | C | C | R | I | I |
| Open Questions register | I | — | — | A/R | C | C |
| Roadmap, milestones, backlog | I (A khi đổi exit gate) | C | C | A/R | C | C |
| Project status, risk register | I | — | — | A/R | C | C |
| Change requests | A (L1/L2) | C | C | R | C | C |
| Feature Spec | A | C | C | R | C | C |
| Task decomposition | I | — | — | A/R | C | C |
| Unity architecture proposal | A | C | C | R | C | — |
| Gameplay & system code | I | — | — | A | R | — |
| Automated tests & test reports | I | — | — | A | R | — |
| Art Direction exploration | A | C | C | C | — | R |
| Concept art (asset quan trọng) | A | C | C | C | I | R |
| Final assets | I | — | — | A | C | R |
| Asset technical validation | I | — | — | A | R | R |
| Asset integration vào Unity | I | — | — | A | R | C |
| Visual review in-game | C | — | — | A | C | R |
| World/story content (canon) | A | C | C | R (cấu trúc, continuity) | I | C |
| Narrative runtime (story/quest/dialogue engine) | I | — | — | A | R | — |
| Audio assets | A | C | C | C | — | — |
| Audio production (R) | `UNASSIGNED` | | | | | |
| Audio integration | I | — | — | A | R | — |
| PC / Android builds | I | — | — | A | R | — |
| Test evidence review | I | — | — | A/R | C | C |
| Playtest & experience acceptance | A/R | — | — | C | C | C |
| Release checklist | A | — | — | R | R | C |

Ghi chú: Với dòng "Audio assets", vai trò R đang `UNASSIGNED` — không agent nào được tự nhận sản xuất audio chuyên nghiệp ([06_audio_integration/DEPARTMENT](../06_audio_integration/DEPARTMENT.md)).

---

## 3. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo | Claude |
