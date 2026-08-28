# Operating Dashboard — ShopSense AI

> Worksheet nguồn để validator và rubric truy vết evidence. Bản vận hành rút gọn
> nằm ở `one-page-dashboard.md` cùng thư mục; không ép bảng 12 cột này lên một trang.

- Học viên: Cao Thị Thu Trang
- Mã học viên: 2A202601885
- Mô hình: B2B
- Cập nhật: 2026-08-28
- North Star: Median time-to-first-value ≤ 7 ngày trên cohort tuần

## Chẩn đoán mô hình

ShopSense AI là B2B vì bên trả tiền là các chủ shop e-commerce SME Việt Nam có doanh thu 100–800 triệu ₫/tháng và 1–5 nhân viên chăm sóc khách hàng, chính chủ shop và nhân viên của họ là người cấu hình catalog, tông giọng và luật escalation rồi vận hành trợ lý mỗi ngày, còn ShopSense không giữ thương hiệu hay quan hệ độc lập với người mua hàng cuối vì họ chỉ nhắn tin trong khung chat mang tên shop trên Shopee, TikTok Shop và Messenger. Chúng tôi không có bề mặt trực tiếp và không sở hữu dữ liệu định danh của người dùng cuối, nên theo mục 2.5 của sổ tay đây là chẩn đoán B2B chứ không phải B2B2C.

| Dữ liệu đầu vào | Trạng thái | Nằm ở đâu hoặc cần gì để đo | Ngày có số |
|---|---|---|---|
| Unit economics Day 24 | ĐO ĐƯỢC | File CaoThiThuTrang_Day24.xlsx (3 tab), đã ẩn dữ liệu khách: ARPU 499.000 ₫, CAC 1.200.000 ₫, GM 81%, churn 6%, payback 3,0 tháng | 2026-08-28 |
| Value Metric và Cost/Job Day 25 | ĐO ĐƯỢC | File CaoThiThuTrang_Day25_model.xlsx (6 tab): Value Metric Hybrid, Cost/Job 294 ₫, GM 67,3%, breakeven containment 63,9% | 2026-08-28 |

## Kiểm kê đèn ứng viên

Mở bảng đèn B2B trong handbook, copy đủ 11 đèn và đánh dấu đúng một trạng thái cho từng đèn theo dữ liệu ShopSense AI hôm nay.

| Đèn ứng viên từ handbook | Tầng | Trạng thái | Bằng chứng hiện có hoặc kế hoạch đo |
|---|---|---|---|
| Time-to-first-value (TTFV) | L | ✅ | Event kích hoạt gói và mốc 20 hội thoại containment đạt QA đã có trong onboarding log |
| Pipeline coverage | L | ❌ | Kênh PLG self-serve, không có pipeline sales; thay bằng phễu dùng thử ở O-01 |
| % deal chết ở khâu security/procurement | L | ❌ | SME tự mua qua thẻ, không có khâu procurement; không áp dụng |
| POC → paid | O | 🔧 | Đổi thành trial→paid; cần chốt định nghĩa cohort dùng thử 14 ngày trước 2026-09-15 |
| Sales cycle (ngày) | O | ❌ | PLG không có chu kỳ bán; thay bằng channel connect rate 72h ở L-02 |
| Usage depth trong tài khoản | O | 🔧 | Cần event 'ai_reply_sent' và 'human_reply_sent' theo shop trước 2026-09-20 |
| Chi phí triển khai ÷ ACV | O | 🔧 | Onboarding self-serve; cần gắn giờ CS hỗ trợ với shop_id trước 2026-09-20 |
| Tập trung doanh thu | O | ✅ | Billing export theo shop, shop lớn nhất hiện chiếm 4% MRR |
| NRR | G | 🔧 | Đủ hai cohort quý vào 2027-02-28 |
| Gross Margin | G | ✅ | Billing export ghép token log Day 25, GM hiện tại 67,3% |
| CAC payback | G | ✅ | Mô hình Day 24, payback base 3,0 tháng |

