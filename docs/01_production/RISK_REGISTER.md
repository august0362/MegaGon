# Risk Register

> **Document Owner:** Claude (Risk Manager) · **Approver:** Game Director (với rủi ro High) · **Status:** `ACTIVE` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [PROJECT_STATUS](PROJECT_STATUS.md) · [ROADMAP](ROADMAP.md) · [D-0011](../00_governance/DECISION_LOG.md#d-0011--cấu-trúc-tài-liệu-quy-ước-id-và-từ-vựng-trạng-thái)

Thang đánh giá: **Likelihood** và **Impact** = Low / Medium / High. Rủi ro High được báo GD trong PROJECT_STATUS. Trạng thái: `OPEN`, `MITIGATING`, `CLOSED`, `OCCURRED`.

---

| ID | Rủi ro | Loại | L | I | Giảm thiểu | Owner | Status |
|---|---|---|---|---|---|---|---|
| R-001 | **Phình phạm vi**: RPG có nhiều hệ thống (quest, inventory, progression, narrative) dễ vượt khả năng sản xuất | Sản xuất | High | High | Vertical Slice First (P3); phạm vi từng milestone khóa bằng exit gate; mọi thêm phạm vi qua CR | Claude | `OPEN` |
| R-002 | **Mất ngữ cảnh khi chuyển giao** do agent không kết nối với nhau, nhiều phiên | Tổ chức | High | Medium | Handoff tự đủ ngữ cảnh; repository là nguồn sự thật; giao thức đầu/cuối phiên ([WORKFLOW §5](../00_governance/WORKFLOW.md#5-giao-thức-phiên-làm-việc-mọi-agent-thực-thi)) | Claude | `OPEN` |
| R-003 | **Hình ảnh AI thiếu nhất quán**: nhân vật lệch giữa các ảnh, sprite sheet sai grid, frame animation không liền mạch | Sản xuất nội dung | High | High | Xác minh năng lực sớm (M1-ART-002); bắt buộc sketch/review; technical validation; dùng công cụ bổ sung và chỉnh tay khi cần | Claude / Antigravity | `OPEN` |
| R-004 | **Rủi ro bản quyền/originality**: asset AI hoặc thiết kế giống game tham khảo hay tác phẩm có bản quyền | Pháp lý | Medium | High | P12; ghi provenance trong ASSET_MANIFEST; review originality trong Art Review; không prompt theo tên game/nghệ sĩ cụ thể | Claude / Antigravity | `OPEN` |
| R-005 | **Codex không chạy được Unity Editor/batchmode** (license, môi trường sandbox) → test/build không kiểm chứng được | Kỹ thuật | Medium | High | M1-PRD-001 xác minh sớm; phương án dự phòng: GD chạy test/build trên máy cục bộ theo hướng dẫn của Codex, hoặc CI ([OQ-022](../00_governance/OPEN_QUESTIONS.md)) | Claude | `OPEN` |
| R-006 | **Điều khiển cảm ứng và hiệu năng Android kém** do phát hiện muộn | Kỹ thuật / Thiết kế | Medium | High | ★ Android smoke build ở M2; mục Platform Considerations bắt buộc trong spec | Claude / Codex | `OPEN` |
| R-007 | **Nghẽn quyết định** tại Game Director (nhiều quyết định L1/L2) | Tổ chức | Medium | Medium | Gom quyết định theo nhóm và theo thời điểm cần (OPEN_QUESTIONS); đề xuất có khuyến nghị rõ; lên kế hoạch cho phần không bị chặn | Claude | `OPEN` |
| R-008 | **Tài liệu trôi lệch** (drift) giữa spec, code và quyết định | Tổ chức | Medium | Medium | Traceability ID; rà soát tại milestone gate; CHANGE_CONTROL | Claude | `OPEN` |
| R-009 | **Chưa có nguồn audio** | Sản xuất nội dung | High | Medium | Ghi `UNASSIGNED`; giải quyết OQ-026 trước M5; dùng placeholder audio có license trong prototype | Claude / GD | `OPEN` |
| R-010 | **Ý kiến trái chiều giữa ChatGPT và Gemini** gây chậm hoặc lẫn lộn quyết định | Tổ chức | Medium | Low | Claude trình bày song song, nêu giả định khác biệt; GD quyết định | Claude | `OPEN` |
| R-011 | **Xung đột merge scene/prefab Unity** khi nhiều phiên/agent cùng sửa | Kỹ thuật | Medium | Medium | Force Text serialization; owner scene/prefab theo task; prefab nhỏ; Git LFS cho nhị phân | Codex / Claude | `OPEN` |
| R-012 | **Save data không tương thích** giữa các phiên bản | Kỹ thuật | Medium | Medium | Schema version + migration từ M3; tách save DTO khỏi runtime object | Codex | `OPEN` |
| R-013 | **Over-engineering kiến trúc** (framework, abstraction thừa) | Kỹ thuật | Medium | Medium | P4; review kiến trúc theo nguyên tắc "đủ cho milestone hiện tại + một bước" | Claude | `OPEN` |
| R-014 | **Khối lượng và chất lượng nội dung narrative** (hội thoại, quest) không có writer chuyên trách | Sản xuất nội dung | Medium | Medium | Narrative runtime data-driven; GD duyệt theo lô; xác định nguồn viết nội dung trước M5 | Claude / GD | `OPEN` |
| R-015 | **Mất lịch sử tài liệu** vì chưa có version control | Tổ chức | Medium | Medium | Giải quyết OQ-009 sớm trong M1; trước đó GD sao lưu thư mục | GD / Claude | `OPEN` |
| R-016 | **Thay đổi chính sách/licensing Unity hoặc yêu cầu cửa hàng** (ví dụ yêu cầu target API Android) | Bên ngoài | Low | Medium | Kiểm tra tại thời điểm chọn phiên bản Unity (OQ-006) và trước release (RELEASE_CHECKLIST) | Claude | `OPEN` |
