# aws

Dịch vụ|Tổng quan ngắn|Best Practice tiêu biểu|Use Case thực tế nổi bật
---|---|---|---
IAM|Quản trị quyền/quản lý access|Least privilege, MFA, roles|Phân quyền team dev/ops
EC2|Máy chủ ảo đám mây linh hoạt|Chọn đúng loại, scaling, bảo mật|Web hosting, Big Data
VPC|Mạng ảo riêng, kiểm soát mạng|Subnet, AZ, security, hybrid|Tách môi trường test/prod
Route53|DNS quản lý domain, high availability|Routing policy, health check|Global DNS, failover
SNS|Gửi cảnh báo, thông báo|Topic naming, DLQ, monitor|Push notification, alert IT
Lambda|Serverless, chạy code theo event|Least privilege, nhẹ, log monitor|Xử lý file, microservices
EventBridge|Routing event serverless|Tối ưu rule, phân chia event bus|SaaS integration, workflow
CloudWatch|Quan sát, monitor hệ thống|Dashboard, alarm, cost monitor|Realtime alert, scaling
ElastiCache|Cache Redis/Memcached managed|Multi-AZ, private subnet|Cache DB, pub-sub
Backup|Sao lưu tự động đa dịch vụ|Policy, lifecycle, test restore|Auditing, disaster recovery


```text
+------------------------+        +---------------------+
|        Route53         | ------>|  Internet / Client  |
+------------------------+        +---------------------+
            |
            v
+------------------------+
|  Elastic Load Balancer |
+------------------------+
            |
            v
+---------------------------------------+
|               VPC                     |
|   +------------+     +-------------+ |
|   | Public Subnet|   | Private Subnet| |
|   | (ELB, NAT GW)|   |  (EC2, Lambda)| |
|   +------------+     +-------------+ |
|       |                    |           |
|       v                    v           |
|   +--------+    +------------------+  |
|   |  SNS   |    |   ElastiCache     |  |
|   +--------+    +------------------+  |
|                        |               |
|                        v               |
|                   +---------+          |
|                   |  RDS /  |          |
|                   | DynamoDB|          |
|                   +---------+          |
|                                       |
|      +-------------+    +-----------+ |
|      | EventBridge |    | CloudWatch| |
|      +-------------+    +-----------+ |
|           |                   |        |
|           v                   v        |
|    +--------------+    +--------------+|
|    |    Lambda    |    | AWS Backup   ||
|    +--------------+    +--------------+|
+---------------------------------------+
            |
           IAM (quản lý quyền truy cập cho toàn bộ các dịch vụ)

```

Giải thích sơ đồ:

Route53 làm DNS điều hướng domain đến Elastic Load Balancer (ELB) trong VPC.

ELB phân phối traffic người dùng đến các ứng dụng trên EC2 hoặc thực thi serverless qua Lambda trong private subnet.

Các instance trong private subnet truy cập ElastiCache để cache dữ liệu hot, giảm tải trực tiếp lên database (RDS/DynamoDB).

SNS gửi thông báo (alert, notification) đến người quản trị hoặc hệ thống khi có sự kiện quan trọng.

CloudWatch thu thập logs và metrics, cung cấp dashboard và cảnh báo lỗi, phối hợp với SNS để cảnh báo.

EventBridge giữ vai trò trung tâm xử lý các sự kiện, workflow phức tạp và liên kết các service với nhau hoặc với bên ngoài.

Lambda đồng thời được dùng để xử lý theo sự kiện (event-driven), tối ưu tự động hóa workflow.

Toàn bộ tài nguyên đều nằm trong VPC để kiểm soát bảo mật mạng.

IAM quản lý quyền truy cập bảo đảm nguyên tắc Least Privilege trên mọi dịch vụ.

AWS Backup quản lý sao lưu toàn bộ dữ liệu từ EC2, ElastiCache, RDS… theo chính sách backup.

