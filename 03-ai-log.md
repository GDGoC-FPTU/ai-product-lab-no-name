# 📝 Phase 6 — AI Log (Nhật ký chiêm nghiệm)

**Người viết:** [Tên - MSSV]  
**Ngày:** 29/05/2026

---

## AI Giúp Cái Gì?

**Brainstorm ý tưởng:** Dùng prompt "*Gợi ý 5 bài toán vận hành cho Vinpearl*" → AI đưa ra list khá hay (lễ tân, housekeeping, F&B forecast). Copy vào bảng SCAN xong.

**Viết Problem Statement:** Hỏi AI về 6-field format → nó draft ra business impact, metrics, operational boundary khá chi tiết. Nhóm lấy đó làm base rồi refine.

**Thiết kế workflow:** Prompt "*vẽ quy trình AI Concierge cho bài toán này*" → AI lên được 6 bước, thời gian, xác định AI fit (LLM + Agent). Giúp visualize nhanh.

**Viết lý giải GO/NO-GO:** AI viết justification khá solid (ROI, payback 6 tháng, tech risk thấp). Copy vào báo cáo, thêm con số cụ thể.

---

## AI Sai Cái Gì?

**1. Con số tài chính quá ảo:**
- AI nói "tiết kiệm 50-100M VNĐ/tháng" nhưng chả có dữ liệu real. Lúc nào tôi hỏi kỹ thì nó confess không có actual data Vinpearl.

**2. HITL quá naive:**
- AI đề xuất "90% request xử lý full AI, chỉ exception mới escalate" → thực ra guest phức tạp hơn, có khoảng 30-40% request cần human decision.

**3. Data readiness chưa sâu:**
- AI nói "6 tháng data là ok" nhưng không đánh giá quality, không hỏi về missing data hay seasonal bias.

---

## Fix Thế Nào?

**1. Kiểm soát con số:**
Prompt lại: "*Mỗi ước lượng tài chính phải kèm công thức (số phòng × occupancy × conversion)*" → AI bây giờ hoặc cung cấp công thức cụ thể, hoặc thành thật nói không đủ dữ liệu.

**2. Làm sáng quy tắc HITL:**
Hỏi AI "*Liệt kê 10 loại request khách, với mỗi loại ghi rõ: AI full? hay cần HITL? ai duyệt?*" → Lúc này AI phân tích từng case (discount → supervisor, disability → specialist), không generic.

**3. Thêm data quality check:**
Prompt: "*Trước fine-tune, gợi ý checklist: bao % records đầy đủ? seasonal imbalance? time to label?*" → AI giúp plan data prep thực tế.

---

## Học Được Gì?

AI tốt để brainstorm & draft nhanh, nhưng **phải validate lại** với thực tế. Số liệu, assumption, workflow cần con người check kỹ. AI output không = final answer, nó cần human sense-check.
S
Bài học: Luôn có quy trình **AI → Human Review → Decision**, đừng tin AI 100%.


---
