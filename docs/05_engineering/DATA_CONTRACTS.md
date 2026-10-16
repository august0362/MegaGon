# Data Contracts

> **Document Owner:** Claude · **Approver:** Game Director (contract dùng chung — L1) · **Status:** `UNDER_REVIEW` — chưa có contract nào `APPROVED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [MODULE_BOUNDARIES](MODULE_BOUNDARIES.md) · [STORY_ARCHITECTURE](../03_narrative/STORY_ARCHITECTURE.md) · [QUEST_DIALOGUE_DESIGN](../03_narrative/QUEST_DIALOGUE_DESIGN.md) · [ASSET_SPEC](../04_art/ASSET_SPEC.md)

Data contract là thỏa thuận về **cấu trúc dữ liệu** giữa người tạo dữ liệu (Claude/GD/Antigravity) và người dùng dữ liệu (Codex/runtime). Theo P6, công việc song song chỉ bắt đầu khi contract liên quan `APPROVED`.

---

## 1. Nguyên tắc

1. **ID ổn định dạng chuỗi**, tiền tố theo loại, chữ hoa, tiếng Anh: `CHR_`, `ENM_`, `BOSS_`, `ITM_`, `SKL_`, `QST_`, `DLG_`, `AREA_`, `FAC_`, `CS_` (cutscene), `FLAG_`. ID không đổi sau khi đã dùng trong save data.
2. Text hiển thị dùng **localization key**, không chứa text trực tiếp.
3. Tham chiếu chéo dùng ID, được validator kiểm tra.
4. Mỗi contract có **version**; thay đổi phá vỡ tương thích (breaking change) → L1 + migration cho save data nếu ảnh hưởng.
5. Trường chưa quyết định ghi `TBD`; không bịa trường để "cho đủ".

## 2. Mẫu định nghĩa contract

```markdown
### DC-<NAME> v<N> — <Tên>
- Status: PROPOSED / APPROVED (Decision D-NNNN)
- Producer: … · Consumer: …
- Storage: ScriptableObject / JSON / …
- Fields:
| Field | Type | Required | Mô tả | Ràng buộc / validation |
- Validation rules:
- Save impact: có / không (trường nào được lưu)
- Platform notes:
- Change log:
```

## 3. Danh mục contract dự kiến

| Contract | Mục đích | Cần cho | Phụ thuộc | Status |
|---|---|---|---|---|
| DC-INPUT-ACTIONS | Danh sách input action gameplay dùng (Move, Attack…) | M2 | OQ-005, OQ-008 | `TBD` |
| DC-TUNING-MOVEMENT | Tham số di chuyển | M2 | OQ-004 | `TBD` |
| DC-ATTACK | Định nghĩa đòn đánh (pha, hitbox, sát thương) | M2 | OQ-005 | `TBD` |
| DC-ENEMY | Định nghĩa kẻ địch | M2 | OQ-005 | `TBD` |
| DC-EVENTS | Danh sách event liên module | M2 | MODULE_BOUNDARIES | `TBD` |
| DC-SPRITE-IMPORT | Asset contract: PPU, pivot, đặt tên, frame | M2 (placeholder) / M4 | OQ-014, OQ-015 | `TBD` |
| DC-CONDITION-EFFECT | Tập Condition/Effect narrative | M3 | STORY_ARCHITECTURE | `PROPOSED` (khái niệm) |
| DC-QUEST | Định nghĩa quest | M3 | QUEST_DIALOGUE_DESIGN | `PROPOSED` (khái niệm) |
| DC-DIALOGUE | Định nghĩa dialogue | M3 | OQ-020 | `PROPOSED` (khái niệm) |
| DC-LOCALIZATION | Bảng key–text | M3 | OQ-021 | `TBD` |
| DC-SAVE | Cấu trúc save file, schemaVersion | M3 | OQ-019 | `TBD` |
| DC-ITEM | Định nghĩa vật phẩm | M5 | OQ-023 | `TBD` |
| DC-SKILL | Định nghĩa kỹ năng | M5 | OQ-017 | `TBD` |
| DC-PROGRESSION | Chỉ số, cấp độ | M5 | OQ-018 | `TBD` |
| DC-AUDIO-EVENTS | Ánh xạ event → audio | M5 | AUDIO_PLAN | `TBD` |

## 4. Ví dụ minh họa

> **`EXAMPLE — NOT APPROVED`** — chỉ để minh họa định dạng. Tên trường, giá trị và cấu trúc **không** phải yêu cầu.

```json
{
  "id": "QST_EXAMPLE_FIRST_ERRAND",
  "type": "Side",
  "titleKey": "quest.example_first_errand.title",
  "availability": [ { "condition": "StoryFlag", "flag": "FLAG_EXAMPLE_INTRO_DONE", "value": true } ],
  "objectives": [
    { "type": "TalkTo", "target": "CHR_NPC_EXAMPLE", "count": 1 },
    { "type": "Collect", "target": "ITM_EXAMPLE_HERB", "count": 3 }
  ],
  "onComplete": [ { "effect": "SetFlag", "flag": "FLAG_EXAMPLE_ERRAND_DONE" } ]
}
```
