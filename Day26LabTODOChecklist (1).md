# ✅ TODO LIST — Day 26 · Track 1 · AI Product Handbook
**Lab:** Operating Dashboard (đèn báo sớm + luật hành động)
**Thời lượng:** 120 phút · Mức: Trung cấp
**File duy nhất được sửa:** `submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md`

> **Nguyên tắc xuyên suốt**
> - Leading indicator chỉ có nghĩa khi nói rõ **báo trước cho metric nào** và **độ trễ bao lâu**.
> - Ngưỡng không nguồn + luật không có "phản xạ bị cấm" = thông tin trang trí, không phải công cụ vận hành.
> - Chỉ dùng **một** trong ba bảng B2C / B2B / B2B2C.
> - Không bịa số. Thiếu dữ liệu thì ghi "chưa đo được" + cách đo + ngày có số.

---

## 📦 ĐẦU RA CUỐI CÙNG (Definition of Done)

- [ ] Worksheet Markdown đầy đủ 12 cột: `submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md`
- [ ] Bản rút gọn **1 trang** dùng được cho họp vận hành hằng tuần
- [ ] Phụ lục **tối đa 1 trang**, chứng minh **≥ 2 ngưỡng suy từ unit economics** `[MH]`
- [ ] Validator trả **PASS**
- [ ] PDF **≤ 2 trang**, tên file: `[Tên]_Day26_dashboard.pdf`
- [ ] Nộp lên LMS trước buổi tiếp theo, giữ lại file Markdown nguồn

---

## ⏱️ TIMELINE 120 PHÚT (bám mốc để không trượt tiến độ)

| Mốc | Việc | Checkpoint |
|---|---|---|
| 0:00–0:15 | Chốt loại mô hình + kiểm kê dữ liệu | CP1 |
| 0:15–0:40 | Dựng cây ba tầng, chọn North Star + 6–8 thẻ đèn | CP2 |
| 0:40–1:10 | Đặt ngưỡng 🟢🟡🔴 có nguồn | CP3 |
| 1:10–1:40 | Viết 5 luật quyết định | CP4 |
| 1:40–1:50 | Cổng 30/60/90 + kill criteria | CP5A |
| 1:50–1:53 | Critique (AI hoặc peer) | — |
| 1:53–1:56 | Validate cấu trúc | — |
| 1:56–1:58 | Tự chấm rubric | — |
| 1:58–2:00 | Xuất PDF + nộp | — |

---

## BƯỚC 1 — Mở đúng tài liệu và xác định đầu ra

### 1.1 Kiểm tra repo
- [ ] Mở repo **Day 26 — AI Product Handbook** (fork nếu giảng viên yêu cầu), clone về máy
- [ ] Chạy tại root repo:
  ```bash
  git remote get-url origin
  git status --short
  ```
- [ ] Xác nhận remote trỏ về repo giảng viên hoặc fork của bạn từ
      `https://github.com/VinUni-AI20k/Day26-Track-1-AI-Product-Handbook.git`
- [ ] ⚠️ Nếu URL không liên quan repo này → **DỪNG LẠI**, xác nhận với giảng viên trước khi làm

### 1.2 Nắm vai trò từng file trong repo
- [ ] `README.md` — đầu ra, cấu trúc repo, lệnh quality gate
- [ ] `Day26-AI-Product-Handbook.md` — benchmark, bảng đèn B2C/B2B/B2B2C, prompt phản biện
- [ ] `templates/operating-dashboard-template.md` — **file nguồn bạn copy và điền**
- [ ] `templates/one-page-dashboard-template.md` — bản rút gọn để xuất trang 1 PDF
- [ ] `examples/b2b-supportpilot-example.md` — ví dụ hư cấu, **không phải đáp án**
- [ ] `lab.config.json` — minimum bar validator đọc → **chỉ đọc, không sửa**
- [ ] `scripts/validate_submission.py` + `tests/` → **chỉ chạy, không sửa để làm xanh bài**
- [ ] `submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md` — file **duy nhất** bạn chỉnh sửa

