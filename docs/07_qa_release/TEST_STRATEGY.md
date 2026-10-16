# Test Strategy

> **Document Owner:** Claude (QA Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [ACCEPTANCE_CRITERIA](ACCEPTANCE_CRITERIA.md) · [DEFINITION_OF_READY_DONE §3](../00_governance/DEFINITION_OF_READY_DONE.md#3-bằng-chứng-được-chấp-nhận) · [UNITY_ARCHITECTURE_PROPOSAL §10](../05_engineering/UNITY_ARCHITECTURE_PROPOSAL.md#10-testability)

---

## 1. Nguyên tắc

1. **Không có bằng chứng = chưa kiểm thử.** "Đã viết test" ≠ "test đã chạy và pass".
2. Tự động hóa những gì lặp lại và xác định được; con người đánh giá cảm giác và trải nghiệm.
3. Test theo rủi ro: hệ thống có trạng thái bền vững (save, quest) và hệ thống cốt lõi (combat) được test kỹ nhất.
4. Báo cáo trung thực phần **chưa kiểm chứng**.

## 2. Các tầng kiểm thử

| Tầng | Công cụ (đề xuất) | Ai viết/chạy | Khi nào | Đối tượng |
|---|---|---|---|---|
| Unit (EditMode) | Unity Test Framework | Codex | Mỗi task có logic | Logic C# thuần |
| Integration (PlayMode) | Unity Test Framework | Codex | Feature hoàn tất | Hệ thống phối hợp |
| Data validation | Editor validators | Codex | Mỗi thay đổi dữ liệu | Tham chiếu, ID, quest khả thi |
| Regression | Toàn bộ suite tự động + checklist thủ công | Codex | Trước mỗi milestone gate | Toàn bộ |
| Gameplay test cơ bản | Kịch bản thủ công | Codex (khi có thể) / GD | Feature gameplay | Luồng chơi chính |
| Narrative progression | PlayMode + debug tools | Codex | Mỗi thay đổi narrative | Quest/story hoàn thành được, save/load |
| Visual review | Ảnh chụp/video in-game | Antigravity | Sau tích hợp asset | Nhất quán, tỉ lệ, pivot |
| Playtest trải nghiệm | Checklist cảm giác | **GD** | Milestone | Cảm giác, vui, rõ ràng |
| Performance | Unity Profiler, quan sát FPS trên thiết bị | Codex / người giữ thiết bị | M2 (smoke), M6 (đầy đủ) | FPS, bộ nhớ, thời gian load |
| Build validation | Build log + chạy thử | Codex | Mỗi milestone có build | Build thành công, khởi động, chơi được |

## 3. Năng lực chạy test — cần xác minh

Khả năng Codex chạy Unity ở batchmode trong môi trường của nó **chưa được xác minh** (M1-PRD-001, R-005). Nếu không chạy được, phương án:
1. Codex cung cấp lệnh/hướng dẫn; GD chạy trên máy cục bộ và gửi lại output.
2. Thiết lập CI (OQ-022).

Trong cả hai trường hợp, report phải ghi rõ **ai chạy, ở đâu, output gì**.

## 4. Quy ước test case

ID: `TC-<MODULE>-NNN`. Mỗi test case gắn với acceptance criterion trong spec (traceability: Spec → AC → TC → kết quả).

## 5. PC và Android

| Hạng mục | PC | Android |
|---|---|---|
| Cấu hình thử nghiệm | `TBD` (OQ-011) | `TBD` (OQ-011) — tối thiểu một thiết bị thật cấu hình thấp/trung bình |
| Input | Bàn phím + chuột; gamepad nếu được duyệt | Cảm ứng, đa chạm |
| Màn hình | Các độ phân giải phổ biến, cửa sổ/toàn màn hình | Nhiều tỉ lệ, notch/safe area |
| Vòng đời | Alt-tab, thu nhỏ | Xuống nền, cuộc gọi đến, khóa màn hình, kill app → save/load |
| Hiệu năng | FPS mục tiêu `TBD` | FPS mục tiêu `TBD`, nhiệt, bộ nhớ |

Performance budget (FPS, bộ nhớ, kích thước build) được đề xuất trong M1–M2 và duyệt trước M6.

## 6. Bug report

```markdown
### BUG-NNN — <tiêu đề ngắn>
- Severity: Blocker / Critical / Major / Minor / Trivial
- Nền tảng / build / Unity version:
- Các bước tái hiện:
- Kết quả mong đợi / thực tế:
- Bằng chứng: ảnh, video, log
- Task/Spec liên quan:
- Status: OPEN → IN_PROGRESS → FIXED → VERIFIED → CLOSED (hoặc WONT_FIX có lý do, do GD/Claude quyết)
```

| Severity | Định nghĩa |
|---|---|
| Blocker | Không thể tiếp tục chơi/build/test |
| Critical | Mất dữ liệu save, crash, kẹt tiến trình |
| Major | Tính năng sai đáng kể, có cách vượt qua |
| Minor | Sai nhỏ, ảnh hưởng ít |
| Trivial | Thẩm mỹ, chính tả |

## 7. Test report tối thiểu

Môi trường (Unity version, nền tảng, thiết bị) · lệnh/công cụ · số test pass/fail/skip · output hoặc đường dẫn file kết quả · danh sách phần chưa kiểm chứng.
