# 01 — PROBLEM SCAN (Cá nhân)


## Thông tin cá nhân (context)

Tôi là **AI Product Engineer** tại **Vin Smart Future**, phụ trách mảng **Vinmec** — chuỗi bệnh viện tư nhân lớn nhất Việt Nam với hơn 40 cơ sở trên toàn quốc và hơn 10,000 nhân viên y tế.

Công việc hằng ngày gồm:
- Làm việc trực tiếp với đội vận hành bệnh viện (scheduling team, head nurses, department heads) để hiểu pain point
- Scoping và thiết kế giải pháp AI cho các quy trình lâm sàng và vận hành
- Phối hợp với Data Engineer để đánh giá feasibility của data pipeline hiện tại (HIS, EMR)
- Viết PRD (Product Requirements Document) và prompt prototype cho từng use case
- Báo cáo ROI và tiến độ lên Ban Giám đốc Vin Smart Future

**Phạm vi tập trung:** Tối ưu lịch hẹn khám & điều phối bác sĩ tại Vinmec

---

## Phase 1 — Scan: 5+ Bài toán (dùng 4 Lenses)

### Danh sách bài toán

| # | Lens | Bài toán | Stakeholder bị ảnh hưởng |
|---|------|----------|--------------------------|
| 1 | Lặp lại | Nhân viên lễ tân phải xác nhận lịch hẹn thủ công qua điện thoại cho từng bệnh nhân — lặp lại ~200–300 cuộc gọi/ngày/cơ sở | Nhân viên lễ tân, bệnh nhân |
| 2 | Lặp lại | Bác sĩ phải nhập tay ghi chú "lý do tái khám" và "thời gian dự kiến" vào HIS sau mỗi lượt khám để hệ thống xếp lịch tiếp theo | Bác sĩ, scheduling team |
| 3 | Tốn thời gian | Điều phối viên mất 45–60 phút mỗi sáng để điều chỉnh lịch bác sĩ khi có ca cấp cứu hoặc bác sĩ nghỉ đột xuất — làm thủ công trên spreadsheet | Điều phối viên, bác sĩ trực, bệnh nhân có lịch hẹn |
| 4 | Tốn thời gian | Trưởng khoa mất 2–3 giờ/tuần để lập lịch phân công bác sĩ cho tuần kế tiếp, phải cân đối ca trực, chuyên môn, và số lượng bệnh nhân dự báo | Trưởng khoa, bác sĩ |
| 5 | AI có thể tốt hơn | Dự báo số lượng bệnh nhân theo ngày/giờ/chuyên khoa còn làm thủ công (dựa trên kinh nghiệm), dẫn đến phân bổ bác sĩ sai so với nhu cầu thực tế | Trưởng khoa, bệnh nhân (thời gian chờ) |
| 6 | AI có thể tốt hơn | Gợi ý slot lịch hẹn phù hợp cho bệnh nhân hiện do nhân viên chọn thủ công, chưa cân nhắc đến lịch sử khám, chuyên môn bác sĩ, hay thời gian đi lại | Bệnh nhân, nhân viên booking |
| 7 | Pain từ người khác | Bác sĩ phàn nàn: bị xếp lịch dày (8–10 bệnh nhân/giờ) vào cuối ca do hệ thống không biết thời gian thực tế mỗi ca khám, gây kiệt sức | Bác sĩ, chất lượng khám bệnh |
| 8 | Pain từ người khác | Bệnh nhân phàn nàn: đặt lịch online xong vẫn phải chờ 60–90 phút tại viện vì lịch không khớp với thực tế vận hành | Bệnh nhân, NPS của Vinmec |
| 9 | Tốn thời gian | Báo cáo hiệu suất sử dụng phòng khám (room utilization) được tổng hợp thủ công từ HIS mỗi tuần, mất 3–4 giờ/cơ sở | Quản lý vận hành, Giám đốc cơ sở |
| 10 | Lặp lại | Nhắc lịch hẹn cho bệnh nhân (SMS/call) được gửi theo batch thủ công, không cá nhân hoá theo loại khám, nguy cơ quên, hay kênh liên lạc ưa thích | Nhân viên chăm sóc khách hàng, bệnh nhân |

