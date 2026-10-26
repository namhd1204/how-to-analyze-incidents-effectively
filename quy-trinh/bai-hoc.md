---
description: "Cách rút ra bài học kinh nghiệm hữu ích, có thể áp dụng mở rộng sau sự cố."
icon: lightbulb
---

# Bước 5: Rút bài học kinh nghiệm

Bài học kinh nghiệm cần trả lời ba câu hỏi:

* Làm thế nào là tốt, làm thế nào là tệ?
* Có áp dụng mở rộng cho tình huống hoặc nhóm khác được không?
* Có nên đưa vào runbook, checklist hoặc buổi chia sẻ không?

Hồ sơ nên có hai nhóm bài học:

* **Kinh nghiệm phát hiện, xử lý nhanh sự cố.**
* **Kinh nghiệm về phương pháp, kỹ thuật, kỹ năng phát triển sản phẩm.**

{% hint style="info" %}
**Ví dụ bài học tốt:**

* "Khi xử lý sự cố, tập trung tìm log liên quan ngay từ đầu thay vì thử đoán nguyên nhân."
* "Khi báo full connection tới cơ sở dữ liệu, cân nhắc cả việc restart ứng dụng client đang giữ kết nối."
{% endhint %}

## Cách rút ra bài học hữu ích

### 1. Nhìn lại toàn bộ vòng đời sự cố

| Nhóm | Câu hỏi | Ví dụ |
|---|---|---|
| Làm tốt, cần giữ | Điều gì giúp phát hiện hoặc xử lý tốt? | Phát hiện nhanh nhờ alert gửi về kênh chat |
| Làm chưa tốt | Điều gì làm chậm hoặc làm tệ hơn? | Khắc phục mất 26 phút vì không biết ai có quyền xem log |
| May mắn | Điều gì lần này thuận lợi nhưng lần sau chưa chắc? | Lỗi xảy ra ngoài giờ cao điểm |

### 2. Nâng từ sự việc lên nguyên tắc

Bài học tốt là quy tắc dùng lại được, không phải kể lại sự cố.

{% columns %}
{% column %}
### Yếu

"Cần cẩn thận khi dùng async trong ForEach."
{% endcolumn %}

{% column %}
### Tốt

"Khi dùng async trong vòng lặp LINQ ở C#, phải kiểm tra hành vi thực tế bằng test tải và đưa vào checklist code review."
{% endcolumn %}
{% endcolumns %}

### 3. Cụ thể, hành động được

Đọc xong phải biết cần làm gì khác đi, ở khâu nào, theo cách nào.

### 4. Hỏi "ở đâu khác cũng có thể xảy ra?"

Đây là cách biến bài học của một dự án thành giá trị cho cả tổ chức.

### 5. Làm cùng nhóm sau sự cố

Tổ chức buổi rút kinh nghiệm không quy lỗi cá nhân (blameless postmortem) với người trực tiếp xử lý, QA, vận hành. Làm sớm khi mọi người còn nhớ rõ, thường trong vài ngày đầu.

### 6. Truy ngược được về nguyên nhân

Mỗi bài học nên gắn với một nguyên nhân hoặc vấn đề cụ thể. Nếu không, đó có thể chỉ là lời khuyên chung chung.

## Nơi lưu và chia sẻ bài học

| Loại bài học | Nơi lưu |
|---|---|
| Cách phát hiện, chẩn đoán, xử lý nhanh | Runbook xử lý sự cố |
| Lỗi kỹ thuật cần tránh | Checklist code review, quy chuẩn lập trình |
| Điểm cần kiểm tra trước khi phát hành | Checklist release |
| Kỹ năng, kiến thức mới | Buổi chia sẻ kỹ thuật, tài liệu onboarding |

## Câu hỏi tự kiểm tra

* Người ở nhóm khác đọc có biết phải làm gì khác đi không?
* Bài học có truy ngược được về một nguyên nhân cụ thể không?
* Đã có nơi lưu để người mới cũng tìm thấy chưa?
