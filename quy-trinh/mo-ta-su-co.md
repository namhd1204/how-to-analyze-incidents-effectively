---
description: "Nội dung cần có và cách thu thập thông tin cho bước Mô tả sự cố."
icon: file-lines
---

# Bước 1: Mô tả sự cố

Mô tả sự cố là nền móng của hồ sơ. Các bước sau đều dựa trên những sự thật được ghi ở đây, nên thiếu hoặc sai ở bước này thì phân tích phía sau sẽ lệch.

## Nội dung cần có

{% stepper %}
{% step %}
## Trigger và biểu hiện

* **Trigger**: điều gì kích hoạt sự cố (đợt release, thay đổi cấu hình, tăng tải, thao tác của người dùng...).
* **Biểu hiện**: người dùng hoặc hệ thống thấy gì (không đăng nhập được, màn hình trống số liệu, chậm, service down...).
{% endstep %}

{% step %}
## Diễn biến theo dòng thời gian

Các mốc chính: bắt đầu xảy ra, phát hiện, xử lý, khắc phục xong.
{% endstep %}

{% step %}
## Phạm vi và mức độ ảnh hưởng

Bao nhiêu khách hàng, chức năng, sản phẩm bị ảnh hưởng; nặng đến đâu; kéo dài bao lâu.
{% endstep %}
{% endstepper %}

## Nguyên tắc trình bày

* **Ngắn gọn, cô đọng, logic**, nổi bật ý chính.
* **Định lượng**: ngày giờ, số liệu thay vì từ chung chung.
* **Trực quan**: timeline, biểu đồ, ảnh chụp, bảng.

{% columns %}
{% column %}
### Chưa tốt

"Hệ thống bị chậm một lúc, nhiều khách hàng phản ánh. Sau đó đội xử lý và hệ thống bình thường lại."
{% endcolumn %}

{% column %}
### Tốt

"Từ 08:41 đến 09:07 ngày 14/03 (26 phút), 1.200 khách hàng (khoảng 8% người dùng hoạt động) không đăng nhập được web app. Tỷ lệ request lỗi tăng từ 0,2% lên 37%."
{% endcolumn %}
{% endcolumns %}

{% hint style="info" %}
**Ví dụ về dùng số liệu để loại trừ giả thuyết:** "Vào 08:41 ngày 02/10, hệ thống cảnh báo service down. Trước đó, 1 pod dùng 0,015 core / 291 MiB, trong khi giới hạn là 0,5 core / 500 MiB (3% CPU, 58% RAM). Do đó loại trừ nguyên nhân thiếu tài nguyên."
{% endhint %}

## Cách thu thập thông tin

| Nội dung cần mô tả | Nguồn thu thập gợi ý |
|---|---|
| Trigger | Lịch sử release/deploy (CI/CD), change log, thay đổi cấu hình/hạ tầng, commit/PR gần thời điểm lỗi, đợt tăng tải bất thường |
| Biểu hiện | Ticket hỗ trợ, ảnh chụp màn hình, error message, log ứng dụng, cảnh báo từ hệ thống giám sát |
| Mốc thời gian | Timestamp của alert, log, lịch sử chat xử lý sự cố, ticket, lịch sử deploy/rollback |
| Phạm vi ảnh hưởng | Query log hoặc dữ liệu để đếm khách hàng, request lỗi, giao dịch bị ảnh hưởng; dashboard CPU, RAM, response time, error rate |
| Mức độ ảnh hưởng | Tỷ lệ lỗi, thời gian gián đoạn, có mất/sai dữ liệu không, thiệt hại cho khách hàng |

### Quy trình thu thập

{% stepper %}
{% step %}
## Thu thập sớm, ngay trong lúc xử lý

Log, ảnh chụp dashboard và chat có thể bị ghi đè hoặc xoá (log rotation, thời gian lưu của công cụ giám sát). Hãy lưu lại ngay.
{% endstep %}

{% step %}
## Lập timeline thô

Gộp alert, chat, ticket, lịch sử deploy vào một bảng và sắp theo thời gian.
{% endstep %}

{% step %}
## Đối chiếu nhiều nguồn

Giờ phát hiện thường khác giờ bắt đầu xảy ra thực tế. Lấy mốc bắt đầu từ log hoặc metric, không lấy từ lúc có người báo.
{% endstep %}

{% step %}
## Định lượng phạm vi

Dùng số liệu cụ thể thay vì "nhiều khách hàng".
{% endstep %}

{% step %}
## Hỏi người trực tiếp xử lý

Dev, vận hành, hỗ trợ khách hàng biết những điều log không ghi.
{% endstep %}

{% step %}
## Rút gọn và trực quan hoá

Giữ ý chính và số liệu quan trọng, chuyển chi tiết phụ vào phụ lục. Vẽ timeline, chụp biểu đồ trước và sau sự cố.
{% endstep %}
{% endstepper %}

## Mẫu timeline

| Thời điểm | Sự kiện | Nguồn |
|---|---|---|
| 08:15 | Triển khai phiên bản mới lên production | Lịch sử deploy |
| 08:41 | Tỷ lệ lỗi bắt đầu tăng | Dashboard giám sát |
| 08:52 | Khách hàng đầu tiên báo lỗi | Ticket hỗ trợ |
| 09:00 | Đội phát triển bắt đầu xử lý | Kênh chat sự cố |
| 09:07 | Rollback xong, lỗi về mức bình thường | Lịch sử deploy, dashboard |

{% hint style="warning" %}
Phần mô tả chỉ nêu **sự thật đã xảy ra**. Không phân tích nguyên nhân và không quy lỗi ở đây. Những nội dung đó thuộc [Bước 3: 5Why](5why.md).
{% endhint %}
