# Operating Dashboard — ShopSense AI

> Trang 1 để xuất PDF. Mọi giá trị khớp worksheet nguồn `operating-dashboard.md`;
> chi tiết nguồn và hai phép tính [MH] nằm ở phụ lục trang 2.

**Model:** B2B · **Cập nhật:** 2026-08-28 · **Owner phiên họp:** Product Ops

**Chẩn đoán:** Chủ shop e-commerce SME Việt Nam trả tiền · nhân viên chăm sóc khách của shop dùng · ShopSense không có bề mặt hay dữ liệu định danh với người mua cuối (chat mang tên shop) → B2B.

**North Star:** Median time-to-first-value · hiện tại 9 ngày · mục tiêu ≤ 7 ngày · trạng thái 🟡

## Cây đèn 3 tầng

| Tầng · ID | Metric và định nghĩa ngắn | Hiện tại · 🟢 / 🟡 / 🔴 · Nguồn | Nhịp · Owner | Báo trước cho · Luật |
|---|---|---|---|---|
| L · L-01 | TTFV: ngày từ kích hoạt đến 20 hội thoại containment đạt QA (median cohort) | 9 ngày · ≤7 / 8–14 / >14 ngày · [TB] | TUẦN · Product Ops | Trial→paid, churn năm đầu · R-01 |
| L · L-02 | Channel connect 72h: % shop bật ≥1 kênh và AI tự trả lời trong 72 giờ | 61% · ≥80% / 60–79% / <60% · [TB] | NGÀY · Growth | TTFV · R-01 |
| L · L-03 | Containment: % hội thoại AI đóng không cần nhân viên shop (7 ngày) | 78% · ≥75% / 64–74% / <64% · [TB] | TUẦN · Product Ops | GM sau AI, churn · R-02 |
| O · O-01 | Trial→paid: % shop hết dùng thử kích hoạt thanh toán trong 14 ngày | 22% · ≥30% / 20–29% / <20% · [BM] | THÁNG · Growth | Net new MRR · R-03 |
| O · O-02 | Chi phí AI/hội thoại: token LLM API (gồm retry) ÷ hội thoại đạt QA | 200 ₫ · ≤170 / 171–270 / >270 ₫ · [MH] | TUẦN · FinOps | Gross margin · R-04 |
| G · G-01 | Monthly logo churn: shop huỷ trong tháng ÷ shop trả phí đầu tháng | 6% · ≤6% / 6,1–9,3% / >9,3% · [MH] | THÁNG · Finance | LTV/CAC, payback · R-05 |
| G · G-02 | Net new MRR: MRR cuối kỳ − MRR đầu kỳ (triệu ₫/tháng) | +18 tr · ≥+25 / +5..+24 / <+5 tr ₫ · [TB] | THÁNG · Finance | ARR, NPV · R-05 |

## Luật quyết định

| ID | NẾU · TRONG · VÀ | THÌ | KHÔNG THÌ | Dừng? |
|---|---|---|---|---|
| R-01 | TTFV > 14 ngày · 2 cohort tuần · mỗi cohort ≥ 8 shop | Đóng băng nhận shop dùng thử mới 14 ngày, cắt onboarding còn 1 kênh + 1 nhóm sản phẩm | Không tăng ngân sách quảng cáo để kéo thêm shop khi onboarding đang tắc | CÓ |
| R-02 | Containment < 64% · 3 tuần · ≥ 1.000 hội thoại/tuần | Dừng bật AI tự động cho shop mới, khoá về 3 intent an toàn nhất, sửa prompt + RAG trong 1 sprint | Không bỏ QA nội bộ để containment trông cao hơn | CÓ |
| R-03 | Trial→paid < 20% · 2 chu kỳ (~8 tuần) · ≥ 40 shop hết dùng thử | Chuyển 1 product owner sang activation, rút wizard còn 3 bước, nạp sẵn mẫu catalog theo ngành | Không giảm giá gói Growth để ép chuyển đổi khi shop chưa đạt first value | KHÔNG |
| R-04 | Chi phí AI/hội thoại > 270 ₫ · 2 tuần · ≥ 5.000 hội thoại | Giới hạn context window, hạ model tier cho intent đơn giản, đàm phán lại quota API trước kỳ billing | Không tắt retry/QA để chi phí trông thấp hơn | CÓ |
| R-05 | Logo churn > 9,3% · 2 tháng · cohort ≥ 30 shop trả phí | Chuyển roadmap tháng kế sang 3 nguyên nhân huỷ lớn nhất có evidence từ phỏng vấn offboarding | Không tăng ngân sách acquisition để bù shop rời đi | KHÔNG |

