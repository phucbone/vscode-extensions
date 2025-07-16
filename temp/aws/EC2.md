# AWS EC2 (Elastic Compute Cloud)

## Tổng quan:

EC2 cung cấp máy chủ ảo (instance) theo yêu cầu, hỗ trợ nhiều loại workload từ ứng dụng web đến phân tích dữ liệu lớn.

## Best Practice:

- Chọn loại instance phù hợp nhu cầu (compute, memory, storage).
- Thiết lập Auto Scaling và sử dụng Elastic Load Balancer để tối ưu chi phí và hiệu suất.
- Sử dụng key pair cho SSH thay vì mật khẩu, gắn Security Group đúng đắn.
- Snapshot/AMI định kỳ để backup máy chủ.

## Use Case thực tế:

Web hosting; xử lý Big Data với Hadoop/Spark; xây dựng các môi trường dev/test linh hoạ
