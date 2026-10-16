# Project Charter — Untitled 2D Adventure RPG

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [DECISION_LOG](DECISION_LOG.md) · [OPEN_QUESTIONS](OPEN_QUESTIONS.md) · [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md) · [ROADMAP](../01_production/ROADMAP.md)

Tài liệu này xác định **dự án là gì, đã chốt những gì, chưa chốt những gì, ai làm gì và theo nguyên tắc nào**. Mọi tài liệu khác phải nhất quán với Charter. Khi Charter mâu thuẫn với một Decision Record `APPROVED` mới hơn, Decision Record thắng và Charter phải được cập nhật (xem [DECISION_POLICY](DECISION_POLICY.md#1-single-source-of-truth)).

---

## 1. Tóm tắt dự án — các quyết định đã được phê duyệt

| Thuộc tính | Giá trị | Trạng thái | Nguồn |
|---|---|---|---|
| Project Name | TBD — thư mục làm việc tên `MegaGon`, **không** được coi là tên game | `TBD` | [OQ-029](OPEN_QUESTIONS.md) |
| Genre | 2D Adventure RPG | `APPROVED` | [D-0001](DECISION_LOG.md#d-0001--thể-loại-2d-adventure-rpg) |
| Game Engine / Language | Unity / C# | `APPROVED` | [D-0002](DECISION_LOG.md#d-0002--engine-unity-ngôn-ngữ-c) |
| Target Platforms | PC + Android | `APPROVED` | [D-0003](DECISION_LOG.md#d-0003--nền-tảng-mục-tiêu-pc--android) |
| Combat Style | Real-time Action | `APPROVED` | [D-0004](DECISION_LOG.md#d-0004--phong-cách-chiến-đấu-real-time-action) |
| Multiplayer | Ngoài phạm vi triển khai ban đầu; khả năng mở rộng tương lai TBD | `APPROVED` / `TBD` | [D-0005](DECISION_LOG.md#d-0005--multiplayer-ngoài-phạm-vi-ban-đầu) · [OQ-028](OPEN_QUESTIONS.md) |
| Development Model | AI-assisted, human-directed | `APPROVED` | [D-0006](DECISION_LOG.md#d-0006--mô-hình-phát-triển-và-phân-vai-agent) |
| Ngôn ngữ tài liệu chính | Tiếng Việt (giữ thuật ngữ kỹ thuật tiếng Anh) | `APPROVED` | [D-0007](DECISION_LOG.md#d-0007--ngôn-ngữ-tài-liệu-chính-tiếng-việt) |
| Art Direction | Chưa chốt — phải nghiên cứu, phác thảo, so sánh | `TBD` | [OQ-014](OPEN_QUESTIONS.md) |
| Project Phase | Initialization / Pre-production (M0) | Thực tế hiện tại | [PROJECT_STATUS](../01_production/PROJECT_STATUS.md) |

### Những gì chưa được quyết định

Tên game, thế giới/cốt truyện, góc nhìn camera, hệ thống nhân vật/lớp nhân vật, phong cách đồ họa và animation, hệ thống kỹ năng, chỉ số và progression, cơ chế di chuyển chi tiết, chế độ lưu, quy mô bản đồ/số chương, phiên bản Unity, render pipeline, package, kiến trúc gameplay chi tiết, thời gian phát hành, ngân sách.

Tất cả được theo dõi trong [OPEN_QUESTIONS.md](OPEN_QUESTIONS.md). **Không agent nào được tự chuyển các mục này sang `APPROVED`.**

---

## 2. Mục tiêu của giai đoạn hiện tại

| Giai đoạn | Mục tiêu | Kết quả cần có |
|---|---|---|
| **M0 — Governance Foundation** (hiện tại) | Thiết lập tổ chức, phân quyền, quy trình, tài liệu | Bộ tài liệu quản trị nhất quán, được Game Director nghiệm thu |
| **M1 — Vision & Design Discovery** (kế tiếp) | Chốt các quyết định cốt lõi đủ để làm prototype | Các Decision Record nhóm A trong [OPEN_QUESTIONS](OPEN_QUESTIONS.md) được duyệt |

Chi tiết toàn bộ milestone: [MILESTONES.md](../01_production/MILESTONES.md).

---

## 3. Phạm vi

### 3.1. Trong phạm vi (đã duyệt ở mức tổng quan)

- Game 2D Adventure RPG chơi đơn (single-player), chiến đấu real-time action.
- Hai nền tảng: PC và Android — thiết kế input, UI, hiệu năng phải tính cả hai ngay từ đầu.
- Phát triển theo mô hình AI-assisted, Game Director điều hành và phê duyệt.
- Mục tiêu sản phẩm gần nhất theo roadmap: **Playable Demo** (M7).

### 3.2. Ngoài phạm vi ban đầu

- Multiplayer, online, server-side features.
- Monetization (business model chưa quyết định — [OQ-025](OPEN_QUESTIONS.md)).
- Nền tảng khác ngoài PC và Android (iOS, console, web).
- Sản xuất content hàng loạt trước khi core mechanics và Art Direction được duyệt.

### 3.3. Chưa xác định

Quy mô nội dung của bản hoàn chỉnh, kênh phát hành, thời gian, ngân sách — xem [OPEN_QUESTIONS](OPEN_QUESTIONS.md) nhóm C.

---

## 4. Cơ cấu tổ chức

### 4.1. Hai tầng

| Tầng | Thành viên | Vai trò | Chi tiết |
|---|---|---|---|
| **A — Strategic & Creative Decision** | Game Director (người dùng) | Quyết định cuối cùng | [agents/GAME_DIRECTOR.md](../../agents/GAME_DIRECTOR.md) |
| | ChatGPT | Strategic & System Design Advisor — chỉ tư vấn | [agents/CHATGPT.md](../../agents/CHATGPT.md) |
| | Gemini Pro | Independent Creative & Technical Advisor — chỉ tư vấn | [agents/GEMINI.md](../../agents/GEMINI.md) |
| **B — Project Execution & Delivery** | Claude | Project Lead — đặc tả, điều phối, giám sát | [agents/CLAUDE.md](../../agents/CLAUDE.md) |
| | Codex | Software Implementation & Basic QA | [agents/CODEX.md](../../agents/CODEX.md) |
| | Antigravity | Visual Production | [agents/ANTIGRAVITY.md](../../agents/ANTIGRAVITY.md) |

Tổng hợp năng lực, giới hạn và mô hình giao tiếp: [AGENT_ROLES.md](AGENT_ROLES.md).

### 4.2. Bảy bộ phận

| # | Bộ phận | Primary Executor | Phê duyệt | Charter |
|---|---|---|---|---|
| 01 | Production & Management | Claude | Game Director (L1/L2) | [DEPARTMENT](../01_production/DEPARTMENT.md) |
| 02 | Game Design | Claude (đặc tả) · Codex (triển khai) | Game Director | [DEPARTMENT](../02_game_design/DEPARTMENT.md) |
| 03 | Narrative & Worldbuilding | Claude (đặc tả, continuity) · Codex (runtime) | Game Director | [DEPARTMENT](../03_narrative/DEPARTMENT.md) |
| 04 | Art & Visual Production | Antigravity | Game Director | [DEPARTMENT](../04_art/DEPARTMENT.md) |
| 05 | Game Engineering | Codex (triển khai) · Claude (đặc tả kiến trúc) | Game Director (kiến trúc lớn) | [DEPARTMENT](../05_engineering/DEPARTMENT.md) |
| 06 | Audio & Content Integration | Sản xuất audio: `UNASSIGNED` · Tích hợp: Codex | Game Director | [DEPARTMENT](../06_audio_integration/DEPARTMENT.md) |
| 07 | QA & Release | Codex (QA cơ bản) · Claude (giám sát) | Game Director (nghiệm thu) | [DEPARTMENT](../07_qa_release/DEPARTMENT.md) |

---

## 5. Nguyên tắc cốt lõi (Core Principles)

Mười hai nguyên tắc dưới đây đã được Game Director đưa ra ([D-0009](DECISION_LOG.md#d-0009--12-nguyên-tắc-cốt-lõi)). Cột "Áp dụng" mô tả cách nguyên tắc được thực thi trong quy trình.

| # | Nguyên tắc | Áp dụng |
|---|---|---|
| P1 | **Design Before Implementation** — không xây hệ thống lớn khi chưa có đặc tả và phạm vi rõ | Task không đạt [Definition of Ready](DEFINITION_OF_READY_DONE.md#1-definition-of-ready) thì không giao |
| P2 | **Prototype Before Scale** — ưu tiên bản mẫu chơi được, chưa tạo content hàng loạt | M2 dùng placeholder art; content hàng loạt chỉ sau M5 |
| P3 | **Vertical Slice First** — một lát cắt hoàn chỉnh trước khi mở rộng | M5 là cổng bắt buộc trước khi mở rộng nội dung |
| P4 | **Modular but Practical** — chia module theo trách nhiệm thực tế, tránh phụ thuộc vòng và abstraction thừa | [MODULE_BOUNDARIES](../05_engineering/MODULE_BOUNDARIES.md) quy định hướng phụ thuộc |
| P5 | **Data-driven Content** — kỹ năng, vật phẩm, nhiệm vụ, hội thoại dùng dữ liệu cấu hình khi phù hợp | [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md) |
| P6 | **Contract-first Collaboration** — thống nhất giao diện trước khi làm song song | Code và art chỉ chạy song song khi contract ở trạng thái `APPROVED` |
| P7 | **Art Consistency Before Quantity** — asset quan trọng phải có concept được duyệt | Quy trình Art bắt buộc trong [04_art/DEPARTMENT](../04_art/DEPARTMENT.md#9-workflows) |
| P8 | **Testable Deliverables** — mỗi task có cách kiểm chứng rõ ràng | Trường "Validation Method" bắt buộc trong [TASK_TEMPLATE](../templates/TASK_TEMPLATE.md) |
| P9 | **Human Creative Control** — quyết định sáng tạo và phạm vi lớn thuộc về Game Director | [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md) |
| P10 | **Traceability** — Decision → Specification → Task → Implementation → Test Evidence → Acceptance | Mọi task phải tham chiếu Spec/Decision ID; mọi báo cáo phải tham chiếu Task ID |
| P11 | **PC and Android Awareness** — input, UI, hiệu năng, tài nguyên phải xét cả hai nền tảng | Mục "Platform Considerations" bắt buộc trong [FEATURE_SPEC_TEMPLATE](../templates/FEATURE_SPEC_TEMPLATE.md) |
| P12 | **Original Intellectual Property** — các game tham khảo (ví dụ Ngọc Rồng Online, Ninja School) chỉ để tham khảo thể loại/trải nghiệm | Cấm sao chép nhân vật, logo, sprite, bản đồ, âm nhạc, lời thoại; xem [ASSET_SPEC §9](../04_art/ASSET_SPEC.md#9-copyright-và-originality) |

---

## 6. Ràng buộc và giả định vận hành

| # | Nội dung | Loại |
|---|---|---|
| C1 | Các AI agent **không tự kết nối với nhau**. Game Director chuyển tài liệu/task giữa các agent; repository là bộ nhớ chung. | Ràng buộc |
| C2 | Năng lực thực tế của từng agent (Codex chạy Unity batchmode, Antigravity tạo sprite sheet nhất quán…) **chưa được xác minh**. | Giả định cần kiểm chứng — [RISK_REGISTER](../01_production/RISK_REGISTER.md) R-005, R-003 |
| C3 | Chưa có agent sản xuất âm thanh. Vai trò audio production là `UNASSIGNED`. | Ràng buộc |
| C4 | Chưa có thời hạn, ngân sách, phần cứng thử nghiệm được xác định. Không đặt deadline. | Ràng buộc |
| C5 | Thư mục dự án hiện chưa dùng version control. | Thực tế — [OQ-009](OPEN_QUESTIONS.md) |

---

## 7. Tiêu chí thành công

- **Tiêu chí sản phẩm:** `TBD` — phụ thuộc Game Vision ([OQ-001](OPEN_QUESTIONS.md)).
- **Tiêu chí quy trình (áp dụng ngay):**
  1. Mọi quyết định L1/L2 có Decision Record và đúng người phê duyệt.
  2. Mọi task có Task ID, tiêu chí nghiệm thu và bằng chứng hoàn thành.
  3. Không có báo cáo "đã kiểm thử" nào thiếu bằng chứng.
  4. Mỗi milestone đóng bằng exit gate được Game Director phê duyệt.

---

## 8. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo Charter trong M0 | Claude |
