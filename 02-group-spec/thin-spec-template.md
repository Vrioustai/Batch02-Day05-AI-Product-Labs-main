## 1. Track, product/app và user
* **Track:** Track D - Tự chọn (Lĩnh vực Food & Local Delivery).
* **Product/app thật:** Grab Food (Tính năng tích hợp phát hiện seeding).
* **User cụ thể:** Người dùng Grab Food đang phân vân lựa chọn quán ăn dựa trên review.
* **Nhóm có phải user thật không?:** Có, nhóm đóng vai trò là người đặt đồ ăn thường xuyên và đã trực tiếp quan sát thấy vấn đề review rác.

---

## 2. Evidence summary
| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
| :--- | :--- | :--- | :--- |
| Nhiều review 5 sao có nội dung giống hệt nhau ("Ngon, sẽ quay lại"). | Tự trải nghiệm / App Store | Hệ thống sao hiện tại quá dễ bị thao túng, không còn đáng tin. | Chuyển từ chấm điểm sao đơn thuần sang hiển thị "Chỉ số nghi vấn Seeding". |
| Quán 4.9 sao nhưng thực tế giao đồ kém chất lượng. | Group cộng đồng Grab | User cảm thấy bị lừa dối bởi "vỏ bọc" AI/thuật toán của nền tảng. | Thêm tính năng trích dẫn lý do tại sao AI nghi ngờ (*Explainable AI*) để lấy lại niềm tin. |

---

## 3. Pain statement
> 😟 **Pain Statement:**
> Người dùng Grab Food đang gặp khó ở bước thẩm định chất lượng quán qua review, vì vấn nạn seeding review rác tràn lan làm nhiễu loạn thông tin, dẫn tới trải nghiệm tệ khi nhận đồ ăn và mất niềm tin vào nền tảng. 
> 
> *Bằng chứng cốt lõi:* "Đặt quán 4.9 sao mà đồ ăn giao tới như đồ ôi thiu, review toàn nick ảo".

---

## 4. Build slice
Đối với người dùng Grab Food đang xem đánh giá quán ăn, nguyên mẫu (*prototype*) sẽ ứng dụng AI để phân tích ngữ nghĩa và tần suất xuất hiện của review, từ đó tính toán ra **Chỉ số nghi vấn Seeding (0-100%)**, đồng thời kiểm soát lỗi gắn cờ nhầm quán uy tín bằng cơ chế trích dẫn bằng chứng cụ thể.

---

## 5. Auto/Aug decision
* **Lựa chọn:** **Augmentation** *(Tăng cường)*.
* **Lý do chọn:** AI mang tính xác suất (*probabilistic*), rủi ro gắn cờ sai (*False Positive*) cho các quán ăn chân chính là rất lớn. Việc chỉ gợi ý điểm nghi vấn giúp giảm thiểu tối đa ma sát khi AI sai (*cost of reject = 0*).
* **Human role:** **Decider** *(Người dùng xem điểm số xác suất, đọc lý do đối chứng và tự đưa ra quyết định cuối cùng có mua hay không)*.

---

## 6. Four paths
| Path | Prototype phải thể hiện gì? |
| :--- | :--- |
| **Happy** | AI nhận diện đúng cụm review ảo $\rightarrow$ Hiển thị cảnh báo "Nghi vấn seeding 85%" $\rightarrow$ User chủ động tránh được quán tệ. |
| **Low-confidence** | Review có dấu hiệu lạ nhưng chưa đủ bằng chứng $\rightarrow$ AI hiển thị trạng thái "Chưa đủ dữ liệu để kết luận". |
| **Failure** | Một quán uy tín bỗng dưng viral thật nhưng AI nhầm là seeding $\rightarrow$ Hiển thị thêm nút "Báo cáo gắn cờ sai" để quán gửi yêu cầu minh oan. |
| **Correction** | User phát hiện mẫu seeding tinh vi mới mà AI bỏ sót $\rightarrow$ User chủ động đánh dấu "Review rác" $\rightarrow$ Hệ thống ghi nhận để AI học và cập nhật bộ lọc. |

---

## 7. Failure mode nguy hiểm nhất
> ⚠️ **Rủi ro cốt lõi:**
> Nếu user đang xem một quán ăn uy tín vừa mới chạy chiến dịch marketing viral (**trigger**), AI có thể sai lầm gắn cờ "Nghi vấn seeding 90%" (**failure**). Hậu quả là gây thiệt hại uy tín và doanh thu nghiêm trọng cho quán (**impact**).
> 
> *Giải pháp xử lý:* Prototype bắt buộc phải triển khai cơ chế **Show source** (trích dẫn các cụm review bị coi là giống nhau để user tự đối chứng trực quan).
> *Owner phụ trách kiểm thử path này:* [Tên thành viên phụ trách Test].

---

## 8. Owner plan cho sáng Day 06
| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
| :--- | :--- | :--- |
| **Tài** | Research / evidence | File `evidence_pack.md` kèm screenshot review rác thực tế. |
| **Thảo** | SPEC | Bản `lightweight_spec.md` gồm Canvas và ROI cho 3 kịch bản. |
| **Đức** | Prototype | Kịch bản Prompt / Logic xử lý so sánh ngữ nghĩa các cụm review. |
| **Huy** | Test / failure path | Bảng kịch bản kiểm thử 4 paths và thiết lập ngưỡng Precision mục tiêu (>95%). |
