# AWS SNS (Simple Notification Service)

## Tổng quan:

SNS dùng để gửi tin nhắn, thông báo real-time từ app đến nhiều subscriber qua nhiều protocol (email, SMS, HTTP, Lambda...).

## Best Practice:

- Đặt tên topic rõ ràng, đồng bộ giữa các môi trường.
- Kết hợp CloudWatch cảnh báo lỗi gửi/nhận tin.
- Thiết lập Dead Letter Queue để xử lý message lỗi, cấu hình retry hợp lý.
- Hạn chế quyền truy cập topic, chỉ cho phép chủ thể hợp lệ.

## Use Case thực tế:

Push notification cho ứng dụng mobile/web; cảnh báo hệ thống (DevOps) qua Slack/email; kich hoạt workflow tự động giữa các dịch vụ AWS
