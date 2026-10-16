# Department 06 — Audio & Content Integration

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [AUDIO_PLAN](AUDIO_PLAN.md) · [CONTENT_PIPELINE](CONTENT_PIPELINE.md) · [ASSET_MANIFEST](../04_art/ASSET_MANIFEST.md)

> **Chưa có agent sản xuất âm thanh chuyên trách.** Vai trò sản xuất audio là `UNASSIGNED`. Không agent nào (kể cả Codex hay Antigravity) được coi là có khả năng tạo toàn bộ âm thanh/nhạc chuyên nghiệp.

## 1. Mission

Đảm bảo mọi nội dung (art, audio, dữ liệu) đi vào game theo một pipeline rõ ràng, được kiểm tra, và âm thanh phục vụ đúng trải nghiệm khi nguồn audio được xác định.

## 2. Scope

**Trong phạm vi:** yêu cầu audio, yêu cầu SFX, yêu cầu nhạc, quy tắc import content, tích hợp asset, ánh xạ event → audio, kiểm tra content, tổ chức tài nguyên.
**Ngoài phạm vi:** sản xuất visual asset (04), quyết định nguồn/ngân sách audio (GD).

## 3. Roles

| Vai trò | Đảm nhận | Ghi chú |
|---|---|---|
| Audio Director | `UNASSIGNED` | GD quyết định định hướng âm thanh khi cần; Claude soạn yêu cầu |
| Sound Designer | `UNASSIGNED` | Chờ [OQ-026](../00_governance/OPEN_QUESTIONS.md) |
| Music Composer | `UNASSIGNED` | Chờ OQ-026 |
| Content Integrator | Codex | Import và gắn asset vào game |
| Asset Pipeline Engineer | Codex (Claude đặc tả) | Import settings, validator, cấu trúc thư mục |
| Content Validator | Codex (tự động) · Claude (review) | Kiểm tra dữ liệu, asset, tham chiếu |

## 4. Responsibilities

- Soạn danh sách yêu cầu audio theo hệ thống và sự kiện (Claude).
- Duy trì [CONTENT_PIPELINE](CONTENT_PIPELINE.md) — đường đi của mọi content từ bàn giao tới build.
- Tích hợp và kiểm tra content (Codex).
- Theo dõi license và provenance của audio (Claude), giống ASSET_MANIFEST cho hình ảnh.

## 5. Deliverables

AUDIO_PLAN, CONTENT_PIPELINE, audio event mapping (DC-AUDIO-EVENTS), audio manifest (khi có audio), content validators, báo cáo tích hợp.

## 6. Input Requirements

Quyết định nguồn audio (OQ-026); hệ thống gameplay và event (02, 05); tông giọng (OQ-012); asset đã VALIDATED (04).

## 7. Output Contracts

- Audio bàn giao theo thông số trong [AUDIO_PLAN §4](AUDIO_PLAN.md#4-thông-số-kỹ-thuật--proposed).
- Content chỉ vào `Assets/_Project/` sau khi qua validation ([CONTENT_PIPELINE](CONTENT_PIPELINE.md)).

## 8. Dependencies

- Phụ thuộc: GD (nguồn audio, ngân sách), 02/05 (event), 04 (asset), 03 (ngữ cảnh cảm xúc).
- Bị phụ thuộc: M5 (audio tối thiểu), M7 (basic audio), 07 (content validation).

## 9. Workflows

- **Audio:** Claude soạn yêu cầu (AUDIO_PLAN) → GD chọn nguồn (OQ-026) → nguồn audio sản xuất/cung cấp → kiểm tra license + kỹ thuật → Codex tích hợp theo event mapping → GD nghe thử, nghiệm thu.
- **Content:** theo [CONTENT_PIPELINE](CONTENT_PIPELINE.md).

## 10. Quality Gates

- Không audio nào vào build khi chưa rõ license.
- Không content nào vào build khi chưa qua validation.
- Mọi event quan trọng của gameplay có âm thanh phản hồi trong Vertical Slice (danh sách cụ thể do 02 + Claude chốt).

## 11. Approval Authority

GD: nguồn audio, định hướng âm thanh, nghiệm thu audio. Claude: pipeline và quy tắc import (L0), trừ khi cần dependency mới (L1).

## 12. Assigned Agents

Tích hợp/validation: **Codex**. Yêu cầu, pipeline, license tracking: **Claude**. Sản xuất audio: `UNASSIGNED`.

## 13. Documentation Ownership

Claude: AUDIO_PLAN, CONTENT_PIPELINE. Codex: cập nhật trạng thái tích hợp.

## 14. Escalation Rules

- Chưa có nguồn audio khi M5 bắt đầu → Claude báo GD (R-009).
- Audio/asset có license không rõ → dừng tích hợp, báo GD.
- Pipeline gây lỗi tích hợp lặp lại → Claude điều chỉnh pipeline (L0) hoặc đề xuất công cụ (L1).
