# Workshop — Mổ App AI Thật

**Thời gian:** 35-45 phút  
**Hình thức:** cá nhân trước, chia sẻ theo nhóm sau  
**Output:** finding note + sketch `as-is / to-be`

Mục tiêu không phải chấm "UI đẹp hay xấu". Mục tiêu là dùng sản phẩm thật như một bài needfinding: tìm chỗ product gãy trong workflow thật, rồi viết finding đó thành quyết định product.

## 1. Chọn một sản phẩm để dùng thử

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| MoMo — Moni | Trợ thủ tài chính, phân tích chi tiêu, chatbot | App MoMo |
| Vietnam Airlines — NEO | Chatbot hỗ trợ vé, hành lý, khiếu nại | Website/Zalo VNA |
| V-App — V-AI | Trợ lý voice/text, gợi ý theo ngữ cảnh | App V-App |

## 2. Dùng thử: Promise vs Reality (AI Moni - MoMo)

### 1. Product hứa gì?

Trở thành một trợ lý ảo thông minh độc quyền của MoMo ("Mình là Moni, trợ lý của MoMo").

Được thiết kế để hỗ trợ quản lý tài chính cá nhân, lập kế hoạch chi tiêu, và giải đáp/hỗ trợ các tác vụ nằm trong hệ sinh thái sản phẩm của MoMo.

### 2. User nào được hứa sẽ được giúp?

Người dùng hệ sinh thái ứng dụng MoMo.

Cụ thể trong bối cảnh này: Những người dùng có nhu cầu quản lý tài chính (muốn phân bổ ngân sách 8 triệu đồng/tháng), hoặc những người dùng muốn tiêu thụ dịch vụ trực tiếp (đặt vé máy bay, vé xem phim).

### 3. Bạn kỳ vọng AI làm được task nào?

- **Task Tài chính:** Lên được một kế hoạch chi tiêu thực tế, biết lắng nghe phản hồi của người dùng để điều chỉnh tỷ lệ phần trăm (nhu cầu thiết yếu, tiết kiệm, giải trí) thay vì chỉ xào nấu các con số ngẫu nhiên.
- **Task Tiện ích MoMo:** Truy xuất được tính năng "Du lịch - Đi lại" (đặt vé máy bay) hoặc "Giải trí" (đặt vé xem phim) vốn là những dịch vụ lõi rất mạnh của nền tảng MoMo.
- **Task Xử lý ngoại lệ (Edge cases):** Bắt lỗi và phản hồi mượt mà khi người dùng cố tình nhập các prompt phi logic (bẫy thời gian) hoặc nhập mã code/đoạn text siêu dài (stress-test giao diện).

### 4. Khi dùng thật, điểm gãy xuất hiện ở đâu?

**Điểm gãy 1 (Thiếu Root-cause Analysis):** Khi người dùng phàn nàn "không hợp lý", AI rơi vào vòng lặp (loop) tự động sinh ra các bảng tính mới một cách máy móc. Trợ lý không biết cách đặt câu hỏi ngược lại để tìm hiểu tại sao người dùng thấy không hợp lý.

**Điểm gãy 2 (Rào cản API/Tool):** Dù xưng là trợ lý của MoMo, nhưng AI hoàn toàn "mù" thông tin về các dịch vụ đang có sẵn trên app, tự tạo ra rào cản ngăn người dùng thực hiện giao dịch sinh lời cho nền tảng.

**Điểm gãy 3 (Xử lý Fallback thô sơ):** Khi bị quá tải bởi các câu hỏi gài bẫy hoặc text rác, AI chỉ có một lớp khiên duy nhất là lặp lại câu giới thiệu bản thân, làm đứt gãy hoàn toàn trải nghiệm hội thoại.

### Bằng chứng thu thập được (Evidence)

**Screenshot / Nguồn:** Trích xuất từ file ghi màn hình `7896794148761_2.mp4`.

**Prompt/Input đã thử:**

- *Test Logic:* "mày chia không đúng", "không thấy chi tiêu hợp lý", "Thứ Sáu là ngày trong tuần, không phải tháng".
- *Test Dịch vụ:* "giá vé máy bay tới cao bằng", "đặt vé xem phim".
- *Test QA (Tràn viền):* Một đoạn mã JSON rất dài chứa nội dung cố tình làm vỡ giao diện (layout-breaking bugs).

**Hành vi quan sát được:**

- AI liên tục render lại các bảng chi tiêu khác nhau từ 00:00 đến 01:03 mà không giải quyết được "nỗi đau" thực sự của user.
- Không có typing indicator, các khối văn bản và bảng biểu (table) dài ngoằng xuất hiện đột ngột gây ngợp thông tin.
- Khi bị nhồi đoạn JSON rác, UI không vỡ (tin tốt), nhưng AI trả lời bằng văn mẫu hoàn toàn lạc đề.

