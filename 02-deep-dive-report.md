# 02 — Deep-Dive Report (Bài Nhóm)
## Phase 3 & Phase 5 — DEEP-DIVE & EVALUATE

---

## 👥 Thông tin nhóm

| Thông tin | Chi tiết |
|---|---|
| **Tên nhóm** | No Name |
| **Repository** | ai-product-lab-no-name |

> ⚠️ **Lưu ý:** Các thành viên vui lòng bổ sung Họ tên và MSSV của từng người vào bảng dưới đây trước khi nộp bài.

| # | Họ và tên | MSSV |
|---|-----------|------|
| 1 |Lê Quốc Anh|2A202600824|
| 2 |Hoàng Hải  |2A202600948|
| 3 |Vũ Ngọc Vinh|2A202600864 |
| 4 |Nguyễn Danh Thành|2A202600581|

---

## 🗳️ Quyết định lựa chọn bài toán

**Bài toán được chọn:** Tự động phân loại và điều hướng khiếu nại cư dân trên App Vinhomes Resident.

**Lý do lựa chọn:**
- Quy trình hiện tại hoàn toàn thủ công, lặp lại hằng ngày với khối lượng lớn — phù hợp để áp dụng LLM Feature.
- Metric đo lường rõ ràng, dễ kiểm chứng sau khi triển khai.
- Rủi ro thấp: sai sót trong phân loại khiếu nại không gây nguy hiểm trực tiếp, dễ kiểm soát bằng Human-in-the-loop.
- Dữ liệu đầu vào (text khiếu nại tiếng Việt) phong phú và có sẵn từ hệ thống App hiện tại.

---

# 🏗️ Phase 3 — DEEP-DIVE

## 3.1. Current-State Workflow

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│ Bước 1           │     │ Bước 2           │     │ Bước 3           │     │ Bước 4           │
│ Cư dân gửi       │     │ CSKH đọc thủ     │     │ CSKH chuyển      │     │ Bộ phận xử lý    │
│ phản ánh qua     │ ──→ │ công từng phản   │ ──→ │ tiếp thủ công    │ ──→ │ tiếp nhận và     │
│ App Vinhomes     │     │ ánh, phán đoán   │     │ đến đúng bộ      │     │ phản hồi cư dân  │
│ Resident         │     │ loại khiếu nại   │     │ phận xử lý       │     │                  │
│                  │     │                  │     │                  │     │                  │
│ Ai: Cư dân       │     │ Ai: Nhân viên    │     │ Ai: Nhân viên    │     │ Ai: Kỹ thuật /   │
│ ⏱ 0 phút         │     │ CSKH             │     │ CSKH             │     │ An ninh / Vệ sinh│
│                  │     │ ⏱ 5–8 phút/lượt  │     │ ⏱ 3–5 phút/lượt  │     │ ⏱ Biến động      │
│                  │     │ 🔴 Bottleneck    │     │ 🔴 Bottleneck    │     │                  │
│                  │     │ 🔄 Handoff       │     │ 🔄 Handoff       │     │                  │
└──────────────────┘     └──────────────────┘     └──────────────────┘     └──────────────────┘

🔴 = Bottlenecks (Bước 2 và 3)
🔄 = Handoff points
⏱ Tổng thời gian xử lý thủ công: 8–13 phút/lượt × ~50 lượt/ngày = ~10 tiếng nhân công/ngày
```

---

## 3.2. Problem Statement (6-field)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH tại Ban Quản Lý các khu đô thị Vinhomes — làm việc ca hành chính, chịu trách nhiệm tiếp nhận và phân loại toàn bộ phản ánh từ cư dân gửi qua App Vinhomes Resident. |
| **2. Current Workflow** | Cư dân gửi phản ánh dạng text tự do qua App → Nhân viên CSKH đọc thủ công từng tin → Phán đoán loại khiếu nại (kỹ thuật điện nước, thang máy, an ninh, vệ sinh, tài chính, tiếng ồn...) → Chuyển tiếp thủ công qua email/điện thoại đến bộ phận xử lý tương ứng. Toàn bộ quy trình thủ công, không có công cụ hỗ trợ phân loại tự động. |
| **3. Bottleneck** | Bước 2 & 3: Đọc và phân loại thủ công (~5–8 phút/lượt) + Chuyển tiếp thủ công (~3–5 phút/lượt). Với ~50 khiếu nại/ngày tại một khu đô thị lớn, nhân viên CSKH mất toàn bộ thời gian làm việc chỉ để phân loại và route, không còn thời gian xử lý các ca phức tạp cần tư vấn trực tiếp. |
| **4. Business Impact** | ~10 tiếng nhân công lãng phí/ngày/khu đô thị cho tác vụ phân loại thuần túy. Thời gian phản hồi trung bình đến cư dân là 12 tiếng, gây bức xúc và ảnh hưởng đến chỉ số hài lòng cư dân (NPS) của Vinhomes. Chi phí nhân sự CSKH cao cho tác vụ có thể tự động hóa hoàn toàn. |
| **5. Success Metric** | 1. 85% khiếu nại được phân loại và route đúng bộ phận trong vòng < 30 giây (Efficiency + Accuracy). 2. Giảm thời gian phản hồi trung bình đến cư dân từ 12 tiếng xuống dưới 2 tiếng (Response Time). 3. Nhân viên CSKH giảm thời gian dành cho tác vụ phân loại từ ~10 tiếng/ngày xuống còn < 1 tiếng/ngày (chỉ xử lý ngoại lệ). |
| **6. Operational Boundary** | **AI được phép:** Đọc nội dung phản ánh text của cư dân, phân loại vào 1 trong 8 danh mục định sẵn (điện nước, thang máy, an ninh, vệ sinh môi trường, tiếng ồn, tài chính/phí dịch vụ, hạ tầng chung, khác), tạo ticket và route tự động đến bộ phận xử lý tương ứng, gửi tin nhắn xác nhận tự động đến cư dân. **TUYỆT ĐỐI CẤM:** AI không được tự ý cam kết thời hạn xử lý hoặc đưa ra quyết định về mức bồi thường/miễn phí dịch vụ — các trường hợp này bắt buộc chuyển lên CSKH cấp cao duyệt thủ công. AI không được xử lý các khiếu nại liên quan đến tranh chấp pháp lý hoặc an toàn khẩn cấp (cháy nổ, ngập lụt nghiêm trọng) — phải kích hoạt quy trình khẩn cấp riêng. |

---

## 3.3. Future-State Flow & AI Fit

**AI Fit:** ✅ **LLM Feature** — Phân loại text tiếng Việt có cấu trúc rõ ràng, output có thể kiểm chứng ngay, không cần Agent tự trị.

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│ Bước 1           │     │ Bước 2           │     │ Bước 3           │     │ Bước 4           │
│ Cư dân gửi       │     │ 🔵 AI tự động    │     │ 🔵 Hệ thống      │     │ 🟢 CSKH review   │
│ phản ánh qua     │ ──→ │ phân tích text   │ ──→ │ auto-route       │ ──→ │ các ca ngoại lệ  │
│ App Vinhomes     │     │ và phân loại     │     │ ticket đến đúng  │     │ và ca khẩn cấp   │
│ Resident         │     │ khiếu nại        │     │ bộ phận + gửi    │     │ (HITL)           │
│                  │     │ (< 30 giây)      │     │ xác nhận cư dân  │     │                  │
└──────────────────┘     └──────────────────┘     └──────────────────┘     └──────────────────┘
                                                                                    │
                                                          ↩️ Fallback:              │
                                                          Nếu AI confidence < 70%  │
                                                          hoặc phát hiện từ khóa   │
                                                          khẩn cấp (cháy, ngập,    │
                                                          tranh chấp pháp lý)      │
                                                          → Chuyển thẳng lên CSKH  │
                                                          xử lý thủ công như cũ    │
```