> 📌 Handbook dùng snapshot benchmark ngày **2026-08-27**. Mọi `[BM]` trong bài thật vẫn phải có **URL gốc + ngày bạn tự kiểm tra**.

### 1.3 Chạy known-good checks TRƯỚC khi copy template
- [ ] macOS/Linux:
  ```bash
  python3 scripts/validate_submission.py examples/b2b-supportpilot-example.md
  python3 -m unittest discover -s tests -v
  ```
- [ ] Windows PowerShell:
  ```powershell
  python scripts\validate_submission.py examples\b2b-supportpilot-example.md
  python -m unittest discover -s tests -v
  ```
- [ ] Kết quả bắt buộc: example trả **PASS** và **OK** sau `Ran 14 tests`
- [ ] Nếu không đạt → kiểm tra: đúng root repo? Python 3.10+? Chưa sửa config/validator/tests?

### 1.4 Tạo file bài làm riêng
- [ ] macOS/Linux:
  ```bash
  mkdir -p "submissions/<MÃ-HỌC-VIÊN>"
  cp templates/operating-dashboard-template.md \
     "submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md"
  ```
- [ ] Windows PowerShell:
  ```powershell
  New-Item -ItemType Directory -Force "submissions\<MÃ-HỌC-VIÊN>"
  Copy-Item "templates\operating-dashboard-template.md" `
            "submissions\<MÃ-HỌC-VIÊN>\operating-dashboard.md"
  ```
- [ ] Chạy validator khi template còn trắng để lấy baseline:
  ```bash
  python3 scripts/validate_submission.py submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md
  ```
- [ ] Xác nhận lần chạy đầu báo **FAIL** vì placeholder chưa thay → đây là baseline đúng

**🎯 Kết quả mong đợi:** mở đúng repo, example + 14 tests xanh, có file bài làm riêng với baseline FAIL chỉ vì template chưa điền.

---

## BƯỚC 2 — Chuẩn bị đầu vào từ Day 24–25

- [ ] Mở lại hai đầu ra cũ (Day 24 unit economics, Day 25 Value Metric / Cost per Job)
- [ ] Ghi sẵn vào nháp các giá trị sau:
  - [ ] ARPU hoặc doanh thu trên Value Metric
  - [ ] CAC và CAC payback mục tiêu
  - [ ] Gross margin mục tiêu
  - [ ] Cost/Job — **tách riêng token / inference cost**
  - [ ] Retention hoặc renewal assumption
  - [ ] Kênh phân phối và **người thực sự trả tiền**
  - [ ] Người dùng trực tiếp và người dùng cuối bị tác động
- [ ] Nếu thiếu Day 24 hoặc Day 25: **không bịa số** → ghi "chưa đo được" + dữ liệu cần thu + ngày dự kiến có số
- [ ] ⚠️ Không tự nhận một ngưỡng cảm tính là ngưỡng `[MH]`

### Ba loại nguồn ngưỡng — học thuộc điều kiện dùng

| Ký hiệu | Nghĩa | Điều kiện sử dụng |
|---|---|---|
| `[BM]` | Benchmark công bố | Có **URL gốc** và **ngày bạn kiểm tra** |
| `[MH]` | Suy từ mô hình | Có **input Day 24–25**, **phép tính** và **kết quả** |
| `[TB]` | Baseline của chính bạn | Có **cách đo**, **chu kỳ đo**, **ngày dự kiến chốt baseline** |

- [ ] Nhớ: **mỗi metric dùng đúng MỘT loại nguồn**

**🎯 Kết quả mong đợi:** đủ input để giải thích ngưỡng, hoặc đã ghi trung thực dữ liệu còn thiếu.

---

## BƯỚC 3 — Chọn đúng loại mô hình

- [ ] ⚠️ Không chọn theo kế hoạch tương lai — trả lời theo cách sản phẩm hoạt động **hôm nay**
- [ ] Trả lời 3 câu chẩn đoán:
  - [ ] Ai trả tiền?
  - [ ] Ai trực tiếp dùng sản phẩm?
  - [ ] Nếu có bên trung gian: bạn có chạm được người dùng cuối, quan sát hành vi và giữ một phần quan hệ với họ không?

| Loại | Dấu hiệu chẩn đoán | Đèn bật trước |
|---|---|---|
| **B2C** | Cá nhân trả tiền và trực tiếp dùng | Retention curve có phẳng không? |
| **B2B** | Doanh nghiệp trả tiền và chính tổ chức đó dùng | Time-to-first-value |
| **B2B2C** | Partner trả tiền/phân phối, khách của partner là end-user, bạn chạm được họ | Partner activation rate |

- [ ] Viết câu chẩn đoán trong section **Chẩn đoán mô hình** theo cấu trúc:
  ```
  Chúng tôi là [B2C/B2B/B2B2C] vì tiền đến từ [...], người dùng thật là [...],
  và chúng tôi [có/không có] bề mặt trực tiếp với người dùng cuối qua [...].
  ```
- [ ] Kiểm kê từng dữ liệu thành 3 trạng thái: **đo được** / **đo trong hai tuần** / **chưa biết cách đo**

**🎯 Kết quả mong đợi:** mô hình được chốt bằng dòng tiền và hành vi thực tế, không bằng nhãn nghe hấp dẫn.

---

## BƯỚC 4 — Hiểu cây tín hiệu ba tầng (nền tảng lý thuyết)

| Tầng | Độ trễ | Bản chất |
|---|---|---|
| **Leading** | Ngày hoặc tuần | Đổi sớm, **báo trước**, dễ can thiệp |
| **Operating** | Tuần hoặc tháng | Đòn bẩy đội có thể kéo trong vận hành |
| **Lagging** | Tháng hoặc quý | Kết quả: LTV, CAC payback, NPV, doanh thu quý |

- [ ] Với mỗi metric định gọi là Leading, tự trả lời câu test:
  ```
  Metric này báo trước cho metric nào, với độ trễ khoảng bao lâu?
  ```
- [ ] Nếu không trả lời được → đó chỉ là con số dễ nhìn, **chưa phải tín hiệu sớm** → loại hoặc hạ tầng

**🎯 Kết quả mong đợi:** phân biệt được metric dùng để **lái** với metric chỉ dùng để **nhìn lại kết quả**.

---

## BƯỚC 5 — CP1 · Trạm chốt loại và dữ liệu (15 phút · xong ở phút 15)

Trong file bài làm:
- [ ] Điền **học viên**, **mã học viên**, **sản phẩm**, **loại mô hình**, **ngày cập nhật** (ISO `YYYY-MM-DD`)
- [ ] Viết câu **chẩn đoán mô hình** (từ Bước 3)
- [ ] Chọn một **North Star** ban đầu (tên đèn + giá trị mục tiêu)
- [ ] Ghi các dữ liệu **đang đo được** và **chưa đo được** (bảng Dữ liệu đầu vào: trạng thái · nằm ở đâu/cần gì · ngày có số)
- [ ] Điền bảng **Kiểm kê đèn ứng viên** từ đúng bảng handbook theo loại mô hình, mỗi hàng đánh dấu đúng một trạng thái ✅ / 🔧 / ❌
  - [ ] B2C: **8 hàng** · B2B: **11 hàng** · B2B2C: **9 hàng** — xóa hàng thừa

**Checkpoint CP1:**
- [ ] Có **đúng một** loại mô hình
- [ ] Câu chẩn đoán nêu rõ **người trả tiền** và **người dùng**
- [ ] Mỗi khoảng trống dữ liệu có **cách đo** hoặc **ngày xem lại**

**🎯 Kết quả mong đợi:** CP1 hoàn thành ở phút 15 với loại mô hình và danh sách khoảng trống dữ liệu rõ ràng.

---

## BƯỚC 6 — CP2 · Trạm dựng cây ba tầng (25 phút · xong ở phút 40)

### Ràng buộc số lượng (validator kiểm)
- [ ] Tổng cộng **6–8 metric**
- [ ] **≥ 2 Leading** (`L-01`, `L-02`, …)
- [ ] **≥ 1 Operating** (`O-01`, …)
- [ ] **≤ 3 Lagging** (`G-01`, …)
- [ ] **≥ 1 metric bắt chi phí AI** trước khi nó làm xấu gross margin (vd. `O-02` Chi phí AI / job)

### Mỗi hàng metric phải có đủ 12 cột
- [ ] `ID` (đúng prefix L / O / G)
- [ ] `Đèn` — tên metric
- [ ] `Định nghĩa và công thức` — đủ chặt để **hai người đo ra cùng một số**
- [ ] `Nhịp · Owner` — dùng dấu phân tách `·` (vd. `TUẦN · PRODUCT OPS`)
- [ ] `Hiện tại` — giá trị hiện tại nếu đã có
- [ ] `🟢` / `🟡` / `🔴` — ba vùng **khác nhau, không chồng lấn**
- [ ] `Nguồn` — đúng một tag `[BM]` / `[MH]` / `[TB]` + chi tiết
- [ ] `Ngày kiểm tra` (`YYYY-MM-DD`)
- [ ] `Báo trước cho` — metric downstream
- [ ] `Luật` — ID luật quyết định sẽ kích hoạt (`R-01`…`R-05`)

- [ ] ⚠️ **Không copy nguyên bảng trong handbook.** Bảng đó là thực đơn; dashboard chỉ giữ metric bạn thực sự mở **mỗi tuần**

**🎯 Kết quả mong đợi:** CP2 hoàn thành ở phút 40 với một North Star và 6–8 thẻ đèn có chuỗi dự báo hợp lý.

---

## BƯỚC 7 — CP3 · Trạm đặt ngưỡng (30 phút · xong ở phút 70)

Với **mỗi** metric:
- [ ] Chọn `[BM]`, `[MH]` hoặc `[TB]` (đúng một loại)
- [ ] Đặt ba vùng 🟢 🟡 🔴 **không chồng lấn**
- [ ] Viết một câu giải thích **vì sao ranh giới đó phù hợp**
- [ ] Ghi **ngày kiểm tra** cho mọi benchmark `[BM]`
- [ ] Với `[MH]`: ghi **phép tính vào phụ lục** (`MH-01`, `MH-02`)

### Mẫu phép tính suy từ mô hình
```
Gross margin mục tiêu           = 55%
Doanh thu mỗi job               = 20.000 đ
Tổng chi phí biến đổi tối đa    = 20.000 × (1 − 55%) = 9.000 đ/job
Chi phí biến đổi khác           = 5.500 đ/job
→ Inference cost tối đa         = 3.500 đ/job
```

- [ ] Có **ít nhất hai phép tính kiểu này** (`MH-01` và `MH-02`, nội dung khác nhau)
- [ ] Mỗi phép tính có **số** và **dấu `=`**, input có **đơn vị**, kết quả ghi rõ **ID đèn áp dụng**
- [ ] ⚠️ Không lấy số tròn chỉ vì dễ nhớ
- [ ] ⚠️ Không dùng benchmark trung vị như mục tiêu mặc định

**🎯 Kết quả mong đợi:** CP3 hoàn thành ở phút 70; mọi đèn có ba màu, nguồn, lý do và ít nhất hai ngưỡng `[MH]` có phép tính.

---

## BƯỚC 8 — CP4 · Trạm viết luật quyết định (30 phút · xong ở phút 100)

### Cấu trúc bắt buộc 5 phần cho mỗi luật
```
NẾU        metric vượt ngưỡng nào
TRONG      bao lâu
VÀ         mẫu tối thiểu hoặc điều kiện xác nhận nào
THÌ        hành động cụ thể bắt đầu bằng động từ
KHÔNG THÌ  phản xạ sai nào bị cấm
```

- [ ] Viết **đúng năm luật**, ID `R-01` → `R-05`
- [ ] Đánh dấu **ít nhất hai luật dừng** (cột `Luật dừng? = CÓ`)
- [ ] Dùng động từ hành động: **đóng băng, cắt, dừng, đàm phán lại, chuyển, giới hạn**
- [ ] Mỗi luật gắn với ID đèn tương ứng ở cột `Luật` của bảng metric

### ⛔ Kết thúc bị cấm (không cho biết ai làm gì tuần sau)
- [ ] Không dùng "xem xét lại"
- [ ] Không dùng "cân nhắc"
- [ ] Không dùng "theo dõi thêm"
- [ ] Không dùng "cải thiện sản phẩm"

**🎯 Kết quả mong đợi:** CP4 hoàn thành ở phút 100 với năm luật đủ cấu trúc và ít nhất hai luật thật sự dừng một hành động.

---

## BƯỚC 9 — CP5A · Trạm cổng gác 90 ngày (10 phút · phút 100 → 110)

### Tạo đúng ba cổng

| Cổng | Điều bắt buộc |
|---|---|
| **Ngày 30** | Một metric về **học / validation** — không phải doanh thu |
| **Ngày 60** | Một metric chứng minh **vận hành hoặc hành vi thật** |
| **Ngày 90** | Một metric chứng minh **mô hình có thể tiếp tục** |

Mỗi cổng phải có:
- [ ] **Đúng một** metric gác cổng
- [ ] Một **ngưỡng có số**
- [ ] **Bằng chứng vật lý** phải tồn tại: log, file, báo cáo hoặc cohort
- [ ] Một quyết định thuộc **GO / FIX / PIVOT / KILL**

- [ ] ⚠️ **FIX chỉ dùng một lần** cho cùng một vấn đề. Lần thứ hai = giả định gốc sai → **PIVOT hoặc KILL**
- [ ] Viết thêm **một kill criterion** có **số** và **mốc thời gian**
- [ ] ⛔ Tránh câu không kiểm chứng được như "không có traction tốt"
- [ ] Điền section **Chưa đo được**: đèn/giả định · cần gì để đo · ai chịu trách nhiệm · ngày có số

**🎯 Kết quả mong đợi:** CP5A hoàn thành ở phút 110 với ba cổng falsifiable và một kill criterion rõ; còn 10 phút để critique, validate, tự chấm và xuất bài.

---

## BƯỚC 10 — Critique & AI Support Log (3 phút · phút 110 → 113)

- [ ] Tự viết xong bản đầu **trước**, rồi mới critique
- [ ] Mở các prompt ở **phần 5 của handbook**, ưu tiên theo thứ tự:
  - [ ] **Dashboard Tier Audit**
  - [ ] **Threshold Justification Challenger**
  - [ ] **Decision Rule Red-Team**
  - [ ] **Wrong-Reflex Finder**
- [ ] Nếu không có chatbot / mạng: dùng cùng bộ câu hỏi để tự critique hoặc đổi bài với một bạn

### 📝 AI Support Log — section `## Ghi nhận AI critique`

