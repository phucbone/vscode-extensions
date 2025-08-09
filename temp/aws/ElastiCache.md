# AWS ççç

## Tổng quan:

ElastiCache quản lý Redis/Memcached trên AWS, phục vụ cache hóa dữ liệu, giúp tăng tốc ứng dụng.

## Best Practice:

- Sử dụng Multi-AZ replication cho Redis để tăng HA.
- Bảo vệ cache bằng subnet private và hạn chế security group access.
- Cấu hình backup/tự động recovery.

## Use Case thực tế:

Cache session, caching kết quả truy vấn DB; queue real-time (Pub/Sub Redis); giảm tải RDS trong các ứng dụng web hoặc analytics lớn.
