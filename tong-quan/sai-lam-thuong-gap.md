---
description: "Những sai lầm thường gặp khi phân tích sự cố và cách tránh từng sai lầm."
icon: triangle-exclamation
---

# Các sai lầm thường gặp

Phần lớn hồ sơ phân tích sự cố chưa đạt chất lượng vì mắc một hoặc nhiều lỗi dưới đây.

{% columns %}
{% column %}
### Mô tả khó hiểu

* Dài dòng, nhiều chữ, lạc trọng tâm.
* Sơ sài, cộc lốc, thiếu thông tin quan trọng.
{% endcolumn %}

{% column %}
### Nguyên nhân gốc rễ sai

* Sa vào tiểu tiết: kỹ thuật lập trình, thông số cấu hình.
* Đổ lỗi khách quan: tài liệu, công cụ, năng lực, bên thứ 3.
* Bỏ sót yếu tố chủ quan: không tuân thủ, thiếu quy trình.
{% endcolumn %}
{% endcolumns %}

Ngoài ra còn:

* Bài học và biện pháp phòng ngừa sai hoặc thiếu.
* Phân công nhiệm vụ không rõ ràng.

## Cách tránh từng sai lầm

| Sai lầm | Dấu hiệu nhận biết | Cách tránh |
|---|---|---|
| Mô tả dài dòng | Người đọc không tóm tắt được trong 1 phút | Viết câu tóm tắt đầu tiên; chuyển chi tiết phụ vào phụ lục |
| Mô tả sơ sài | Có từ "nhiều", "lâu", "một số" mà không có số | Bổ sung thời điểm, số khách hàng, tỷ lệ lỗi, thời gian gián đoạn |
| Sa vào tiểu tiết kỹ thuật | Nguyên nhân gốc là "sai tham số X" | Hỏi tiếp: tại sao sai tham số lại không bị chặn? |
| Đổ lỗi khách quan | Nguyên nhân gốc là "do công cụ/tài liệu/bên thứ 3" | Hỏi: ta đã làm gì để giảm rủi ro từ yếu tố đó? |
| Bỏ sót yếu tố chủ quan | Không nhắc đến quy trình hay năng lực | Tự hỏi: có quy trình chưa? Có tuân thủ không? Năng lực có đủ không? |
| Bài học, phòng ngừa sai hoặc thiếu | Biện pháp không liên quan nguyên nhân | Lập bảng truy vết nguyên nhân, bài học, biện pháp |
| Phân công không rõ | Task không có người hoặc hạn | Mỗi task có nội dung, người thực hiện, thời hạn, tiêu chí hoàn thành |
| Chỉ trích cá nhân | Hồ sơ nêu tên người làm sai | Hỏi về hệ thống: tại sao quy trình cho phép sai sót này lọt qua? |
