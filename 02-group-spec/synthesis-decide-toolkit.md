# Toolkit — Synthesis & Decide (TrustBite AI)

---

## 1. Gom evidence thành cụm

Nhóm thực hiện gom các bằng chứng theo nỗi đau (pain) của người dùng thay vì tính năng:

- **"Vỏ bọc 5 sao ảo":** Người dùng tin vào điểm số sao cao nhưng nhận đồ ăn kém chất lượng hoặc ôi thiu.
- **"Nội dung trùng lặp máy móc":** Nhiều review 5 sao có cấu trúc ngữ nghĩa giống hệt nhau (ví dụ: "Ngon, rẻ, sẽ quay lại") xuất hiện dày đặc.
- **"Sợ bị dắt mũi":** Người dùng cảm thấy hệ thống đánh giá hiện tại quá dễ bị thao túng bởi các dịch vụ seeding.

---

## 2. Viết insight

User **[người dùng đặt đồ ăn bận rộn]** không chỉ cần **[biết số sao trung bình của một quán ăn]**.
Họ thật ra cần **[một trọng tài độc lập kiểm chứng độ tin cậy và trích dẫn bằng chứng cụ thể]**,
vì **[nhiều quan sát thực tế cho thấy các kỹ thuật seeding hiện nay đã vượt qua rào cản của các bộ lọc từ khóa truyền thống trên app]**.

---

## 3. Viết opportunity

Cơ hội là dùng AI (kết hợp Random Forest + SBERT + Gemini) để **[Augment khả năng thẩm định tính xác thực của review]**,
giúp user **[tránh được các "bẫy" seeding để ra quyết định đặt hàng an toàn hơn]**,
trong khi vẫn kiểm soát **[rủi ro gắn cờ sai cho quán thật bằng cách hiển thị điểm xác suất kèm bằng chứng thay vì tự ý ẩn quán]**.

---

## 4. Chọn build slice

Bản mẫu (prototype) đạt các tiêu chí sau:

- **User cụ thể chưa?** Đạt: Người dùng Grab Food đang phân vân trước các đánh giá quán.
- **Task đủ hẹp chưa?** Đạt: Phân tích cụm review và hiển thị "Chỉ số nghi vấn Seeding" thời gian thực.
- **AI decision rõ chưa?** Đạt: Random Forest quyết định điểm tin cậy; Gemini quyết định lời khuyên cảnh báo.
- **Failure path rõ chưa?** Đạt: Một quán ăn uy tín bị viral thật (nhiều khách khen cùng lúc) nhưng bị AI nhầm là seeding.
- **Có evidence không?** Đạt: Từ trải nghiệm thực tế về sự trùng lặp ngữ nghĩa review rác.

---

## 5. Quyết định: Giảm scope sang Augmentation

**Tình huống:** Rủi ro gắn cờ sai (False Positive) gây thiệt hại nặng nề cho uy tín của quán ăn là rất cao.

**Quyết định:** Chọn Augmentation (AI gợi ý chỉ số, người dùng là người quyết định cuối). Nhóm tập trung build luồng phát hiện seeding dựa trên sự trùng lặp ngữ nghĩa (Semantic Similarity) vì đây là năng lực mạnh nhất của SBERT trong dự án.

---

## 6. Câu chốt cuối

> Dựa trên bằng chứng về việc review giả mạo gây mất niềm tin của người dùng, nhóm sẽ build **TrustBite AI** (SBERT + Random Forest), cho **người dùng đặt đồ ăn**, để giải quyết **sự thao túng hệ thống đánh giá**, bằng cách **AI Augment việc phân tích sự tương đồng ngữ nghĩa review**, và sẽ test failure path **quán thật bị gắn cờ nhầm do có chiến dịch marketing viral thật sự**.

---

## 7. Backlog

Những thứ không build trong Day 06:

- [ ] Hệ thống xác thực review dựa trên hóa đơn thực tế (Verified Purchase).
- [ ] Giao diện dành riêng cho chủ quán để gửi bằng chứng minh oan (Trust Recovery).
- [ ] Tính năng phân tích mạng lưới seeding dựa trên IP và định danh thiết bị.
- [ ] Tự động báo cáo tài khoản seeding chuyên nghiệp cho nền tảng.