Lời khuyên để vẽ sơ đồ trong công cụ:
Sử dụng biểu tượng AWS chuẩn (AWS Architecture Icons) cho các dịch vụ: Route53, ELB, EC2, Lambda, ElastiCache, SNS, CloudWatch, EventBridge, Backup, IAM.

Vẽ từng lớp/tầng: Internet -> DNS (Route53) -> Load Balancer -> VPC (phân thành subnet công khai và riêng tư) -> các dịch vụ backend.

Kết nối các dịch vụ theo hướng luồng dữ liệu/sự kiện.

Ghi chú ngắn gọn bên cạnh mỗi dịch vụ về vai trò của nó trong kiến trúc.


```text
+------------------------+        +---------------------+
|        Route53         | ------>|  Internet / Client  |
+------------------------+        +---------------------+
            |
            v
+------------------------+
|  Application Load      |
|  Balancer (ALB)        |
+------------------------+
            |
            v
+-----------------------------------------------+
|                  VPC                          |
|   +---------------+     +------------------+  |
|   | Public Subnet  |     |  Private Subnet  |  |
|   | (ALB, NAT GW)  |---->| Amazon EKS Cluster|  |
|   +---------------+     |  (Worker Nodes)   |  |
|                         |  - Pods/Containers|  |
|                         +-------------------+  |
|                                 |              |
|           +----------------------+-----------+ |
|           |                                  | |
|       +--------+                      +-------------+
|       | ElastiCache|                  | RDS/DynamoDB|
|       +--------+                      +-------------+
|
|   +----------------+    +------------------+       |
|   | EventBridge    |    | CloudWatch       |       |
|   +----------------+    +------------------+       |
|            |                     |                   |
|            v                     v                   |
|        +---------+          +----------+             |
|        | Lambda  |          | SNS      |             |
|

```


Giải thích chi tiết
Route53 quản lý DNS, điều hướng truy cập về ALB.

ALB (Application Load Balancer) phân phối request HTTP/HTTPS đến các dịch vụ chạy trong EKS cluster.

VPC chứa public subnet (chứa ALB, NAT Gateway) và private subnet chứa các Worker Nodes của EKS, nơi chạy Pod/Container.

Amazon EKS Cluster thay thế EC2 instance truyền thống, điều phối các container ứng dụng, gồm:

Worker Nodes (EC2 hoặc Fargate profile) chạy Pods chứa ứng dụng.

Pods kết nối đến ElastiCache (cache dữ liệu) và RDS/DynamoDB để lưu trữ chính.

EventBridge xử lý các sự kiện tích hợp giữa các microservice, các event từ ngoài hoặc từ bên trong cluster.

Lambda dùng để chạy các hàm serverless, được kích hoạt bởi EventBridge hoặc SNS.

SNS gửi thông báo, cảnh báo khi CloudWatch hoặc Lambda phát hiện sự kiện quan trọng.

CloudWatch giám sát Cluster (logs, metrics, health) và các AWS Resource khác, kết hợp với SNS để thông báo.

AWS Backup sao lưu dữ liệu quan trọng từ RDS, ElastiCache, các Persistent Volume (PV) gắn với EKS.

IAM quản lý toàn bộ quyền truy cập, cho phép kiểm soát an toàn chi tiết từ người dùng đến các dịch vụ.

Đặc điểm chính so với EC2 thông thường:
Thay vì chạy ứng dụng trực tiếp trên EC2, giờ đa phần workload được container hóa và chạy trong Kubernetes (EKS).

ALB tích hợp với Kubernetes Ingress Controller để định tuyến request đến đúng Pod/service trong cluster dựa trên path hoặc hostname.

EKS hỗ trợ tự động scale container theo nhu cầu, kết hợp với Auto Scaling Group cho worker node hoặc sử dụng serverless với Fargate.

Tận dụng hệ sinh thái Kubernetes và AWS cùng lúc, linh hoạt hơn để xây dựng kiến trúc microservices hoặc cloud-native.
