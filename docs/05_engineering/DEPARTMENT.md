# Department 05 — Game Engineering

> **Document Owner:** Claude (đặc tả kiến trúc) · **Primary Executor:** Codex · **Approver:** Game Director (kiến trúc lớn) · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [UNITY_ARCHITECTURE_PROPOSAL](UNITY_ARCHITECTURE_PROPOSAL.md) · [MODULE_BOUNDARIES](MODULE_BOUNDARIES.md) · [DATA_CONTRACTS](DATA_CONTRACTS.md) · [TECH_DECISIONS](TECH_DECISIONS.md) · [agents/CODEX.md](../../agents/CODEX.md)

## 1. Mission

Xây dựng nền tảng kỹ thuật Unity đủ vững để mở rộng, đủ đơn giản để một đội AI-assisted duy trì được, và chạy tốt trên cả PC lẫn Android.

## 2. Scope

**Trong phạm vi:** kiến trúc Unity project, scene management, input, character movement, physics/collision, combat, skills, enemy AI, world management, narrative runtime, quest runtime, inventory, equipment, progression, save/load, UI implementation, tooling, hỗ trợ automated testing.
**Ngoài phạm vi:** quyết định thiết kế gameplay (02), nội dung narrative (03), sản xuất art (04), sản xuất audio (06).

## 3. Roles

Mọi vai trò lập trình do **Codex** thực hiện; Claude giữ vai trò đặc tả và review.

| Vai trò | Trách nhiệm chính | Module |
|---|---|---|
| Technical Architect | Claude đề xuất kiến trúc · GD duyệt · Codex phản biện khả thi | Toàn bộ |
| Core Programmer | Bootstrap, services, events, game state | Core |
| Character Programmer | Điều khiển, di chuyển | Character |
| Combat Programmer | Hit/hurt, damage, combat states | Combat, Skills |
| AI Programmer | Hành vi kẻ địch | AI |
| World Programmer | Area/scene loading, interactables, spawners | World |
| Narrative Programmer | Story/Quest/Dialogue runtime | Narrative |
| Systems Programmer | Inventory, equipment, progression | Inventory, Progression |
| UI Programmer | HUD, menu, điều khiển cảm ứng | UI |
| Tools Programmer | Editor tools, validators, debug tools | Editor |
| Persistence Programmer | Save/load, schema, migration | Persistence |

## 4. Responsibilities

- Triển khai theo spec và contract `APPROVED`.
- Giữ ranh giới module theo [MODULE_BOUNDARIES](MODULE_BOUNDARIES.md).
- Viết và chạy test; cung cấp bằng chứng.
- Tạo tool hỗ trợ content (validator, debug narrative).
- Báo cáo technical debt và rủi ro hiệu năng (đặc biệt Android).

## 5. Deliverables

Unity project (từ M2), mã nguồn theo module, test suites, editor tools, build PC/Android, tài liệu kỹ thuật module, handoff reports.

## 6. Input Requirements

Tech decisions `APPROVED` (OQ-006 → OQ-010), Feature Specs, data contracts, asset theo ASSET_SPEC, task records đạt DoR.

## 7. Output Contracts

- Code tuân thủ hướng phụ thuộc và quy ước trong MODULE_BOUNDARIES.
- Mọi dữ liệu cấu hình có validator (khi contract yêu cầu).
- Mọi thay đổi có test hoặc lý do không test được ghi trong report.
- Build kèm log.

## 8. Dependencies

- Phụ thuộc: 02 (spec gameplay), 03 (spec runtime, dữ liệu), 04/06 (asset), GD (quyết định công nghệ).
- Bị phụ thuộc: 07 (build, test), 04 (integration feedback), 06 (pipeline).

## 9. Workflows

1. Tech OQ → Claude phân tích ([TECH_DECISIONS](TECH_DECISIONS.md)), Codex góp ý khả thi → GD quyết định.
2. Spec → task → Codex triển khai trên branch → test → handoff report → Claude review → (GD cho phép) merge.
3. Codex phát hiện bất khả thi → báo tác động **trước** khi thay đổi lớn → Claude xử lý (spec update / CR).

## 10. Quality Gates

- Không package/dependency mới khi chưa `APPROVED`.
- Không phụ thuộc vòng giữa module; không vi phạm hướng phụ thuộc.
- Logic gameplay có thể test được tách khỏi MonoBehaviour khi hợp lý.
- Test chạy thật và có output trước khi báo DONE.
- `main` luôn mở được trong Unity và build được (khi có VCS).

## 11. Approval Authority

GD: Unity version, render pipeline, input system, package, kiến trúc nền tảng, data contract dùng chung (L1). Claude: cấu trúc nội bộ module, contract nội bộ, thứ tự triển khai (L0). Codex: chi tiết triển khai trong task.

## 12. Assigned Agents

Primary Executor: **Codex**. Đặc tả kiến trúc, review: **Claude**. Phản biện kiến trúc: ChatGPT, Gemini. Phê duyệt: **Game Director**.

## 13. Documentation Ownership

Claude: UNITY_ARCHITECTURE_PROPOSAL, MODULE_BOUNDARIES, DATA_CONTRACTS, TECH_DECISIONS. Codex: tài liệu triển khai trong code và ghi chú kỹ thuật module (khi có Unity project), đề xuất sửa tài liệu kiến trúc qua report.

## 14. Escalation Rules

- Mâu thuẫn spec/contract, cần dependency mới, vấn đề hiệu năng Android, không chạy được test/build → Codex báo Claude.
- Thay đổi ảnh hưởng nhiều module hoặc save data → Claude lập đề xuất L1 → GD.
