# Story Architecture

> **Document Owner:** Claude · **Approver:** Game Director (kiến trúc L1) · **Status:** `UNDER_REVIEW` — kiến trúc `PROPOSED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [QUEST_DIALOGUE_DESIGN](QUEST_DIALOGUE_DESIGN.md) · [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md) · [MODULE_BOUNDARIES](../05_engineering/MODULE_BOUNDARIES.md) · [UNITY_ARCHITECTURE_PROPOSAL](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md)

Tài liệu mô tả **cách câu chuyện được tổ chức và vận hành**, không phải nội dung câu chuyện. Toàn bộ kiến trúc dưới đây là `PROPOSED` (L1) cho tới khi GD duyệt.

---

## 1. Content vs Runtime

| | Narrative Content | Narrative Runtime |
|---|---|---|
| Là gì | Thế giới, nhân vật, chương, quest, lời thoại, cutscene | Code đọc dữ liệu narrative, theo dõi trạng thái, kích hoạt sự kiện |
| Dạng | Tài liệu canon + file dữ liệu | C# trong Unity |
| Ai quyết | Game Director | GD duyệt kiến trúc; Codex triển khai |
| Thay đổi khi | Viết thêm/sửa nội dung | Cần tính năng narrative mới |
| Quy tắc | Không nằm trong code | Không chứa nội dung cụ thể (không hardcode tên NPC, lời thoại, quest) |

Kiểm tra tách biệt: **thay toàn bộ dữ liệu narrative bằng bộ dữ liệu khác mà không sửa code** — runtime vẫn chạy (tiêu chí M3).

## 2. Cấu trúc nội dung — `PROPOSED`

```
Story
 └─ Chapter (CH_NN)          — đơn vị lớn của cốt truyện chính
     └─ Story Beat (BEAT_…)  — sự kiện cốt truyện then chốt
         ├─ Main Quest(s)    — người chơi thực hiện beat
         └─ Cutscene(s)      — trình bày beat
Side Quest (độc lập, có điều kiện mở theo Story State)
```

Số chương: `TBD` ([OQ-024](../00_governance/OPEN_QUESTIONS.md)).

## 3. Các thành phần trạng thái

| Thành phần | Định nghĩa | Ví dụ khái niệm (`EXAMPLE — NOT APPROVED`) | Ai ghi | Ai đọc |
|---|---|---|---|---|
| **World State** | Trạng thái bền vững của thế giới: cửa mở/đóng, NPC xuất hiện hay không, khu vực đã mở khóa | `area.gate_east.opened = true` | Story Events, Quest outcomes | World module, Dialogue conditions |
| **Story State** | Vị trí của người chơi trong cốt truyện chính: chương hiện tại, beat đã hoàn thành | `chapter = 2; beat.BEAT_X = completed` | Narrative Progression | Quest availability, Dialogue, Cutscene Triggers |
| **Quest State** | Trạng thái từng quest và từng objective | `QST_A: Active, obj 2/3` | Quest engine (từ gameplay events) | UI, Dialogue conditions, Story Progression |
| **Dialogue State** | Lịch sử hội thoại: node đã xem, lựa chọn đã chọn | `DLG_NPC1.intro.seen = true` | Dialogue engine | Dialogue conditions |
| **Character Relationships** | Quan hệ người chơi–NPC/phe (nếu thiết kế có) — **có hay không là `TBD`** | `rel.FAC_X = 10` | Story Events, Dialogue effects | Dialogue conditions, Quest availability |
| **Story Events** | Sự kiện rời rạc phát ra khi điều gì đó xảy ra; không phải trạng thái | `OnBossDefeated(BOSS_X)`, `OnQuestCompleted(QST_A)` | Gameplay, Quest, Dialogue | Narrative Progression, Cutscene Triggers |
| **Narrative Progression** | Bộ quy tắc: khi điều kiện X thỏa → cập nhật Story/World State, mở quest | "Khi QST_A hoàn thành và beat Y đã xong → mở CH_02" | (là luật, định nghĩa bằng dữ liệu) | Story State |
| **Cutscene Triggers** | Điều kiện kích hoạt cutscene + cờ "đã xem" | "Vào Area Z lần đầu khi chapter = 1" | Dữ liệu | Cutscene player |

Nguyên tắc: **State** là dữ liệu bền vững cần lưu; **Event** là tín hiệu tức thời không lưu. Mọi thay đổi State đi qua một điểm duy nhất trong Narrative module để dễ test và debug.

## 4. Luồng tương tác

```
 Gameplay (Combat, World, Interaction)
        │  phát Story Events (ví dụ: EnemyKilled, ItemCollected, AreaEntered, NpcTalked)
        ▼
 ┌──────────────── Narrative Module ────────────────┐
 │ Quest Engine ──cập nhật──► Quest State            │
 │      │ QuestCompleted event                        │
 │      ▼                                             │
 │ Narrative Progression (luật dữ liệu)               │
 │      ├──► Story State                              │
 │      ├──► World State ──► World module áp dụng     │
 │      └──► Cutscene Triggers ──► Cutscene player    │
 │ Dialogue Engine ◄── đọc Conditions từ mọi State    │
 │      └── Effects ──► State (qua Progression)       │
 └────────────────────────────────────────────────────┘
        │  đọc (read-only)
        ▼
       UI (quest log, dialogue box)        Persistence ◄── snapshot mọi State
