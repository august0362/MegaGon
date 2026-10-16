# Untitled 2D Adventure RPG

> Tên game: `TBD` · Thư mục làm việc: `MegaGon` (không phải tên game chính thức — [OQ-029](docs/00_governance/OPEN_QUESTIONS.md))
> **Phase:** Initialization / Pre-production — **M0 Governance Foundation** (`GATE_REVIEW`)
> **Last Updated:** 2026-10-15

Dự án game 2D Adventure RPG, chiến đấu real-time action, phát triển bằng Unity/C# cho PC và Android, theo mô hình **AI-assisted, human-directed**.

Hiện repository **chỉ chứa tài liệu quản trị**. Chưa có Unity project, code hay asset.

---

## Bắt đầu từ đâu

| Bạn là | Đọc trước |
|---|---|
| Game Director | [PROJECT_STATUS](docs/01_production/PROJECT_STATUS.md) → [OPEN_QUESTIONS](docs/00_governance/OPEN_QUESTIONS.md) → [DECISION_LOG](docs/00_governance/DECISION_LOG.md) |
| Claude | [CLAUDE.md](CLAUDE.md) |
| Codex, Antigravity, agent khác | [AGENTS.md](AGENTS.md) |
| ChatGPT, Gemini (do GD cung cấp) | [PROJECT_CHARTER](docs/00_governance/PROJECT_CHARTER.md) + file vai trò trong [agents/](agents/) |

## Bản đồ tài liệu

| Khu vực | Nội dung |
|---|---|
| [agents/](agents/) | Vai trò, quyền hạn, cách báo cáo của từng thành viên |
| [docs/00_governance/](docs/00_governance/) | Charter, phân quyền, workflow, chính sách quyết định, decision log, open questions, change control, DoR/DoD |
| [docs/01_production/](docs/01_production/) | Roadmap, milestones, backlog, project status, risk register |
| [docs/02_game_design/](docs/02_game_design/) | Khung game design, combat, hệ thống, level design |
| [docs/03_narrative/](docs/03_narrative/) | World bible, kiến trúc cốt truyện, nhân vật, quest/dialogue |
| [docs/04_art/](docs/04_art/) | Khám phá Art Direction, brief, asset spec, manifest |
| [docs/05_engineering/](docs/05_engineering/) | Đề xuất kiến trúc Unity, module, data contract, tech decisions |
| [docs/06_audio_integration/](docs/06_audio_integration/) | Kế hoạch audio, content pipeline |
| [docs/07_qa_release/](docs/07_qa_release/) | Chiến lược test, acceptance criteria, release checklist |
| [docs/templates/](docs/templates/) | Mẫu decision, spec, task, milestone, art review |

## Ba quy tắc quan trọng nhất

1. **Chỉ Game Director phê duyệt** các quyết định thiết kế, sáng tạo, phạm vi và kiến trúc lớn. Đồng thuận giữa các AI không phải phê duyệt.
2. **Chưa có trong [DECISION_LOG](docs/00_governance/DECISION_LOG.md) thì chưa phải quyết định.** Chat history không phải nguồn sự thật.
3. **Không có bằng chứng thì chưa phải hoàn thành.**
