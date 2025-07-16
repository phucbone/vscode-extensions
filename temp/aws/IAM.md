# AWS IAM (Identity and Access Management)

## Tổng quan:

IAM giúp kiểm soát ai được truy cập, cấp quyền gì với tài nguyên AWS. Đây là nền tảng cho bảo mật và phân quyền trên AWS.

## Best Practice:

- Thực hiện nguyên tắc Least Privilege: Chỉ cấp quyền tối thiểu cần thiết.
- Bật MFA (Multi-Factor Authentication) cho tài khoản quản trị.
- Sử dụng IAM roles thay vì IAM users cho dịch vụ.
- Thường xuyên review, xoá tài khoản hoặc quyền không dùng đến.

## Use Case:

Một công ty cần phân tách quyền truy cập giữa nhóm phát triển (xem logs) và nhóm vận hành (quản lý EC2), tạo các policy và attach vào IAM group phù hợp
