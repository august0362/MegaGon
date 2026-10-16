# Department 04 — Art & Visual Production

> **Document Owner:** Claude (charter) · **Primary Executor:** Antigravity · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ART_DIRECTION_EXPLORATION](ART_DIRECTION_EXPLORATION.md) · [ART_BRIEF_TEMPLATE](ART_BRIEF_TEMPLATE.md) · [ASSET_SPEC](ASSET_SPEC.md) · [ASSET_MANIFEST](ASSET_MANIFEST.md) · [agents/ANTIGRAVITY.md](../../agents/ANTIGRAVITY.md)

## 1. Mission

Tạo ra bản sắc hình ảnh nguyên bản, nhất quán và đạt chuẩn kỹ thuật, qua một quy trình có phác thảo, review và phê duyệt.

## 2. Scope

**Trong phạm vi:** khám phá Art Direction, tham khảo hình ảnh, sketch, concept, character/environment design, sprite và animation, VFX, UI Art, asset spec, asset manifest, chuẩn đặt tên và xuất file.
**Ngoài phạm vi:** quyết định Art Direction (GD), tích hợp vào Unity và shader/code (Codex), nội dung câu chuyện (03).

## 3. Roles

| Vai trò | Đảm nhận | Trọng tâm |
|---|---|---|
| Art Director | **GD** quyết định · Antigravity đề xuất · Claude tổng hợp so sánh | Định hướng phong cách, giữ nhất quán |
| Concept Artist | Antigravity | Sketch, concept variants |
| Character Artist | Antigravity | Nhân vật, quái, boss |
| Environment Artist | Antigravity | Tileset, background, prop |
| 2D Animator | Antigravity (năng lực **chưa xác minh**) | Animation sprite |
| VFX Artist | Antigravity (sprite VFX) · Codex (particle/shader trong Unity) | Hiệu ứng |
| UI Artist | Antigravity | Giao diện, icon |
| Technical Artist | Claude (spec) · Codex (import, validation) | Pivot, PPU, atlas, import settings |

## 4. Responsibilities

- Thực hiện quy trình khám phá Art Direction ([ART_DIRECTION_EXPLORATION](ART_DIRECTION_EXPLORATION.md)).
- Sản xuất asset theo Art Brief và ASSET_SPEC.
- Kiểm tra nhất quán và kỹ thuật trước khi bàn giao.
- Ghi provenance mọi asset vào ASSET_MANIFEST.
- Visual review sau khi tích hợp.

## 5. Deliverables

Moodboard, rough sketches, concept variants, style guide (sau khi Art Direction duyệt), character design sheets, environment concepts, sprite/sprite sheet, animation, VFX sprites, UI art, mục ASSET_MANIFEST, Art Review Records.

## 6. Input Requirements

Art Brief; Game Vision và tông giọng (OQ-001, OQ-012); góc nhìn camera (OQ-002 — quyết định số hướng sprite); character profile (03); yêu cầu animation từ combat (02); ràng buộc kỹ thuật (ASSET_SPEC, render pipeline).

## 7. Output Contracts

Asset bàn giao phải tuân thủ [ASSET_SPEC](ASSET_SPEC.md): kích thước, PPU, pivot, đặt tên, định dạng, frame. Mỗi lô bàn giao có handoff report ([ANTIGRAVITY §11](../../agents/ANTIGRAVITY.md#11-reporting-format)) và mục manifest.

## 8. Dependencies

- Phụ thuộc: GD (Art Direction, concept), 02 (camera, combat animation), 03 (profile nhân vật, thế giới), 05 (render pipeline, import).
- Bị phụ thuộc: 05/06 (tích hợp), 07 (Visual QA), M4, M5.

## 9. Workflows

Quy trình bắt buộc cho asset quan trọng:

```
Art Brief → Sketch → Review → Concept Approval → Final Asset → Technical Validation → Integration → Visual Acceptance
   (Claude)   (AG)   (GD+CL)      (GD)             (AG)          (CL+CX)             (CX)        (AG review, GD accept)
```

| Bước | Thực hiện | Đầu ra | Cổng |
|---|---|---|---|
| Art Brief | Claude | AB-NNN | Brief đủ thông tin |
| Sketch | Antigravity | Rough sketches `PROPOSED` | Nộp ≥2 hướng khi brief yêu cầu khám phá |
| Review | GD (Claude chuẩn bị Art Review) | AR-NNN | Chọn hướng / yêu cầu sửa |
| Concept Approval | GD | Concept `APPROVED` | Bắt buộc với asset quan trọng |
| Final Asset | Antigravity | File theo ASSET_SPEC | — |
| Technical Validation | Claude + Codex | Checklist ASSET_SPEC §10 | Đạt toàn bộ mục bắt buộc |
| Integration | Codex | Asset trong Unity | Hiển thị đúng PC + Android |
| Visual Acceptance | Antigravity review, GD nghiệm thu (asset quan trọng) | ACC/AR record | Đạt |

**Asset quan trọng** = nhân vật người chơi, NPC chính, boss, kẻ địch chủ lực, môi trường đặc trưng của Region, UI chính, logo. **Asset phụ** (prop, biến thể tile, icon phụ) theo style guide đã duyệt có thể bỏ bước Concept Approval riêng, nhưng vẫn qua Technical Validation và nghiệm thu theo lô.

**Không sản xuất hàng loạt** trước khi Art Direction và concept mẫu được duyệt.

## 10. Quality Gates

- Không final asset nào khi concept (với asset quan trọng) chưa `APPROVED`.
- Không asset nào vào Unity khi chưa qua Technical Validation.
- Không asset nào thiếu provenance trong manifest.
- Không chấp nhận ảnh AI thô làm final asset mà không kiểm tra kỹ thuật và originality.

## 11. Approval Authority

GD: Art Direction (L2), concept asset quan trọng (L1), visual acceptance asset quan trọng. Claude: technical validation, nghiệm thu kỹ thuật asset phụ (L0) — GD nghiệm thu lô tại milestone.

## 12. Assigned Agents

Primary Executor: **Antigravity**. Brief & validation: **Claude**. Tích hợp: **Codex**. Phê duyệt: **Game Director**. Phản biện thẩm mỹ: ChatGPT, Gemini.

## 13. Documentation Ownership

Claude duy trì ART_DIRECTION_EXPLORATION, ART_BRIEF_TEMPLATE, ASSET_SPEC. Antigravity cập nhật ASSET_MANIFEST khi bàn giao; Claude xác minh. Art Brief/Review lưu tại `docs/04_art/briefs/`, `docs/04_art/reviews/`.

## 14. Escalation Rules

- Công cụ không đạt yêu cầu kỹ thuật → Antigravity báo Claude → điều chỉnh quy trình/công cụ hoặc CR cho ASSET_SPEC.
- Nghi ngờ vấn đề bản quyền → dừng asset đó, báo Claude → GD.
- Style drift (lệch phong cách) giữa các lô → Claude mở Art Review, GD quyết định.
