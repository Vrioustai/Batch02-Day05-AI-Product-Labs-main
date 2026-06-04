# Thin SPEC — TrustBite AI (GrabShield)

---

## 1. Track, product/app và user

- **Track:** Track D - Tự chọn (Lĩnh vực Food & Local Delivery)
- **Product/app thật:** Grab Food (Tích hợp tính năng phát hiện seeding)
- **User cụ thể:** Người dùng Grab Food đang phân vân lựa chọn quán ăn dựa trên đánh giá
- **Nhóm có phải user thật không?** Có, nhóm đóng vai trò là người đặt đồ ăn thường xuyên và trực tiếp trải nghiệm vấn đề review rác

---

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Nhiều review 5 sao có nội dung giống hệt nhau hoặc cùng mô típ ngữ nghĩa. | Tự trải nghiệm/Quan sát | Hệ thống sao hiện tại quá dễ bị thao túng, không còn đáng tin. | Chuyển từ chấm điểm sao đơn thuần sang hiển thị "Chỉ số nghi vấn Seeding". |
| Quán 4.9 sao nhưng thực tế đồ ăn kém chất lượng hoặc ôi thiu. | Review App Store/Cộng đồng | Người dùng cảm thấy bị lừa bởi "vỏ bọc" thuật toán của nền tảng. | Thêm tính năng giải thích lý do nghi ngờ (Explainability) để lấy lại niềm tin. |

---

## 3. Pain statement

User người đặt đồ ăn đang gặp khó ở bước thẩm định chất lượng quán qua review, vì vấn nạn seeding review rác tràn lan làm nhiễu thông tin, dẫn tới trải nghiệm tệ khi nhận đồ ăn và mất niềm tin vào app. Bằng chứng chính là các cụm đánh giá có cấu trúc ngữ nghĩa tương đồng 90% xuất hiện dày đặc.

---

## 4. Build slice

Cho người dùng Grab Food đang xem đánh giá quán, prototype sẽ dùng AI để phân tích sự trùng lặp ngữ nghĩa (SBERT) và tần suất review, tạo ra Chỉ số nghi vấn TrustBite, và xử lý lỗi gắn cờ nhầm quán uy tín bằng cơ chế trích dẫn bằng chứng cụ thể.

---

## 5. Auto/Aug decision

- **Chọn:** Augmentation
- **Lý do chọn:** AI mang tính xác suất, rủi ro gắn cờ sai (False Positive) cho quán thật gây hậu quả uy tín nặng nề. Việc chỉ gợi ý điểm nghi vấn giúp giảm ma sát khi AI sai (cost of reject = 0).
- **Human role:** Decider — Người dùng xem điểm xác suất và tự quyết định có đặt hàng hay không.

---

## 6. Four Paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| **Happy** | AI nhận diện đúng cụm review ảo → Hiện cảnh báo "85% nghi vấn" → User tránh được quán tệ. |
| **Low-confidence** | Dữ liệu review quá ít hoặc mập mờ → AI hiện "Chưa đủ dữ liệu để kết luận". |
| **Failure** | Quán uy tín bị viral thật nhưng AI nhầm là seeding → Hiện nút "Phản hồi/Minh oan" cho chủ quán. |
| **Correction** | User thấy mẫu seeding mới mà AI bỏ sót → User đánh dấu "Báo cáo" → AI học để cập nhật bộ lọc. |

---

## 7. Failure mode nguy hiểm nhất

Nếu một quán ăn uy tín đột ngột chạy chiến dịch Marketing viral thật thu hút nhiều khách **(trigger)**, AI có thể sai lầm gắn cờ "Nghi vấn seeding 90%" **(failure)**, hậu quả là hủy hoại danh tiếng và doanh thu của quán **(impact)**.

Prototype sẽ xử lý bằng **show source** — trích dẫn các review bị coi là giống nhau để user tự đối chứng và tự quyết định. Owner kiểm thử path này là [Tên thành viên phụ trách Test].

---

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| Thành viên 1 | Research / evidence | File `evidence_pack.md` kèm screenshot review rác. |
| Thành viên 2 | SPEC | Bản `thin_spec.md` gồm Canvas và ROI 3 kịch bản. |
| Thành viên 3 | Prototype | Code Random Forest + SBERT + Gemini Agent trên Streamlit. |
| Thành viên 4 | Test / failure path | Bảng kịch bản test 4 paths và kết quả đo Precision (>95%). |
| Thành viên 5 | Demo script / repo | Video quay demo luồng phát hiện seeding thời gian thực. |
