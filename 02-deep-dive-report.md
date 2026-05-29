# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)

### Bài toán được chọn
**Problem Card #1 — Vinpearl Concierge AI**
- **Bài toán:** Khách hàng không nắm được lịch hoạt động & dịch vụ phù hợp, làm giảm trải nghiệm lưu trú
- **Bottleneck:** Tra cứu lịch + tư vấn dịch vụ (5-10 phút/lượt)
- **Impact:** Mất 10-20M VNĐ/tháng (upsell thấp)
- **Giải pháp:** AI Concierge Bot (LLM + Agentic Loop + HITL)

---

**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = 5-10 phút/lượt**.

### Quy trình hiện tại (Current-State Workflow):
```
Khách hàng
   │
   ├─→ 1️⃣ [Khách tìm thông tin] 
   │        (Khách đến lễ tân hoặc gọi điện thoại)
   │        ⏱ ~1 phút
   │
   ├─→ 2️⃣ 🔄 [Handoff: Khách ↔ Lễ tân] 
   │        (Tiếp nhận yêu cầu)
   │        ⏱ ~1 phút
   │
   ├─→ 3️⃣ 🔴 [BOTTLENECK: Lễ tân tra cứu]
   │        (Kiểm tra lịch hoạt động từ hệ thống / giấy tờ / gọi bộ phận)
   │        ⏱ ~3-5 phút ❌ TỐN THỜI GIAN
   │
   ├─→ 4️⃣ 🔴 [BOTTLENECK: Tư vấn dịch vụ thủ công]
   │        (Gợi ý không nhất quán, phụ thuộc vào kinh nghiệm lễ tân)
   │        ⏱ ~2-3 phút ❌ KHÔNG CHUẨN
   │
   └─→ 5️⃣ 🔄 [Handoff: Quyết định]
            (Khách chọn hoặc hỏi thêm → quay lại bước 3)
            ⏱ ~1 phút

**Tổng cộng: 5-10 phút/lượt** (quá lâu cho một lần truy vấn đơn giản)
```

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

### 1. Actor / Operator
- **Khách hàng (Guest):** Người lưu trú tại Vinpearl muốn tìm hiểu về các hoạt động, dịch vụ trong resort
- **Nhân viên lễ tân:** Người phải trả lời và tư vấn cho khách

### 2. Current Workflow
1. Khách đến lễ tân hoặc gọi điện thoại hỏi về hoạt động/dịch vụ
2. Lễ tân tra cứu từ lịch in sẵn, email, hoặc ghi chú nội bộ
3. Lễ tân kiểm tra tính khả dụng / điều kiện tham gia
4. Lễ tân tư vấn thủ công dựa trên kinh nghiệm
5. Khách quyết định đặt phòng/dịch vụ hoặc hỏi thêm → quay lại bước 2

### 3. Bottleneck
**Bước 3-4:** Tra cứu lịch hoạt động + tư vấn dịch vụ
- Lệ tân thường bị nhầm lịch, gợi ý không phù hợp với sở thích/ngân sách khách
- Phải gọi nhiều bộ phận (Activities, F&B, Spa, Beach) để xác nhận
- Không có gợi ý AI nên "upsell" thấp (chỉ bán chính hãng)
- Trong giờ cao điểm, khách phải chờ lâu (lễ tân bận)
- **⏱ 5-10 phút/lượt**

### 4. Business Impact
**Chi phí / Tổn thất:**
- Lễ tân bị "kẹt" → không tiếp khách mới → mất doanh thu khách check-in
- Khách không tìm được dịch vụ phù hợp → không book thêm → mất doanh thu dịch vụ ước tính 15-20% revenue F&B, Activity
- Khách chưa hài lòng với trải nghiệm → đánh giá thấp
- **Ước tính tổn thất:** 10-20 triệu VNĐ/tháng (nếu Vinpearl có 80 phòng, occupancy 70%, conversion upsell 30%)

**SLA vi phạm:**
- Guest satisfaction score < 4/5 stars
- Guest wait time > 5 min (không đạt chuẩn Vinpearl)

### 5. Success Metric
✅ **Ngưỡng thành công:**
1. **85% yêu cầu được xử lý dưới 30 giây** (thay vì 5-10 phút hiện tại)
2. **Tăng booking dịch vụ nội khu thêm 20%** (từ 30% → 36% occupancy)
3. **Giảm 50% workload cho lễ tân** (lễ tân có thể tiếp 3x khách hơn)
4. **Guest satisfaction score tăng từ 3.8 → 4.5/5 stars** (vì dịch vụ nhanh, gợi ý chính xác)
5. **Tiết kiệm chi phí lễ tân:** không cần tuyển thêm staff (NLU ~50M VNĐ/năm)