## Đèn báo sớm

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| L-01 | Time-to-first-value (TTFV) | Số ngày từ khi shop kích hoạt gói Growth đến khi trợ lý AI tự xử lý trọn vẹn (containment) 20 hội thoại khách thật đạt QA nội bộ; lấy median theo cohort tuần | TUẦN · PRODUCT OPS | 9 ngày | ≤7 ngày | 8–14 ngày | >14 ngày | [TB] Chưa có chuẩn ngành cho SME đa kênh VN; dùng 2 cohort đầu làm chuẩn tạm và chốt baseline sau 4 cohort. Ranh giới 7 ngày đặt bằng nửa chu kỳ thanh toán tháng để shop thấy giá trị trước kỳ trừ tiền đầu tiên | 2026-08-28 | Trial→paid (O-01) và logo churn năm đầu (G-01) | R-01 |
| L-02 | Channel connect rate 72h | (Số shop mới kết nối ≥1 kênh Shopee, TikTok Shop hoặc Messenger và bật AI trả lời tự động trong 72 giờ) ÷ (số shop bắt đầu dùng thử trong kỳ) | NGÀY · GROWTH | 61% | ≥80% | 60–79% | <60% | [TB] Đo 4 tuần bằng event 'channel_connected' rồi chốt baseline. Ngưỡng 80% chọn vì shop không kết nối trong 72h đầu gần như không quay lại theo quan sát onboarding thủ công hiện tại | 2026-08-28 | Time-to-first-value (L-01) | R-01 |
| L-03 | Containment rate | (Số hội thoại end-user AI xử lý đến kết thúc không có tin nhắn nào của nhân viên shop) ÷ (tổng hội thoại end-user hợp lệ trong 7 ngày); loại spam và tin nhắn broadcast | TUẦN · PRODUCT OPS | 78% | ≥75% | 64–74% | <64% | [TB] Đo 4 cohort rồi chốt baseline. Ranh giới đỏ 64% neo theo breakeven containment 63,9% tính ở Day 25: dưới mức này phần escalate ăn hết lãi gộp của phần AI tự xử lý | 2026-08-28 | Gross margin sau chi phí AI và logo churn (G-01) | R-02 |

## Đèn vận hành

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| O-01 | Trial→paid conversion | (Số shop kích hoạt thanh toán gói Growth trong vòng 14 ngày sau khi hết dùng thử) ÷ (số shop kết thúc dùng thử trong tháng) | THÁNG · GROWTH | 22% | ≥30% | 20–29% | <20% | [BM] RevenueCat State of Subscription Apps 2026 (công bố 19/03/2026), trial→paid app AI = 8,5%, https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026 , kiểm tra 2026-08-28; dùng 8,5% làm sàn tham chiếu, đặt mục tiêu 30% cao hơn vì SME chủ động tìm giải pháp CSKH nên ý định mua rõ hơn app tiêu dùng | 2026-08-28 | Net new MRR (G-02) | R-03 |
| O-02 | Chi phí AI trên mỗi hội thoại | Tổng chi phí LLM API (token input và output, gồm retry) ÷ số hội thoại AI xử lý đạt QA trong tuần; không gồm infra và giờ QA nội bộ | TUẦN · FINOPS | 200 ₫ | ≤170 ₫ | 171–270 ₫ | >270 ₫ | [MH] MH-01 suy trần 170 ₫ từ giá overage 900 ₫, GM mục tiêu 70% và chi phí biến đổi phi-AI 100 ₫; trên 270 ₫ thì lãi gộp biên của hội thoại overage về 0 | 2026-08-28 | Gross margin sau chi phí AI (Day 24) | R-04 |

## Đèn kết quả

