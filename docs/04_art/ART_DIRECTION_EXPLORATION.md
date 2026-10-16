# Art Direction Exploration

> **Document Owner:** Claude (quy trình) · **Executor:** Antigravity · **Approver:** Game Director · **Status:** `UNDER_REVIEW` — Art Direction `TBD` · **Version:** 0.1 · **Last Updated:** 2026-10-15
> **Related:** [04_art/DEPARTMENT](DEPARTMENT.md) · [ASSET_SPEC](ASSET_SPEC.md) · [ART_REVIEW_TEMPLATE](../templates/ART_REVIEW_TEMPLATE.md) · [OQ-014](../00_governance/OPEN_QUESTIONS.md)

> **Art Direction chưa được quyết định.** Tài liệu này tổ chức quá trình khám phá để Game Director có đủ căn cứ lựa chọn. Không phương án nào dưới đây là khuyến nghị cuối cùng.

---

## 1. Các hướng ứng viên

| Hướng | Đặc điểm | Ưu | Nhược / rủi ro | Tác động kỹ thuật |
|---|---|---|---|---|
| **Pixel Art** | Độ phân giải thấp, lưới pixel rõ | Phù hợp nhiều game 2D RPG; file nhỏ; đọc tốt trên màn hình nhỏ | AI tạo ảnh thường **không** tôn trọng lưới pixel → cần chỉnh tay/công cụ chuyên dụng; animation frame-by-frame tốn công | Pixel-perfect camera, filter Point, PPU cố định |
| **Hand-drawn 2D** | Nét vẽ tay, màu sơn | Bản sắc mạnh, biểu cảm | Animation frame-by-frame rất tốn; nhất quán giữa các frame khó | Texture lớn hơn; cân nhắc bộ nhớ Android |
| **Anime-inspired 2D** | Tỉ lệ, đường nét kiểu anime | Hấp dẫn với nhiều người chơi; AI tạo ảnh mạnh ở phong cách này | Dễ trùng lặp, thiếu bản sắc; rủi ro giống tác phẩm có sẵn | Thường hợp skeletal animation |
| **Hybrid / Stylized 2D** | Ví dụ: nhân vật vector/skeletal trên nền vẽ tay; chibi/SD | Linh hoạt, có thể tối ưu chi phí animation | Cần style guide chặt để không lạc phong cách | Phụ thuộc tổ hợp |
| **Khác** | Theo đề xuất của GD, advisor hoặc Antigravity | — | — | — |

Lựa chọn phụ thuộc mạnh vào **góc nhìn camera (OQ-002)**: top-down/isometric có thể cần sprite nhiều hướng (4 hoặc 8), làm tăng chi phí theo cấp số.

## 2. Tiêu chí đánh giá

| Tiêu chí | Câu hỏi |
|---|---|
| Phù hợp Vision | Có truyền tải đúng cảm xúc và tông giọng không? |
| Bản sắc | Có khác biệt, dễ nhận diện, không giống game có sẵn không? |
| Đọc được khi chơi | Nhân vật, kẻ địch, đòn đánh có rõ trên màn hình điện thoại không? |
| Chi phí sản xuất | Chi phí cho một nhân vật đầy đủ animation; số hướng sprite |
| Khả thi với công cụ hiện có | Antigravity + công cụ bổ sung có tạo được nhất quán không? (đã xác minh ở M1-ART-002?) |
| Hiệu năng | Kích thước texture, bộ nhớ trên Android |
| Animation | Phương pháp phù hợp (OQ-015) |

## 3. Quy trình khám phá

| # | Bước | Thực hiện | Đầu ra | Milestone |
|---|---|---|---|---|
| 1 | **Research** | Antigravity | Danh sách tham khảo theo hướng (ghi nguồn; chỉ để học, không sao chép) | M1 ★ |
| 2 | **Moodboard** | Antigravity | Một moodboard cho mỗi hướng ứng viên (≥3) | M1 ★ |
| 3 | **Rough Sketch** | Antigravity | Phác thảo **cùng một đối tượng thử nghiệm** (một nhân vật + một góc môi trường) ở mỗi hướng | M1–M4 |
| 4 | **Concept Variants** | Antigravity | 2–3 hướng được GD chọn lọc, phát triển sâu hơn: nhân vật trong môi trường, mockup màn hình chơi gồm UI, ở tỉ lệ PC và điện thoại | M4 |
| 5 | **Comparative Review** | Claude chuẩn bị, GD + (tùy chọn) ChatGPT/Gemini đánh giá | Art Review Record so sánh theo tiêu chí §2 | M4 |
| 6 | **Game Director Approval** | GD | Decision Record Art Direction `APPROVED` → OQ-014 đóng | M4 |
| 7 | **Final Asset Production** | Antigravity | Style guide + asset mẫu | M4 |
| 8 | **Technical Validation** | Claude + Codex | Checklist ASSET_SPEC | M4 |
| 9 | **Integration** | Codex | Asset mẫu chạy trong Unity, PC + Android | M4 |

★ Bước 1–2 trong M1 thuộc đề xuất D-0012 (`PROPOSED`).

Ghi chú: đối tượng thử nghiệm ở bước 3–4 dùng nhân vật trung tính `EXAMPLE — NOT APPROVED`, không phải nhân vật canon, cho tới khi có Character Register.

## 4. Đầu ra bắt buộc để GD so sánh

Với mỗi hướng lọt vào Comparative Review:
1. Nhân vật thử nghiệm: đứng yên, tư thế hành động, cùng tỉ lệ in-game.
2. Một mảnh môi trường.
3. **Mockup màn hình chơi** ở kích thước thật trên PC và điện thoại (kèm UI giả lập) — để đánh giá độ đọc được.
4. Ước lượng chi phí sản xuất một nhân vật đầy đủ animation (do Antigravity + Claude ước lượng, có nêu giả định).
5. Kết quả thử nghiệm nhất quán (cùng nhân vật ở nhiều tư thế/frame).

## 5. Sau khi Art Direction được duyệt

- Claude và Antigravity soạn **Style Guide**: bảng màu, tỉ lệ nhân vật, độ dày nét, ánh sáng, mức chi tiết, quy tắc UI.
- Cập nhật [ASSET_SPEC](ASSET_SPEC.md): PPU, kích thước, pivot, frame — từ `TBD` thành `PROPOSED` rồi `APPROVED`.
- Xem xét lại OQ-007 (render pipeline) nếu phong cách cần ánh sáng 2D hoặc pixel-perfect.