### 6. Operational Boundary
**✅ AI ĐƯỢC PHÉP:**
- Truy vấn cơ sở dữ liệu lịch hoạt động, giá dịch vụ, yêu cầu
- Phân tích sở thích khách (từ booking history, search pattern)
- Gợi ý hoạt động/dịch vụ phù hợp theo budget, thời gian, sở thích
- Trả lời FAQ tự động (giờ hoạt động, giá tiền, yêu cầu, dress code)
- Cung cấp thông tin thực tế (tờ rơi, link đặt vé, hướng dẫn)

**🔴 AI KHÔNG ĐƯỢC:**
- Xác nhận booking dịch vụ (phải xác nhận cuối cùng từ nhân viên)
- Thay đổi giá hoặc thực hiện thanh toán trực tiếp
- Cam kết về trải nghiệm chất lượng mà chưa kiểm chứng
- Tiết lộ thông tin khách hàng riêng tư

**🟠 CẦN DUYỆT:**
- Nếu khách yêu cầu exception (muốn giảm giá, thay đổi lịch trình)
- Nếu AI detect khách VIP (booking lần đầu, travel + gia đình) → escalate sang manager
- Nếu khách có vấn đề đặc biệt (allergia, disability) → gọi nhân viên chuyên đội

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [x] **LLM Feature + Agentic Loop** (kết hợp cả hai).
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

### Future-State Workflow (AI-Powered Concierge):
```
Khách hàng
   │
   ├─→ 1️⃣ 🔵 [AI Concierge Bot nhận yêu cầu]
   │        (Multi-channel: WhatsApp, in-room tablet, Voice, Website)
   │        ⏱ ~5 giây (LLM thực hiện)
   │
   ├─→ 2️⃣ 🔵 [AI parse intent + constraints]
   │        - Detect: ngôn ngữ, loại hoạt động (Activity/Dining/Spa/...)
   │        - Extract: ngôn sách, sở thích, thời gian, số lượng người
   │        - Call function: retrieval_activities_by_filters()
   │        ⏱ ~3 giây (LLM + RAG)
   │
   ├─→ 3️⃣ 🔵 [AI retrieve + rank gợi ý]
   │        - Gọi APIs: Vinpearl activity DB, inventory, pricing
   │        - Rank bằng relevance score + popularity + guest history
   │        - Format: top-3 gợi ý + upsell options
   │        ⏱ ~10 giây (Agent loop)
   │
   ├─→ 4️⃣ 🔵 [AI format response tự nhiên]
   │        - Trả lời bằng language model ngôn ngữ khách
   │        - Bao gồm: mô tả, giá, link đặt vé, đánh giá từ khách khác
   │        ⏱ ~5 giây
   │        ✅ TỔNG CỘNG: ~25-30 giây (đạt SLA!)
   │
   ├─→ 5️⃣ 🟢 [HUMAN REVIEW (nếu cần)]
   │        └─ Nếu confidence < 70% → escalate lên lễ tân
   │        └─ Nếu khách yêu cầu exception → duyệt manager
   │        └─ Nếu tính toán giá / discount → duyệt supervisor
   │        ⏱ ~2-3 phút (chỉ khi cần thiết)
   │
   ├─→ 6️⃣ 🔵 [AI confirm booking + send confirmation]
   │        (Gửi receipt, hướng dẫn, reminder trước 1 giờ)
   │        ⏱ ~5 giây
   │
   └─→ ✅ DONE - Khách hài lòng, lễ tân giải phóng

```

### AI Architecture (Tech Stack):
**🏗️ Architecture Diagram:**
```
┌─────────────────┐
│  Multi-Channel  │  (WhatsApp, In-room tablet, Voice, Web)
│   Input         │
└────────┬────────┘
         │
         ↓
┌──────────────────────────────────────┐
│  🔵 LLM Agentic Loop                  │
│  (Claude 3.5 Sonnet hoặc GPT-4)       │
│                                      │
│  System Prompt:                      │
│  "You are a Vinpearl Concierge..."   │
│                                      │
│  Available Tools:                    │
│  - get_activities()                  │
│  - get_pricing()                     │
│  - get_availability()                │
│  - get_guest_history()               │
│  - book_activity()                   │
│  - escalate_to_human()               │
└──────────────────────────────────────┘
         │
    ┌────┴─────────────────┐
    ↓                      ↓
┌───────────────┐  ┌──────────────────┐
│ 🟢 HITL Queue │ │ 🔵 Format Output │
│ (Escalation)  │  │ (Send Response)  │
└───────────────┘  └──────────────────┘
         │                 │
         └────────┬────────┘
                  ↓
           ┌────────────────┐
           │ 👤 Guest       │ (Multi-language support)
           └────────────────┘
```

