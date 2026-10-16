# Game Director / Product Owner

> **Document Owner:** Claude (soạn) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [AUTHORITY_MATRIX](../docs/00_governance/AUTHORITY_MATRIX.md) · [DECISION_POLICY](../docs/00_governance/DECISION_POLICY.md) · [AGENT_ROLES](../docs/00_governance/AGENT_ROLES.md)

**Game Director là người dùng — chủ sở hữu dự án và là người có quyền quyết định cuối cùng.** Không AI agent nào được thay thế quyền phê duyệt này.

---

## 1. Mission

Định hướng sản phẩm, quyết định những điều tạo nên bản sắc của game và nghiệm thu chất lượng trải nghiệm cuối cùng.

## 2. Responsibilities

- Định hướng game, phê duyệt Game Vision.
- Lựa chọn Art Direction.
- Phê duyệt hệ thống gameplay, thế giới và cốt truyện.
- Phê duyệt thay đổi kiến trúc lớn và thay đổi công nghệ chính.
- Phê duyệt exit gate của các milestone.
- Chơi thử và nghiệm thu sản phẩm quan trọng.
- **Chuyển tiếp** task record và báo cáo giữa các agent (vì các agent không kết nối trực tiếp — [AGENT_ROLES §2](../docs/00_governance/AGENT_ROLES.md#2-mô-hình-giao-tiếp)).

## 3. Decision Authority

- Toàn quyền L2. Phê duyệt L1. Có thể bác bỏ mọi quyết định L0 của Claude.
- Có thể ủy quyền một phần (ví dụ cho Claude nghiệm thu asset phụ) — ủy quyền phải được ghi thành Decision Record.

## 4. Allowed Actions

Mọi hành động. Gợi ý thực hành tốt: khi quyết định trong chat, yêu cầu Claude ghi lại thành Decision Record ngay trong phiên đó.

## 5. Forbidden Actions

Không có giới hạn quyền. Các lưu ý để giữ quyền kiểm soát:

- Tránh phê duyệt ngầm ("ừ, cứ làm đi" cho một đề xuất chưa rõ phạm vi) — agent sẽ ghi đúng phạm vi được nói rõ.
- Tránh đưa quyết định trực tiếp cho Codex/Antigravity mà không qua Claude — quyết định sẽ không được ghi vào DECISION_LOG và dễ mất truy vết.

## 6. Required Inputs

Để quyết định tốt, GD nên nhận được: đề xuất theo định dạng [DECISION_POLICY §2.1](../docs/00_governance/DECISION_POLICY.md#21-định-dạng-đề-xuất-cho-l1l2), bằng chứng kiểm thử, build chơi được (khi nghiệm thu), phân tích của ChatGPT/Gemini (khi cần).

## 7. Expected Outputs

- Quyết định rõ ràng: duyệt / bác bỏ / duyệt có điều kiện / yêu cầu thêm phương án.
- Phản hồi nghiệm thu: đạt / không đạt kèm lý do.

## 8. Collaboration Rules

- Dùng ChatGPT và Gemini để phân tích, tranh luận; dùng Claude để biến quyết định thành đặc tả và kế hoạch.
- Khi chuyển kết quả từ agent này sang agent khác, chuyển **file/tài liệu trong repository**, không chỉ đoạn chat.

## 9. Escalation Rules

GD là điểm chuyển cấp cuối cùng. Khi GD chưa sẵn sàng quyết định, mục liên quan giữ `UNDER_REVIEW` và Claude lên kế hoạch cho phần việc không bị chặn.

## 10. Definition of Done (với một quyết định)

Quyết định của GD được coi là hoàn tất khi đã có trong [DECISION_LOG](../docs/00_governance/DECISION_LOG.md) với trạng thái `APPROVED`/`REJECTED` và Approval Evidence.

## 11. Reporting Format (cách GD ra quyết định để agent ghi chính xác)

```
Quyết định: <Decision ID hoặc OQ ID>
Kết luận: Duyệt / Bác bỏ / Duyệt có điều kiện / Cần thêm phương án
Điều kiện hoặc ghi chú: …
```
