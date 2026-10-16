# Decision Log

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `ACTIVE` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [DECISION_POLICY](DECISION_POLICY.md) · [OPEN_QUESTIONS](OPEN_QUESTIONS.md) · [CHANGE_CONTROL](CHANGE_CONTROL.md) · [DECISION_RECORD_TEMPLATE](../templates/DECISION_RECORD_TEMPLATE.md)

Đây là sổ quyết định chính thức của dự án. **Một quyết định chưa có ở đây thì chưa tồn tại**, dù đã được nói trong chat. Quy tắc duy trì: [DECISION_POLICY §1.1](DECISION_POLICY.md#11-quy-tắc-duy-trì-nghiêm-ngặt-decision_log-và-open_questions).

Quy ước: record ngắn ghi trực tiếp trong file này. Khi một record dài hơn ~1 trang, tách sang `docs/00_governance/decisions/D-NNNN-<slug>.md` và giữ dòng chỉ mục ở đây.

---

## Chỉ mục

| ID | Tiêu đề | Level | Status | Owner | Ngày |
|---|---|---|---|---|---|
| D-0001 | Thể loại 2D Adventure RPG | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0002 | Engine Unity, ngôn ngữ C# | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0003 | Nền tảng mục tiêu PC + Android | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0004 | Phong cách chiến đấu Real-time Action | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0005 | Multiplayer ngoài phạm vi ban đầu | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0006 | Mô hình phát triển và phân vai agent | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0007 | Ngôn ngữ tài liệu chính tiếng Việt | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0008 | Cơ cấu 7 bộ phận | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0009 | 12 nguyên tắc cốt lõi | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0010 | Khung milestone M0–M7, chỉ thực thi M0 | L2 | `APPROVED` | Game Director | 2026-10-15 |
| D-0011 | Cấu trúc tài liệu, quy ước ID và từ vựng trạng thái | L0 | `APPROVED` | Claude | 2026-10-15 |
| D-0012 | Điều chỉnh nhỏ cho kế hoạch milestone | L1 | `PROPOSED` | Game Director | 2026-10-15 |

---

## Records

### D-0001 — Thể loại 2D Adventure RPG

- **Level / Status:** L2 · `APPROVED`
- **Context:** Xác định thể loại nền tảng của dự án.
- **Decision:** Game là 2D Adventure RPG.
- **Decision Owner:** Game Director
- **Approval Evidence:** Master Prompt v1.0 do Game Director cung cấp ngày 2026-10-15, mục 1 "Thông tin dự án đã được phê duyệt".
- **Consequences:** Mọi thiết kế phải phục vụ trải nghiệm phiêu lưu và nhập vai trong không gian 2D. Góc nhìn 2D cụ thể vẫn `TBD` ([OQ-002](OPEN_QUESTIONS.md)).
- **Related:** [PROJECT_CHARTER](PROJECT_CHARTER.md), [GAME_DESIGN](../02_game_design/GAME_DESIGN.md)

### D-0002 — Engine Unity, ngôn ngữ C#

- **Level / Status:** L2 · `APPROVED`
- **Decision:** Unity, lập trình bằng C# theo hệ sinh thái Unity.
- **Decision Owner:** Game Director · **Approval Evidence:** như D-0001.
- **Consequences:** Phiên bản Unity, render pipeline, input system, package vẫn `TBD` ([OQ-006](OPEN_QUESTIONS.md), [OQ-007](OPEN_QUESTIONS.md), [OQ-008](OPEN_QUESTIONS.md)).
- **Related:** [UNITY_ARCHITECTURE_PROPOSAL](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md), [TECH_DECISIONS](../05_engineering/TECH_DECISIONS.md)

### D-0003 — Nền tảng mục tiêu PC + Android

- **Level / Status:** L2 · `APPROVED`
- **Decision:** Phát triển cho PC và Android.
- **Decision Owner:** Game Director · **Approval Evidence:** như D-0001.
- **Consequences:** Input (bàn phím/chuột và cảm ứng), UI scaling, hiệu năng và dung lượng phải xét cho cả hai nền tảng từ khi đặc tả (nguyên tắc P11). Cấu hình thử nghiệm `TBD` ([OQ-011](OPEN_QUESTIONS.md)). Các nền tảng khác ngoài phạm vi.
- **Related:** [TEST_STRATEGY](../07_qa_release/TEST_STRATEGY.md)

### D-0004 — Phong cách chiến đấu Real-time Action

- **Level / Status:** L2 · `APPROVED`
- **Decision:** Chiến đấu thời gian thực theo hướng action (không phải turn-based).
- **Decision Owner:** Game Director · **Approval Evidence:** như D-0001.
- **Consequences:** Cảm giác điều khiển, độ trễ input và điều khiển cảm ứng trên Android là rủi ro thiết kế chính. Chi tiết cơ chế `TBD` ([OQ-005](OPEN_QUESTIONS.md)).
- **Related:** [COMBAT_DESIGN](../02_game_design/COMBAT_DESIGN.md)

### D-0005 — Multiplayer ngoài phạm vi ban đầu

- **Level / Status:** L2 · `APPROVED` (phần "ngoài phạm vi ban đầu") · phần "mở rộng tương lai" `TBD`
- **Decision:** Không triển khai multiplayer trong phạm vi ban đầu.
- **Decision Owner:** Game Director · **Approval Evidence:** như D-0001.
- **Consequences:** Kiến trúc không xây sẵn hạ tầng mạng. Không bắt buộc thiết kế "network-ready". Khả năng mở rộng tương lai: [OQ-028](OPEN_QUESTIONS.md).

### D-0006 — Mô hình phát triển và phân vai agent

- **Level / Status:** L2 · `APPROVED`
- **Decision:** AI-assisted, human-directed. Hai tầng: (A) Game Director quyết định, ChatGPT và Gemini tư vấn; (B) Claude là Project Lead, Codex triển khai code và QA cơ bản, Antigravity sản xuất hình ảnh. Ba cấp quyết định L0/L1/L2.
- **Decision Owner:** Game Director · **Approval Evidence:** Master Prompt v1.0, mục 2 và 3.
- **Consequences:** Xem [AGENT_ROLES](AGENT_ROLES.md), [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md), [agents/](../../agents/).

### D-0007 — Ngôn ngữ tài liệu chính tiếng Việt

- **Level / Status:** L2 · `APPROVED`
- **Decision:** Tài liệu viết bằng tiếng Việt, giữ thuật ngữ kỹ thuật tiếng Anh khi phù hợp.
- **Decision Owner:** Game Director · **Approval Evidence:** Master Prompt v1.0, mục 1 và 13.
- **Consequences:** Ngôn ngữ **trong game** (localization) là câu hỏi riêng, chưa quyết định ([OQ-021](OPEN_QUESTIONS.md)). Code, tên file, identifier dùng tiếng Anh ([MODULE_BOUNDARIES](../05_engineering/MODULE_BOUNDARIES.md)).

### D-0008 — Cơ cấu 7 bộ phận

- **Level / Status:** L2 · `APPROVED`
- **Decision:** 01 Production & Management · 02 Game Design · 03 Narrative & Worldbuilding · 04 Art & Visual Production · 05 Game Engineering · 06 Audio & Content Integration · 07 QA & Release.
- **Decision Owner:** Game Director · **Approval Evidence:** Master Prompt v1.0, mục 4.
- **Consequences:** Mỗi bộ phận có một `DEPARTMENT.md`. Vai trò sản xuất audio là `UNASSIGNED`.

### D-0009 — 12 nguyên tắc cốt lõi

- **Level / Status:** L2 · `APPROVED`
- **Decision:** Áp dụng 12 nguyên tắc P1–P12 ghi trong [PROJECT_CHARTER §5](PROJECT_CHARTER.md#5-nguyên-tắc-cốt-lõi-core-principles).
- **Decision Owner:** Game Director · **Approval Evidence:** Master Prompt v1.0, mục 9.

### D-0010 — Khung milestone M0–M7, chỉ thực thi M0

- **Level / Status:** L2 · `APPROVED` (khung và exit gate định hướng)
- **Decision:** Dự án đi theo khung M0–M7. Phiên khởi tạo **chỉ thực thi M0**; M1–M7 ở mức kế hoạch. Quyết định ưu tiên sau M0: Game Vision, Combat Direction, Art Direction.
- **Decision Owner:** Game Director
- **Approval Evidence:** Master Prompt v1.0, mục 10 và 16; tin nhắn bổ sung của Game Director ngày 2026-10-15 ("Prompt trên chỉ yêu cầu thực thi M0; những milestone còn lại mới ở cấp độ kế hoạch").
- **Consequences:** Tiêu chí nghiệm thu chi tiết của từng milestone do Claude viết trong [MILESTONES](../01_production/MILESTONES.md) ở trạng thái `PROPOSED` cho tới khi GD duyệt. Không đặt deadline.

### D-0011 — Cấu trúc tài liệu, quy ước ID và từ vựng trạng thái

- **Level / Status:** L0 · `APPROVED` (bởi Claude trong phạm vi L0; GD có thể bác bỏ)
- **Context:** Cần quy ước thống nhất để truy vết và để các agent không tự đặt quy ước riêng.
- **Decision:**
  1. Cây tài liệu theo Master Prompt mục 5, bổ sung một file: [`docs/01_production/RISK_REGISTER.md`](../01_production/RISK_REGISTER.md) (Risk register là trách nhiệm của bộ phận 01 nhưng chưa có file trong cây bắt buộc).
  2. Quy ước ID và từ vựng trạng thái theo [DECISION_POLICY §5–6](DECISION_POLICY.md#5-từ-vựng-trạng-thái).
  3. Thư mục con (`tasks/`, `reports/`, `specs/`, `briefs/`, `reviews/`, `decisions/`) chỉ tạo khi có nội dung đầu tiên — không tạo thư mục/file rỗng.
- **Decision Owner:** Claude
- **Consequences:** Mọi agent dùng chung quy ước này.

### D-0012 — Điều chỉnh nhỏ cho kế hoạch milestone

- **Level / Status:** L1 · `PROPOSED`
- **Context:** Khung M0–M7 đã duyệt. Claude đề xuất ba điều chỉnh để giảm rủi ro mà không đổi thứ tự hay mục tiêu milestone.
- **Options:**
  - **A. Giữ nguyên khung** — đơn giản, nhưng rủi ro Android và năng lực agent bị phát hiện muộn (M6).
  - **B. Thêm ba điều chỉnh (khuyến nghị):**
    1. **M1** thêm task *xác minh năng lực agent*: Codex chạy Unity batchmode/test/build; Antigravity thử tạo nhân vật nhất quán và sprite frame (chỉ để thử năng lực, không phải asset chính thức).
    2. **M1** bắt đầu *Research + Moodboard* của Art Direction song song (bước 1–2 của quy trình Art), để quyết định Art Direction không chặn M4.
    3. **M2** thêm *Android smoke build*: build prototype lên ít nhất một thiết bị Android để kiểm tra điều khiển cảm ứng sớm. Không thay thế M6.
- **Trade-offs:** B tăng một ít công việc ở M1–M2 nhưng phát hiện sớm hai rủi ro lớn nhất ([R-003](../01_production/RISK_REGISTER.md), [R-005](../01_production/RISK_REGISTER.md), [R-006](../01_production/RISK_REGISTER.md)).
- **Recommendation:** Phương án B.
- **Decision cần phê duyệt:** "Game Director có đồng ý thêm ba điều chỉnh trên vào M1 và M2 không?"
- **Decision Owner:** Game Director · **Approval Evidence:** — (chưa có)
- **Related:** [ROADMAP](../01_production/ROADMAP.md), [MILESTONES](../01_production/MILESTONES.md)
