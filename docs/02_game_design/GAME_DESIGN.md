# Game Design — Tổng quan

> **Document Owner:** Claude · **Approver:** Game Director · **Status:** `UNDER_REVIEW` (cấu trúc) · nội dung chủ yếu `TBD` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [COMBAT_DESIGN](COMBAT_DESIGN.md) · [SYSTEMS_OVERVIEW](SYSTEMS_OVERVIEW.md) · [LEVEL_DESIGN](LEVEL_DESIGN.md) · [OPEN_QUESTIONS](../00_governance/OPEN_QUESTIONS.md)

Tài liệu gốc của Game Design. Ghi những gì **đã duyệt**, khung cho những gì **chưa duyệt**, và các phương án cần quyết định.

---

## 1. Những gì đã được phê duyệt

| Mục | Giá trị | Decision |
|---|---|---|
| Thể loại | 2D Adventure RPG | D-0001 |
| Chiến đấu | Real-time Action | D-0004 |
| Nền tảng | PC + Android | D-0003 |
| Chế độ chơi | Single-player trong phạm vi ban đầu | D-0005 |

**Game tham khảo về thể loại và trải nghiệm** (không sao chép nội dung — P12): Ngọc Rồng Online, Ninja School. Việc dùng chúng làm tham chiếu chỉ để thảo luận cảm giác thể loại; điều gì được học hỏi cụ thể từ chúng phải được ghi rõ trong Decision Record khi bàn tới.

## 2. Game Vision — `TBD`

[OQ-001](../00_governance/OPEN_QUESTIONS.md). Game Vision phải trả lời:

| Câu hỏi | Trạng thái |
|---|---|
| Người chơi cảm thấy gì? (cảm xúc chủ đạo) | `TBD` |
| 3–5 game pillars (nguyên tắc thiết kế không được vi phạm) | `TBD` |
| Người chơi mục tiêu (độ tuổi, kinh nghiệm, thói quen chơi PC/mobile) | `TBD` |
| Thời lượng một phiên chơi điển hình (ảnh hưởng thiết kế Android) | `TBD` |
| Điểm khác biệt so với các game cùng thể loại | `TBD` |
| Tham vọng quy mô (demo ngắn / game hoàn chỉnh nhỏ / lớn) | `TBD` |

> `EXAMPLE — NOT APPROVED` — dạng một pillar: *"Mỗi trận đánh phải đọc được: người chơi luôn hiểu vì sao mình trúng đòn."* Đây chỉ là ví dụ về **cách viết** pillar.

## 3. Core Gameplay Loop — `TBD`

[OQ-003](../00_governance/OPEN_QUESTIONS.md). Core loop được mô tả ở ba tầng:

| Tầng | Câu hỏi | Trạng thái |
|---|---|---|
| Moment-to-moment (giây) | Người chơi làm gì liên tục? | `TBD` |
| Session (phút) | Một phiên chơi có mục tiêu và phần thưởng gì? | `TBD` |
| Long-term (giờ) | Điều gì kéo người chơi quay lại? | `TBD` |

> `EXAMPLE — NOT APPROVED` — cấu trúc thường gặp ở Adventure RPG: *Khám phá → Gặp thử thách → Chiến đấu/Giải quyết → Nhận phần thưởng → Mạnh hơn/Mở khóa khu vực → Khám phá tiếp.* Không phải quyết định của dự án.

## 4. Góc nhìn camera — `TBD`

[OQ-002](../00_governance/OPEN_QUESTIONS.md) · Level L2. Đây là quyết định có ảnh hưởng rộng nhất sau Vision.

| Phương án | Ưu điểm | Nhược điểm | Tác động chính |
|---|---|---|---|
| **Side-scrolling** | Combat dễ đọc, platforming, nhảy tạo chiều sâu điều khiển | Khám phá theo trục ngang; thế giới mở khó thể hiện | Physics có trọng lực; level dạng tuyến/metroidvania |
| **Top-down (thẳng hoặc 3/4)** | Khám phá thế giới tự nhiên, phổ biến ở RPG; hợp điều khiển joystick ảo | Khó thể hiện độ cao, nhảy; combat cần nhắm hướng | Di chuyển 4/8 hướng hoặc tự do; tile map |
| **Isometric** | Chiều sâu thị giác, chất lượng hình ảnh cao | Chi phí art cao (nhiều hướng sprite), sort order phức tạp, va chạm khó | Art cost lớn nhất; engineering phức tạp hơn |
| **Khác / lai** | — | — | Cần đề xuất cụ thể |

Tiêu chí so sánh khi quyết định: phù hợp Vision, cảm giác combat real-time, khả năng điều khiển cảm ứng, chi phí art (số hướng sprite), độ phức tạp kỹ thuật.

## 5. Platform Considerations (bắt buộc cho mọi thiết kế)

| Khía cạnh | PC | Android |
|---|---|---|
| Input | Bàn phím + chuột; gamepad `TBD` ([OQ-008](../00_governance/OPEN_QUESTIONS.md)) | Cảm ứng: joystick ảo / nút ảo / cử chỉ — `TBD` |
| UI | Màn hình lớn, độ chính xác chuột cao | Vùng chạm tối thiểu, safe area, ngón tay che màn hình |
| Phiên chơi | Thường dài hơn | Có thể ngắn, bị gián đoạn (cuộc gọi, chuyển app) → ảnh hưởng save |
| Hiệu năng | Đa dạng cấu hình | Giới hạn GPU/RAM/nhiệt/pin |

Quy tắc: không thiết kế cơ chế chỉ chơi được bằng chuột/bàn phím rồi "chuyển sang" cảm ứng sau.

## 6. Bản đồ tài liệu thiết kế

| Hệ thống | Tài liệu |
|---|---|
| Chiến đấu, kỹ năng, kẻ địch, boss | [COMBAT_DESIGN](COMBAT_DESIGN.md) |
| Danh sách hệ thống, trạng thái, phụ thuộc | [SYSTEMS_OVERVIEW](SYSTEMS_OVERVIEW.md) |
| Level, khám phá | [LEVEL_DESIGN](LEVEL_DESIGN.md) |
| Quest, dialogue (thiết kế) | [QUEST_DIALOGUE_DESIGN](../03_narrative/QUEST_DIALOGUE_DESIGN.md) |
