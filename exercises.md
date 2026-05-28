# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature tăng từ 0.0 đến 1.5, phản hồi trở nên ngẫu nhiên và đa dạng hơn. Ở temperature 0.0, mô hình luôn chọn token có xác suất cao nhất (xác định), dẫn đến phản hồi lặp lại. Ở temperature cao (1.5), mô hình có thể chọn các token ít xác suất hơn, tạo ra phản hồi sáng tạo nhưng có thể kém tuân thủ logic.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature ở 0.3-0.5. Vì chatbot hỗ trợ khách hàng cần phản hồi chính xác, nhất quán và đáng tin cậy hơn là sáng tạo. Temperature thấp đảm bảo câu trả lời theo logic và tránh thông tin sai lệch, đồng thời vẫn giữ một chút biến thiên để tránh phản hồi nhàm chán.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tính toán: 10,000 người × 3 gọi × 350 token = 10.5M token/ngày. GPT-4o chi phí: (10.5M × 5.00 + 10.5M × 20.00)/1M = $262.50/ngày. GPT-4o-mini chi phí: (10.5M × 0.150 + 10.5M × 0.600)/1M = $7.88/ngày. GPT-4o đắt hơn khoảng **33 lần** so với GPT-4o-mini.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> **GPT-4o xứng đáng:** Các tác vụ yêu cầu suy luận phức tạp, tóm tắt tài liệu dài, phân tích code, hoặc dịch chuyên sâu. Ví dụ: hỗ trợ DevOps phân tích log lỗi, tư vấn pháp lý phức tạp, hoặc tạo nội dung marketer. **GPT-4o-mini tốt hơn:** Các tác vụ đơn giản như phân loại, trích xuất dữ liệu cơ bản, trả lời FAQ, hoặc kiểm tra chính tả. Ví dụ: chatbot e-commerce, bộ lọc spam, hoặc auto-tagging sản phẩm.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming rất quan trọng cho ứng dụng web/mobile yêu cầu phản hồi tức thời như chatbot, code generator, hoặc AI assistant. Người dùng nhận được token đầu tiên trong 0.1-0.5 giây thay vì chờ vài giây, cải thiện trải nghiệm đáng kể. Tuy nhiên, non-streaming phù hợp hơn cho xử lý batch (ETL, duyệt danh sách hàng loạt), tác vụ backend không cần phản hồi tức thời, hoặc khi bạn cần token count chính xác trước khi hiển thị. Non-streaming cũng đơn giản hơn khi xử lý lỗi và không cần quản lý kết nối streaming.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
