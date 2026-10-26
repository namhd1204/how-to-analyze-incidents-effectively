---
description: "6 nguyên tắc phân tích sự cố hiệu quả kèm cách áp dụng cho từng nguyên tắc."
icon: list-check
---

# 6 nguyên tắc phân tích hiệu quả

Sáu nguyên tắc dưới đây là điểm chung của những hồ sơ phân tích sự cố chất lượng cao. Mỗi tab gồm nguyên tắc, ví dụ và cách áp dụng.

{% tabs %}
{% tab title="1. Mô tả ngắn gọn" %}
**Nguyên tắc:** mô tả ngắn gọn, cô đọng, logic, nổi bật ý chính, có thông tin định lượng (ngày tháng, số liệu).

**Ví dụ:** "Thí điểm trên 10.000 khách hàng, trung bình hơn 1.000 hóa đơn/ngày trong 3 ngày liên tiếp, tổng khoảng 2 triệu hóa đơn, nhưng vẫn không phát hiện lỗi."

**Áp dụng:**

* Viết câu tóm tắt đầu tiên: cái gì lỗi, từ khi nào, kéo dài bao lâu, ảnh hưởng bao nhiêu.
* Thay từ định tính ("nhiều", "lâu") bằng con số.
* Đẩy chi tiết phụ vào phụ lục.
* Kiểm tra: người ngoài dự án đọc trong 1 phút có nắm được chuyện gì xảy ra không?

Chi tiết: [Bước 1](../quy-trinh/mo-ta-su-co.md).
{% endtab %}

{% tab title="2. Trực quan" %}
**Nguyên tắc:** dùng hình ảnh, sơ đồ, bảng biểu để người đọc nắm nhanh.

**Ví dụ:** nêu số liệu một pod dùng 0,015 core/291 MiB so với giới hạn 0,5 core/500 MiB, từ đó loại trừ giả thuyết thiếu tài nguyên.

**Áp dụng:**

* Timeline dạng bảng hoặc sơ đồ.
* Ảnh chụp biểu đồ CPU, RAM, error rate trước, trong và sau sự cố.
* Sơ đồ luồng chỉ chỗ lỗi xảy ra.
* Sơ đồ 5Why dạng cây.
* Mỗi hình có chú thích nói hình này chứng minh điều gì.
{% endtab %}

{% tab title="3. Xác định vấn đề" %}
**Nguyên tắc:** quy trình càng chặt thì càng khó để lỗi lọt ra khách hàng. Vì vậy cần đánh giá đầy đủ tất cả các khâu để không bỏ sót vấn đề.

**Ví dụ:** 3 vấn đề trong một sự cố: API bị gọi liên tục, thí điểm diện lớn vẫn không phát hiện lỗi, thời gian khắc phục lâu (26 phút).

**Áp dụng:**

* Lập bảng rà từng khâu: phân tích, thi công, review, kiểm thử, thí điểm, triển khai, giám sát, xử lý sự cố.
* Luôn có ít nhất 3 nhóm: lỗi xảy ra, lỗi không bị phát hiện, xử lý chậm.
* Khâu "không có vấn đề" thì ghi rõ bằng chứng.

Chi tiết: [Bước 2](../quy-trinh/xac-dinh-van-de.md).
{% endtab %}

{% tab title="4. Xác định nguyên nhân" %}
**Nguyên tắc:** tập trung vào yếu tố chủ quan, cải tiến được: con người (năng lực chuyên môn, năng lực tuân thủ) và phương pháp (quy chuẩn, quy trình, quy định).

**Ví dụ:** có quy trình, nhân viên tuân thủ, nhưng năng lực chưa đủ: giải pháp thiết kế chưa tối ưu vì dùng async trong vòng lặp LINQ mà C# không hỗ trợ tốt.

**Áp dụng:**

* Chạy 5Why đến khi gặp nguyên nhân thuộc Man hoặc Method.
* Với nguyên nhân "khách quan", hỏi: ta đã làm gì để giảm rủi ro?
* Tự hỏi ba câu: có quy trình chưa? Có tuân thủ không? Năng lực có đủ không?
* Hỏi về hệ thống, không hỏi về cá nhân.

Chi tiết: [5Why](../quy-trinh/5why.md), [5M](../quy-trinh/5m.md).
{% endtab %}

{% tab title="5. Bài học kinh nghiệm" %}
**Nguyên tắc:** bài học phải trả lời làm thế nào là tốt, thế nào là tệ, áp dụng mở rộng cho đâu, có đưa vào runbook hay chia sẻ không.

**Ví dụ:** "Khi xử lý sự cố, tập trung tìm log ngay từ đầu." "Khi full connection, cân nhắc cả việc restart ứng dụng client đang giữ kết nối."

**Áp dụng:**

* Viết bài học thành quy tắc dùng lại được.
* Chia hai nhóm: phát hiện/xử lý nhanh; kỹ thuật/kỹ năng phát triển.
* Với mỗi bài học, hỏi: ở đâu khác cũng có thể gặp?

Chi tiết: [Bước 5](../quy-trinh/bai-hoc.md).
{% endtab %}

{% tab title="6. Biện pháp phòng ngừa" %}
**Nguyên tắc:** chỉ ra quy trình, quy chuẩn nào cần cập nhật; rà soát hàng loạt nếu cần; giao task rõ nội dung, người thực hiện, thời hạn.

**Áp dụng:**

* Mỗi nguyên nhân gốc có ít nhất một biện pháp.
* Ưu tiên tự động hoặc chặn cứng hơn là nhắc nhở.
* Phủ ba hướng: ngăn xảy ra, phát hiện sớm, xử lý nhanh.
* Mỗi task có nội dung, một người chịu trách nhiệm, thời hạn, tiêu chí hoàn thành.
* Theo dõi đến khi đóng và rà soát lại sau 1 đến 3 tháng.

Chi tiết: [Bước 6](../quy-trinh/phong-ngua.md).
{% endtab %}
{% endtabs %}

## Dùng 6 nguyên tắc theo giai đoạn

| Giai đoạn | Nguyên tắc cần dùng |
|---|---|
| Viết mô tả sự cố | 1, 2 |
| Xác định vấn đề | 3 |
| Tìm nguyên nhân gốc rễ | 4 (cùng 5Why, 5M) |
| Bài học và phòng ngừa | 5, 6 |
