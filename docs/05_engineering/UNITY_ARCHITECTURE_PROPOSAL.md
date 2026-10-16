# Unity Architecture Proposal

> **Document Owner:** Claude · **Approver:** Game Director (L1) · **Status:** `UNDER_REVIEW` — toàn bộ nội dung `PROPOSED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [MODULE_BOUNDARIES](MODULE_BOUNDARIES.md) · [DATA_CONTRACTS](DATA_CONTRACTS.md) · [TECH_DECISIONS](TECH_DECISIONS.md) · [STORY_ARCHITECTURE](../03_narrative/STORY_ARCHITECTURE.md)

> **Mọi đề xuất trong tài liệu này là `PROPOSED`.** Không có Unity project, code, scene hay package nào được tạo trong M0. Unity version, render pipeline, input system: `TBD` ([TECH_DECISIONS](TECH_DECISIONS.md)).

---

## 1. Nguyên tắc định hướng

1. **Đủ cho milestone hiện tại + một bước.** Không xây cho nhu cầu giả định (P4). Multiplayer ngoài phạm vi (D-0005) → không thiết kế network-ready.
2. **Dùng tính năng có sẵn của Unity trước** khi tự xây hoặc thêm thư viện.
3. **Dữ liệu tách khỏi logic** (P5); **logic tách khỏi presentation** khi mang lại khả năng test.
4. **Hướng phụ thuộc một chiều** giữa module ([MODULE_BOUNDARIES](MODULE_BOUNDARIES.md)).
5. **Mỗi pattern phải trả lời được "nó giải quyết vấn đề cụ thể nào của dự án này".**

## 2. Component-based design

**Đề xuất:** dùng MonoBehaviour như "lớp kết nối" (đọc input, animation, collider, hiển thị), còn quy tắc tính toán (sát thương, điều kiện quest, chuyển trạng thái) đặt trong class C# thuần khi logic đủ phức tạp để cần test.

| | Ưu | Nhược |
|---|---|---|
| MonoBehaviour thuần | Đơn giản, quen thuộc, nhanh cho prototype | Khó unit test, dễ phình to |
| MonoBehaviour + logic C# thuần (đề xuất) | Test EditMode được, rõ trách nhiệm | Thêm một lớp — chỉ áp dụng khi logic đủ phức tạp |
| ECS/DOTS | Hiệu năng rất cao với số lượng lớn | Quá phức tạp cho quy mô này; không đề xuất |

Quy tắc: component nhỏ, một trách nhiệm (ví dụ `Health`, `Hurtbox`, `MovementController`) thay vì một class "Player" khổng lồ.

## 3. Event-driven communication

**Đề xuất:** C# events/delegates cho giao tiếp trong cùng module; một **event channel nhẹ** cho sự kiện liên module (ví dụ `EnemyKilled` từ Combat tới Quest).

| Phương án | Ưu | Nhược |
|---|---|---|
| Gọi trực tiếp | Dễ đọc, dễ debug | Tạo phụ thuộc chặt giữa module |
| C# events | Type-safe, nhanh | Cần quản lý subscribe/unsubscribe |
| ScriptableObject event channels | Kết nối qua Inspector, tách module tốt | Khó truy vết luồng; nhiều asset |
| Global event bus (string/type-keyed) | Linh hoạt | Dễ lạm dụng, khó debug, lỗi runtime |

Đề xuất cụ thể (chốt ở M1-ENG-002): event liên module định nghĩa dưới dạng kiểu dữ liệu trong Core; số lượng event giữ ít và có danh sách trong tài liệu. **Không** dùng event cho mọi thứ — trong cùng module, gọi trực tiếp là bình thường.

## 4. State machines

**Đề xuất:** state machine viết tay, đơn giản (enum hoặc class state nhỏ) cho Player, Enemy AI, Game flow. Animator Controller chỉ dùng cho **hiển thị** animation, không chứa logic gameplay.

| | Ưu | Nhược |
|---|---|---|
| FSM viết tay (đề xuất) | Dễ test, dễ đọc, không phụ thuộc | Tự viết |
| Animator làm logic | Trực quan | Logic lẫn với animation, khó test, khó review qua text |
| Thư viện FSM / Behaviour Tree bên thứ ba | Tính năng sẵn | Phụ thuộc thêm (L1); chưa cần cho M2 |

Behaviour Tree chỉ xem xét nếu AI boss (M5) vượt quá khả năng FSM.

## 5. Scene Management

**Đề xuất:** một scene **Bootstrap** (khởi tạo services, cấu hình) + scene **Persistent** (player, camera, UI, các hệ thống sống suốt phiên) + các scene **Area** nạp/gỡ additive.

| Phương án | Ưu | Nhược |
|---|---|---|
| Một scene mỗi màn, load đơn | Đơn giản nhất | Mất trạng thái khi chuyển scene; dùng `DontDestroyOnLoad` tràn lan |
| Bootstrap + additive Areas (đề xuất) | Trạng thái liên tục, chuyển khu vực mượt, giảm bộ nhớ | Phức tạp hơn một chút; cần quy tắc rõ về object thuộc scene nào |
| Một scene lớn duy nhất | Không có loading | Không mở rộng được; bộ nhớ Android |

Ánh xạ Area ↔ scene phụ thuộc camera và quy mô thế giới — chốt sau OQ-002/OQ-024. Prototype M2 có thể dùng một scene đơn.

## 6. Data-driven content

**Đề xuất:**
- **Định nghĩa nội dung** (item, skill, enemy, quest…) — ScriptableObject: tích hợp Unity Inspector, tham chiếu asset trực tiếp, Codex tạo editor/validator.
- **Dữ liệu viết nhiều text** (dialogue) — theo quyết định OQ-020 (có thể là file text ngoài ScriptableObject).
- **Save data** — DTO thuần C# serialize ra JSON (§9), **không** serialize ScriptableObject hay MonoBehaviour.

| Định dạng | Hợp với | Hạn chế |
|---|---|---|
| ScriptableObject | Định nghĩa nội dung, cấu hình tuning | Binary-ish YAML khó đọc diff lớn; không dùng cho save |
| JSON/CSV | Bảng dữ liệu lớn, text, save data, sinh/kiểm tra bằng công cụ ngoài | Cần importer/validator |

Mọi định nghĩa có **ID chuỗi ổn định** (không dùng tên asset hoặc GUID làm ID gameplay) — xem [DATA_CONTRACTS](DATA_CONTRACTS.md).

## 7. Dependency management

**Đề xuất:** **composition root** trong Bootstrap tạo và nối các service chính; truyền tham chiếu qua Inspector hoặc khởi tạo thủ công. Hạn chế singleton: chấp nhận một số ít service toàn cục rõ ràng (ví dụ save service) được đăng ký tại Bootstrap.

| Phương án | Ưu | Nhược |
|---|---|---|
| Singleton tràn lan | Nhanh | Phụ thuộc ẩn, khó test, thứ tự khởi tạo mơ hồ |
| Composition root + tham chiếu tường minh (đề xuất) | Rõ ràng, test được, không thư viện | Viết tay phần nối |
| DI framework (ví dụ VContainer, Zenject/Extenject) | Mạnh, chuẩn | Thêm dependency (L1), đường cong học, có thể thừa cho quy mô này |

**Assembly Definitions — mức vừa phải (đề xuất):** không mỗi hệ thống một assembly. Đề xuất 5 runtime assembly + editor + test:

| Assembly | Chứa | Được tham chiếu |
|---|---|---|
| `Game.Core` | Kiểu dùng chung, ID, event types, interfaces (ví dụ save participant), utilities | — |
| `Game.Gameplay` | Character, Combat, Skills, AI, World, Inventory, Progression | Core |
| `Game.Narrative` | Narrative, Quests, Dialogue | Core, Gameplay |
| `Game.Persistence` | Save/load, schema, migration | Core |
| `Game.UI` | HUD, menu, touch controls | Core, Gameplay, Narrative |
| `Game.Audio` *(có thể gộp vào Gameplay ban đầu)* | Event-to-audio mapping | Core |
| `Game.Editor` | Tools, validators | Tất cả (Editor only) |
| `Game.Tests.EditMode` / `Game.Tests.PlayMode` | Test | Các assembly cần test |

Lý do: assembly giúp compile nhanh hơn và **cưỡng chế hướng phụ thuộc** (compiler báo lỗi nếu vi phạm) — hữu ích khi nhiều phiên AI cùng viết code. Có thể bắt đầu với ít hơn ở M2 và tách dần.

## 8. Cấu trúc Unity project dự kiến — `PROPOSED`

**Vị trí trong repository** ([OQ-010](../00_governance/OPEN_QUESTIONS.md)) — hai phương án:
- **A. Unity project trong thư mục con `unity/`** (khuyến nghị): tách tài liệu khỏi các thư mục Unity tự sinh (`Library/`, `Temp/`, `Logs/`, `UserSettings/`); CI hỗ trợ đường dẫn project tùy chỉnh.
- **B. Unity project ở gốc repository:** quen thuộc với công cụ mặc định; gốc repository lẫn tài liệu và thư mục Unity.

Cấu trúc bên trong (phương án A):

```
unity/
├── Assets/
│   ├── _Project/                 # mọi thứ của dự án — tách khỏi asset bên thứ ba
│   │   ├── Scripts/
│   │   │   ├── Runtime/
│   │   │   │   ├── Core/          # Game.Core
│   │   │   │   ├── Gameplay/      # Game.Gameplay
│   │   │   │   │   ├── Character/
│   │   │   │   │   ├── Combat/
│   │   │   │   │   ├── Skills/
│   │   │   │   │   ├── AI/
│   │   │   │   │   ├── World/
│   │   │   │   │   ├── Inventory/
│   │   │   │   │   └── Progression/
│   │   │   │   ├── Narrative/     # Game.Narrative
│   │   │   │   │   ├── Story/
│   │   │   │   │   ├── Quests/
│   │   │   │   │   └── Dialogue/
│   │   │   │   ├── Persistence/   # Game.Persistence
│   │   │   │   ├── UI/            # Game.UI
│   │   │   │   └── Audio/
│   │   │   ├── Editor/            # Game.Editor — tools, validators, debug
│   │   │   └── Tests/
│   │   │       ├── EditMode/
│   │   │       └── PlayMode/
│   │   ├── Content/               # Game Content — dữ liệu (ScriptableObject, JSON)
│   │   │   ├── Characters/ Enemies/ Skills/ Items/
│   │   │   ├── Quests/ Dialogue/ Story/
│   │   │   └── Localization/
│   │   ├── Art/                   # Art Assets — chỉ asset đã VALIDATED
│   │   │   ├── Characters/ Enemies/ Environments/
│   │   │   ├── UI/ VFX/
│   │   │   └── _Placeholder/
│   │   ├── Audio/                 # Music/ SFX/ _Placeholder/
│   │   ├── Prefabs/
│   │   ├── Scenes/                # Bootstrap/ Persistent/ Areas/ _Test/
│   │   └── Settings/              # input actions, render pipeline assets, quality
│   └── ThirdParty/                # asset/plugin bên thứ ba đã được duyệt (nếu có)
├── Packages/
└── ProjectSettings/
art_source/                        # (ngoài Unity) file nguồn art, concept — quản lý bằng LFS
```

Thư mục chỉ được tạo khi có nội dung (D-0011). Chưa tạo gì trong M0.

## 9. Save/load

**Đề xuất:**
- Mỗi hệ thống có trạng thái bền vững triển khai một interface "save participant" (định nghĩa trong Core): xuất/nhập DTO của riêng nó.
- `Persistence` gom DTO thành một save file JSON có `schemaVersion`, ghi vào `Application.persistentDataPath`, ghi nguyên tử (file tạm → đổi tên).
- Android: lưu khi app chuyển nền (`OnApplicationPause`) theo chế độ lưu được duyệt (OQ-019).
- Không serialize object Unity; chỉ ID và giá trị.
- Yêu cầu narrative cụ thể: [STORY_ARCHITECTURE §6](../03_narrative/STORY_ARCHITECTURE.md#6-save-load-requirements).

| Định dạng | Ưu | Nhược |
|---|---|---|
| JSON (đề xuất) | Đọc được, debug dễ, migration dễ | Lớn hơn binary; người chơi PC có thể sửa (chấp nhận được cho single-player) |
| Binary | Nhỏ, khó sửa | Khó debug, khó migration |
| PlayerPrefs | Đơn giản | Không phù hợp dữ liệu lớn/có cấu trúc |

Thư viện JSON cụ thể (JsonUtility tích hợp sẵn vs thư viện khác) chốt ở [TECH_DECISIONS TD-08](TECH_DECISIONS.md#td-08--save-format-và-thư-viện-json).

## 10. Testability

| Loại | Công cụ (đề xuất) | Đối tượng |
|---|---|---|
| Unit (EditMode) | Unity Test Framework | Logic C# thuần: damage, state transition, condition evaluator, save serialization |
| Integration (PlayMode) | Unity Test Framework | Hệ thống phối hợp trong scene test: quest hoàn thành khi enemy chết |
| Data validation | Editor validator | ID trùng/thiếu, tham chiếu hỏng, quest không hoàn thành được |
| Manual / playtest | Kịch bản + checklist | Cảm giác điều khiển, visual |

Thiết kế cho test: tránh `static` state ẩn; inject phụ thuộc (thời gian, random) để test xác định được.

## 11. PC/Android compatibility

| Khía cạnh | Đề xuất |
|---|---|
| Input | Lớp abstraction "action" (Move, Attack, Interact…) — gameplay không đọc phím/chạm trực tiếp ([TD-03](TECH_DECISIONS.md#td-03--input-handling)) |
| UI | Canvas Scaler theo reference resolution; tôn trọng safe area; vùng chạm đủ lớn; touch controls là một UI layer riêng bật theo nền tảng |
| Hiệu năng | Sprite atlas; hạn chế overdraw và ánh sáng 2D trên Android; object pooling cho projectile/VFX khi cần (đo trước khi tối ưu) |
| Build Android | IL2CPP + ARM64 (yêu cầu 64-bit của Google Play); cấu hình chi tiết ở [TD-09](TECH_DECISIONS.md#td-09--cấu-hình-build-android) |
| Vòng đời app | Xử lý pause/resume, mất focus, xoay màn hình (orientation `TBD`) |
| Code đặc thù nền tảng | Gom vào một chỗ; tránh `#if UNITY_ANDROID` rải rác trong gameplay |

## 12. Những gì cố ý KHÔNG làm (ở giai đoạn này)

- Không ECS/DOTS; không DI framework; không thư viện FSM/BT; không Addressables (xem xét lại khi nội dung lớn — M5+).
- Không network layer hay kiến trúc "sẵn sàng multiplayer".
- Không mỗi hệ thống một package/assembly/service.
- Không plugin modding, không hệ thống scripting riêng.

## 13. Quyết định cần GD phê duyệt

Tóm tắt: [TECH_DECISIONS](TECH_DECISIONS.md). Kiến trúc trong tài liệu này sẽ được trình như một Decision Record L1 trong M1 (M1-ENG-002), sau khi có camera và Combat Direction.