Ghi lại **tối đa 3 ý** đã nhận được và xử lý:

| Phản biện | Chấp nhận hay bác bỏ | Thay đổi đã thực hiện | Lý do |
|---|---|---|---|
| `<Ý phản biện 1>` | CHẤP NHẬN / BÁC BỎ | `<Thay đổi cụ thể>` | `<Lý do>` |
| `<Ý phản biện 2>` | CHẤP NHẬN / BÁC BỎ | `<Thay đổi cụ thể>` | `<Lý do>` |
| `<Ý phản biện 3>` | CHẤP NHẬN / BÁC BỎ | `<Thay đổi cụ thể>` | `<Lý do>` |

- [ ] Mỗi dòng nêu rõ **thay đổi đã thực hiện** và **lý do**
- [ ] Ngưỡng và quyết định cuối cùng vẫn **truy được về dữ liệu hoặc lập luận của bạn**

**🎯 Kết quả mong đợi:** ở phút 113, critique đã giúp tìm điểm mù nhưng bạn vẫn sở hữu toàn bộ lập luận.

---

## BƯỚC 11 — Validate cấu trúc bài làm (3 phút · phút 113 → 116)

- [ ] Chạy:
  ```bash
  python3 scripts/validate_submission.py submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md
  ```

### Validator kiểm những gì
- [ ] Đúng một loại B2C / B2B / B2B2C
- [ ] 6–8 metric · ≥ 2 Leading · ≥ 1 Operating · ≤ 3 Lagging
- [ ] Có metric về **chi phí AI**
- [ ] Mọi metric có nguồn `[BM]` / `[MH]` / `[TB]`
- [ ] ≥ 2 ngưỡng `[MH]` và 2 phép tính phụ lục
- [ ] Đúng năm luật và ≥ 2 luật dừng
- [ ] Đủ cổng ngày 30, 60, 90
- [ ] Có kill criteria và phần "chưa đo được"

