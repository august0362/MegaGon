# Agent Roles — Tổng quan

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md) · [WORKFLOW](WORKFLOW.md) · [agents/](../../agents/)

Tài liệu này là bản đồ tổng quan. Chi tiết nhiệm vụ, quyền hạn, hành động được phép/cấm của từng agent nằm trong file riêng ở thư mục [agents/](../../agents/).

---

## 1. Danh sách thành viên

| Thành viên | Tầng | Vai trò | Quyền phê duyệt | File vai trò |
|---|---|---|---|---|
| Game Director (người dùng) | A | Product Owner, quyết định cuối cùng | **Có** — L1, L2 | [GAME_DIRECTOR.md](../../agents/GAME_DIRECTOR.md) |
| ChatGPT | A | Strategic & System Design Advisor | **Không** | [CHATGPT.md](../../agents/CHATGPT.md) |
| Gemini Pro | A | Independent Creative & Technical Advisor | **Không** | [GEMINI.md](../../agents/GEMINI.md) |
| Claude | B | Project Lead | Chỉ L0 | [CLAUDE.md](../../agents/CLAUDE.md) |
| Codex | B | Software Implementation & Basic QA | Chỉ chi tiết trong phạm vi task | [CODEX.md](../../agents/CODEX.md) |
| Antigravity | B | Visual Production | Chỉ chi tiết trong phạm vi task | [ANTIGRAVITY.md](../../agents/ANTIGRAVITY.md) |

---

## 2. Mô hình giao tiếp

Các agent **không kết nối trực tiếp với nhau**. Mọi trao đổi đi qua hai kênh:

1. **Repository (tài liệu)** — bộ nhớ chung, nguồn sự thật. Agent đọc tài liệu trước khi làm và ghi kết quả vào tài liệu sau khi làm.
2. **Game Director (người chuyển tiếp)** — chuyển task record, báo cáo, đề xuất giữa các agent.

```
            ┌──────────────── Game Director ────────────────┐
            │   (quyết định + chuyển tiếp tài liệu)          │
   ChatGPT ─┤                                                ├─ Gemini
            │                                                │
            └──── Claude ──── task record ────► Codex / Antigravity
                    ▲                               │
                    └──────── handoff report ◄──────┘
                  (tất cả lưu trong repository)
```

Hệ quả bắt buộc:

- Mọi handoff phải **tự đủ ngữ cảnh** (self-contained): người nhận không cần đọc chat của agent khác.
- Không agent nào được giả định agent khác "đã biết" điều gì chưa được ghi vào repository.
- Quy trình chi tiết: [WORKFLOW §2](WORKFLOW.md#2-handoff-protocol).

---

## 3. Năng lực đã xác minh và chưa xác minh

| Agent | Năng lực được giả định | Trạng thái xác minh | Cách xác minh (dự kiến) |
|---|---|---|---|
| Codex | Viết C# cho Unity | Chưa xác minh trên dự án này | Task đầu tiên của M2 |
| Codex | Chạy Unity Editor ở batchmode (test, build) trong môi trường của Codex | **Chưa xác minh — rủi ro cao** ([R-005](../01_production/RISK_REGISTER.md)) | M1-PRD-001 |
| Codex | Build Android (SDK/NDK, ký APK/AAB) | Chưa xác minh | M2 Android smoke build |
| Antigravity | Tạo ảnh tham khảo, moodboard, sketch | Chưa xác minh | M1-ART-002 |
| Antigravity | Giữ nhất quán nhân vật qua nhiều ảnh | **Chưa xác minh — rủi ro cao** ([R-003](../01_production/RISK_REGISTER.md)) | M1-ART-002 |
| Antigravity | Sprite sheet đúng grid, nền trong suốt, frame animation dùng được | **Chưa xác minh** — không được giả định làm được bằng một lần sinh ảnh | M1-ART-002, M4 |
| Bất kỳ agent nào | Sản xuất âm thanh/nhạc chuyên nghiệp | **Không có** — `UNASSIGNED` | [OQ-026](OPEN_QUESTIONS.md) |

Kết quả xác minh được ghi vào bảng này và [PROJECT_STATUS](../01_production/PROJECT_STATUS.md).

---

## 4. Ánh xạ bộ phận × agent

| Bộ phận | GD | ChatGPT | Gemini | Claude | Codex | Antigravity |
|---|---|---|---|---|---|---|
| 01 Production | Phê duyệt L1/L2 | Tư vấn | Tư vấn | **Primary** | Báo cáo | Báo cáo |
| 02 Game Design | Phê duyệt | Tư vấn | Tư vấn | **Đặc tả** | **Triển khai** | — |
| 03 Narrative | Phê duyệt, sở hữu sáng tạo | Đề xuất ý tưởng | Đề xuất ý tưởng | **Đặc tả, continuity** | **Runtime** | Minh họa (khi được giao) |
| 04 Art | Phê duyệt | Phản biện | Phản biện | Brief, kiểm tra kỹ thuật | Tích hợp | **Primary** |
| 05 Engineering | Phê duyệt kiến trúc lớn | Phản biện | Phản biện | **Đặc tả kiến trúc** | **Primary** | — |
| 06 Audio & Integration | Phê duyệt | Tư vấn | Tư vấn | Yêu cầu, mapping | **Tích hợp** | — |
| 06 — Audio production | | | | | | `UNASSIGNED` |
| 07 QA & Release | **Nghiệm thu cuối** | — | — | **Giám sát** | **QA cơ bản** | Visual QA |

### 4.1. Vai trò chưa có agent chuyên trách

| Vai trò | Bộ phận | Xử lý tạm thời |
|---|---|---|
| Audio Director, Sound Designer, Music Composer | 06 | `UNASSIGNED`. Claude chỉ viết yêu cầu audio; nguồn audio chờ [OQ-026](OPEN_QUESTIONS.md). |
| Story Writer, Dialogue Writer | 03 | Không có agent chuyên trách. Bản nháp có thể đến từ GD, ChatGPT, Gemini hoặc Claude (khi GD yêu cầu) và luôn ở trạng thái `PROPOSED` cho tới khi GD duyệt. |
| Performance Tester trên thiết bị thật | 07 | Phụ thuộc thiết bị thử nghiệm ([OQ-011](OPEN_QUESTIONS.md)); GD hoặc người được GD chỉ định thực hiện trên thiết bị. |

---

## 5. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo | Claude |
