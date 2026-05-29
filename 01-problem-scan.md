# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinBus | Repetitive + Time-consuming | Đối soát vé và doanh thu tuyến: Nhân viên mất 3-5 giờ/ngày tổng hợp log vé giấy/QR, đối chiếu hệ thống và báo cáo. Sai lệch 6-10%/tháng, gây thất thoát 2-4% doanh thu tuyến. |
| 2 | VinBus | Time-consuming | Lập lịch vận hành tuyến theo thủ công: Điều phối viên phải cân đối số chuyến, giờ cao điểm, bảo trì xe bằng Excel. Mất 15-25 giờ/tuần, tỷ lệ chạy thiếu chuyến 8-12%, ảnh hưởng SLA. |
| 3 | VinBus | AI-upgrade + Stakeholder Pain | Phân loại phản ánh khách hàng từ tổng đài/app: 1,500-2,500 phản hồi/tháng được đọc tay để phân loại lỗi tuyến, thái độ lái xe, chậm chuyến. Phản hồi chậm 3-5 ngày, 20-30% case không được xử lý kịp. |
| 4 | VinBus | Time-consuming | Dự báo nhu cầu theo giờ và tối ưu tần suất: Hiện dựa trên kinh nghiệm điều phối, dẫn tới thừa chuyến 10-15% giờ thấp điểm và thiếu chuyến 12-18% giờ cao điểm, mất 4-7% doanh thu tiềm năng/tháng. |
| 5 | VinBus | Repetitive | Xử lý sự cố vận hành (kẹt xe, xe hỏng, đổi lái): 300-500 sự cố/tháng, điều phối viên gọi điện thủ công để reroute và cập nhật thông báo. Mất 30-60 phút/sự cố, 25% thông báo chậm gây phàn nàn. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

---

### ✅ QUICK PROBLEM CARD #1: Phân tích tình cảm khách hàng

```
┌─────────────────────────────────────────────────────────────┐
│ Bài toán (1 câu):                                           │
│ 2,000+ review/tháng được đọc thủ công bởi CSKH để phân     │
│ loại vấn đề → phản hồi chậm 5-7 ngày, 25% không giải quyết│
│                                                             │
│ Công ty thành viên: [X] WinMart                             │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ → CSKH team, Customer (chờ phản hồi), NPS score (-15%)      │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Nhận review ──> 2. Đọc & phân loại sentiment            │
│   3. Xác định issue ──> 4. Soạn response ──> 5. Gửi phản hồi│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 phân tích (⏱ 180 phút)│
│ AI hỗ trợ: Sentiment tagging + suggest template response   │
│                                                             │
│ Đo thành công (Metric):                                     │
│ • Giảm TTBH (Time-to-first-response): 5 ngày ──> 4 giờ     │
│ • Tăng resolution rate: 75% ──> 92% (1st contact)          │
│ • Tăng NPS: +8-10 points (customer satisfaction)            │
│                                                             │
│ Quick Architecture: [X] Rule  [ ] LLM  [ ] Agent            │
└─────────────────────────────────────────────────────────────┘
```

**🔴 Phân tích 3 điểm yếu (CFO/Trưởng phòng Vận hành):**

1. **Logic sai lệch - AI giải quyết triệu chứng, không căn bệnh:**
   - "25% phàn nàn không được giải quyết" tại sao? Vì sản phẩm kém, dịch vụ tệ, hay vì CSKH không trả lời?
   - Nếu là vấn đề sản phẩm, AI phân tích sentiment nhanh hơn không giải quyết được issue gốc → customer vẫn bất mãn
   - Bạn cần fix product quality trước, không phải optimize CSKH response speed

2. **Metric không đo ROI:**
   - "+8-10 NPS points" có value bao nhiêu tiền? Bao lâu mới thấy retention tăng?
   - CFO hỏi: "Giảm 4 giờ response time → customer retention tăng mấy %? Doanh thu tăng mấy triệu?"
   - Không có conversion metric, không thể justify invest

3. **Rule-based tốt hơn LLM:**
   - Sentiment analysis: Keyword-based classification đơn giản hơn LLM (VD: "tệ, kinh khủng, thất vọng" = negative)
   - Response generation: Template-based (complaint type A → use template A) không cần LLM generate text
   - LLM có risk: hallucinate, generate response không match brand voice, cần human review lại → không tiết kiệm thời gian

---

### ✅ QUICK PROBLEM CARD #2 (VinBus): Phân loại phản ánh khách hàng

