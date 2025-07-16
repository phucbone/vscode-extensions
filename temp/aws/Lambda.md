# AWS Lambda

## Tổng quan:

Lambda cho phép chạy code theo sự kiện, không cần quản lý server, thanh toán dựa trên số lần chạy và thời gian thực thi.

## Best Practice:

- Chỉ cung cấp quyền tối thiểu cần cho mỗi hàm Lambda.
- Tối ưu package code, theo dõi logs với CloudWatch.
- Thực thi chức năng nhỏ gọn, tránh làm Lambda quá lớn, phân rã thành microservices.

## Use Case thực tế:

Xử lý file real-time (resize ảnh khi upload S3); xây dựng backend serverless; workflow event-driven (trigger bởi SNS, S3, API Gateway...); xử lý dữ liệu IoT
