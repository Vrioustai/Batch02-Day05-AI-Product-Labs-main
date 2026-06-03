# Định Hướng Chiến Lược Dự Án: TrustBite AI (GrabShield) - Giai Đoạn Phát Triển

## 1. Phân Cụm Bằng Chứng (Evidence Clustering)
*Thay vì liệt kê tính năng, bằng chứng được gom nhóm trực tiếp dựa trên nỗi đau (pain) và hành vi thực tế của người dùng:*

* **"Treo đầu dê bán thịt chó":** Người dùng đặt trọn niềm tin vào điểm số 4.9 - 5 sao của quán nhưng thực tế nhận lại đồ ăn ôi thiu, kém chất lượng.
* **"Review rác tràn lan":** Xuất hiện hàng loạt các bình luận có nội dung, cú pháp giống hệt nhau, không mang lại bất kỳ giá trị tham khảo nào cho người mua sau.
* **"Sợ bị gắn cờ oan":** Các chủ cửa hàng lo lắng hệ thống quét tự động của Grab có thể khóa nhầm quán khi lượng khách ủng hộ thực tế tăng đột biến (ví dụ: quán bỗng dưng viral).

---

## 2. Insight Khách Hàng (User Insight)
> 💡 **Core Insight:**
> Người dùng ứng dụng giao đồ ăn không chỉ đơn thuần cần nhìn vào điểm số sao trung bình của một quán. Thứ họ thực sự cần là **sự minh bạch** và **căn cứ xác thực** để hỗ trợ ra quyết định. Nhiều bằng chứng thực tế cho thấy hệ thống đánh giá bằng sao hiện tại đang bị thao túng dễ dàng bởi các kỹ thuật seeding tinh vi, làm đổ vỡ nghiêm trọng niềm tin vào nền tảng.

---

## 3. Cơ Hội Sản Phẩm (Product Opportunity)
* **Giải pháp đột phá:** Dùng AI để **Augment (Tăng cường)** khả năng đọc hiểu và phân tích tính xác thực của review, giúp user chủ động né tránh các "bẫy" seeding.
* **Kiểm soát rủi ro:** Giảm thiểu tối đa tỷ lệ gắn cờ sai (*False Positive*) bằng cách **chỉ hiển thị điểm số xác suất nghi vấn và trích dẫn lý do khách quan**, thay vì để hệ thống tự ý ẩn review của quán mà không có sự đồng ý của con người.

---

## 4. Xác Định Phân Đoạn Xây Dựng (Build Slice Validation)
*Kiểm tra tính khả thi của phân đoạn qua bộ 5 câu hỏi cốt lõi để chốt phạm vi:*

* [x] **User cụ thể chưa?** Đạt — Người dùng Grab Food đang trực tiếp xem review quán ăn.
* [x] **Task đủ hẹp chưa?** Đạt — Chỉ tập trung phân tích sự trùng lặp ngữ nghĩa và gắn cờ nghi vấn cho review.
* [x] **AI decision rõ chưa?** Đạt — AI chịu trách nhiệm tính toán và hiển thị "Chỉ số nghi vấn Seeding" (*Seeding Probability Score*).
* [x] **Failure path rõ chưa?** Đạt — Xử lý trường hợp quán ăn uy tín bị viral thật sự nhưng AI nhầm tưởng là hoạt động seeding.
* [x] **Có evidence không?** Đạt — Dựa trên đánh giá thực tế từ App Store và phản hồi trực tiếp từ các chủ quán.

---

## 5. Quyết Định Phạm Vi (Scope Decision)
* **Tình huống rủi ro:** Nguy cơ gắn cờ sai gây thiệt hại trực tiếp đến uy tín và doanh thu của các quán ăn chân chính là rất cao.
* **Quyết định:** Lựa chọn mô hình **Augmentation** *(AI gợi ý/phân loại, user quyết định cuối)*. 
* **Hành động cụ thể:** Chủ động **giảm scope** xuống, chỉ tập trung vào việc phát hiện seeding dạng nội dung lặp lại (*semantic similarity*) vì đây là bằng chứng trực quan, dễ thấy và khả thi nhất để hoàn thiện demo trong vòng 1 ngày.

---

## 6. Tuyên Bố Định Hướng Cốt Lõi (Core Mission Statement)
> 🎯 **Câu chốt dự án:**
> Dựa trên bằng chứng về việc review giả mạo gây mất tiền và niềm tin của người dùng, nhóm sẽ xây dựng nguyên mẫu hệ thống gắn cờ nghi vấn seeding kèm điểm xác suất cho người dùng Grab Food để giải quyết sự thao túng hệ thống đánh giá, bằng cách ứng dụng AI **Augment** việc phân tích ngữ nghĩa các cụm review, đồng thời tập trung kiểm thử kỹ lưỡng *failure path* khi một quán ăn uy tín bị gắn cờ nhầm do có lượng khách ủng hộ đột biến.

---

## 7. Danh Sách Tạm Hoãn (Backlog - Out of Scope cho Day 06)
*Các tính năng và luồng xử lý dữ liệu phức tạp sẽ không được xây dựng trong giai đoạn này:*

* [ ] Hệ thống xác thực review dựa trên đối chiếu hóa đơn thực tế và định vị GPS (Dữ liệu thực).
* [ ] Giao diện quản trị dành riêng cho chủ quán để đối chất, gửi bằng chứng minh oan (*Trust Recovery*).
* [ ] Cơ chế tự động khóa/chặn tài khoản của các "seeders" chuyên nghiệp hoặc tài khoản ảo.
* [ ] Thuật toán phân tích lịch sử đánh giá xuyên suốt nhiều quán để truy quét mạng lưới seeding quy mô lớn.