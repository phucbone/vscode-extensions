# EventBridge

## Tổng quan:

EventBridge là dịch vụ event bus serverless cho routing sự kiện giữa AWS services, app custom, SaaS bên ngoài.

## Best Practice:

- Định nghĩa rule events chính xác, tránh trùng lặp vô hạn.

- Tách event bus theo môi trường/dev/prod/team giúp dễ quản lý.

- Sử dụng CloudWatch monitor performance event bus.

## Use Case thực tế:

Kết nối SaaS với AWS (eg: Zendesk ticket vào workflow); tự động hóa các quy trình vận hành IT; phân tách microservices dùng chung một bus sự kiện