```

Hướng phụ thuộc: Narrative có thể đọc kiểu dữ liệu của Gameplay (ví dụ ID vật phẩm cho phần thưởng); Gameplay **không** gọi trực tiếp Narrative mà phát event. Chi tiết: [MODULE_BOUNDARIES](../05_engineering/MODULE_BOUNDARIES.md).

## 5. Hệ thống điều kiện và hiệu ứng (Conditions & Effects) — `PROPOSED`

Dùng chung cho quest, dialogue, cutscene trigger, progression:

- **Condition:** biểu thức đọc State. Ví dụ dạng: `QuestState(QST_A) == Completed`, `StoryFlag(F) == true`, `HasItem(ITM_X, 1)`.
- **Effect:** thao tác ghi State hoặc phát lệnh. Ví dụ dạng: `SetFlag(F)`, `StartQuest(QST_B)`, `GiveItem(ITM_X, 1)`, `PlayCutscene(CS_1)`.

Tập condition/effect cụ thể sẽ được chốt trong data contract (M1–M3). Bắt đầu với tập nhỏ, mở rộng khi nội dung cần (P4).

## 6. Save-Load Requirements

Yêu cầu khung (`PROPOSED`); chế độ lưu (manual/auto/checkpoint) là `TBD` ([OQ-019](../00_governance/OPEN_QUESTIONS.md)).

| # | Yêu cầu |
|---|---|
| SL-1 | Lưu được: World State, Story State, Quest State, Dialogue State, Character Relationships (nếu có), cờ cutscene đã xem. |
| SL-2 | Không lưu Story Events (tức thời) — hệ thống phải khôi phục đúng chỉ từ State. |
| SL-3 | Save data tham chiếu nội dung bằng **ID ổn định**, không bằng tên hiển thị hay đường dẫn asset. |
| SL-4 | Save data có `schemaVersion`; khi schema đổi phải có migration hoặc thông báo không tương thích. |
| SL-5 | Thêm quest/dialogue mới vào bản cập nhật không làm hỏng save cũ (State thiếu key → giá trị mặc định). |
| SL-6 | Tải game giữa quest → quest tiếp tục đúng objective; không phát lại phần thưởng đã nhận. |
| SL-7 | Android: lưu an toàn khi app bị đưa xuống nền/đóng đột ngột (ghi file nguyên tử — atomic write). |
| SL-8 | Có test tự động: save → load → so sánh State trùng khớp. |

## 7. Debug và kiểm thử narrative

- Công cụ debug (Editor hoặc in-game, chỉ bản dev) để xem và đặt State: nhảy chương, hoàn thành quest, đặt cờ — giúp test nhanh mà không phải chơi lại.
- Kiểm tra tĩnh dữ liệu: quest tham chiếu ID không tồn tại, dialogue node không thể tới, quest không thể hoàn thành.
- Chi tiết: [TEST_STRATEGY](../07_qa_release/TEST_STRATEGY.md).