> **💡 Self-check I1.1 — Scan Breadth**
> - [v] Có ít nhất 5 bài toán
> - [v] Dùng đủ 4/4 lenses (Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác)
> - [v] Bài toán đến từ workflow thật của Vinmec, không chung chung
> - [v] Có ghi rõ stakeholder bị ảnh hưởng cho từng bài

---

## Phase 2 — Quick-Assess: 3 Quick Problem Cards

### Card #1

```
┌──────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                │
│ Công ty: Vinmec — Mảng: Tối ưu lịch hẹn             │
│                                                      │
│ Bài toán: Điều phối viên mất 45–60 phút mỗi sáng    │
│ để tái phân công lịch bác sĩ khi có sự cố đột xuất  │
│ (bác sĩ nghỉ bệnh, ca cấp cứu kéo dài)              │
│                                                      │
│ Ai đang đau?                                         │
│   - Điều phối viên (operator): làm thủ công,         │
│     dễ sai, áp lực giờ cao điểm sáng                │
│   - Bác sĩ: nhận thông báo thay đổi lịch muộn       │
│   - Bệnh nhân: không được báo kịp, chờ vô ích       │
│                                                      │
│ Workflow hiện tại:                                   │
│   1. Nhận thông báo bác sĩ nghỉ (thường 6–7 giờ)    │
│   2. Mở spreadsheet lịch ngày hôm đó                 │
│   3. Tra danh sách bác sĩ có thể thay thế (thủ công) │
│   4. Gọi điện hỏi từng bác sĩ có nhận ca không      │
│   5. Cập nhật lịch trên HIS                          │
│   6. Gọi/nhắn tin từng bệnh nhân bị ảnh hưởng       │
│                                                      │
│ Bước nào tốn nhất?                                   │
│   Bước 3–4 (⏱ ~30 min): không có tool hỗ trợ,       │
│   phải tra thủ công + gọi điện tuần tự               │
│                                                      │
│ AI có thể giúp ở bước nào?                           │
│   Bước 3–6: tự động gợi ý bác sĩ thay thế phù hợp  │
│   (chuyên môn, lịch trống, workload) → notify        │
│   bác sĩ + bệnh nhân tự động                        │
│                                                      │
│ Đo thành công bằng gì?                               │
│   Giảm thời gian xử lý sự cố từ 45–60 min           │
│   → dưới 10 min; đo trên 30 sự cố liên tiếp         │
│                                                      │
│ Quick gut: ☑ LLM Agent                               │
│   → Cần chuỗi hành động: query lịch trống →          │
│     rank bác sĩ phù hợp → gửi notification →        │
│     cập nhật HIS. Rule-based không đủ linh hoạt      │
│     khi ràng buộc thay đổi theo ngày.                │
└──────────────────────────────────────────────────────┘
```

---

### Card #2

