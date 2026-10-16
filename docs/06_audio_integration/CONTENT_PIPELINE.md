# Content Pipeline

> **Document Owner:** Claude · **Executor:** Codex · **Status:** `UNDER_REVIEW` — `PROPOSED` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ASSET_SPEC](../04_art/ASSET_SPEC.md) · [ASSET_MANIFEST](../04_art/ASSET_MANIFEST.md) · [AUDIO_PLAN](AUDIO_PLAN.md) · [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md) · [UNITY_ARCHITECTURE_PROPOSAL §8](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md#8-cấu-trúc-unity-project-dự-kiến--proposed)

Đường đi của mọi content (art, audio, dữ liệu) từ lúc bàn giao tới lúc có trong build. Áp dụng khi Unity project tồn tại (M2+).

---

## 1. Luồng tổng quát

```
Bàn giao (Antigravity / nguồn audio / tác giả dữ liệu)
   │  handoff report + mục manifest
   ▼
Staging (ngoài Unity Assets — ví dụ art_source/ hoặc thư mục bàn giao)
   │  Technical Validation (checklist ASSET_SPEC §10 / AUDIO_PLAN §4 / validator dữ liệu)
   ▼
Import vào Unity (Codex) — đúng thư mục, đúng import settings
   │  Validator trong Editor
   ▼
Integration (prefab, dữ liệu, mapping)
   │  Test + Visual/Audio review
   ▼
In build  →  cập nhật manifest: INTEGRATED → ACCEPTED
```

## 2. Quy tắc import

| Loại | Thư mục Unity (đề xuất) | Import settings chính |
|---|---|---|
| Sprite nhân vật/kẻ địch | `_Project/Art/Characters`, `/Enemies` | Sprite mode, PPU theo ASSET_SPEC, pivot, filter (Point nếu pixel art), compression theo nền tảng |
| Tile | `_Project/Art/Environments` | Như trên, khớp grid |
| UI | `_Project/Art/UI` | Theo UI spec |
| Audio | `_Project/Audio/SFX`, `/Music` | Load type theo AUDIO_PLAN §4 |
| Dữ liệu | `_Project/Content/...` | Theo data contract |
| Placeholder | `.../_Placeholder` | Đánh dấu rõ để dễ tìm và thay |

Import settings nên được áp dụng tự động (preset hoặc asset postprocessor do Codex viết) thay vì chỉnh tay từng file — giảm lỗi khi nhiều phiên làm việc.

## 3. Validation tự động — `PROPOSED`

| Validator | Kiểm tra |
|---|---|
| Asset naming | Tên file đúng ASSET_SPEC §6 |
| Sprite | PPU, pivot, kích thước khung đồng nhất trong animation |
| Data references | ID tồn tại, không trùng; asset được tham chiếu tồn tại |
| Narrative | Quest hoàn thành được, dialogue node tới được, key localization tồn tại |
| Manifest | Mọi asset trong `_Project/Art` và `_Project/Audio` có mục trong manifest |

Validator chạy được từ menu Editor và từ batchmode (để dùng trong CI về sau).

## 4. Tổ chức tài nguyên và hiệu năng

- Sprite atlas theo nhóm hiển thị cùng nhau (ví dụ theo Area) — chiến lược cụ thể chốt khi có Art Direction.
- Không đưa concept, moodboard, file nguồn vào `Assets/` (tránh tăng kích thước project và build).
- Theo dõi kích thước build Android từ M2 (ghi trong báo cáo build).

## 5. Trách nhiệm

| Bước | Người thực hiện | Người kiểm tra |
|---|---|---|
| Bàn giao + manifest | Antigravity / nguồn audio | Claude |
| Technical validation | Codex (tự động) + Claude | Claude |
| Import + integration | Codex | Claude (review), Antigravity (visual review) |
| Nghiệm thu | GD (asset quan trọng) | — |