```
┌─────────────────────────────────────────────────────────────┐
│ Bài toán (1 câu):                                           │
│ 1,500-2,500 phản hồi/tháng từ tổng đài/app được đọc tay    │
│ để phân loại lỗi tuyến, thái độ lái, chậm chuyến           │
│ → Phản hồi chậm 3-5 ngày, 20-30% case không xử lý kịp      │
│                                                             │
│ Công ty thành viên: [X] VinBus                              │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ → CSKH team, Trưởng tuyến, Khách hàng (chờ giải quyết)     │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Nhận phản hồi (phone/app) ──> 2. Đọc & phân loại       │
│   3. Xác định root cause ──> 4. Forward tới bộ phận         │
│   5. Follow-up ──> 6. Gửi response                          │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 120-180 phút)  │
│ AI hỗ trợ: Phân loại nội dung + routing tự động            │
│                                                             │
│ Đo thành công (Metric):                                     │
│ • Giảm TTBH: 3-5 ngày ──> 2 giờ (automatic triage)          │
│ • Tăng resolution: 70% ──> 95% (within SLA)                 │
│ • Giảm workload: 2,000 case/tháng xử lý bằng tay ──> <500   │
│                                                             │
│ Quick Architecture: [X] Rule  [ ] LLM  [ ] Agent            │
└─────────────────────────────────────────────────────────────┘
```

**🔴 Phân tích 3 điểm yếu (CFO/Trưởng phòng Vận hành):**

1. **Logic không rõ ràng - Phân loại không bằng fix vấn đề:**
   - "2,000 phản hồi/tháng" nhưng chỉ 20-30% không xử lý → tức là 1,400-1,600 được xử lý rồi. Vậy AI phân loại nhanh có giúp gì?
   - Nếu vấn đề là nhân lực CSKH thiếu, bạn cần thêm staff, không phải AI
   - Nếu vấn đề là process chậm, tính root cause rồi fix nó (VD: tuyến nào sự cố thường xuyên → improve tuyến đó)

2. **Metric không capture business impact:**
   - "Giảm TTBH từ 3-5 ngày ──> 2 giờ" có value bao nhiêu? Khách hàng giữ lại hay chuyển sang competitor?
   - CFO hỏi: "Từ 70% ──> 95% resolution, doanh thu khách tăng mấy %? Churn rate giảm mấy %?"
   - Nếu khách hàng chỉ care về kết quả fix vấn đề, không care về response speed → AI optimization vô ích

3. **Rule-based + domain expertise tốt hơn LLM:**
   - Phân loại phản hồi: "Nếu content có 'xe hỏng' → ticket type = breakdown; Nếu có 'chậm' → type = delay" (regex/keywords, không cần NLP)
   - Routing: Rule-based (VD: breakdown → Maintenance team; delay → Operations) → deterministic, trackable
   - LLM risk: Nhập nhằng giữa các loại (VD: "xe chạy chậm vì hỏng" → LLM phân loại sai), cần human verify lại → không tiết kiệm thời gian

---

### ✅ QUICK PROBLEM CARD #3 (VinBus): Dự báo nhu cầu & tối ưu tần suất

```
┌─────────────────────────────────────────────────────────────┐
│ Bài toán (1 câu):                                           │
│ Dự báo nhu cầu theo giờ & tối ưu tần suất hiện dựa trên    │
│ kinh nghiệm → thừa 10-15% (giờ thấp), thiếu 12-18% (cao)   │
│ → mất 4-7% doanh thu tiềm năng/tháng                        │
│                                                             │
│ Công ty thành viên: [X] VinBus                              │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ → Trưởng điều phối, CFO (lost revenue), Khách (xe chật)    │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Thu thập booking data ──> 2. Manual planning           │
│   3. Xác định tần suất chuyến ──> 4. Schedule ──> 5. Monitor│
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 planning (⏱ 900 phút)│
│ AI hỗ trợ: Forecast demand by hour + recommend fleet size  │
│                                                             │
│ Đo thành công (Metric):                                     │
│ • Giảm capacity underutilization: 15% ──> <5% (off-peak)   │
│ • Giảm unfulfilled demand: 18% ──> <8% (peak hour)         │
│ • Tăng revenue per bus: +6-10% (load factor improve)        │
│                                                             │
│ Quick Architecture: [ ] Rule  [X] LLM  [X] Agent           │
└─────────────────────────────────────────────────────────────┘
```

**🔴 Phân tích 3 điểm yếu (CFO/Trưởng phòng Vận hành):**