### Fallback Strategy (↩️):
| Tình huống lỗi | Fallback action |
|---|---|
| **LLM confidence < 70%** | Escalate → Lễ tân xử lý manual (có AI transcription ghi lại) |
| **API availability DB down** | Return cached top-rated activities từ tháng trước |
| **Khách hỏi vấn đề phức tạp** (e.g., disability accomodation) | Route → SMS alert lễ tân + video call |
| **Request timeout > 60s** | "Xin lỗi, hệ thống tạm chậm. Lễ tân sẽ gọi bạn trong 2 phút." |
| **Spam / Abuse** | Flag request → Human review + block if needed |

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [x] **Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?**
   - ✅ **Có:** Vinpearl booking system (guest profile, activity logs, past inquiries)
   - ✅ **Available:** 6 tháng historical data từ WhatsApp bot logs, lễ tân chat transcripts
   - ⚠️ **Cần chuẩn bị:** Activity inventory DB (lịch diễn ra, slot availability)
   - **Action:** Tổng hợp ~500 conversation examples trong 2 tuần

2. [x] **Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?**
   - ✅ **Có:** HITL mechanism đã thiết kế:
     - Confidence score < 70% → auto-escalate lễ tân
     - Exception requests → manager review
     - Booking chỉ confirm sau khi human approve
   - ✅ **Fallback đầy đủ:** Nếu API down → return cached data
   - ✅ **Log + audit trail:** Tất cả conversation lưu để review sau
   - **Risk residual:** <5% (trong tầm kiểm soát)

3. [x] **Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?**
   - ✅ **Lễ tân:** Hứa support (thay vì tra cứu, họ chỉ approve exceptions)
   - ✅ **Manager:** Ủng hộ → giảm chi phí, tăng revenue
   - ✅ **IT:** Có khả năng integrate APIs
   - ⚠️ **Potential concern:** Lễ tân lo mất việc → **Action:** retrain sang "Guest Advocate" role (escalation, VIP care)

---

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

[x] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**

> **✅ LÝ DO GO (Bắt đầu Prototype):**
>
> **1. Business Case Mạnh (Strong ROI):**
>    - **Current state:** Lễ tân xử lý 5-10 phút/lượt, occupancy 70%, chỉ 30% booking thêm dịch vụ
>    - **Target state:** <30 giây/lượt, occupancy 80%+, 50% booking thêm (upsell)
>    - **Impact tài chính:** ~20-30 triệu VNĐ/tháng revenue add-on + 15-20M chi phí lễ tân tiết kiệm
>    - **Payback period:** <6 tháng
>
> **2. Kỹ thuật Khả Thi (Low Tech Risk):**
>    - 🔵 **LLM + Agentic Loop:** Công nghệ matured (Claude 3.5, GPT-4)
>    - ✅ **HITL & Fallback design:** Risk được mitigate
>    - ✅ **Data sẵn sàng:** 6 tháng transcripts có thể fine-tune ngay
>    - ⚠️ **API integration:** Có IT support, timeline 3-4 tuần
>
> **3. Khả Năng Thực Hiện (Execution Ready):**
>    - **Scope nhỏ:** Pilot tại 1 resort (Vinpearl Nha Trang) trước
>    - **Timeline MVP:** 6 tuần (2 tuần data prep + 2 tuần development + 2 tuần UAT)
>    - **Team:** 1 AI Engineer + 1 Backend dev + 1 QA (có sẵn)
>    - **Cost estimate:** ~2-3 billion VNĐ (low cost, high return)
>
> **4. Dự Kiến Rủi Ro & Giải Pháp:**
>    - ⚠️ **Quality risk:** LLM hallucination → mitigation: RAG + HITL confirmation
>    - ⚠️ **Staff resistance:** Lễ tân lo mất việc → mitigation: retrain + role shift
>    - ⚠️ **Integration delay:** APIs chậm → mitigation: fallback caching + async calls
>    - ⚠️ **Language/cultural fit:** Khách quốc tế → mitigation: multi-lang support + human fallback
>
> **🎯 SUCCESS CRITERIA (Sprint-end review):**
>    - ✅ 70% accuracy (intent + recommendation)
>    - ✅ <30s latency (P95)
>    - ✅ 80% HITL escalation rate < 15% (chỉ exception)
>    - ✅ Guest satisfaction +0.5 stars (vs baseline)
>    - ✅ Booking upsell +15% (conservative vs 20% target)
>
> **📅 NEXT STEP:**
>    - **Week 1-2:** Data collection & labeling (500 conversations)
>    - **Week 3-4:** LLM fine-tuning + tool integration
>    - **Week 5-6:** UAT + staff training + go-live pilot
>    - **Decision gate:** If metrics hit thresholds → roll-out chain Vinpearl khác

---