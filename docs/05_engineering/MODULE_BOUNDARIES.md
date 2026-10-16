# Module Boundaries

> **Document Owner:** Claude · **Approver:** Game Director (L1) · **Status:** `UNDER_REVIEW` — `PROPOSED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [UNITY_ARCHITECTURE_PROPOSAL](UNITY_ARCHITECTURE_PROPOSAL.md) · [DATA_CONTRACTS](DATA_CONTRACTS.md) · [SYSTEMS_OVERVIEW](../02_game_design/SYSTEMS_OVERVIEW.md)

Định nghĩa trách nhiệm từng module và quy tắc phụ thuộc. Áp dụng cho Codex khi Unity project được tạo. Tất cả `PROPOSED`.

---

## 1. Danh sách module

| Module | Assembly (đề xuất) | Trách nhiệm | Không chịu trách nhiệm |
|---|---|---|---|
| **Core** | Game.Core | ID types, event types liên module, interfaces dùng chung (save participant, time, random), bootstrap, game flow (menu ↔ gameplay ↔ pause) | Logic gameplay cụ thể |
| **Character** | Game.Gameplay | Điều khiển nhân vật từ input actions, di chuyển, va chạm nhân vật | Tính sát thương |
| **Combat** | Game.Gameplay | Hitbox/hurtbox, damage, health, chết, phản hồi đòn đánh | Quyết định AI |
| **Skills** | Game.Gameplay | Kích hoạt kỹ năng, cooldown, tài nguyên | UI hiển thị kỹ năng |
| **AI** | Game.Gameplay | Hành vi kẻ địch (FSM) | Sinh kẻ địch |
| **World** | Game.Gameplay | Nạp Area, spawner, interactable, áp dụng World State | Quyết định cốt truyện |
| **Inventory / Progression** | Game.Gameplay | Vật phẩm, trang bị, chỉ số, cấp độ (nếu được duyệt) | Phần thưởng quest (chỉ nhận lệnh) |
| **Narrative** (Story, Quests, Dialogue) | Game.Narrative | Story/Quest/Dialogue State, progression rules, conditions/effects, cutscene triggers | Nội dung cụ thể (nằm trong dữ liệu) |
| **Persistence** | Game.Persistence | Gom DTO, ghi/đọc file, schema version, migration | Biết chi tiết từng hệ thống |
| **UI** | Game.UI | HUD, menu, dialogue box, quest log, touch controls | Logic gameplay |
| **Audio** | Game.Audio (hoặc Gameplay) | Phát âm thanh theo event mapping | Quyết định khi nào sự kiện xảy ra |
| **Editor Tools** | Game.Editor | Validator, debug tools, importer | Runtime |

## 2. Hướng phụ thuộc

```
            UI ─────────────┐
            │               │
            ▼               ▼
        Narrative ──► Gameplay ──► Core ◄── Persistence
                                     ▲
                                   Audio
Editor ──► (mọi module, chỉ trong Editor)
Tests  ──► (module được test)
```

Quy tắc:
1. Chỉ phụ thuộc theo chiều mũi tên. **Không phụ thuộc vòng.**
2. **Gameplay không tham chiếu Narrative hay UI.** Gameplay phát event (định nghĩa trong Core); Narrative/UI lắng nghe.
3. **Narrative được tham chiếu kiểu dữ liệu Gameplay** (ví dụ item definition cho phần thưởng) và gửi lệnh qua API công khai của Gameplay.
4. **UI chỉ đọc trạng thái và gửi input/lệnh**, không chứa quy tắc gameplay.
5. **Persistence chỉ biết interface trong Core**, không biết từng hệ thống cụ thể.
6. Trong cùng module, gọi trực tiếp là bình thường — không bắt buộc dùng event.

## 3. Giao tiếp liên module

| Từ → Tới | Cách | Ví dụ khái niệm (`EXAMPLE — NOT APPROVED`) |
|---|---|---|
| Gameplay → Narrative | Event trong Core | `EnemyKilled(enemyId)`, `ItemCollected(itemId, n)`, `AreaEntered(areaId)` |
| Narrative → Gameplay | API công khai của Gameplay | `inventory.Add(itemId, n)` khi quest trao thưởng |
| Narrative → World | World State + event | `WorldFlagChanged(flag)` → World mở cửa |
| Gameplay/Narrative → UI | Event hoặc UI đọc trạng thái | Health thay đổi → HUD cập nhật |
| UI → Gameplay | Input actions / lệnh | Nút cảm ứng → action Attack |
| Mọi hệ thống ↔ Persistence | Interface save participant | Xuất/nhập DTO |

Danh sách event liên module chính thức được giữ trong DATA_CONTRACTS khi chốt (giữ số lượng nhỏ).

## 4. Quy ước code

| Mục | Quy ước |
|---|---|
| Ngôn ngữ identifier, comment trong code | Tiếng Anh (D-0007 áp dụng cho tài liệu, không cho code) |
| Namespace | `Game.<Module>` — ví dụ `Game.Gameplay.Combat` |
| Định dạng | Theo quy ước C# phổ biến (PascalCase cho type/method, camelCase cho local, `_camelCase` cho private field) — chi tiết có thể chốt bằng `.editorconfig` khi tạo project |
| Serialized field | `[SerializeField] private` thay vì public field |
| Magic number | Không — đưa vào dữ liệu cấu hình hoặc hằng số có tên |
| Text hiển thị | Không hardcode — qua bảng localization key |
| Log | Có tiền tố module; log debug tắt trong bản release |

## 5. Quy tắc thay đổi ranh giới

Thêm module, gộp module, đổi hướng phụ thuộc → L1, qua [CHANGE_CONTROL](../00_governance/CHANGE_CONTROL.md). Codex phát hiện ranh giới gây khó khăn → báo Claude kèm ví dụ cụ thể.