1. **Logic lạc - AI dự báo ≠ giải quyết vấn đề chi phí:**
   - "Mất 4-7% doanh thu" không phải do dự báo kém, mà do fleet size cố định. Nếu thêm 5-10 xe, vấn đề giải quyết.
   - AI dự báo demand tốt hơn, nhưng vẫn cần resources để cover peak → CapEx không giảm, chỉ optimize scheduling
   - CFO hỏi: "Chi phí add 5 xe + operation = X tỷ/năm. Revenue uplift = 6-10% = Y tỷ. ROI = Y/X là bao nhiêu?"

2. **Metric quá lạc quan & không capture seasonality:**
   - "Giảm underutilization từ 15% ──> 5%" giả định demand pattern ổn định. Nhưng Tết, mưa, sự kiện → demand spike không dự đoán được
   - Historical forecasting method (moving average) đã handle 80% cases. AI forecast gain chỉ ~10-15% accuracy improvement
   - Nếu bạn claim +6-10% revenue, bạn có holdout test data từ peak season không?

3. **Rule-based heuristic + small ML models tốt hơn LLM:**
   - Demand forecasting không cần LLM. Dùng ARIMA/Prophet để predict hourly demand, sau đó greedy packing algorithm để schedule buses
   - LLM không hiểu logistics constraints (VD: bus turnaround time = 30 phút, driver shift = 8 giờ) → forecast sẽ không feasible
   - Simple rule: IF (forecast demand per hour) > threshold THEN add contingency bus; ELSE run as planned
   - Simpler = faster iteration, easier audit, less compute cost

---

### ✅ QUICK PROBLEM CARD #6 (VinBus): Xử lý sự cố vận hành

```
┌─────────────────────────────────────────────────────────────┐
│ Bài toán (1 câu):                                           │
│ 300-500 sự cố/tháng (kẹt xe, xe hỏng, đổi lái) được điều   │
│ phối viên gọi điện thủ công reroute + thông báo             │
│ → 30-60 phút/sự cố, 25% thông báo chậm gây phàn nàn        │
│                                                             │
│ Công ty thành viên: [X] VinBus                              │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ → Dispatcher team, Lái xe (manual instruction), Khách       │
│                                                             │
│ Workflow thủ công hiện tại:                                 │
│   1. Phát hiện sự cố ──> 2. Dispatcher nhận phone call      │
│   3. Xác định vấn đề ──> 4. Gọi lái khác ──> 5. Thông báo  │
│   6. Monitor & update ──> 7. Close case                     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-5 decision (⏱ 40 phút)│
│ AI hỗ trợ: Auto-detect sự cố + suggest reroute solution    │
│                                                             │
│ Đo thành công (Metric):                                     │
│ • Giảm MTTI (Mean Time To Incident): 40 phút ──> 5 phút    │
│ • Tăng messaging success: 75% ──> 98% (real-time alert)    │
│ • Giảm passenger complaints: -25% (fast resolution)         │
│                                                             │
│ Quick Architecture: [X] Rule  [ ] LLM  [ ] Agent            │
└─────────────────────────────────────────────────────────────┘
```

**🔴 Phân tích 3 điểm yếu (CFO/Trưởng phòng Vận hành):**

1. **Logic ưu tiên sai - Speed không phải constraint chính:**
   - Sự cố kẹt xe: Nếu jam, không gọi xe khác cũng không giúp. Vấn đề là tuyến nên qua đường nào → phân tích traffic real-time
   - Sự cố xe hỏng: Cần backup driver + repair logistics, không phải gọi nhanh hơn sẽ tốt hơn
   - AI "auto-detect" sự cố từ GPS/IoT có thể work, nhưng "suggest reroute" cần real-time traffic data + optimization khó

2. **Metric không thực tế:**
   - "Giảm MTTI từ 40 phút ──> 5 phút" là nói AI phát hiện sự cố tự động. Nhưng hiện tại driver báo sự cố bằng app/call rồi, không phải chờ.
   - Real bottleneck: Decision making & rerouting optimization, không phải phát hiện sự cố
   - "Tăng messaging success 75% ──> 98%" - 75% là số gì? SMS fail rate? Hay passenger không check notification?

3. **Rule-based traffic + logic flow tốt hơn AI:**
   - Sự cố detection: IF GPS stopped for >5 min OR speed = 0 in middle of road → suspect accident (rule, không cần AI)
   - Rerouting: Pre-computed alternative routes per tuyến + capacity check (IF alternative bus available THEN assign; ELSE wait for next)
   - Notification: Batch send SMS+push app = best effort delivery (technical standard, không cần ML improve)
   - Complexity: 80% cases handled by simple rule engine; only edge cases need human judgment

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---
