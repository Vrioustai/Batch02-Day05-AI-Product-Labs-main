# Template — Evidence Pack

Nộp kèm thin SPEC cuối Day 05.

---

## 1. Nhóm và track

- **Tên nhóm:** TrustBite AI (GrabShield)
- **Track:** Track D - Tự chọn (Lĩnh vực Food & Local Delivery)
- **Product/app đã chọn:** Grab Food (Tính năng tích hợp phát hiện seeding)
- **Build slice đang nghĩ:** Hệ thống hiển thị "Chỉ số nghi vấn Seeding" (Probability Score) thời gian thực trên giao diện review của quán ăn

---

## 2. Self-use evidence

Nhóm tự dùng app GrabFood và ghi lại điểm gãy trong hệ thống tin cậy hiện tại.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
| Nhiều đánh giá 5 sao cho một quán có nội dung lặp lại về mặt ngữ nghĩa dù từ ngữ khác nhau. | [Link ảnh từ Repo] | Failure | Cần dùng Vietnamese SBERT để bắt được sự trùng lặp ngữ nghĩa mà bộ lọc từ khóa truyền thống bỏ sót. |
| Một quán bị "phốt" đột ngột có hàng loạt review khen cùng một mô típ xuất hiện trong thời gian ngắn. | [Link ảnh từ Repo] | Low-confidence | Tần suất và nội dung review là tín hiệu cốt lõi để tính toán xác suất seeding. |

---

## 3. User / review / social evidence

Nguồn: Review trên App Store và các group cộng đồng người dùng Grab.

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| "Đặt quán 4.9 sao mà đồ ăn giao tới ôi thiu, xem kỹ mới thấy toàn nick ảo khen lấy lệ." | App Store Review | Người dùng đặt đồ ăn | Mất niềm tin (Trust breakdown) do hệ thống sao bị thao túng. |
| "Nhiều quán uy tín bị đối thủ seeding 1 sao hàng loạt gây thiệt hại doanh thu." | Group Cộng đồng | Chủ cửa hàng | Rủi ro gắn cờ sai (False Positive) ảnh hưởng đến uy tín kinh doanh. |

> Đây là giả định dựa trên quan sát thực tế vấn nạn seeding. Nhóm sẽ kiểm chứng bằng bảng khảo sát 5-10 người dùng thường xuyên trước checkpoint M1 Day 06.

---

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| **Yelp** | Hiển thị "Consumer Alert" khi có hoạt động đánh giá bất thường. | Warning path: Cảnh báo thay vì chặn hoàn toàn. | Có, thiết kế tag cảnh báo trên UI. |
| **Fakespot (Amazon)** | Phân tích review và chấm điểm tin cậy từ A đến F. | Scoring: Chuyển từ nhãn Đúng/Sai sang thang điểm xác suất. | Có, dùng mô hình Random Forest để tính điểm. |

---

## 5. Evidence → Insight

**Evidence nổi bật nhất:** Người dùng cảm thấy bị lừa bởi "vỏ bọc" 5 sao nhưng không muốn hệ thống tự ý ẩn quán vì họ muốn tự kiểm chứng lý do.

**Insight:** User không chỉ gặp vấn đề về quán ăn tệ (surface problem). Thật ra họ cần sự minh bạch (transparency) và căn cứ xác thực (explainability) để hỗ trợ ra quyết định an toàn.

**Opportunity:** AI có thể giúp bằng cách Augment (Tăng cường) khả năng thẩm định review, đưa ra chỉ số nghi vấn và trích dẫn bằng chứng qua Agent Gemini.

---

## 6. Evidence đổi SPEC như thế nào?

- [ ] Đổi user chính
- [ ] Đổi pain statement
- [ ] Đổi build slice
- [x] Đổi Auto/Aug decision
- [x] Đổi 4 paths
- [x] Đổi failure mode

### Ghi rõ 1-2 thay đổi quan trọng

- **Trước evidence, nhóm định:** Tự động ẩn các review nghi ngờ seeding (Automation).
- **Sau evidence, nhóm đổi thành:** Gắn cờ nghi vấn và hiển thị điểm xác suất (Augmentation).
- **Lý do:** Do AI mang tính xác suất và rủi ro gắn cờ sai cho quán uy tín là thảm họa. Việc chọn Augmentation giúp giảm ma sát khi AI sai và để người dùng là người đưa ra quyết định cuối cùng (HITL).