> ⚠️ **PASS không chứng minh ngưỡng hợp lý.** Nó chỉ chứng minh bài đủ cấu trúc để đưa sang human review. Validator **không** xác minh URL `[BM]` còn truy cập được, benchmark còn mới, hay phép tính kinh doanh hợp lý.

### Nếu FAIL — sửa từ lỗi đầu tiên theo thứ tự

| Nhóm lỗi | Kiểm tra trước |
|---|---|
| `placeholder` hoặc `metadata` | Thay toàn bộ `<...>`, điền đúng B2C/B2B/B2B2C và ngày ISO `YYYY-MM-DD` |
| `metrics` hoặc `Đèn...` | Đủ 6–8 hàng, đúng prefix ID, ba vùng khác nhau, nguồn và ngày kiểm tra |
| `ngưỡng [MH]` hoặc `Phụ lục [MH]` | Có ≥ 2 hàng `[MH]` và 2 phép tính chứa **số** cùng **dấu `=`** |
| `Luật quyết định` | Đúng năm luật, ID `R-01`→`R-05`, ≥ 2 luật dừng, hành động không mơ hồ |
| `Cổng gác 90 ngày` | Đúng ba hàng 30/60/90; ngưỡng có số; quyết định thuộc GO/FIX/PIVOT/KILL |
| `Kill criteria` hoặc `Chưa đo được` | Có số, mốc thời gian, một khoảng trống thật, cách đo và ngày có số |

