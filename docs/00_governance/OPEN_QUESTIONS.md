# Open Questions

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `ACTIVE` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [DECISION_LOG](DECISION_LOG.md) · [DECISION_POLICY](DECISION_POLICY.md) · [MILESTONES](../01_production/MILESTONES.md)

Sổ đăng ký mọi vấn đề **chưa được quyết định**. Không mục nào ở đây được coi là yêu cầu chính thức. Quy tắc duy trì: [DECISION_POLICY §1.1](DECISION_POLICY.md#11-quy-tắc-duy-trì-nghiêm-ngặt-decision_log-và-open_questions).

**Vòng đời một câu hỏi:** `TBD` → (Claude/advisor phân tích) `PROPOSED` → (Decision Record trình GD) `UNDER_REVIEW` → giải quyết: ghi Decision ID và chuyển xuống mục [Đã giải quyết](#đã-giải-quyết). Không xóa.

Sắp xếp theo **thời điểm cần quyết định** và **thứ tự phụ thuộc**. Không cần trả lời các nhóm sau trước khi tới lúc.

---

## Ưu tiên của M1 — bộ ba quyết định định hướng

Theo [D-0010](DECISION_LOG.md#d-0010--khung-milestone-m0m7-chỉ-thực-thi-m0), sau M0 cần tập trung vào:

1. **Game Vision** — [OQ-001](#nhóm-a--cần-trong-m1-trước-khi-bắt-đầu-m2)
2. **Combat Direction** — [OQ-005](#nhóm-a--cần-trong-m1-trước-khi-bắt-đầu-m2), cần [OQ-002](#nhóm-a--cần-trong-m1-trước-khi-bắt-đầu-m2) (camera) trước
3. **Art Direction** — [OQ-014](#nhóm-b--cần-trước-hoặc-trong-m3m4): bắt đầu khám phá ngay trong M1, quyết định trước M4

Đây là thời điểm phù hợp để dùng ChatGPT và Gemini so sánh, phản biện, sau đó GD quyết định và Claude đặc tả.

---

## Nhóm A — Cần trong M1, trước khi bắt đầu M2

| ID | Câu hỏi | Level | Ảnh hưởng | Phụ thuộc | Status | Phân tích |
|---|---|---|---|---|---|---|
| OQ-001 | **Game Vision**: trải nghiệm cốt lõi, game pillars, người chơi mục tiêu, cảm xúc chủ đạo, tham vọng quy mô | L2 | Toàn bộ thiết kế | — | `TBD` | [GAME_DESIGN §2](../02_game_design/GAME_DESIGN.md#2-game-vision--tbd) |
| OQ-002 | **Góc nhìn camera**: side-scrolling, top-down, top-down 3/4, isometric, hoặc khác | L2 | Movement, combat, level, art, physics, UI | OQ-001 | `TBD` | [GAME_DESIGN §4](../02_game_design/GAME_DESIGN.md#4-góc-nhìn-camera--tbd) |
| OQ-003 | **Core gameplay loop** | L1 | Mọi hệ thống, progression | OQ-001 | `TBD` | [GAME_DESIGN §3](../02_game_design/GAME_DESIGN.md#3-core-gameplay-loop--tbd) |
| OQ-004 | **Mô hình di chuyển**: 4/8 hướng hay tự do, nhảy, dash, quán tính, va chạm | L1 | Character, physics, level metrics | OQ-002 | `TBD` | [SYSTEMS_OVERVIEW](../02_game_design/SYSTEMS_OVERVIEW.md) |
| OQ-005 | **Combat Direction cho prototype**: mô hình tấn công, nhắm mục tiêu, hit detection, phòng thủ/né, kích hoạt kỹ năng | L1 | Combat, AI, input, animation, UI cảm ứng | OQ-002, OQ-003 | `TBD` | [COMBAT_DESIGN](../02_game_design/COMBAT_DESIGN.md) |
| OQ-006 | **Phiên bản Unity** (LTS cụ thể) | L1 | Toàn bộ engineering | — | `TBD` | [TECH_DECISIONS TD-01](../05_engineering/TECH_DECISIONS.md#td-01--phiên-bản-unity) |
| OQ-007 | **Render pipeline** (URP 2D Renderer / Built-in) | L1 | Lighting, shader, art pipeline, hiệu năng Android | Nên xét cùng OQ-014 | `TBD` | [TECH_DECISIONS TD-02](../05_engineering/TECH_DECISIONS.md#td-02--render-pipeline) |
| OQ-008 | **Input system và control scheme**: Input System package hay Input Manager cũ; bàn phím/chuột, gamepad trên PC, cảm ứng trên Android | L1 | Character, combat, UI | OQ-005 | `TBD` | [TECH_DECISIONS TD-03](../05_engineering/TECH_DECISIONS.md#td-03--input-handling) |
| OQ-009 | **Version control và hosting**: Git + LFS, nơi lưu remote, quyền commit/merge của agent | L1 | Mọi cộng tác, lịch sử tài liệu | — | `TBD` | [TECH_DECISIONS TD-04](../05_engineering/TECH_DECISIONS.md#td-04--version-control) · [WORKFLOW §6](WORKFLOW.md#6-git-branch-pull-request--proposed) |
| OQ-010 | **Vị trí Unity project trong repository** và cấu trúc thư mục/assembly | L1 | Engineering, CI | OQ-009 | `PROPOSED` | [UNITY_ARCHITECTURE_PROPOSAL §8](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md#8-cấu-trúc-unity-project-dự-kiến--proposed) |
| OQ-011 | **Cấu hình thử nghiệm**: PC tối thiểu, thiết bị Android tối thiểu, ai giữ thiết bị | L1 | Performance budget, QA | — | `TBD` | [TEST_STRATEGY §5](../07_qa_release/TEST_STRATEGY.md#5-pc-và-android) |

## Nhóm B — Cần trước hoặc trong M3/M4

| ID | Câu hỏi | Level | Ảnh hưởng | Phụ thuộc | Status | Phân tích |
|---|---|---|---|---|---|---|
| OQ-012 | **Bối cảnh thế giới và tông giọng** (premise) | L2 | Narrative, art, level | OQ-001 | `TBD` | [WORLD_BIBLE](../03_narrative/WORLD_BIBLE.md) |
| OQ-013 | **Cấu trúc cốt truyện chính**, nhân vật chính | L1 | Narrative, quest, level | OQ-012 | `TBD` | [STORY_ARCHITECTURE](../03_narrative/STORY_ARCHITECTURE.md) |
| OQ-014 | **Art Direction** (Pixel Art / Hand-drawn / Anime-inspired / Hybrid / khác) | L2 | Mọi asset, animation, render pipeline, UI | OQ-001, OQ-002 | `TBD` — khám phá bắt đầu M1 | [ART_DIRECTION_EXPLORATION](../04_art/ART_DIRECTION_EXPLORATION.md) |
| OQ-015 | **Phương pháp animation**: frame-by-frame, skeletal (2D Animation/Spine), hybrid | L1 | Art pipeline, engineering, chi phí | OQ-014 | `TBD` | [ASSET_SPEC §5](../04_art/ASSET_SPEC.md#5-animation-frame-requirements) |
| OQ-016 | **Hệ thống nhân vật**: một nhân vật chính, nhiều lớp nhân vật, party | L1 | Combat, skill, progression, narrative | OQ-001, OQ-005 | `TBD` | [SYSTEMS_OVERVIEW](../02_game_design/SYSTEMS_OVERVIEW.md) |
| OQ-017 | **Hệ thống kỹ năng**: cách nhận, nâng cấp, tài nguyên (mana/cooldown/…) | L1 | Combat, UI, data | OQ-005, OQ-016 | `TBD` | [COMBAT_DESIGN §5](../02_game_design/COMBAT_DESIGN.md#5-kỹ-năng-skills--tbd) |
| OQ-018 | **Chỉ số và progression** | L1 | Balance, inventory, save | OQ-016, OQ-025 | `TBD` | [SYSTEMS_OVERVIEW](../02_game_design/SYSTEMS_OVERVIEW.md) |
| OQ-019 | **Chế độ lưu**: manual/auto/checkpoint, số slot | L1 | Persistence, UX, Android lifecycle | OQ-003 | `TBD` | [STORY_ARCHITECTURE §6](../03_narrative/STORY_ARCHITECTURE.md#6-save-load-requirements) |
| OQ-020 | **Công cụ authoring narrative**: tự xây (ScriptableObject/JSON) hay dùng thư viện (ví dụ Ink, Yarn Spinner) | L1 | Narrative runtime, workflow viết nội dung | OQ-021 | `TBD` | [QUEST_DIALOGUE_DESIGN §5](../03_narrative/QUEST_DIALOGUE_DESIGN.md#5-authoring-format--tbd) |
| OQ-021 | **Ngôn ngữ trong game**: chỉ tiếng Việt, hay thêm tiếng Anh/khác | L2 | Text pipeline, UI, font, dữ liệu dialogue | OQ-001 | `TBD` | [QUEST_DIALOGUE_DESIGN §6](../03_narrative/QUEST_DIALOGUE_DESIGN.md#6-localization) |
| OQ-022 | **CI / build automation** | L1 | QA, build validation | OQ-006, OQ-009 | `TBD` | [TECH_DECISIONS TD-07](../05_engineering/TECH_DECISIONS.md#td-07--ci-và-build-automation) |

## Nhóm C — Cần trước M5 hoặc muộn hơn

| ID | Câu hỏi | Level | Ảnh hưởng | Phụ thuộc | Status |
|---|---|---|---|---|---|
| OQ-023 | **Inventory và equipment**: có hay không, quy tắc | L1 | UI, progression, save | OQ-018 | `TBD` |
| OQ-024 | **Quy mô nội dung**: kích thước bản đồ, số khu vực, số chương | L2 | Toàn bộ sản xuất | OQ-001, OQ-013 | `TBD` |
| OQ-025 | **Business model**: premium, free-to-play, khác — ảnh hưởng progression/economy | L2 | Progression, UI, phát hành | OQ-001 | `TBD` |
| OQ-026 | **Nguồn audio**: thư viện có license, người làm audio, công cụ AI audio (cần xác minh chất lượng và license) | L1 | Bộ phận 06, M5 | Ngân sách (OQ-030) | `TBD` — vai trò `UNASSIGNED` |
| OQ-027 | **Kênh phát hành** (ví dụ Steam, itch.io, Google Play) và yêu cầu của cửa hàng | L2 | Release checklist, build | OQ-025 | `TBD` |
| OQ-028 | **Multiplayer tương lai**: có cần giữ khả năng mở rộng hay không | L2 | Kiến trúc dài hạn | OQ-001 | `TBD` |
| OQ-029 | **Tên game** (thư mục `MegaGon` có phải codename không?) | L2 | Branding, store, package name Android | — | `TBD` |
| OQ-030 | **Thời gian phát hành và ngân sách** | L2 | Phạm vi, nguồn lực, audio | — | `TBD` |

---

## Đã giải quyết

| ID | Câu hỏi | Decision | Ngày |
|---|---|---|---|
| — | Chưa có | — | — |

---

## Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo 30 câu hỏi mở, nhóm theo thời điểm cần quyết định | Claude |