```
┌──────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                │
│ Công ty: Vinmec — Mảng: Tối ưu lịch hẹn             │
│                                                      │
│ Bài toán: Hệ thống đặt lịch online không gợi ý slot │
│ phù hợp — nhân viên booking chọn thủ công, không     │
│ cân nhắc lịch sử khám hay chuyên môn bác sĩ         │
│                                                      │
│ Ai đang đau?                                         │
│   - Bệnh nhân: được xếp vào bác sĩ không phù hợp   │
│     chuyên môn, phải tái khám lần 2                  │
│   - Nhân viên booking: mất 5–8 phút/cuộc gọi để    │
│     tìm slot, xử lý ~150 booking/ngày               │
│   - Bác sĩ: nhận bệnh nhân không đúng chuyên sâu    │
│                                                      │
│ Workflow hiện tại:                                   │
│   1. Bệnh nhân gọi/nhắn tin yêu cầu đặt lịch        │
│   2. Nhân viên hỏi triệu chứng, loại khám           │
│   3. Mở HIS, tra lịch trống của chuyên khoa         │
│   4. Chọn slot đầu tiên còn trống (không có logic)  │
│   5. Xác nhận với bệnh nhân qua điện thoại           │
│   6. Nhập tay vào HIS                                │
│                                                      │
│ Bước nào tốn nhất?                                   │
│   Bước 3–4 (⏱ ~4 min/booking × 150/ngày = 10h):     │
│   tra thủ công, không có ranking, không có context  │
│   từ lịch sử khám của bệnh nhân                      │
│                                                      │
│ AI có thể giúp ở bước nào?                           │
│   Bước 2–4: NLP hiểu triệu chứng → map sang         │
│   chuyên khoa phù hợp → rank slot theo lịch sử      │
│   bệnh nhân + chuyên môn bác sĩ + giờ ưa thích      │
│                                                      │
│ Đo thành công bằng gì?                               │
│   Giảm thời gian xử lý từ 5–8 min → dưới 2 min;     │
│   tỷ lệ bệnh nhân gặp đúng chuyên khoa tăng từ      │
│   baseline hiện tại lên ≥ 90%; đo sau 1 tháng triển │
│   khai thử tại 1 cơ sở pilot                         │
│                                                      │
│ Quick gut: ☑ LLM + Rule Hybrid                       │
│   → NLP để hiểu triệu chứng (LLM), rule cứng để     │
│     đảm bảo compliance y tế (không xếp sai khoa).   │
└──────────────────────────────────────────────────────┘
```

---

### Card #3

```
┌──────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                │
│ Công ty: Vinmec — Mảng: Tối ưu lịch hẹn             │
│                                                      │
│ Bài toán: Trưởng khoa mất 2–3 giờ/tuần lập lịch     │
│ phân công bác sĩ thủ công, không có dự báo nhu cầu  │
│ bệnh nhân, dẫn đến phân bổ sai công suất            │
│                                                      │
│ Ai đang đau?                                         │
│   - Trưởng khoa: tốn thời gian lãnh đạo vào task    │
│     hành chính lặp lại, dễ sai khi thiếu data       │
│   - Bác sĩ: một số bị quá tải, một số rảnh rỗi      │
│     trong cùng tuần do phân công không đều           │
│   - Bệnh nhân: thời gian chờ tăng khi bác sĩ ít     │
│     hơn nhu cầu thực tế                              │
│                                                      │
│ Workflow hiện tại:                                   │
│   1. Trưởng khoa xem lịch tuần trước                 │
│   2. Ước đoán nhu cầu tuần tới (dựa kinh nghiệm)    │
│   3. Điền lịch vào Excel / hệ thống nội bộ          │
│   4. Gửi email thông báo cho từng bác sĩ             │
│   5. Xử lý xin đổi ca của bác sĩ thủ công           │
│                                                      │
│ Bước nào tốn nhất?                                   │
│   Bước 2–3 (⏱ ~90 min): không có dự báo định lượng, │
│   phải cân đối nhiều ràng buộc (chuyên môn, số ca,  │
│   ngày nghỉ phép, quy định trực tối thiểu)           │
│                                                      │
│ AI có thể giúp ở bước nào?                           │
│   Bước 2–4: forecast nhu cầu bệnh nhân theo tuần    │
│   → tự động draft lịch tối ưu theo ràng buộc →      │
│   trưởng khoa chỉ cần review và approve              │
│                                                      │
│ Đo thành công bằng gì?                               │
│   Giảm thời gian lập lịch từ 2–3 giờ/tuần           │
│   → dưới 30 phút/tuần; độ lệch giữa công suất       │
│   bác sĩ và nhu cầu thực tế giảm ≥ 20%              │
│   (đo qua room utilization report sau 4 tuần)        │
│                                                      │
│ Quick gut: ☑ ML Forecast + LLM Draft                 │
│   → ML (time-series) để dự báo nhu cầu;             │
│     LLM để soạn draft lịch từ output dự báo          │
│     + ràng buộc nghiệp vụ. Human-in-the-loop        │
│     (trưởng khoa approve) là bắt buộc vì liên        │
│     quan đến quyết định nhân sự y tế.                │
└──────────────────────────────────────────────────────┘
```

