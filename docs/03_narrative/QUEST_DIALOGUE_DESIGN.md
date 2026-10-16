# Quest & Dialogue Design

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` — mô hình `PROPOSED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [STORY_ARCHITECTURE](STORY_ARCHITECTURE.md) · [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md) · [SYSTEMS_OVERVIEW](../02_game_design/SYSTEMS_OVERVIEW.md)

Mô hình dữ liệu và quy tắc thiết kế cho quest và dialogue. Nội dung quest/dialogue cụ thể chưa có.

---

## 1. Mô hình Quest — `PROPOSED`

```
Quest (QST_…)
 ├─ type: Main | Side | (khác: TBD)
 ├─ availability: Condition[]        — khi nào quest có thể nhận
 ├─ start: cách bắt đầu (từ dialogue effect, story event, tự động)
 ├─ objectives: Objective[]          — tuần tự hoặc song song (TBD có hỗ trợ cả hai không)
 │    └─ Objective: type, target ID, required count, optional?
 ├─ rewards: Effect[]                — phần thưởng (tùy thuộc hệ thống progression TBD)
 └─ onComplete: Effect[]             — cập nhật Story/World State
```

**Trạng thái quest:** `Unavailable → Available → Active → Completed` (+ `Failed` nếu thiết kế cho phép — `TBD`).

**Loại objective khởi đầu cho M3** (`PROPOSED`, tập nhỏ): `TalkTo(NPC)`, `Reach(Location)`, `Defeat(Enemy, count)`, `Collect(Item, count)`. Mở rộng khi nội dung yêu cầu.

## 2. Mô hình Dialogue — `PROPOSED`

```
Dialogue (DLG_…)
 └─ Node (id)
     ├─ speaker: CHR_… 
     ├─ textKey: key trong bảng text (không chứa text trực tiếp)
     ├─ conditions: Condition[]      — node có hiển thị không
     ├─ effects: Effect[]            — khi node được hiển thị
     └─ next: Node | Choice[]
          └─ Choice: textKey, conditions, effects, next
```

Có hỗ trợ lựa chọn phân nhánh hay chỉ hội thoại tuyến tính là quyết định thiết kế `TBD` (phụ thuộc Vision). Mô hình trên hỗ trợ cả hai.

## 3. Quy tắc thiết kế

- Quest và dialogue là **dữ liệu**, không phải code (P5).
- Mọi tham chiếu dùng ID ổn định (`QST_`, `DLG_`, `CHR_`, `ITM_`, `AREA_`…).
- Không có quest nào có thể rơi vào trạng thái không hoàn thành được (kiểm tra tĩnh + test).
- Text hiển thị qua key để chuẩn bị localization.
- Độ dài dòng thoại phải vừa hộp thoại ở màn hình Android nhỏ nhất được hỗ trợ (giới hạn ký tự `TBD` sau khi có UI).

## 4. Quy trình sản xuất nội dung

1. Claude (hoặc GD) viết **outline** quest: mục đích, liên kết story beat, objectives, phần thưởng — `PROPOSED`.
2. GD duyệt outline (theo lô với quest phụ).
3. Viết dialogue (`PROPOSED`) → continuity review (Claude) → GD duyệt.
4. Nhập dữ liệu theo authoring format đã chọn (Codex hoặc công cụ authoring).
5. Narrative QA: chơi hết quest, kiểm tra điều kiện, save/load giữa chừng.

## 5. Authoring Format — `TBD`

[OQ-020](../00_governance/OPEN_QUESTIONS.md). Các phương án:

| Phương án | Ưu | Nhược |
|---|---|---|
| **ScriptableObject tự xây** | Tích hợp Unity sâu, không phụ thuộc bên thứ ba, kiểm soát hoàn toàn | Phải tự xây editor; viết hội thoại dài trong Inspector bất tiện |
| **JSON/YAML/CSV tự định nghĩa** | Dễ viết ngoài Unity, dễ diff, dễ để AI sinh bản nháp và kiểm tra | Phải tự viết importer và validator |
| **Thư viện narrative (ví dụ Ink, Yarn Spinner)** | Ngôn ngữ viết hội thoại chuyên dụng, công cụ có sẵn | Phụ thuộc bên thứ ba (L1), phải tích hợp với State/Condition của dự án, cần đánh giá license và hỗ trợ Unity version |

Khuyến nghị sơ bộ của Claude: đánh giá trong M1–M2 dựa trên lượng hội thoại dự kiến (OQ-024) và việc có phân nhánh hay không. Chưa khuyến nghị cụ thể khi chưa có Vision.

## 6. Localization

- Ngôn ngữ trong game: `TBD` ([OQ-021](../00_governance/OPEN_QUESTIONS.md)). Tài liệu dự án bằng tiếng Việt (D-0007) không đồng nghĩa game chỉ có tiếng Việt.
- Bất kể quyết định, text đi qua bảng key–text từ đầu (chi phí thấp, tránh phải làm lại).
- Font phải hỗ trợ đầy đủ dấu tiếng Việt — kiểm tra trên cả PC và Android.
