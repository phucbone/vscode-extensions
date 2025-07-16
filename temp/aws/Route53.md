# AWS Route53

## Tổng quan:

Route53 là dịch vụ DNS cloud, cung cấp quản lý domain, routing, Health Checks và failover.

## Best Practice:

- Sử dụng các routing policy như latency-based, weighted cho HA và tối ưu hiệu suất.
- Giám sát endpoints với health check, cấu hình failover tự động.
- Quản lý records nội bộ với Private DNS cho các tài nguyên trong VPC.

## Use Case thực tế:

DNS cho ứng dụng toàn cầu (phân phối traffic dựa trên vị trí địa lý, độ trễ); đảm bảo high availability bằng failover routing; quản lý domain cho các môi trường dev/test/prod riêng
