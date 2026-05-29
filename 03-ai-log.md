# 03 — AI Log & Reflection (Bài Cá Nhân)
## Phase 6 — Nhật Ký Chiêm Nghiệm: AI Làm Thought-Partner

---

## 🤖 AI giúp gì trong buổi lab hôm nay?

Trong buổi lab, mình đã dùng Gemini và Claude như thought-partner để hỗ trợ các việc sau:

**1. Brainstorm và chọn bài toán (Phase 1–2):**
Mình dùng prompt gợi ý trong worksheet để yêu cầu AI liệt kê các pain point vận hành tại Vinmec. AI gợi ý nhiều bài toán thú vị, trong đó có bài toán điều phối lại lịch bác sĩ khi có sự cố đột xuất — một vấn đề xảy ra hàng ngày tại mọi cơ sở nhưng chưa được tự động hóa. AI cũng giúp mình ước tính con số tác động (~80 sự cố/ngày toàn hệ thống 40 cơ sở) để thuyết phục nhóm chọn bài toán này thay vì các bài toán khác.

**2. Thiết kế Future-State Flow (Phase 3.3):**
Mình nhờ AI gợi ý cách chia nhỏ quy trình thành các bước AI có thể xử lý. AI đề xuất cấu trúc Agentic Loop gồm 5 bước (Parse → Query & Rank → Notify bác sĩ → HITL xác nhận → Cập nhật HIS + Notify bệnh nhân), giúp mình hình dung rõ điểm nào cần Human-in-the-loop và điểm nào có thể tự động hoàn toàn.

**3. Tính toán ROI (Phase 5):**
Mình hỏi AI cách ước lượng chi phí vận hành LLM API và SMS gateway theo số lượng sự cố thực tế. AI giúp mình lập bảng chi phí chi tiết và so sánh với lượng nhân công tiết kiệm được, ra con số ROI ~76x trong năm đầu — giúp quyết định GO trở nên thuyết phục hơn trước Ban Giám Đốc.

---

## ❌ AI sai gì?

**1. Đề xuất kiến trúc quá phức tạp ngay từ đầu:**

Khi mình hỏi về giải pháp kỹ thuật, AI ngay lập tức đề xuất xây dựng một *"Multi-Agent hệ thống với Scheduling Agent, Notification Agent, Compliance Agent và Monitoring Agent phối hợp theo kiến trúc event-driven với message queue"*. Đây là kiến trúc production-grade hoàn chỉnh, quá phức tạp cho một prototype lab. Thực tế bài toán chỉ cần một Agentic Loop đơn giản gọi HIS API + gửi notification — không cần đến 4 agent riêng biệt.

**2. Hallucination về quy định pháp lý:**

Khi mình hỏi về compliance dữ liệu y tế tại Việt Nam, AI tự tin trích dẫn *"Thông tư 46/2018/TT-BYT quy định cụ thể về việc gửi thông báo tự động cho bệnh nhân phải có chữ ký số của bác sĩ phụ trách"*. Sau khi mình kiểm tra, thông tư này không có điều khoản như vậy — AI đã hallucinate một quy định không tồn tại, gây mất thời gian kiểm chứng.

---

## 🔧 Sửa đổi ra sao?

**Với vấn đề kiến trúc phức tạp:**
Mình thêm ràng buộc vào prompt: *"Hãy đề xuất giải pháp MVP đơn giản nhất có thể chạy được trong 2–3 sprint (6 tuần) với 2 kỹ sư. Không đề xuất multi-agent nếu một Agentic Loop đơn có thể giải quyết được bài toán."* AI sau đó đơn giản hóa xuống còn một orchestration layer duy nhất — phù hợp hơn với thực tế nguồn lực của nhóm.

**Với vấn đề hallucination pháp lý:**
Mình thay đổi cách hỏi: thay vì hỏi *"Quy định nào áp dụng?"*, mình hỏi *"Những rủi ro pháp lý nào cần lưu ý khi gửi thông báo tự động cho bệnh nhân tại Việt Nam? Chỉ nêu rủi ro chung, không trích dẫn điều luật cụ thể nếu không chắc chắn."* AI trả về danh sách rủi ro tổng quát (bảo vệ dữ liệu cá nhân, consent của bệnh nhân, trách nhiệm pháp lý khi thông báo sai) mà không hallucinate thêm điều luật cụ thể — thông tin đủ để ghi vào phần rủi ro còn lại cần theo dõi.
