# Tech Decisions

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` — chưa có quyết định kỹ thuật nào `APPROVED` ngoài D-0002 · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [OPEN_QUESTIONS](../00_governance/OPEN_QUESTIONS.md) · [DECISION_LOG](../00_governance/DECISION_LOG.md) · [UNITY_ARCHITECTURE_PROPOSAL](UNITY_ARCHITECTURE_PROPOSAL.md)

Phân tích kỹ thuật cho các câu hỏi mở. Đây là **tài liệu phân tích**, không phải sổ quyết định: khi GD quyết định, kết quả được ghi vào [DECISION_LOG](../00_governance/DECISION_LOG.md) và mục ở đây chỉ trỏ tới Decision ID.

**Lưu ý về độ chính xác thông tin:** trạng thái hỗ trợ của các phiên bản Unity, yêu cầu của cửa hàng ứng dụng và điều khoản license thay đổi theo thời gian. Mọi thông tin loại này phải được **kiểm tra lại tại thời điểm quyết định** từ nguồn chính thức (Unity, Google Play).

| TD | Chủ đề | OQ | Status | Decision |
|---|---|---|---|---|
| TD-01 | Phiên bản Unity | OQ-006 | `TBD` | — |
| TD-02 | Render pipeline | OQ-007 | `TBD` | — |
| TD-03 | Input handling | OQ-008 | `TBD` | — |
| TD-04 | Version control | OQ-009 | `TBD` | — |
| TD-05 | Vị trí Unity project | OQ-010 | `PROPOSED` | — |
| TD-06 | Test framework | — | `PROPOSED` | — |
| TD-07 | CI và build automation | OQ-022 | `TBD` | — |
| TD-08 | Save format và thư viện JSON | OQ-019 | `PROPOSED` | — |
| TD-09 | Cấu hình build Android | OQ-011 | `PROPOSED` | — |

---

### TD-01 — Phiên bản Unity

- **Phương án:** (A) bản LTS mới nhất tại thời điểm bootstrap M2; (B) bản LTS cũ hơn đã ổn định lâu; (C) bản không-LTS (Tech/Supported update) để có tính năng mới.
- **Trade-off:** LTS mới — hỗ trợ dài nhất, nhưng có thể còn lỗi đầu kỳ. LTS cũ — nhiều tài liệu/ví dụ, nhưng thời gian hỗ trợ còn lại ngắn hơn. Không-LTS — rủi ro ổn định, không khuyến nghị cho dự án dài hạn.
- **Cần kiểm tra khi quyết định:** thời hạn hỗ trợ LTS; điều khoản license/pricing Unity hiện hành; khả năng cài phiên bản đó trong môi trường của Codex (M1-PRD-001); tương thích Android target API mà Google Play đang yêu cầu.
- **Khuyến nghị sơ bộ:** A — bản LTS hiện hành, cố định phiên bản patch trong `ProjectVersion.txt`, chỉ nâng cấp qua CR.

### TD-02 — Render pipeline

- **Phương án:** (A) URP với 2D Renderer — 2D lights, Sprite Lit/Unlit, pixel-perfect camera; (B) Built-in Render Pipeline.
- **Trade-off:** URP là hướng Unity đang đầu tư cho dự án mới và có bộ công cụ 2D tích hợp; ánh sáng 2D có chi phí trên Android cần đo. Built-in đơn giản nhưng là hướng ít được đầu tư hơn — cần kiểm tra trạng thái hỗ trợ ở phiên bản Unity được chọn.
- **Phụ thuộc:** Art Direction (OQ-014) — pixel art cần pixel-perfect; phong cách có ánh sáng động cần 2D lights.
- **Khuyến nghị sơ bộ:** A (URP 2D), dùng Sprite-Unlit mặc định và chỉ bật 2D lights khi Art Direction cần và đo được hiệu năng Android chấp nhận được.

### TD-03 — Input handling

- **Phương án:** (A) Input System package — input actions, nhiều control scheme, hỗ trợ cảm ứng, gamepad, rebinding; (B) Input Manager cũ.
- **Trade-off:** A phù hợp yêu cầu PC + Android (một bộ action, nhiều scheme), nhưng cấu hình ban đầu phức tạp hơn. B đơn giản nhưng xử lý cảm ứng và nhiều thiết bị kém thuận tiện.
- **Liên quan:** điều khiển cảm ứng (joystick/nút ảo) là UI layer gửi vào cùng action; gamepad trên PC có hỗ trợ hay không là quyết định thiết kế (OQ-008).
- **Khuyến nghị sơ bộ:** A.

### TD-04 — Version control

- **Phương án:** (A) Git + Git LFS, remote trên dịch vụ Git (ví dụ GitHub/GitLab — chọn theo GD); (B) Unity Version Control; (C) không dùng VCS (không khuyến nghị).
- **Trade-off:** Git phổ biến, các AI agent (Codex, Claude Code) làm việc tốt với Git, PR review dễ; cần LFS cho file nhị phân và cấu hình Unity cho merge. Unity VCS tốt với file lớn và locking, nhưng ít quen thuộc với các agent.
- **Cần GD quyết định thêm:** agent nào được commit/push; ai merge vào `main` ([WORKFLOW §6](../00_governance/WORKFLOW.md#6-git-branch-pull-request--proposed)).
- **Khuyến nghị sơ bộ:** A, khởi tạo sớm trong M1 để tài liệu M0 có lịch sử (R-015).

### TD-05 — Vị trí Unity project

Xem [UNITY_ARCHITECTURE_PROPOSAL §8](UNITY_ARCHITECTURE_PROPOSAL.md#8-cấu-trúc-unity-project-dự-kiến--proposed). Khuyến nghị: thư mục con `unity/`.

### TD-06 — Test framework

Unity Test Framework (EditMode + PlayMode) — là package chính thức của Unity, không phải bên thứ ba. Vẫn cần GD xác nhận cùng gói quyết định kiến trúc M1. Khả năng chạy test headless bởi Codex: chờ M1-PRD-001.

### TD-07 — CI và build automation

- **Phương án:** (A) Chưa có CI — Codex/GD chạy test và build cục bộ, nộp log; (B) CI trên dịch vụ Git (ví dụ GitHub Actions với công cụ cộng đồng GameCI) — cần Unity license trong CI; (C) Unity Build Automation (dịch vụ trả phí của Unity).
- **Trade-off:** A không tốn chi phí nhưng phụ thuộc vào kỷ luật nộp bằng chứng. B/C tự động hóa bằng chứng nhưng có chi phí thiết lập và license.
- **Khuyến nghị sơ bộ:** A trong M2; đánh giá B trước M6.

### TD-08 — Save format và thư viện JSON

- **Đề xuất:** JSON, DTO thuần C#, `schemaVersion`, ghi nguyên tử (xem UNITY_ARCHITECTURE_PROPOSAL §9).
- **Thư viện:** `JsonUtility` tích hợp sẵn (không cần dependency, nhưng hạn chế: không hỗ trợ Dictionary, polymorphism) vs thư viện JSON đầy đủ hơn (cần duyệt dependency). Chốt khi thiết kế DC-SAVE (M3).

### TD-09 — Cấu hình build Android

- **Đề xuất:** scripting backend IL2CPP, kiến trúc ARM64 (Google Play yêu cầu hỗ trợ 64-bit); định dạng phát hành AAB cho Google Play, APK cho thử nghiệm nội bộ.
- **TBD:** minimum API level, target API level (theo yêu cầu Google Play hiện hành), orientation (ngang/dọc), Graphics API, keystore và người giữ keystore (GD).
