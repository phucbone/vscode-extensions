# AWS VPC (Virtual Private Cloud)

## Tổng quan:

VPC cho phép tạo mạng ảo riêng biệt, kiểm soát đầy đủ IP, subnet, routing, firewall cho tài nguyên AWS của bạn.

## Best Practice:

- Lập kế hoạch không gian địa chỉ IP và phân tách subnet cho public/private.
- Sử dụng nhiều Availability Zone để tăng tính sẵn sàng.
- Gắn Security Group, NACL phù hợp từng lớp tài nguyên; sử dụng NAT Gateway thay vì mở rộng public subnet cho instance nội bộ.
- Kết nối VPN hoặc Direct Connect với hệ thống on-premise để mở rộng hybrid cloud.

## Use Case thực tế:

Phân vùng riêng biệt để chạy web, database (tách subnet public/private); kết nối VPC giữa các region (peering/teamwork); thiết lập môi trường test/prod tách biệt
