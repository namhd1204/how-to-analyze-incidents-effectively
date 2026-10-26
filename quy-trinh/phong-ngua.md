---
description: "Cách thiết kế, chọn, giao việc và kiểm chứng biện pháp phòng ngừa để sự cố không lặp lại."
icon: shield-halved
---

# Bước 6: Xây dựng biện pháp phòng ngừa

Biện pháp phòng ngừa phải trả lời:

* Làm thế nào để sự cố không lặp lại?
* Cần hành động gì tiếp theo?
* Quy trình, quy chuẩn, quy định nào cần cập nhật?
* Có cần rà soát các sản phẩm, module khác không (xử lý hàng loạt nếu cần)?

Mỗi task phải **rõ về nội dung, người thực hiện, thời hạn**.

## Quy trình 6 bước

{% stepper %}
{% step %}
## Lập bảng truy vết

Nguyên nhân gốc rễ, bài học và biện pháp phải khớp nhau. Mỗi nguyên nhân có ít nhất một biện pháp. Biện pháp không truy ngược được về nguyên nhân thì nên bỏ hoặc xem lại.
{% endstep %}

{% step %}
## Sinh phương án trên cả ba hướng

| Hướng | Câu hỏi | Ví dụ |
|---|---|---|
| Ngăn xảy ra | Làm sao để lỗi này không thể xảy ra? | Pipeline chặn merge nếu thiếu test; lint rule cấm pattern nguy hiểm |
| Phát hiện sớm | Nếu vẫn xảy ra, làm sao biết ngay? | Alert theo chỉ số liên quan; test tải; thí điểm có đo chỉ số cụ thể |
| Giảm thiệt hại, xử lý nhanh | Nếu lọt ra, làm sao giảm ảnh hưởng? | Feature flag; rollback tự động; runbook; quyền truy cập log sẵn |
{% endstep %}

{% step %}
## Chọn phương án theo độ bền vững

Xếp theo mức độ không phụ thuộc vào việc con người phải nhớ:

1. **Loại bỏ hoặc thiết kế lại** để lỗi không thể xảy ra.
2. **Tự động hóa, chặn cứng** (gate trong CI/CD, validation, alert tự động).
3. **Quy trình, checklist** có người kiểm tra.
4. **Đào tạo, nhắc nhở** (yếu nhất, nên đi kèm biện pháp khác).

Với nguyên nhân thuộc Man, đừng chỉ dừng ở đào tạo. Hãy hỏi thêm: có cơ chế nào bắt lỗi nếu người làm vẫn sai không?
{% endstep %}

{% step %}
## Cân nhắc chi phí và rủi ro

Đánh giá mức giảm rủi ro, chi phí, thời gian triển khai và tác dụng phụ. Rủi ro nghiêm trọng, dễ lặp lại thì đầu tư biện pháp mạnh. Rủi ro nhỏ thì dùng biện pháp nhẹ. Chọn vài biện pháp tác động lớn thay vì danh sách dài khó hoàn thành.
{% endstep %}

{% step %}
## Mở rộng phạm vi

* Tìm các sản phẩm, module có cùng pattern rủi ro và rà soát.
* Cập nhật tài liệu dùng chung: quy chuẩn code, checklist release, runbook, tài liệu onboarding.
* Chia sẻ qua buổi tech talk hoặc kênh nội bộ.
{% endstep %}

{% step %}
## Giao việc và theo dõi đến khi đóng

| Thành phần | Yêu cầu |
|---|---|
| Nội dung | Hành động cụ thể, kiểm chứng được (không viết "tăng cường kiểm tra") |
| Người thực hiện | Một người chịu trách nhiệm chính |
| Thời hạn | Ngày cụ thể |
| Tiêu chí hoàn thành | Thế nào là xong |
| Chỉ số hiệu quả | Dấu hiệu chứng minh biện pháp có tác dụng |
{% endstep %}
{% endstepper %}

## Chọn biện pháp theo nhóm 5M

| Nhóm nguyên nhân | Biện pháp điển hình |
|---|---|
| Man | Đào tạo, kèm cặp, chia sẻ kỹ thuật, bổ sung năng lực cho vị trí review |
| Method | Cập nhật quy trình, quy chuẩn, checklist, runbook |
| Machine | Thay đổi cấu hình, nâng cấp hạ tầng, công cụ |
| Material | Kiểm tra đầu vào, ràng buộc dữ liệu, rà soát tài liệu yêu cầu |
| Measurement | Bổ sung alert, dashboard, kịch bản kiểm thử |

## Ví dụ minh họa

Nguyên nhân gốc rễ: *không có quy định kiểm thử cho thay đổi trên luồng đăng nhập (Method)* và *thí điểm không đo chỉ số request treo (Measurement)*. Tên người và ngày tháng là giả định.

| Biện pháp | Hướng | Độ bền vững | Người / Hạn | Tiêu chí hoàn thành |
|---|---|---|---|---|
| Thêm bước test tải bắt buộc vào pipeline cho module luồng đăng nhập | Ngăn xảy ra | Chặn cứng | A / 15/11 | Pipeline chặn release khi test tải không đạt |
| Thêm alert tỷ lệ request treo/timeout vào giám sát | Phát hiện sớm | Tự động | B / 10/11 | Alert đã test, gửi về kênh trực |
| Bổ sung danh sách "luồng quan trọng" vào checklist release; rà soát các sản phẩm khác | Mở rộng | Quy trình | C / 30/11 | Checklist cập nhật, các nhóm xác nhận áp dụng |
| Cập nhật runbook: kiểm tra log, restart client khi full connection | Xử lý nhanh | Quy trình | D / 20/11 | Runbook được duyệt và chia sẻ |

## Cách kiểm chứng biện pháp có hiệu quả

* **Quay ngược thời gian:** nếu biện pháp đã có từ trước, sự cố vừa rồi có bị chặn hoặc phát hiện sớm không?
* **Thử nghiệm thực tế:** với alert hoặc gate tự động, tái hiện tình huống lỗi để xác nhận chúng kích hoạt.
* **Rà soát sau 1 đến 3 tháng:** biện pháp có được áp dụng thật không? Có sự cố tương tự nào xuất hiện không?
* **Người ngoài đọc hiểu được:** người ở dự án khác đọc có biết phải làm gì, ai làm, khi nào xong không.

{% hint style="warning" %}
**Các lỗi cần tránh**

* Biện pháp chung chung: "tăng cường kiểm tra", "nhắc nhở nhân viên".
* Chỉ hotfix rồi coi như đã phòng ngừa.
* Biện pháp không khớp nhóm 5M của nguyên nhân.
* Quá nhiều biện pháp nhỏ, không ai hoàn thành.
* Không giao người, không đặt thời hạn.
* Không theo dõi sau khi giao.
{% endhint %}
