# 03 — AI Log & Reflection (Bài Cá Nhân)
## Phase 6 — Nhật Ký Chiêm Nghiệm: AI Làm Thought-Partner

---

## 🤖 AI giúp gì trong buổi lab hôm nay?

Trong buổi lab, mình đã dùng Claude (Anthropic) và Gemini như một thought-partner để hỗ trợ các việc sau:

**1. Brainstorm bài toán (Phase 1 — SCAN):**
Mình dùng prompt gợi ý trong worksheet để yêu cầu AI liệt kê các pain point vận hành tại các công ty Vingroup. AI trả về danh sách khá đa dạng, có cả số liệu ước tính về thời gian thất thoát, giúp mình nhanh chóng có nguyên liệu để chọn lọc thay vì phải suy nghĩ từ đầu.

**2. Stress-test thẻ bài toán (Phase 2 — QUICK-ASSESS):**
Sau khi viết xong Card #1 (Vinmec Discharge Summary), mình dán vào Claude và yêu cầu AI đóng vai CFO phản biện. AI chỉ ra một điểm yếu mình chưa nghĩ tới: *"Bài toán này phụ thuộc vào chất lượng dữ liệu đầu vào từ hệ thống HIS (Hospital Information System) của Vinmec — nếu dữ liệu không chuẩn hóa thì LLM cũng không draft được tốt."* Nhận xét này giúp mình bổ sung phần Operational Boundary cụ thể hơn.

**3. Hỗ trợ viết System Prompt cho prototype (Phase 4):**
Mình nhờ AI gợi ý cấu trúc system prompt có ranh giới an toàn cho bài toán Vinmec. AI draft khá nhanh phần format JSON output và các boundary cơ bản.

---

## ❌ AI sai gì?

**Hallucination về số liệu thống kê:**

Khi brainstorm Phase 1, mình yêu cầu AI cung cấp số liệu cụ thể về tần suất sự cố tại Vinmec và Vinhomes. AI trả về số liệu rất tự tin như *"Vinmec xử lý trung bình 1.200 hồ sơ xuất viện/ngày trên toàn hệ thống"* — nhưng khi mình hỏi nguồn, AI thừa nhận đây là ước tính, không có nguồn xác thực. Đây là hallucination điển hình: AI tạo ra con số nghe có vẻ hợp lý nhưng hoàn toàn không có cơ sở kiểm chứng.

**Đề xuất kiến trúc quá phức tạp:**

Với bài toán phân loại review Vinpearl (Card #3), AI ban đầu đề xuất xây dựng một *"Multi-Agent pipeline với Crawling Agent, Sentiment Agent, và Alert Agent phối hợp theo cơ chế event-driven"*. Trên thực tế, đây là một tác vụ đơn giản có thể giải quyết hoàn toàn bằng một LLM Feature duy nhất kết hợp API scraping — không cần phức tạp hóa thành multi-agent.

---

## 🔧 Sửa đổi ra sao?

**Với vấn đề hallucination số liệu:**
Mình thêm ràng buộc vào prompt: *"Chỉ cung cấp số liệu có nguồn từ báo cáo công khai của Vingroup hoặc ghi rõ là ước tính dựa trên quy mô ngành. Không được tự tạo số liệu."* Sau khi thêm ràng buộc này, AI chủ động ghi chú `[Ước tính dựa trên quy mô ngành]` bên cạnh mỗi con số, giúp mình dễ phân biệt thông tin đáng tin cậy và thông tin cần kiểm chứng thêm.

**Với vấn đề kiến trúc phức tạp không cần thiết:**
Mình điều chỉnh prompt theo hướng: *"Hãy đề xuất giải pháp đơn giản nhất có thể giải quyết được bài toán này. Ưu tiên LLM Feature đơn lẻ trước, chỉ đề xuất Agent nếu thực sự cần thiết và giải thích rõ lý do."* AI sau đó đơn giản hóa xuống còn một LLM Feature với batch processing hằng đêm — phù hợp hơn nhiều với thực tế và chi phí vận hành của Vinpearl.