# 01 — Problem Scan (Bài Cá Nhân)
## Phase 1 & Phase 2 — SCAN & QUICK-ASSESS

---

# 🔍 Phase 1 — SCAN: Bảng quét cơ hội

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinmec** | Tốn thời gian | Bác sĩ mất 20–30 phút/bệnh nhân để viết tóm tắt hồ sơ xuất viện (Discharge Summary) thủ công từ bệnh án điện tử, dẫn đến quá tải ca trực. |
| 2 | **Xanh SM** | Lặp lại | Điều phối viên phải tra cứu thủ công trạm sạc VinFast còn trụ trống và soạn tin nhắn hướng dẫn gửi tài xế mỗi khi có sự cố hết pin thực địa (~80 lượt/ngày tại Hà Nội). |
| 3 | **Vinhomes** | AI có thể tốt hơn | Hệ thống phân loại khiếu nại cư dân trên App Vinhomes Resident hiện vẫn thủ công, nhân viên CSKH mất 12 tiếng để phân loại và route đúng bộ phận xử lý. |
| 4 | **VinFast** | Pain từ người khác | Khách hàng mô tả lỗi xe bằng tiếng Việt thông thường (ví dụ: *"đi qua gờ giảm tốc kêu cụp cụp ở bánh trước"*), kỹ thuật viên phải tự phán đoán mã lỗi, dễ chẩn đoán sai và tốn thời gian tiếp nhận ban đầu. |
| 5 | **Vinpearl** | Lặp lại | Nhân viên quản lý khách sạn phải đọc thủ công hàng trăm review trên Booking.com, Agoda, Google Maps mỗi tuần để lọc ra các phàn nàn khẩn cấp cần xử lý ngay. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

---

## QUICK PROBLEM CARD #1

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tự động soạn thảo tóm tắt hồ sơ xuất viện        │
│           (Discharge Summary) cho bác sĩ Vinmec.            │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Bác sĩ điều trị tại các bệnh viện Vinmec — đặc biệt       │
│   trong ca trực đêm hoặc ngày có nhiều bệnh nhân xuất viện. │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Bác sĩ đọc lại toàn bộ bệnh án điện tử                 │
│   ──> 2. Tổng hợp kết quả xét nghiệm và chẩn đoán          │
│   ──> 3. Soạn văn bản tóm tắt bằng tay (Word/HIS)          │
│   ──> 4. Trưởng khoa ký duyệt                               │
│   ──> 5. In và giao cho bệnh nhân khi xuất viện             │
│                                                             │
│ Bước nào tốn nhất? Bước 3 (⏱ 20–30 phút/bệnh nhân)         │
│ AI có thể nhảy vào ở bước nào? Bước 2–3                     │
│ (Trích xuất thông tin lâm sàng → Draft tóm tắt ngôn ngữ    │
│  dễ hiểu, bác sĩ chỉ cần review và ký duyệt)               │
│                                                             │
│ Metric đo thành công:                                       │
│   Giảm thời gian soạn từ 25 phút ──> dưới 5 phút/bệnh nhân.│
│   Tỉ lệ bác sĩ chấp nhận bản draft mà không chỉnh sửa lớn  │
│   đạt ≥ 80%.                                                │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

## QUICK PROBLEM CARD #2

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tự động phân loại & điều hướng khiếu nại cư dân  │
│           trên App Vinhomes Resident.                        │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Nhân viên CSKH tại Ban Quản Lý các khu đô thị Vinhomes — │
│   phải đọc thủ công từng phản ánh và phân loại sang đúng    │
│   bộ phận (kỹ thuật, an ninh, vệ sinh, tài chính...).       │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh qua App Vinhomes Resident          │
│   ──> 2. CSKH đọc và phán đoán loại khiếu nại              │
│   ──> 3. Chuyển tiếp thủ công đến bộ phận xử lý            │
│   ──> 4. Bộ phận xử lý tiếp nhận và phản hồi               │
│                                                             │
│ Bước nào tốn nhất? Bước 2–3 (⏱ 8–12 tiếng/ngày tổng cộng) │
│ AI có thể nhảy vào ở bước nào? Bước 2–3                     │
│ (Phân tích nội dung văn bản → Phân loại tự động →           │
│  Route đến đúng bộ phận, CSKH chỉ xử lý các ca ngoại lệ)  │
│                                                             │
│ Metric đo thành công:                                       │
│   85% khiếu nại được phân loại và route đúng trong < 30s.  │
│   Giảm thời gian phản hồi trung bình từ 12 tiếng ──>        │
│   dưới 2 tiếng.                                             │
│                                                             │
│ Quick Architecture: [x] Rule + LLM Feature (Hybrid)        │
└─────────────────────────────────────────────────────────────┘
```

---

## QUICK PROBLEM CARD #3

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Tự động lọc và tổng hợp phàn nàn khẩn cấp từ    │
│           review khách sạn Vinpearl đa nền tảng.            │
│ Công ty thành viên: [x] Vinpearl                            │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Quản lý khách sạn Vinpearl — phải tự đọc hàng trăm review│
│   mỗi tuần trên Booking.com, Agoda, Google Maps để phát     │
│   hiện vấn đề nghiêm trọng cần xử lý ngay.                  │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Nhân viên vào từng nền tảng để đọc review mới          │
│   ──> 2. Copy–paste review vào file Excel theo dõi         │
│   ──> 3. Quản lý đọc và đánh dấu phàn nàn nghiêm trọng     │
│   ──> 4. Họp tuần để xử lý vấn đề phát sinh                │
│                                                             │
│ Bước nào tốn nhất? Bước 1–3 (⏱ 3–4 tiếng/tuần/khách sạn)  │
│ AI có thể nhảy vào ở bước nào? Bước 1–3                     │
│ (Crawl review đa nền tảng → Phân tích sentiment → Gửi      │
│  cảnh báo ngay cho quản lý với các review 1–2 sao khẩn cấp)│
│                                                             │
│ Metric đo thành công:                                       │
│   100% review 1–2 sao được phát hiện và gửi cảnh báo trong │
│   < 1 tiếng sau khi đăng.                                   │
│   Giảm thời gian đọc review thủ công từ 4 tiếng ──>         │
│   dưới 20 phút/tuần/khách sạn.                              │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```