> **💡 Self-check I2 — Quick Cards**
> - [v] 3 cards đầy đủ thông tin, không mơ hồ
> - [v] Mỗi card có workflow rõ (5–6 bước)
> - [v] Mỗi card có stakeholder cụ thể (không chỉ ghi "người dùng")
> - [v] Metric có thể đo được, có baseline và mốc thời gian đo
> - [v] Quick gut ghi đúng mức kiến trúc + lý do chọn mức đó

---

## Phần Kill Rationale

| Card | Quyết định | Lý do |
|------|-----------|-------|
| #1 | ✅ Chọn | Pain point rõ và cấp bách: sự cố xảy ra hàng ngày, ảnh hưởng trực tiếp đến bệnh nhân và bác sĩ. Giải pháp LLM Agent khả thi với data lịch HIS sẵn có. ROI đo được ngay sau triển khai pilot. |
| #2 | ❌ Loại | Tuy impact lớn (150 booking/ngày), nhưng cần tích hợp sâu với EMR và dữ liệu lịch sử bệnh nhân — phụ thuộc vào data readiness chưa đánh giá. Scope rộng, dễ bị chặn ở compliance y tế. Nên để giai đoạn 2. |
| #3 | ✅ Chọn | Trưởng khoa là stakeholder có quyền quyết định triển khai pilot. Bài toán forecast + draft lịch có data input rõ ràng (lịch sử HIS 2+ năm). Giải pháp human-in-the-loop phù hợp với môi trường y tế. |

---

## #PITCH-CHALLENGE-VOTE

## Tôi pitch Card #1

**Problem:**
Mỗi sáng tại Vinmec, khi có bác sĩ nghỉ đột xuất hoặc ca cấp cứu kéo dài, điều phối viên phải xử lý toàn bộ việc tái phân công lịch bằng tay — mất 45–60 phút trong khung giờ áp lực nhất của ngày (6–8 giờ sáng).

**Workflow hiện tại (6 bước):**
1. Nhận thông báo bác sĩ nghỉ (thường qua điện thoại lúc 6–7 giờ sáng)
2. Mở spreadsheet, xác định danh sách bệnh nhân bị ảnh hưởng
3. Tra thủ công danh sách bác sĩ cùng chuyên khoa còn lịch trống
4. Gọi điện tuần tự hỏi từng bác sĩ có nhận ca thay không
5. Cập nhật lịch trên HIS sau khi xác nhận được bác sĩ thay thế
6. Gọi/nhắn tin từng bệnh nhân bị ảnh hưởng để thông báo thay đổi

**Bottleneck:** Bước 3–4 chiếm ~30 phút vì không có công cụ hỗ trợ — điều phối viên phải tra thủ công và liên hệ tuần tự, không biết ai đang rảnh hay ai phù hợp chuyên môn nhất để thay thế.

**AI giải ở đâu:** Bước 3–6 — LLM Agent tự động: query lịch trống theo chuyên khoa → rank bác sĩ phù hợp theo workload + chuyên môn → gửi notification xác nhận đến bác sĩ → tự động notify bệnh nhân bị ảnh hưởng → cập nhật HIS sau khi có xác nhận.

**Metric đo thành công:** Giảm thời gian xử lý sự cố từ 45–60 phút → dưới 10 phút; đo trên 30 sự cố liên tiếp tại 1 cơ sở pilot trong tháng đầu triển khai.

---

[INDIVIDUAL SIGNAL] Một học viên được chấm cao ở phần này khi:

- **Pitch rõ problem → workflow → bottleneck → metric:** Trình bày logic từ vấn đề gốc đến workflow thực tế, chỉ ra đúng bước tắc nghẽn, và kết thúc bằng metric đo được có baseline + mốc thời gian. Tránh nhảy thẳng vào solution.