| ID | Đèn | Định nghĩa và công thức | Nhịp · Owner | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn | Ngày kiểm tra | Báo trước cho | Luật |
|---|---|---|---|---:|---|---|---|---|---|---|---|
| G-01 | Monthly logo churn | (Số shop huỷ gói trả phí trong tháng) ÷ (số shop trả phí đầu tháng); loại shop tạm ngưng theo mùa vụ dưới 30 ngày | THÁNG · FINANCE | 6% | ≤6% | 6,1–9,3% | >9,3% | [MH] MH-02 suy trần churn 9,3%/tháng từ CAC 1.200.000 ₫, LTV/CAC ≥ 3, ARPU 499.000 ₫ và GM 67,3%; vượt mức này thì LTV/CAC tụt dưới 3 và payback vượt 12 tháng | 2026-08-28 | LTV/CAC và CAC payback (Day 24) | R-05 |
| G-02 | Net new MRR mỗi tháng | MRR cuối kỳ trừ MRR đầu kỳ, bằng (MRR mới cộng MRR mở rộng) trừ (MRR huỷ cộng MRR co lại), theo tháng, đơn vị triệu ₫ | THÁNG · FINANCE | +18 triệu ₫ | ≥+25 triệu ₫ | +5 đến +24 triệu ₫ | dưới +5 triệu ₫ | [TB] Chưa đủ 2 quý lịch sử; đo 2 quý rồi chốt baseline. Ngưỡng +25 triệu ₫ ứng với khoảng 50 shop trả phí mới ròng mỗi tháng, nhịp cần để đạt kế hoạch ARR trong mô hình Day 24 | 2026-08-28 | ARR và NPV (Day 24) | R-05 |

## Luật quyết định

| ID | NẾU | TRONG | VÀ | THÌ | KHÔNG THÌ | Luật dừng? |
|---|---|---|---|---|---|---|
| R-01 | Median TTFV > 14 ngày | 2 cohort tuần liên tiếp | mỗi cohort có ≥ 8 shop go-live | Đóng băng nhận shop dùng thử mới trong 14 ngày và cắt phạm vi onboarding còn 1 kênh và 1 nhóm sản phẩm cho tới khi TTFV về ≤ 10 ngày | Không tăng ngân sách quảng cáo để kéo thêm shop khi phễu onboarding đang tắc | CÓ |
| R-02 | Containment rate < 64% | 3 tuần liên tiếp | có ≥ 1.000 hội thoại end-user hợp lệ mỗi tuần | Dừng bật AI tự động cho shop mới, khoá phạm vi trả lời về đúng 3 intent an toàn nhất và sửa prompt cùng nguồn RAG trong 1 sprint | Không bỏ bước QA nội bộ để containment trông cao hơn | CÓ |
| R-03 | Trial→paid < 20% | 2 chu kỳ dùng thử liên tiếp (khoảng 8 tuần) | có ≥ 40 shop kết thúc dùng thử trong kỳ | Chuyển 1 product owner sang làm activation, rút wizard cấu hình còn 3 bước và nạp sẵn mẫu catalog theo ngành hàng | Không giảm giá gói Growth để ép chuyển đổi khi shop chưa đạt first value | KHÔNG |
| R-04 | Chi phí AI mỗi hội thoại > 270 ₫ | 2 tuần liên tiếp | có ≥ 5.000 hội thoại AI xử lý trong kỳ | Giới hạn context window, hạ model tier cho intent đơn giản và đàm phán lại quota API trước kỳ billing kế tiếp | Không tắt retry hoặc QA để chi phí trông thấp hơn | CÓ |
| R-05 | Monthly logo churn > 9,3% | 2 tháng liên tiếp | cohort có ≥ 30 shop trả phí | Chuyển toàn bộ roadmap tháng kế sang 3 nguyên nhân huỷ lớn nhất có evidence từ phỏng vấn offboarding | Không tăng ngân sách acquisition để bù số shop rời đi | KHÔNG |

## Cổng gác 90 ngày

| Ngày | Metric gác cổng | Ngưỡng | Bằng chứng vật lý | Nếu đạt | Nếu trượt |
|---:|---|---|---|---|---|
| 30 | Baseline TTFV từ cohort go-live đầu tiên (learning: đã đo được, không phải kế hoạch đo) | ≥ 10 shop có số TTFV thật và định nghĩa "first value" đã chốt | Cohort sheet và event log 'containment_qa_passed' | GO | FIX |
| 60 | Trial→paid conversion (O-01) — bằng chứng shop trả tiền thật sau khi dùng | ≥ 20% trên ≥ 30 shop kết thúc dùng thử | Cohort billing report xuất từ hệ thống thanh toán | GO | PIVOT |
| 90 | Gross margin sau chi phí AI (metric kinh tế đơn vị, nối Day 24) | ≥ 60% trên ≥ 20.000 hội thoại | Billing export, token log và QA report | GO | KILL |