**Quote từ app (Nguyên văn phản hồi của Moni):**

> "Mình là Moni, trợ lý của MoMo. Mình chỉ có thể hỗ trợ trong phạm vi sản phẩm MoMo. Bạn cần giúp gì khác không?"

*(Phản hồi này xuất hiện liên tục khi user đòi đặt vé máy bay/xem phim, và cả khi user ném đoạn text rác vào.)*

## 3. Vẽ 4 paths

| Khía cạnh / Luồng | Lớp Framework | Kỳ vọng (Promise) | Thực tế (Reality) | Bằng chứng / Điểm gãy | Đề xuất tối ưu (Product Decision) |
|---|---|---|---|---|---|
| Happy Path (Luồng lý tưởng) | Promise | Phân bổ ngân sách chi tiêu chính xác, trực quan theo yêu cầu. | Render bảng số liệu nhanh nhưng thô, gây ngợp. | Bảng biểu xuất hiện đột ngột, thiếu hiệu ứng typing indicator để tạo nhịp nghỉ tự nhiên. | Thêm typing indicator (3 dấu chấm nhấp nháy), chia nhỏ thông tin để phân đoạn phản hồi. |
| Low-confidence (Luồng nghi vấn) | Intent | Khi user chê "chia không đúng", AI phải biết dừng lại để hỏi rõ nguyên nhân. | Tự tin đoán mò, liên tục xào nấu lại số liệu cũ một cách máy móc. | Vòng lặp đập đi xây lại bảng tính từ phút 00:00 - 01:03 trong video. | Thiết kế luồng chẩn đoán (Diagnostic Loop): "Bạn thấy khoản nào chưa hợp lý? Cần tăng hay giảm mục nào?" |
| Failure Path (Luồng xử lý lỗi) | Data / Tool | Hỗ trợ các tác vụ lõi của MoMo như tra cứu giá vé, đặt vé xem phim. | Trở thành một mô hình văn bản thuần túy, hoàn toàn "mù" tính năng nội bộ. | Trả lời văn mẫu: "Mình chỉ hỗ trợ trong phạm vi sản phẩm MoMo" khi user hỏi về vé máy bay/phim. | Kích hoạt cơ chế Function Calling (Gọi tool) để kết nối trực tiếp với API dịch vụ của MoMo. |
| Stress-test (An toàn hệ thống) | Safety / Behavior | Nhận diện văn bản rác, mã code độc hại để cảnh báo hoặc từ chối thông minh. | UI giữ được độ ổn định (không crash) nhưng hành vi phản hồi bị sập bẫy. | Bị dính đòn Prompt Injection (phút 01:26), AI lập tức trả lời lạc đề bằng câu chào mặc định. | Cài đặt bộ lọc Guardrail ở tầng Input để chặn text rác hoặc chuỗi ký tự quá dài trước khi gửi tới LLM. |
| Correction Path (Luồng sửa sai) | UX Recovery | Ghi nhớ ngữ cảnh hội thoại cũ để sửa đổi logic (thời gian, con số) theo ý user. | Bị trôi ngữ cảnh (context drift), dễ sa vào vòng lặp tranh cãi câu chữ với người dùng. | Bị rối loạn logic khi user gài bẫy thời gian "tháng kia là tháng sau" hoặc "hôm kia là thứ sáu". | Tăng cường bộ nhớ ngữ cảnh ngắn hạn (Short-term memory) và bổ sung các nút bấm lựa chọn (Chip buttons) để điều hướng nhanh. |

## 4. Viết finding thành quyết định

### 1. Xử lý Vòng lặp đập đi xây lại (Endless Loop)

Khi user phàn nàn "không thấy chi tiêu hợp lý" hoặc "mày chia không đúng",
AI/product tự động sinh ra các bảng tính ngân sách mới một cách máy móc thay vì hỏi rõ nguyên nhân,
hậu quả là user bị kẹt trong vòng lặp vô nghĩa, trôi màn hình và bị ngợp thông tin.
Lỗi thuộc layer **Intent + UX Recovery**.
Nên sửa bằng **UX / fallback**: Thiết kế luồng Low-confidence (hạ độ tự tin). Bot cần dừng việc tạo bảng, hỏi lại "Bạn muốn ưu tiên tăng/giảm mục nào?" và đưa ra 2-3 chip buttons (ví dụ: Ưu tiên tiết kiệm, Ưu tiên ăn uống) để user chọn.

### 2. Xử lý "Mù" Dịch vụ (Service Blindness)

