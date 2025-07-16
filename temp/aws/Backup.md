# AWS Backup

## Tổng quan:

Backup là dịch vụ tự động hóa sao lưu dữ liệu đa dịch vụ (EC2, RDS, EFS, DynamoDB...) trên AWS.

## Best Practice:

- Thiết lập lifecycle tự động xóa backup cũ, giữ lịch backup hợp lý theo chính sách doanh nghiệp.
- Kết hợp tag tài nguyên để tự động vào kế hoạch backup.
- Kiểm tra định kỳ việc restore backup.

## Use Case thực tế:

Đáp ứng yêu cầu backup/khôi phục dữ liệu tuân thủ chính sách bảo mật hoặc audit; backup toàn bộ hệ thống định kỳ; rollback data khi gặp sự cố hoặc tấn công ransomware