- [ ] ⚠️ **Chỉ sửa** `submissions/<MÃ-HỌC-VIÊN>/operating-dashboard.md`
- [ ] ⛔ Không sửa `lab.config.json`, validator, tests hoặc example để ép kết quả thành PASS

**🎯 Kết quả mong đợi:** ở phút 116, validator trả PASS, không còn placeholder, và bạn vẫn giải thích được bằng lời từng ngưỡng quan trọng.

---

## BƯỚC 12 — Tự chấm theo rubric (2 phút · phút 116 → 118)

| Tiêu chí | Điểm | Câu hỏi tự kiểm tra | ✔ |
|---|---:|---|---|
| **Tier Discipline** | 20 | Leading có thật sự báo trước? Dashboard có quá nhiều Lagging không? | ☐ |
| **Threshold Quality** | 30 | Mọi ngưỡng có nguồn, ngày, lý do và ít nhất hai phép tính `[MH]` không? | ☐ |
| **Decision Rule Quality** | 30 | Luật có hành động cụ thể, time window, sample condition và vế cấm không? | ☐ |
| **90-Day Gates** | 15 | Mỗi cổng có một metric, ngưỡng số, bằng chứng và quyết định không? | ☐ |
| **Honesty** | 5 | Phần "chưa đo được" có nội dung thật, cách đo và ngày có số không? | ☐ |

