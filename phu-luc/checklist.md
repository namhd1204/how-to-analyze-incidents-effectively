---
description: "Checklist tự đánh giá chất lượng hồ sơ phân tích sự cố trước khi hoàn thiện."
icon: square-check
---

# Checklist tự đánh giá hồ sơ

## Tiêu chí tổng quát

* [ ] Chỉ ra được **nguyên nhân gốc rễ**.
* [ ] **Không có yếu tố chỉ trích, đổ lỗi.**
* [ ] Trình bày **trực quan, dễ hiểu**.
* [ ] Có **hình ảnh minh họa, bảng biểu, chỉ số** rõ ràng.
* [ ] Có **hàm lượng nghiên cứu sâu**: kỹ thuật, kỹ năng mới và bài học có thể chia sẻ cho dự án khác.
* [ ] **Biện pháp phòng ngừa** rõ ràng, cụ thể, sát thực tế.

## Câu hỏi kiểm tra theo từng phần

{% tabs %}
{% tab title="Mô tả" %}
* [ ] Có câu tóm tắt đầu tiên nêu rõ cái gì lỗi, từ khi nào, ảnh hưởng bao nhiêu?
* [ ] Có timeline với mốc giờ cụ thể và nguồn?
* [ ] Phạm vi ảnh hưởng được định lượng bằng số liệu?
* [ ] Chỉ nêu sự thật, không lẫn phân tích nguyên nhân?
{% endtab %}

{% tab title="Vấn đề" %}
* [ ] Đã rà đủ các khâu: phân tích, thi công, kiểm thử, thí điểm, triển khai, giám sát?
* [ ] Có cả ba nhóm: lỗi xảy ra, không phát hiện, xử lý chậm?
{% endtab %}

{% tab title="Nguyên nhân" %}
* [ ] Mỗi câu trả lời 5Why có bằng chứng (log, metric, code)?
* [ ] Đã chạm tới nguyên nhân thuộc Man hoặc Method, hành động được?
* [ ] Không dừng ở tiểu tiết kỹ thuật hoặc đổ lỗi khách quan?
* [ ] Đã phân loại 5M?
{% endtab %}

{% tab title="Bài học" %}
* [ ] Viết thành quy tắc dùng lại được, không chỉ kể lại sự việc?
* [ ] Có nêu cách áp dụng cho dự án, nhóm khác?
* [ ] Đã đưa vào runbook, checklist hoặc buổi chia sẻ?
{% endtab %}

{% tab title="Phòng ngừa" %}
* [ ] Mỗi nguyên nhân gốc có ít nhất một biện pháp?
* [ ] Có người thực hiện, thời hạn, tiêu chí hoàn thành?
* [ ] Nếu biện pháp đã có từ trước, sự cố có bị chặn hoặc phát hiện sớm không?
* [ ] Đã rà soát các hệ thống khác có cùng rủi ro?
{% endtab %}
{% endtabs %}