- **Trả lời challenge không lảng tránh:** Ví dụ nếu bị hỏi "dữ liệu lịch HIS có đủ không?", trả lời: "Vinmec đã dùng HIS trên 10 năm, dữ liệu lịch sử bác sĩ và lịch hẹn có sẵn — đây là lý do chọn bài này thay vì bài cần EMR bệnh nhân (Card #2)."

- **Chấp nhận kill card nếu hợp lý:** Linh hoạt điều chỉnh nếu nhóm thấy Card #3 (forecast lịch tuần) có impact lớn hơn hoặc feasible hơn trong context cụ thể của lab.

[GROUP SIGNAL] Một nhóm được chấm tốt khi:

- **Không chọn bài trivial:** Tránh bài "gửi SMS nhắc lịch hẹn" nếu chỉ cần Rule-based, không cần AI thực sự.

- **Không chọn bài "ngầu nhưng không làm nổi":** Ví dụ không chọn "AI chẩn đoán hình ảnh X-quang" nếu không có medical imaging data và medical AI compliance framework.

- **Có kill rationale rõ ràng dựa trên evidence:** ROI đo được, data readiness, feasibility trong thời gian lab — không chỉ dựa trên "bài nghe hay".

---

## 🤖 AI Sử Dụng (ghi để reflection sau)

> Ghi lại dưới đây để chuẩn bị cho **Reflection Log** (Phase 6)

- **AI tool nào dùng?**
  - Claude (Anthropic): dùng để scoping bài toán, viết Quick Problem Cards, và soạn Kill Rationale theo context Vinmec.
  - GitHub Copilot: hỗ trợ gợi ý cấu trúc markdown và format bảng.
  - ChatGPT: kiểm tra logic nghiệp vụ y tế, polish câu tiếng Việt trong phần Pitch.

- **Prompt gì dùng?**
  - "Với vai trò AI Product Engineer tại Vinmec, liệt kê 10 bài toán thực tế trong mảng tối ưu lịch hẹn và điều phối bác sĩ theo 4 lens: Lặp lại, Tốn thời gian, AI có thể tốt hơn, Pain từ người khác." (Claude)
  - "Viết Quick Problem Card chi tiết cho bài toán điều phối lịch khi bác sĩ nghỉ đột xuất tại bệnh viện — gồm workflow 6 bước, bottleneck, AI solution, metric đo thành công." (Claude)
  - "Kiểm tra logic Kill Rationale: tại sao loại Card #2 (booking gợi ý slot) dù có impact lớn?" (ChatGPT)

- **Output AI có giúp không? Tại sao?**
  - Rất hữu ích: AI giúp mở rộng danh sách bài toán nhanh (từ 3–4 ý ban đầu lên 10), đặc biệt ở lens "Pain từ người khác" vốn khó tự nghĩ ra.
  - AI gợi ý stakeholder đa chiều (điều phối viên, bác sĩ, bệnh nhân, trưởng khoa) — tránh bẫy chỉ nhìn từ góc kỹ thuật.
  - Metric đề xuất ban đầu còn chung (ví dụ: "tăng hiệu suất") — phải tự tinh chỉnh thành con số cụ thể và cách đo.

- **AI sai/hời hợt chỗ nào? Bạn sửa gì?**
  - Claude ban đầu đề xuất Quick gut cho Card #3 là "AutoML" — không phù hợp vì không phải bài toán classification/regression thuần tuý. Sửa thành "ML Forecast + LLM Draft" và bổ sung lý do human-in-the-loop bắt buộc trong môi trường y tế.
  - ChatGPT đề xuất loại Card #1 vì "khó tích hợp HIS" — nhưng đây là bài toán đọc lịch (read-only query), không cần write API phức tạp. Giữ lại Card #1 và ghi rõ lý do trong Kill Rationale.
  - Phần Pitch ban đầu AI viết theo hướng "product pitch" (marketing) — phải viết lại theo cấu trúc problem → workflow → bottleneck → metric theo yêu cầu lab.

