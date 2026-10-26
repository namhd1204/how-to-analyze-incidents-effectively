---
description: "Ví dụ một hồ sơ phân tích sự cố hoàn chỉnh (giả định) từ mô tả đến biện pháp phòng ngừa."
icon: file-circle-check
---

# Ví dụ hồ sơ hoàn chỉnh

{% hint style="info" %}
Toàn bộ nội dung dưới đây là **giả định** để minh họa cách điền hồ sơ.
{% endhint %}

## Sự cố: khách hàng không đăng nhập được web app sau release

### 1. Mô tả sự cố

**Tóm tắt:** từ 08:41 đến 09:07 ngày 14/03 (26 phút), 1.200 khách hàng (khoảng 8% người dùng hoạt động) không đăng nhập được web app. Tỷ lệ request lỗi tăng từ 0,2% lên 37%.

**Trigger:** phát hành phiên bản mới lúc 08:15, trong đó màn hình đăng nhập gọi thêm một API tải cấu hình người dùng.

| Thời điểm | Sự kiện | Nguồn |
|---|---|---|
| 08:15 | Triển khai phiên bản mới | Lịch sử deploy |
| 08:41 | Tỷ lệ lỗi bắt đầu tăng | Dashboard giám sát |
| 08:52 | Ticket khách hàng đầu tiên | Hệ thống hỗ trợ |
| 08:55 | Alert tỷ lệ lỗi gửi về kênh trực | Công cụ giám sát |
| 09:00 | Bắt đầu điều tra, mất khoảng 5 phút tìm đúng log | Kênh chat sự cố |
| 09:07 | Rollback xong, lỗi về mức bình thường | Lịch sử deploy |

### 2. Xác định vấn đề

| # | Vấn đề | Nhóm |
|---|---|---|
| 1 | API cấu hình bị gọi lặp liên tục, làm treo request | Xảy ra |
| 2 | Thí điểm 3 ngày trên nhóm khách hàng lớn vẫn không phát hiện lỗi | Không phát hiện |
| 3 | Alert chỉ kích hoạt sau 14 phút kể từ khi lỗi bắt đầu | Không phát hiện |
| 4 | Tổng thời gian khắc phục 26 phút, trong đó 5 phút tìm log | Xử lý chậm |

### 3. Nguyên nhân gốc rễ

**Vấn đề 1 (xảy ra):** request treo, vì API cấu hình bị gọi lặp, vì logic gọi lại khi lỗi không có giới hạn số lần, vì thiết kế không có yêu cầu retry có kiểm soát, vì checklist review không có mục kiểm tra retry với API mới.

**Vấn đề 2 và 3 (không phát hiện):** thí điểm chỉ đo số lượng giao dịch, không đo tỷ lệ request treo, vì tiêu chí thí điểm chưa có chỉ số kỹ thuật; ngưỡng alert đặt theo trung bình 15 phút nên phản ứng chậm.

**Vấn đề 4 (xử lý chậm):** log của dịch vụ đăng nhập nằm ở công cụ ít người có quyền, và runbook chưa nói rõ vị trí log.

| Nguyên nhân gốc rễ | Nhóm 5M | Bằng chứng |
|---|---|---|
| Checklist review không có mục kiểm tra retry và giới hạn gọi API | Method | Checklist hiện hành |
| Tiêu chí thí điểm không có chỉ số kỹ thuật (tỷ lệ lỗi, timeout) | Method | Báo cáo thí điểm |
| Ngưỡng alert quá rộng, không bắt được tăng đột biến | Measurement | Cấu hình alert |
| Runbook thiếu hướng dẫn vị trí log và quyền truy cập | Method | Runbook hiện hành |
| Dev chưa nắm pattern retry an toàn (backoff, giới hạn lần) | Man | Kết quả review code |

### 4. Bài học kinh nghiệm

**Phát hiện, xử lý nhanh:**

* Với sự cố sau release, kiểm tra lịch sử deploy trước tiên và rollback sớm nếu thời điểm lỗi trùng khớp.
* Chuẩn bị sẵn quyền truy cập log cho người trực để không mất thời gian xin quyền.

**Phương pháp, kỹ thuật:**

* Mọi lời gọi API mới trong luồng quan trọng phải có giới hạn retry, backoff và timeout.
* Thí điểm phải đo cả chỉ số kỹ thuật, không chỉ số lượng giao dịch.

### 5. Biện pháp phòng ngừa

| Biện pháp | Nguyên nhân | Hướng | Người / Hạn | Tiêu chí hoàn thành |
|---|---|---|---|---|
| Thêm mục "retry, backoff, timeout" vào checklist review; thêm lint rule nếu khả thi | Checklist thiếu; Dev chưa nắm pattern | Ngăn xảy ra | A / 31/03 | Checklist cập nhật, đã dùng trong ít nhất 5 PR |
| Thêm chỉ số tỷ lệ lỗi và timeout vào tiêu chí thí điểm | Tiêu chí thí điểm thiếu | Phát hiện sớm | B / 31/03 | Mẫu báo cáo thí điểm mới được duyệt |
| Chỉnh alert tỷ lệ lỗi sang cửa sổ 2 phút, ngưỡng 5% | Ngưỡng alert rộng | Phát hiện sớm | C / 21/03 | Alert đã thử với dữ liệu giả lập và kích hoạt đúng |
| Bổ sung vị trí log và cấp quyền cho nhóm trực vào runbook | Runbook thiếu | Xử lý nhanh | D / 28/03 | Runbook được duyệt, người trực thử truy cập thành công |
| Rà soát các dịch vụ có luồng quan trọng khác về retry không giới hạn | Mở rộng | Mở rộng | E / 15/04 | Danh sách rà soát và các lỗi tìm thấy được xử lý hoặc ghi nhận |
| Chia sẻ bài học tại buổi tech talk | Bài học | Mở rộng | A / 10/04 | Buổi chia sẻ diễn ra, tài liệu lưu nội bộ |

**Rà soát hiệu quả:** họp lại sau 3 tháng để kiểm tra các biện pháp đã áp dụng thật và không có sự cố tương tự.