## Cổng 90 ngày

| Ngày | Một metric · ngưỡng | Evidence | Đạt / Trượt |
|---:|---|---|---|
| 30 | Learning — baseline TTFV cohort go-live đầu · ≥ 10 shop có số TTFV thật + định nghĩa "first value" đã chốt | Cohort sheet + event log 'containment_qa_passed' | GO / FIX |
| 60 | Operating — trial→paid conversion (O-01) · ≥ 20% trên ≥ 30 shop kết thúc dùng thử | Cohort billing report từ hệ thống thanh toán | GO / PIVOT |
| 90 | Kinh tế đơn vị — gross margin sau chi phí AI · ≥ 60% trên ≥ 20.000 hội thoại | Billing export + token log + QA report | GO / KILL |

**Kill criteria:** KILL ở ngày 90 nếu sau 1 vòng FIX mà median TTFV vẫn > 14 ngày, hoặc GM sau chi phí AI vẫn < 50% trên ≥ 20.000 hội thoại, và chưa có ≥ 30 shop trả phí giữ churn ≤ 9,3%/tháng trong 2 tháng liên tiếp.

**Chưa đo được:** Containment theo từng intent · cần nhãn intent trên log hội thoại + đối chiếu escalate · owner Product Ops · có số ngày 2026-09-20.

---

## Phụ lục trang 2 — Ngưỡng suy từ mô hình

**MH-01 · Trần chi phí inference mỗi hội thoại (áp cho O-02)**

```
Giá overage mỗi hội thoại                 = 900 ₫              (Day 25)
GM mục tiêu (sàn pessimistic Day 24 67,7% → chốt 70%) = 70%
Tổng chi phí biến đổi tối đa mỗi hội thoại = 900 × (1 − 0,70)  = 270 ₫
Chi phí biến đổi phi-AI (infra + retry 6% + QA HITL 5%), Day 25 = 100 ₫
→ Trần chi phí inference                  = 270 − 100          = 170 ₫/hội thoại
```
Áp dụng O-02: 🟢 ≤170 ₫ · 🟡 171–270 ₫ · 🔴 >270 ₫.

**MH-02 · Trần churn tháng của shop (áp cho G-01)**

```
CAC (Day 24 base)                = 1.200.000 ₫
LTV/CAC mục tiêu                  ≥ 3                         (Bessemer, Day 24)
→ LTV tối thiểu                   = 3 × 1.200.000             = 3.600.000 ₫
ARPU                             = 499.000 ₫/tháng            (Day 24)
Gross margin                     = 67,3%                      (Day 25)
Lãi gộp mỗi tháng                = 499.000 × 0,673            = 335.827 ₫
Số tháng khách cần ở lại         = 3.600.000 ÷ 335.827        = 10,7 tháng
→ Churn tháng tối đa             = 1 ÷ 10,7                   = 9,3%/tháng
```
Áp dụng G-01: 🟢 ≤6% · 🟡 6,1–9,3% · 🔴 >9,3%.

**Nguồn benchmark [BM] đã dùng**

- O-01 trial→paid: RevenueCat — *State of Subscription Apps 2026* (công bố 19/03/2026), app AI 8,5% — https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026 — kiểm tra 2026-08-28. Dùng làm sàn tham chiếu, không phải mục tiêu.
