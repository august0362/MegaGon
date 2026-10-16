# Character Register

> **Document Owner:** Claude (cấu trúc, continuity) · **Content Owner:** Game Director · **Status:** `ACTIVE` (sổ đăng ký) · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [WORLD_BIBLE](WORLD_BIBLE.md) · [ART_BRIEF_TEMPLATE](../04_art/ART_BRIEF_TEMPLATE.md) · [ASSET_MANIFEST](../04_art/ASSET_MANIFEST.md)

Sổ đăng ký mọi nhân vật có tên (người chơi, NPC, kẻ địch có tên, boss). **Hiện chưa có nhân vật nào được phê duyệt.** Hệ thống nhân vật chơi được (một nhân vật / lớp / party) là `TBD` ([OQ-016](../00_governance/OPEN_QUESTIONS.md)).

---

## 1. Quy ước ID

`CHR_<VAI_TRÒ>_<TÊN_NGẮN>` — tiếng Anh, chữ hoa, không dấu.
Vai trò: `PC` (nhân vật người chơi), `NPC`, `ENM` (kẻ địch có tên), `BOSS`.
ID ổn định: không đổi khi đổi tên hiển thị (tên hiển thị nằm trong bảng text).

## 2. Bảng đăng ký

| ID | Tên hiển thị | Vai trò | Phe | Xuất hiện (chương/area) | Profile | Art status | Canon status |
|---|---|---|---|---|---|---|---|
| — | — | — | — | — | — | — | Chưa có nhân vật |

## 3. Mẫu Character Profile

```markdown
### CHR_<…> — <Tên hiển thị>
- Canon status: PROPOSED / APPROVED (Decision: D-NNNN)
- Vai trò trong câu chuyện:
- Phe (FAC_…):
- Mục tiêu / động lực:
- Tính cách (3–5 nét):
- Giọng nói / cách nói chuyện (cho dialogue):
- Quan hệ với nhân vật khác:
- Arc (thay đổi qua câu chuyện):
- Ghi chú hình ảnh cho Art Brief (không phải thiết kế cuối):
- Yêu cầu gameplay (nếu là kẻ địch/boss, liên kết COMBAT_DESIGN):
- Originality check: không dựa trực tiếp vào nhân vật có bản quyền — Claude xác nhận ngày …
```

## 4. Quy tắc

- Một nhân vật chỉ chuyển `APPROVED` khi GD duyệt profile.
- Art Brief cho nhân vật chỉ được tạo sau khi profile ít nhất ở trạng thái `PROPOSED` và được GD cho phép khám phá hình ảnh.
- Nhân vật dùng trong test runtime dùng ID dạng `CHR_TEST_…` và nhãn `EXAMPLE — NOT APPROVED`.
