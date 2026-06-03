# Tài Liệu Phạm Vi Dự Án: TrustBite AI (GrabShield)

## 1. Nhóm và Track
* **Tên nhóm:** TrustBite AI (GrabShield)
* **Track:** Track D - Tự chọn (Lĩnh vực Food & Local Delivery)
* **Product/App đã chọn:** Grab Food (Tính năng tích hợp gắn cờ đánh giá giả mạo)
* **Build Slice đang nghĩ:** Hệ thống hiển thị "Chỉ số nghi vấn Seeding" (*Seeding Probability Score*) thời gian thực trên giao diện review của quán ăn.

---

## 2. Self-use Evidence
*Nhóm tự dùng app GrabFood và ghi lại điểm gãy trong hệ thống tin cậy hiện tại.*

| Observation (Quan sát) | Screenshot/Link | Path liên quan | Điều học được |
| :--- | :--- | :--- | :--- |
| Nhiều đánh giá 5 sao cho một quán mới mở có nội dung giống hệt nhau ("Món ăn ngon, sẽ quay lại"). | [Link ảnh 1] | Failure | Hệ thống hiện tại không lọc được seeding theo cụm ngữ nghĩa giống nhau. |
| Một quán bị phốt trên mạng đột ngột có hàng trăm review 5 sao trong 30 phút để "đẩy sao". | [Link ảnh 2] | Low-confidence | Thời điểm (*timestamp*) là tín hiệu cực kỳ quan trọng để phát hiện bất thường. |

---

## 3. User / Review / Social Evidence
*Nguồn: Review trên App Store và các group cộng đồng người dùng Grab.*

| Quote / Review / Observation | Nguồn | User là ai? | Pain / Failure Mode |
| :--- | :--- | :--- | :--- |
| "Đặt quán 4.9 sao mà đồ ăn giao tới như đồ ôi thiu, đọc kỹ lại mới thấy review toàn nick ảo khen lấy lệ." | App Store Review | Người dùng bận rộn | Mất niềm tin (*Trust breakdown*) do hệ thống số sao (*star system*) bị thao túng. |
| "Nhiều quán làm ăn chân chính bị đối thủ seeding 1 sao hàng loạt mà không có cách nào minh oan với Grab." | Group Tài xế & Chủ quán | Chủ cửa hàng | *False Positive* của hệ thống hiện tại gây thiệt hại kinh doanh trực tiếp. |

> 💡 **Ghi chú của nhóm:** Đây là giả định dựa trên 10 review tiêu cực về độ tin cậy trên App Store. Nhóm sẽ tiến hành phỏng vấn nhanh 5 người dùng thường xuyên trước checkpoint M1 Day 06.

---

## 4. Competitor / Analog Evidence

| App / Mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
| :--- | :--- | :--- | :--- |
| **Yelp** | Hiển thị "Consumer Alert" khi phát hiện hoạt động đánh giá bất thường. | **Warning path:** Cảnh báo thay vì chặn/ẩn hoàn toàn. | **Có**, thiết kế tag cảnh báo trực quan trên UI. |
| **Fakespot (Amazon)** | Phân tích review và chấm điểm tin cậy từ A đến F. | **Scoring:** Chuyển từ nhãn Đúng/Sai (Binary) sang thang điểm xác suất. | **Có**, dùng LLM để tính toán *Probability Score*. |

---

## 5. Evidence -> Insight

* **Evidence nổi bật nhất:** Người dùng cảm thấy bị lừa bởi "vọc bọc" 5 sao nhưng họ không muốn hệ thống tự ý ẩn quán/review vì họ vẫn muốn giữ quyền tự kiểm chứng.
* **Insight:** User không chỉ gặp vấn đề về việc chọn phải quán ăn tệ (*surface problem*). Thật ra họ cần **minh bạch hóa thông tin (transparency)** và **sự hỗ trợ ra quyết định (decision support)** để cảm thấy mình luôn nắm quyền kiểm soát tình huống [8].
* **Opportunity:** AI có thể giúp bằng cách **Augment (Tăng cường)** khả năng đọc hiểu review, đưa ra chỉ số nghi vấn và trích dẫn lý do khách quan tại sao tập hợp review đó bị coi là giả mạo [9].

---

## 6. Evidence đổi SPEC như thế nào?

* [ ] Đổi user chính.
* [ ] Đổi pain statement.
* [ ] Đổi build slice.
* [x] **Đổi Auto/Aug decision.**
* [x] **Đổi 4 paths.**
* [x] **Đổi failure mode.**
* [ ] Đổi owner/test plan.

### Ghi rõ 1-2 thay đổi quan trọng:
* **Trước evidence, nhóm định:** Tự động ẩn toàn bộ các review bị nghi ngờ seeding (*Automation*).
* **Sau evidence, nhóm đổi thành:** Chỉ gắn cờ cảnh báo và hiển thị điểm xác suất (*Augmentation*).
* **Lý do:** Do đặc tính của AI mang tính xác suất và rủi ro gắn cờ sai (*False Positive*) cho các quán uy tín là rất cao. Việc lựa chọn mô hình *Augmentation* giúp giảm thiểu ma sát khi AI nhận diện sai, đồng thời duy trì niềm tin cốt lõi của cả người dùng lẫn chủ quán [10, 11].