- [ ] ⚠️ Đừng tối ưu để validator xanh nhưng dashboard vô dụng — rubric chấm **chất lượng lập luận**, không chỉ số ô đã điền
- [ ] Ghi lại **điểm yếu lớn nhất** của bài trước khi gửi review

**🎯 Kết quả mong đợi:** ở phút 118, bạn biết điểm yếu lớn nhất của bài.

---

## BƯỚC 13 — Xuất PDF và nộp bài (2 phút · phút 118 → 120)

### Rút gọn sang bản một trang
- [ ] Chuyển phần vận hành sang `templates/one-page-dashboard-template.md`
- [ ] Mọi giá trị **khớp worksheet nguồn**; chi tiết nguồn + 2 phép tính `[MH]` nằm ở phụ lục trang 2
- [ ] ⚠️ Không ép bảng 12 cột lên một trang

### Kiểm tra trước khi xuất
- [ ] Dashboard vừa **đúng một mặt giấy**
- [ ] Phụ lục **không quá một trang**
- [ ] Font đọc được khi in **A4**
- [ ] Không có URL hoặc phép tính bị cắt
- [ ] Không có dữ liệu nhạy cảm
- [ ] Mọi benchmark có **ngày kiểm tra**

### Xuất và nộp
- [ ] Tên file: `[Tên]_Day26_dashboard.pdf`
- [ ] PDF **không quá hai trang**
- [ ] Nộp trực tiếp trên **LMS** trước buổi tiếp theo
- [ ] Giữ file Markdown nguồn để sửa khi nhận feedback

