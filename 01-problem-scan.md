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
| 1 | Vinpearl | Repetitive | Nhân viên lễ tân phải trả lời lặp đi lặp lại các câu hỏi hàng ngày như thời gian diễn ra buffet, buggy, spa, giờ hoạt động của resort,...|
| 2 | Vinpearl | Time-consuming| Quản lý điều phối nhân viên dọn phòng thủ công(checklist, gọi điện nội bộ) khiến cho thứ tự dọn dẹp và di chuyển của nhân viên chưa tối ưu dựa trên thời gian checkin checkout thực tế.  |
| 3 | Vinpearl | Stake-holder pain| Khách hàng không nắm được giờ diễn ra của các hoạt động tại bãi biển, resort hay không tìm được dịch vụ phù hợp cho bản thân|
| 4 | Vinpearl | AI-upgrade| | Chatbot CSKH chưa thể hỗ trợ đặt phòng, upsell combo, giảm giá |
| 5 | Vinpearl | AI-upgrade| Bộ phận F&B dự đoán nhu cầu buffet bằng kinh nghiệm dẫn tới lãng phí thực phẩm hoặc thiếu thức ăn vào giờ cao điểm |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Khác hàng tại Vinpearl không nắm được lịch hoạt động và     │
│ dịch vụ phù hợp trong resort, làm giảm trải nghiệm lưu trú  │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                      │
│ [ ] Vinmec   [x] Khác (Vinpearl)                            │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Khách hàng, nhân viên                                       │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Khách tìm thông tin hoạt động/dịch vụ                  │
│   2. Gọi lễ tân hoặc hỏi trực tiếp                          │
│   3. Nhân viên kiểm tra lịch hoạt động                      │
│   4. Gợi ý dịch vụ thủ công                                 │
│   5. Khách tự lựa chọn hoặc tiếp tục hỏi thêm               |
|                                                             |
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Tra cứu lịch hoạt động và tư vấn dịch vụ (⏱ 5-10 phút/lượt)|
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI Concierge có thể tự động gợi ý hoạt động, nhà hàng, beach|
|activity và dịch vụ phù hợp với yêu cầu khách hàng           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - 85% yêu cầu được xử lý dưới 30 giây                       │
│ - Tăng booking dịch vụ nội khu thêm 20%                     │
│ - Giảm 50% workload cho lễ tân                              │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI  [ ] Rule  [x] LLM  [x] Agent                     │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Quản lý điều phối housekeeping thủ công khiến việc dọn      │
│ phòng và check-in/check-out chưa tối ưu.                    │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                      │
│ [ ] Vinmec   [x] Khác (Vinpearl)                            │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Nhân viên housekeeping, supervisor và khách hàng.           │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Supervisor nhận danh sách phòng                        │
│   2. Phân công thủ công qua checklist                       │
│   3. Gọi điện cập nhật trạng thái                           │
│   4. Nhân viên di chuyển dọn phòng                          │
│   5. Lễ tân cập nhật phòng sẵn sàng                         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Điều phối và di chuyển nhân viên (⏱ 10-15 phút/lượt)       │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI tối ưu route dọn phòng và ưu tiên phòng check-in sớm.    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm thời gian turnover phòng 30%                         │
│ - Giảm thời gian check-in chờ đợi xuống dưới 10 phút        │
│ - Giảm overtime housekeeping 20%                            │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI  [ ] Rule  [x] LLM  [x] Agent                     │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Bộ phận F&B dự đoán nhu cầu buffet bằng kinh nghiệm dẫn     │
│ đến lãng phí thực phẩm hoặc thiếu thức ăn giờ cao điểm.     │
│                                                             │
│ Công ty thành viên:                                         │
│ [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes                      │
│ [ ] Vinmec   [x] Khác (Vinpearl)                            │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ Bộ phận bếp, procurement và khách hàng.                     │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Ước lượng số khách                                     │
│   2. Chuẩn bị nguyên liệu                                   │
│   3. Chế biến buffet                                        │
│   4. Theo dõi lượng tiêu thụ                                │
│   5. Điều chỉnh thủ công                                    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Dự đoán nhu cầu buffet (⏱ 30-60 phút/ngày)                 |  
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ AI forecast lượng khách và nhu cầu món ăn theo thời gian.   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm food waste 15–20%                                    │
│ - Giảm thiếu món giờ cao điểm 40%                           │
│ - Tiết kiệm hàng trăm triệu VNĐ/tháng                       │
│                                                             │
│ Quick Architecture:                                         │
│ [ ] No AI  [x] Rule  [x] LLM  [ ] Agent                     │
└─────────────────────────────────────────────────────────────┘
```

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---