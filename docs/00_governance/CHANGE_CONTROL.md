# Change Control

> **Document Owner:** Claude (Project Lead) · **Approver:** Game Director · **Status:** `UNDER_REVIEW` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [DECISION_POLICY](DECISION_POLICY.md) · [DECISION_LOG](DECISION_LOG.md) · [AUTHORITY_MATRIX](AUTHORITY_MATRIX.md)

---

## 1. Khi nào cần Change Request (CR)

Bắt buộc mở CR khi muốn thay đổi:

- Một Decision Record `APPROVED`.
- Một Feature Spec hoặc data contract `APPROVED`.
- Phạm vi hoặc exit gate của milestone.
- Bất kỳ asset concept/style guide đã duyệt.

Không cần CR cho: thay đổi trong nội dung `TBD`/`PROPOSED`, sửa lỗi chính tả, sửa link, cập nhật tài liệu sống (status, backlog) — nhưng vẫn ghi lịch sử thay đổi trong tài liệu.

---

## 2. Phân loại thay đổi

| Loại | Level | Ví dụ | Người duyệt |
|---|---|---|---|
| **Minor** | L0 | Đổi thứ tự task, tách task, đổi tuning trong dải đã duyệt, sửa contract nội bộ một module | Claude (thông báo GD trong PROJECT_STATUS) |
| **Major** | L1 | Đổi cơ chế gameplay, đổi data contract dùng chung, đổi exit gate, thêm package, đổi concept đã duyệt | Game Director |
| **Strategic** | L2 | Đổi tầm nhìn, thể loại, nền tảng, phong cách, quy mô | Game Director |

---

## 3. Quy trình

1. **Raise** — bất kỳ agent nào phát hiện nhu cầu thay đổi ghi CR (mẫu §6) và gửi Claude.
2. **Impact analysis** — Claude phân tích theo checklist §4.
3. **Classify** — Claude xác định Minor/Major/Strategic. Không chắc → chọn cấp cao hơn.
4. **Decide** — Minor: Claude quyết. Major/Strategic: trình GD theo định dạng [DECISION_POLICY §2.1](DECISION_POLICY.md#21-định-dạng-đề-xuất-cho-l1l2).
5. **Record** — tạo Decision Record mới; record cũ chuyển `SUPERSEDED` và ghi "Superseded by D-NNNN".
6. **Propagate** — cập nhật mọi tài liệu, task, contract bị ảnh hưởng; ghi lịch sử thay đổi trong từng tài liệu.
7. **Communicate** — ghi vào [PROJECT_STATUS](../01_production/PROJECT_STATUS.md); tạo task mới nếu cần làm lại.
8. **Verify** — kiểm tra chéo không còn tài liệu nào tham chiếu nội dung cũ như hiện hành.

Trong khi CR đang chờ: phần việc bị ảnh hưởng chuyển `BLOCKED`.

---

## 4. Checklist phân tích tác động

- [ ] Decision, spec, contract nào bị ảnh hưởng?
- [ ] Module code nào phải sửa? Có làm vỡ save data hiện có không?
- [ ] Asset nào phải làm lại?
- [ ] Nội dung narrative nào mất tính nhất quán?
- [ ] Test nào phải viết lại/chạy lại?
- [ ] Ảnh hưởng PC và Android?
- [ ] Ảnh hưởng milestone, exit gate, dependency?
- [ ] Chi phí ước lượng (task mới, làm lại)?

---

## 5. Quy tắc phiên bản tài liệu

| Thay đổi | Version |
|---|---|
| Sửa lỗi nhỏ, làm rõ không đổi nghĩa | +0.0.1 (ví dụ 0.1 → 0.1.1) |
| Thêm/sửa nội dung có ý nghĩa | +0.1 |
| Tài liệu được GD duyệt lần đầu | 1.0 |
| Thay đổi lớn sau khi đã duyệt | +1.0 (qua CR) |

- Mỗi tài liệu chủ chốt có mục "Lịch sử thay đổi".
- **Không xóa** tài liệu lịch sử. Tài liệu thay thế → đánh dấu `SUPERSEDED`, ghi link tài liệu mới ở đầu file.
- Không ghi đè quyết định đã duyệt mà không lưu lịch sử.

---

## 6. Mẫu Change Request

```markdown
### CR-NNN — <Tiêu đề>
- **Raised by / Date:**
- **Đối tượng thay đổi:** (Decision ID / Spec ID / Milestone / Asset)
- **Lý do:**
- **Đề xuất thay đổi:**
- **Phân tích tác động:** (theo checklist §4)
- **Phân loại:** Minor / Major / Strategic
- **Phương án thay thế:**
- **Khuyến nghị (Claude):**
- **Quyết định:** PROPOSED / UNDER_REVIEW / APPROVED / REJECTED — bởi … ngày …
- **Decision Record liên quan:**
- **Tài liệu/task đã cập nhật:**
```

---

## 7. Change Request Log

| CR ID | Tiêu đề | Loại | Raised by | Ngày | Status | Decision |
|---|---|---|---|---|---|---|
| — | Chưa có CR nào | — | — | — | — | — |

---

## 8. Lịch sử thay đổi

| Version | Ngày | Thay đổi | Người thực hiện |
|---|---|---|---|
| 0.1 | 2026-10-15 | Khởi tạo | Claude |