## Kill criteria

KILL hướng sản phẩm vào ngày 90 nếu sau 1 vòng FIX mà median TTFV vẫn > 14 ngày, hoặc gross margin sau chi phí AI vẫn < 50% trên mẫu ≥ 20.000 hội thoại, đồng thời chưa có ≥ 30 shop trả phí giữ được churn ≤ 9,3%/tháng trong 2 tháng liên tiếp.

## Chưa đo được

| Đèn hoặc giả định | Cần gì để đo | Ai chịu trách nhiệm | Ngày có số |
|---|---|---|---|
| Containment rate tách theo intent (hỏi đơn hàng, đổi trả, tư vấn sản phẩm) | Gắn nhãn intent cho log hội thoại và đối chiếu điểm escalate | Product Ops | 2026-09-20 |
| p95 chi phí token theo từng shop (đuôi shop dùng nặng) | Bảng token log theo shop_id tách input và output, đủ 4 tuần dữ liệu | FinOps | 2026-09-30 |

## Phụ lục ngưỡng suy từ mô hình

| ID | Metric | Input Day 24–25 | Phép tính | Kết quả và ngưỡng áp dụng |
|---|---|---|---|---|
| MH-01 | Trần chi phí inference mỗi hội thoại | Giá overage 900 ₫/hội thoại; GM mục tiêu 70% (sàn pessimistic Day 24 là 67,7%); chi phí biến đổi phi-AI 100 ₫/hội thoại gồm infra, retry 6% và QA HITL 5% từ Day 25 | 900 × (1 − 0,70) − 100 = 170 | Trần 170 ₫/hội thoại; áp cho O-02: 🟢 ≤170 ₫, 🟡 171–270 ₫, 🔴 >270 ₫ |
| MH-02 | Trần churn tháng của shop | CAC 1.200.000 ₫ (Day 24 base); LTV/CAC mục tiêu ≥ 3 (Bessemer, Day 24); ARPU 499.000 ₫/tháng; gross margin 67,3% (Day 25) | LTV tối thiểu = 3 × 1.200.000 = 3.600.000 ₫; lãi gộp mỗi tháng = 499.000 × 0,673 = 335.827 ₫; số tháng khách cần ở lại = 3.600.000 ÷ 335.827 = 10,7; churn tối đa = 1 ÷ 10,7 = 9,3%/tháng | Churn ≤ 9,3%/tháng; áp cho G-01: 🟢 ≤6%, 🟡 6,1–9,3%, 🔴 >9,3% |

## Ghi nhận AI critique

| Phản biện | Chấp nhận hay bác bỏ | Thay đổi đã thực hiện | Lý do |
|---|---|---|---|
| L-02 channel connect chỉ là bước thao tác, không phải tín hiệu giá trị, dễ bị nhầm là Leading ngang hàng TTFV | CHẤP NHẬN | Giữ L-02 nhưng hạ vai trò: chỉ báo trước cho L-01, North Star vẫn khoá ở TTFV | Channel connect dự báo TTFV nhưng không dự báo trực tiếp renewal hay doanh thu |
| Ngưỡng trial→paid 30% cao hơn benchmark app AI 8,5% gấp ba lần nên đèn gần như luôn đỏ | BÁC BỎ | Không đổi ngưỡng; ghi rõ 8,5% là sàn tham chiếu và nêu lý do đặt mục tiêu cao hơn cho SME có ý định mua rõ | Giữ mục tiêu tham vọng để không tự ru ngủ; PLG SME khác tập người dùng tò mò của app tiêu dùng |
| Containment đỏ dưới 64% chỉ là con số Day 25, chưa đo lại trên môi trường đa kênh thật | CHẤP NHẬN | Gắn nguồn [TB] cho L-03 và thêm mục "Chưa đo được" cho containment theo intent, hạn 2026-09-20 | Breakeven 63,9% là điểm khởi đầu hợp lệ nhưng phải xác nhận bằng dữ liệu vận hành thật |