**Phân loại AI Fit:**
- 🔵 **AI Step (LLM):** Bước 2 — Phân tích và phân loại text khiếu nại tiếng Việt.
- 🔵 **Rule Step:** Bước 3 — Route tự động dựa trên output phân loại từ LLM (rule-based mapping).
- 🟢 **Human-in-the-Loop (HITL):** Bước 4 — CSKH chỉ xử lý các ca có độ tin cậy thấp, ca khẩn cấp, và ca tranh chấp pháp lý.
- ↩️ **Fallback:** Khi LLM trả về confidence score < 70% hoặc phát hiện từ khóa nguy hiểm → tự động escalate lên CSKH cấp cao.

---

# 🏁 Phase 5 — EVALUATE

## AI Readiness Checklist

| # | Tiêu chí | Đánh giá |
|---|----------|----------|
| 1 | Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? | ✅ **Có** — App Vinhomes Resident đã có lịch sử khiếu nại từ cư dân, có thể export để tạo training/test set. |
| 2 | Rủi ro khi AI sai có nằm trong tầm kiểm soát? | ✅ **Có** — Sai sót phân loại chỉ làm chậm xử lý, không gây nguy hiểm. Fallback về CSKH thủ công khi confidence thấp đảm bảo kiểm soát rủi ro. |
| 3 | Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? | ✅ **Có** — Nhân viên CSKH sẵn sàng vì giải pháp giúp giảm tải tác vụ lặp lại nhàm chán, không lo mất việc (CSKH vẫn xử lý ca phức tạp). |

## Quyết định cuối cùng

✅ **GO — Bắt đầu xây dựng Prototype với scope hẹp**

**Justification (Lý giải dựa trên bằng chứng kỹ thuật và chi phí):**

**Lý do GO:**

1. **Bài toán rõ ràng, dữ liệu có sẵn:** Input là text tiếng Việt tự do, output là 1 trong 8 danh mục cố định — đây là bài toán text classification điển hình mà LLM xử lý tốt. Dữ liệu lịch sử khiếu nại đã có sẵn trong hệ thống App.

2. **ROI cao, chi phí thấp:** Tiết kiệm ~10 tiếng nhân công/ngày/khu đô thị. Với Vinhomes vận hành hàng chục khu đô thị lớn, tổng tiết kiệm nhân công rất đáng kể. Chi phí gọi Gemini API để phân loại ~50 khiếu nại/ngày ước tính dưới 1 USD/ngày — không đáng kể so với chi phí nhân sự.

3. **Rủi ro thấp, kiểm soát được:** Cơ chế Fallback (confidence < 70% → escalate CSKH) và HITL đảm bảo không có khiếu nại nào bị bỏ sót hay xử lý sai hoàn toàn mà không có người kiểm tra.

4. **Scope hẹp, dễ triển khai thí điểm:** Bắt đầu với 1 khu đô thị thí điểm, đo metric thực tế trong 1 tháng, sau đó scale ra toàn hệ thống Vinhomes.

**Ước lượng chi phí triển khai:**
- Development: 2–3 tuần (1 AI Engineer + 1 Backend Developer).
- API cost vận hành: < 30 USD/tháng/khu đô thị (ước tính ~50 khiếu nại/ngày × 30 ngày × ~0.02 USD/call).
- Maintenance: Tái huấn luyện/cập nhật prompt định kỳ mỗi quý
