# AWS CloudWatch

## Tổng quan:

CloudWatch giúp monitor, collect logs/metrics từ toàn bộ tài nguyên AWS, phân tích và cảnh báo real-time.

## Best Practice:

- Định nghĩa custom metrics, dashboard cho app vận hành.

- Thiết lập alarms trên KPI quan trọng (CPU, RAM, errors...)

- Sử dụng log retention và filter; monitor chi phí sử dụng.

## Use Case thực tế:

Monitoring hiệu năng web/app/server; tự động scale EC2/Lambda khi vượt threshold; alert real-time về Slack/Zalo/email khi có lỗi hệ thống