**🎯 Kết quả mong đợi:** ở phút 120, PDF đúng tên, ≤ 2 trang, và bài nộp là một **công cụ vận hành dùng được trong họp tuần**, không phải bảng metric để trình bày.

---

## 🏁 CHECKLIST CUỐI CÙNG (bản chính thức của lab)

- [ ] Đúng một loại mô hình
- [ ] Một North Star và 6–8 metric
- [ ] Ít nhất hai Leading và một metric chi phí AI
- [ ] Không quá ba Lagging
- [ ] Mọi metric có 🟢 🟡 🔴 và nguồn
- [ ] Ít nhất hai ngưỡng `[MH]` có phép tính
- [ ] Đúng năm luật; ít nhất hai luật dừng
- [ ] Đủ cổng ngày 30, 60, 90
- [ ] Kill criterion có số và mốc thời gian
- [ ] Phần "chưa đo được" có cách đo và ngày xem lại
- [ ] Validator trả PASS
- [ ] PDF đúng tên và không quá hai trang

---

## 📐 PHỤ LỤC A — Ngưỡng máy móc từ `lab.config.json`

| Tham số | Giá trị |
|---|---|
| `metric_count_min` / `max` | 6 / 8 |
| `leading_metric_min` | 2 |
| `operating_metric_min` | 1 |
| `lagging_metric_max` | 3 |
| `model_derived_threshold_min` (`[MH]`) | 2 |
| `decision_rule_count` | 5 |
| `stop_rule_min` | 2 |
| `gate_days` | 30, 60, 90 |
| `gate_decisions` | GO, FIX, PIVOT, KILL |
| `gate_pass_decision` | GO |
| `cadence_owner_separator` | `·` |
| `threshold_source_types` | BM, MH, TB |
| `candidate_light_inventory_min` | B2C: 8 · B2B: 11 · B2B2C: 9 |
| `candidate_light_statuses` | ✅ 🔧 ❌ |

---

## 🗂️ PHỤ LỤC B — Bản đồ section của file bài làm

Đánh dấu khi mỗi section đã điền xong, không còn `<...>`:

- [ ] Header: `# Operating Dashboard — <TÊN SẢN PHẨM>` + Học viên / Mã học viên / Mô hình / Cập nhật / North Star
- [ ] `## Chẩn đoán mô hình` (câu chẩn đoán + bảng dữ liệu đầu vào)
- [ ] `## Kiểm kê đèn ứng viên` (đủ số hàng theo loại mô hình, trạng thái ✅/🔧/❌)
- [ ] `## Đèn báo sớm` (L-01, L-02, …)
- [ ] `## Đèn vận hành` (O-01, O-02 chi phí AI/job, …)
- [ ] `## Đèn kết quả` (G-01, G-02, …)
- [ ] `## Luật quyết định` (R-01 → R-05)
- [ ] `## Cổng gác 90 ngày` (30 / 60 / 90)
- [ ] `## Kill criteria`
- [ ] `## Chưa đo được`
- [ ] `## Phụ lục ngưỡng suy từ mô hình` (MH-01, MH-02)
- [ ] `## Ghi nhận AI critique` — **AI support log**