Khi user yêu cầu các tiện ích như "đặt vé xem phim" hoặc "giá vé máy bay tới Cao Bằng",
AI/product từ chối hỗ trợ bằng câu lệnh mặc định "chỉ có thể hỗ trợ trong phạm vi sản phẩm MoMo",
hậu quả là user hụt hẫng, mất niềm tin vào lời hứa "trợ lý MoMo", và nền tảng đánh mất cơ hội chốt giao dịch (transaction).
Lỗi thuộc layer **Promise + Data/Tool**.
Nên sửa bằng **Requirement / Data-tool**: Tích hợp API/Function Calling để AI tra cứu được dịch vụ thực tế, hoặc đơn giản nhất là sửa bằng UX: Bot trả lời và đính kèm deeplink chuyển hướng thẳng đến mini-app Mua vé máy bay/Vé xem phim trên MoMo.

### 3. Xử lý Bẫy Logic Thời Gian (Context Drift)

Khi user cố tình dùng các khái niệm thời gian mẹo như "tháng kia là tháng sau" hoặc "hôm kia là thứ sáu",
AI/product bị cuốn vào việc giải thích và tranh cãi máy móc, quên mất nhiệm vụ chính,
hậu quả là trôi mất ngữ cảnh (context drift) về việc lập ngân sách, gây ức chế cho người dùng.
Lỗi thuộc layer **Intent + UX Recovery**.
Nên sửa bằng **Fallback / UX**: Thiết lập ngưỡng giới hạn tranh luận. Nếu bot nhận thấy vòng lặp giải thích từ ngữ dài quá 2 lượt, bot cần tự động cắt ngang bằng Fallback kéo lại chủ đề chính: "Để Moni lập kế hoạch chính xác nhất, bạn vui lòng nhập ngày tháng theo định dạng (DD/MM) nhé!"

### 4. Xử lý Stress-test Text Rác (Prompt Injection)

Khi user dán một đoạn text/mã JSON khổng lồ vào khung chat để test tràn viền,
AI/product không nhận diện được đây là input bất thường mà chỉ phản hồi bằng câu chào mặc định hoàn toàn lạc đề,
hậu quả là trải nghiệm hội thoại bị đứt gãy, thiếu phản hồi rõ ràng cho user về việc đã vi phạm giới hạn đầu vào.
Lỗi thuộc layer **Safety**.
Nên sửa bằng **Requirement / UX**: Thêm lớp Guardrail chặn độ dài và định dạng input ngay tại client/UI trước khi gửi lên LLM, hiển thị thông báo lỗi hệ thống "Đoạn chat của bạn quá dài hoặc chứa ký tự không hợp lệ".

## 5. Sketch as-is / to-be

| Trạng thái | Luồng As-is (Hiện tại) | Luồng To-be (Đề xuất tối ưu) |
|---|---|---|
| **1. User làm gì?** | Nhập: "Chia ngân sách 8 triệu" | Nhập: "Chia ngân sách 8 triệu" |
| **2. AI làm gì?** | In ra bảng ngân sách ngay lập tức, text dài, chiếm hết màn hình. | Hiển thị typing indicator (đang gõ), sau đó in ra bảng ngân sách tóm tắt gọn gàng. |
| **3. User làm gì?** | Bắt lỗi: "Mày chia không đúng" / "Không hợp lý" | Bắt lỗi: "Mày chia không đúng" / "Không hợp lý" |
| **4. Khi AI không chắc** | **[Điểm gãy]** AI bỏ qua bước chẩn đoán. Tự ý thay đổi các con số ngẫu nhiên và in ra một bảng tính khổng lồ mới. | **[Path đã sửa]** AI hạ độ tự tin, kích hoạt Low-confidence path. AI hỏi lại: "Moni chưa rõ ý bạn. Bạn muốn ưu tiên thay đổi khoản nào?" kèm 3 Chip Buttons: [Tăng Tiết kiệm] / [Giảm Ăn uống] / [Tự chỉnh sửa]. |
| **5. Khi AI sai, User recover thế nào?** | **[Điểm gãy]** User bế tắc, chỉ có thể tiếp tục gõ text phàn nàn. Chat rơi vào vòng lặp (loop) đập đi xây lại liên tục, trôi mất lịch sử hội thoại. | **[Path đã sửa]** User chọn Chip Button hoặc bấm vào nút [Tự chỉnh sửa] ngay trên UI của bảng ngân sách để trực tiếp sửa số. AI cập nhật lại bảng dựa trên đúng điểm user vừa sửa, không vẽ lại từ số 0. |

## 6. Tự kiểm trước khi nộp

- [ ] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [ ] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [ ] Finding được viết thành product decision, không chỉ là nhận xét.
- [ ] Sketch có as-is và to-be.
- [ ] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.
