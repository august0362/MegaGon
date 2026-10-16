# Department 03 — Narrative & Worldbuilding

> **Document Owner:** Claude (đặc tả, continuity) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [WORLD_BIBLE](WORLD_BIBLE.md) · [STORY_ARCHITECTURE](STORY_ARCHITECTURE.md) · [CHARACTER_REGISTER](CHARACTER_REGISTER.md) · [QUEST_DIALOGUE_DESIGN](QUEST_DIALOGUE_DESIGN.md)

## 1. Mission

Xây dựng một thế giới và câu chuyện nguyên bản, nhất quán, và một hệ thống runtime cho phép câu chuyện đó được chơi, lưu và mở rộng bằng dữ liệu.

## 2. Scope

Bộ phận này có **hai mảng tách biệt**:

| Mảng | Gồm | Người sở hữu sáng tạo | Người thực thi |
|---|---|---|---|
| **Narrative Content** — nội dung câu chuyện | World bible, timeline, phe phái, nhân vật, cốt truyện chính, chương, side quest, hội thoại, cutscene | **Game Director** | Bản nháp: GD / ChatGPT / Gemini / Claude (khi GD yêu cầu) — luôn `PROPOSED` tới khi GD duyệt |
| **Narrative Runtime** — hệ thống chạy câu chuyện | Story state, quest engine, dialogue engine, narrative events, cutscene triggers, save/load narrative | Claude (đặc tả) — GD duyệt kiến trúc | **Codex** |

**Ngoài phạm vi:** cơ chế gameplay (02), hình ảnh (04), audio (06).

## 3. Roles

| Vai trò | Mảng | Đảm nhận hiện tại |
|---|---|---|
| Worldbuilder | Content | GD (quyết định) · advisor/Claude (bản nháp) |
| Lore Designer | Content | GD · advisor/Claude (bản nháp) |
| Story Writer | Content | Không có agent chuyên trách — xem [AGENT_ROLES §4.1](../00_governance/AGENT_ROLES.md#41-vai-trò-chưa-có-agent-chuyên-trách) |
| Character Writer | Content | Như trên |
| Narrative Designer | Cả hai | Claude — cấu trúc chương, quest, progression |
| Quest Designer | Cả hai | Claude — cấu trúc quest; nội dung quest do GD duyệt |
| Dialogue Writer | Content | Không có agent chuyên trách |
| Cutscene Designer | Cả hai | Claude (đặc tả trigger, cấu trúc) |
| Continuity Editor | Content | **Claude** — kiểm tra nhất quán canon |

## 4. Responsibilities

- Duy trì cấu trúc World Bible và Character Register; ghi canon chỉ khi GD đã duyệt.
- Đặc tả kiến trúc narrative runtime ([STORY_ARCHITECTURE](STORY_ARCHITECTURE.md)).
- Thiết kế cấu trúc quest/dialogue và định dạng dữ liệu ([QUEST_DIALOGUE_DESIGN](QUEST_DIALOGUE_DESIGN.md)).
- Kiểm tra tính nhất quán narrative (continuity review) trước khi nội dung được nhập vào game.
- Phối hợp với 02 (quest gắn gameplay) và 04 (thiết kế nhân vật dựa trên profile).

## 5. Deliverables

World Bible, Story Architecture, Character Register, Quest & Dialogue Design, nội dung chương/quest/dialogue (khi được duyệt), narrative data files, narrative test scenarios.

## 6. Input Requirements

Game Vision (OQ-001), bối cảnh và tông giọng (OQ-012), cấu trúc cốt truyện (OQ-013), quyết định localization (OQ-021), authoring format (OQ-020).

## 7. Output Contracts

- Nội dung canon: chỉ ghi vào tài liệu với nhãn `APPROVED` + Decision ID hoặc Acceptance Record.
- Dữ liệu narrative cho Codex: theo data contract `APPROVED` trong [DATA_CONTRACTS](../05_engineering/DATA_CONTRACTS.md); mọi ID ổn định (không đổi sau khi phát hành save data).
- Text hiển thị cho người chơi: qua bảng key–text (chuẩn bị cho localization), không viết thẳng vào code.

## 8. Dependencies

- Phụ thuộc: GD (canon), 02 (cơ chế quest, phần thưởng), 05 (runtime), 04 (hình ảnh nhân vật).
- Bị phụ thuộc: 02 Level Design, 04 Character Art, 06 Audio (ngữ cảnh cảm xúc), 07 Narrative QA.

## 9. Workflows

**Content:** OQ → workshop/bản nháp (`PROPOSED`) → continuity review (Claude) → GD duyệt → ghi canon → chuyển thành dữ liệu.
**Runtime:** Decision → spec runtime (Claude) → task (Codex) → test với dữ liệu mẫu `EXAMPLE — NOT APPROVED` → tích hợp nội dung canon.

Hai luồng chạy độc lập: runtime có thể được xây và kiểm thử (M3) trước khi có cốt truyện canon.

## 10. Quality Gates

- Không nội dung nào vào canon khi chưa có phê duyệt của GD.
- Nội dung mẫu trong test luôn có nhãn `EXAMPLE — NOT APPROVED` và không được tái sử dụng làm canon nếu chưa duyệt.
- Continuity review không còn mâu thuẫn trước khi nhập dữ liệu.
- Narrative progression test pass (mọi quest hoàn thành được, không kẹt trạng thái).

## 11. Approval Authority

Game Director: thế giới, tông giọng (L2); cốt truyện chính, nhân vật chính (L1); nội dung phụ (L1, duyệt theo lô). Claude: cấu trúc tài liệu và định dạng nội bộ (L0). Kiến trúc runtime: GD (L1).

## 12. Assigned Agents

Content: **Game Director** (chủ sở hữu) · ChatGPT/Gemini/Claude (bản nháp khi được yêu cầu). Runtime: **Claude** (đặc tả) · **Codex** (triển khai).

## 13. Documentation Ownership

Claude duy trì toàn bộ `docs/03_narrative/`. Nội dung canon trong đó thuộc quyền quyết định của GD.

## 14. Escalation Rules

- Mâu thuẫn canon → Claude báo GD kèm vị trí mâu thuẫn và phương án.
- Yêu cầu narrative cần cơ chế gameplay mới → chuyển 02, quyết định L1.
- Runtime không hỗ trợ một yêu cầu nội dung → Codex báo Claude → spec update hoặc CR.
