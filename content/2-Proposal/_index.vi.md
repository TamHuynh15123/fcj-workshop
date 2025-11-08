---
title: "Bản đề xuất"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại phần này, bạn cần tóm tắt các nội dung trong workshop mà bạn **dự tính** sẽ làm.

# Coffee Cloud – Coffee Shop Order Platform  

### 1. Tóm tắt điều hành
Dự án "Coffee Cloud – Coffee Shop Order Platform" là nền tảng web giúp khách hàng đặt cà phê trực tuyến, tích điểm sau mỗi đơn hàng và đổi voucher ưu đãi.

Hệ thống hỗ trợ ba nhóm người dùng: Customer, Shipper, và Admin, nhằm tối ưu trải nghiệm đặt hàng, giao hàng và quản lý vận hành quán.

Ứng dụng Frontend được xây dựng bằng ReactJS, Backend bằng C#/.NET chạy trên AWS Lambda, kết nối qua API Gateway và được triển khai hoàn toàn trên AWS Free Tier với các dịch vụ: Amplify (Hosting + CI/CD), Cognito (Authentication), Lambda .NET (Backend logic), S3 Storage, DynamoDB, SNS (Notifications), SES (Email Service), IAM, và CloudWatch Logs.  

### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Quán cà phê truyền thống gặp khó khăn trong việc quản lý đơn hàng đông đúc, khách hàng phải chờ đợi lâu để đặt hàng và nhận sản phẩm. Không có hệ thống tích điểm để khuyến khích khách hàng quay lại, và việc theo dõi trạng thái đơn hàng chưa minh bạch.

*Giải pháp*  
Nền tảng Coffee Cloud được xây dựng với kiến trúc serverless trên AWS, sử dụng ReactJS cho frontend, C#/.NET Lambda cho backend logic, DynamoDB để lưu trữ dữ liệu và Cognito để quản lý người dùng. Hệ thống cung cấp ba giao diện riêng biệt cho Customer (đặt hàng, tích điểm), Shipper (nhận và giao hàng), và Admin (quản lý tổng thể). Tích hợp API Gateway để đảm bảo bảo mật và khả năng mở rộng. AWS SNS được sử dụng để gửi thông báo realtime về trạng thái đơn hàng, trong khi SES xử lý email notifications và marketing campaigns. Các tính năng chính bao gồm đặt hàng trực tuyến, hệ thống tích điểm, theo dõi đơn hàng thời gian thực, quản lý inventory và hệ thống thông báo đa kênh.

*Lợi ích và hoàn vốn đầu tư (ROI)*  
Hệ thống giúp tăng doanh thu thông qua kênh online, giảm thời gian chờ đợi của khách hàng và tối ưu hóa quy trình vận hành. Chi phí triển khai thấp nhờ sử dụng AWS Free Tier, ước tính chi phí vận hành hàng tháng dưới $5 USD cho giai đoạn đầu. Hệ thống tích điểm giúp tăng tỷ lệ khách hàng quay lại, dự kiến tăng doanh thu 20-30% so với hình thức truyền thống. Thời gian hoàn vốn ước tính 3-6 tháng nhờ tiết kiệm chi phí nhân lực và tăng hiệu quả bán hàng.  

### 3. Kiến trúc giải pháp  
Coffee Cloud áp dụng kiến trúc serverless hoàn toàn trên AWS để đảm bảo khả năng mở rộng và tiết kiệm chi phí. Frontend ReactJS được deploy trên AWS Amplify với tích hợp CI/CD tự động. Backend API được xây dựng bằng C#/.NET và chạy trên AWS Lambda, kết nối thông qua API Gateway để đảm bảo bảo mật và throttling. Dữ liệu được lưu trữ trong DynamoDB cho hiệu suất cao và S3 cho static assets. Authentication và authorization được quản lý bởi Amazon Cognito với hỗ trợ đa role (Customer, Shipper, Admin).

![Coffee Cloud Platform Architecture](/images/2-Proposal/coffee_architecture.jpg)

*Dịch vụ AWS sử dụng*  
- *AWS Amplify*: Hosting frontend ReactJS với CI/CD pipeline tự động.  
- *AWS Lambda*: Backend logic sử dụng C#/.NET runtime để xử lý business logic.  
- *Amazon API Gateway*: REST API endpoint để kết nối frontend và backend.  
- *Amazon DynamoDB*: NoSQL database lưu trữ dữ liệu users, orders, products, points.  
- *Amazon S3*: Lưu trữ static assets như hình ảnh sản phẩm, documents.  
- *Amazon Cognito*: Authentication và authorization cho 3 loại user roles.  
- *Amazon SNS*: Push notifications và SMS alerts cho trạng thái đơn hàng và promotions.  
- *Amazon SES*: Email service cho order confirmations, receipts và marketing campaigns.  
- *Amazon CloudWatch*: Monitoring và logging cho toàn bộ hệ thống.  
- *AWS IAM*: Quản lý permissions và security policies.  

*Thiết kế thành phần*  
- *Frontend Layer*: ReactJS application hosted trên Amplify với responsive design.  
- *API Layer*: API Gateway làm entry point cho tất cả HTTP requests.  
- *Business Logic Layer*: AWS Lambda functions viết bằng C#/.NET xử lý core logic.  
- *Data Layer*: DynamoDB tables cho structured data, S3 buckets cho file storage.  
- *Authentication Layer*: Cognito User Pools quản lý users với 3 groups (Customer, Shipper, Admin).  
- *Notification Layer*: SNS cho real-time notifications, SES cho email communications.  
- *Monitoring Layer*: CloudWatch theo dõi performance, errors và usage metrics.  

### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
Dự án Coffee Cloud được chia thành 4 giai đoạn chính trong vòng 3 tháng:  
1. *Nghiên cứu và thiết kế*: Phân tích yêu cầu business, thiết kế database schema, wireframe UI/UX và kiến trúc system (Tháng 1).  
2. *Setup Environment và Backend Development*: Cấu hình AWS services, phát triển Lambda functions với C#/.NET, thiết lập DynamoDB tables và API Gateway (Tháng 1-2).  
3. *Frontend Development*: Xây dựng ReactJS application, tích hợp với backend APIs, implement authentication flow với Cognito (Tháng 2).  
4. *Testing và Deployment*: Unit testing, integration testing, performance testing, deploy lên Amplify và monitoring (Tháng 3).  

*Yêu cầu kỹ thuật*  
- *Frontend Requirements*: ReactJS với hooks, React Router cho navigation, Axios cho API calls, CSS frameworks (Bootstrap/Material-UI), responsive design cho mobile và desktop.  
- *Backend Requirements*: C#/.NET 6+ runtime trên Lambda, Entity Framework Core cho data access, JWT authentication, exception handling và logging.  
- *Database Design*: DynamoDB tables cho Users, Products, Orders, OrderItems, Points, Vouchers với proper indexing và relationships.  
- *DevOps Requirements*: Git version control, Amplify CI/CD pipeline, CloudWatch monitoring, IAM roles và policies cho security.  

### 5. Lộ trình & Mốc triển khai  
- *Giai đoạn 1 (Tuần 1-4)*: Nghiên cứu và thiết kế hệ thống  
    - Phân tích yêu cầu business và technical  
    - Thiết kế database schema và API specifications  
    - Tạo wireframes và UI mockups  
    - Setup AWS account và cấu hình ban đầu  
- *Giai đoạn 2 (Tuần 5-8)*: Phát triển Backend và Infrastructure  
    - Tạo DynamoDB tables và configure indexes  
    - Phát triển Lambda functions với C#/.NET  
    - Setup API Gateway và integrate với Lambda  
    - Configure Cognito User Pools và Groups  
- *Giai đoạn 3 (Tuần 9-10)*: Phát triển Frontend  
    - Xây dựng ReactJS components và pages  
    - Implement authentication và authorization  
    - Tích hợp với backend APIs  
    - Responsive design cho mobile  
- *Giai đoạn 4 (Tuần 11-12)*: Testing và Deployment  
    - Unit testing và integration testing  
    - Deploy lên AWS Amplify  
    - Performance optimization và monitoring setup  
    - User acceptance testing và documentation  

### 6. Ước tính ngân sách  
Dự án Coffee Cloud được thiết kế để tận dụng tối đa AWS Free Tier trong giai đoạn đầu phát triển và testing.

*Chi phí AWS Services (Monthly)*  
- AWS Amplify: $0.00 USD (Free Tier: 1000 build minutes, 15GB storage)  
- AWS Lambda: $0.00 USD (Free Tier: 1M requests, 400,000 GB-seconds)  
- Amazon API Gateway: $0.00 USD (Free Tier: 1M API calls)  
- Amazon DynamoDB: $0.00 USD (Free Tier: 25GB storage, 25 RCU/WCU)  
- Amazon S3: $0.00 USD (Free Tier: 5GB standard storage)  
- Amazon Cognito: $0.00 USD (Free Tier: 50,000 MAU)  
- Amazon SNS: $0.00 USD (Free Tier: 1M publications, 100,000 HTTP/HTTPS requests)  
- Amazon SES: $0.00 USD (Free Tier: 62,000 emails/month)  
- Amazon CloudWatch: $0.00 USD (Free Tier: 10 custom metrics, 5GB logs)  

*Chi phí sau Free Tier (Estimated for production)*  
- AWS Amplify: ~$1.00 USD/month (hosting + build minutes)  
- AWS Lambda: ~$0.20 USD/month (based on 10K requests/day)  
- API Gateway: ~$3.50 USD/month (1M requests)  
- DynamoDB: ~$1.25 USD/month (additional RCU/WCU)  
- Amazon SNS: ~$0.50 USD/month (additional notifications + SMS)  
- Amazon SES: ~$1.00 USD/month (additional emails beyond free tier)  

*Tổng ước tính*: $0.00 USD/month (Development), ~$7.45 USD/month (Production)  
*Chi phí phát triển*: Chỉ phát sinh chi phí nhân lực cho developer  

### 7. Đánh giá rủi ro  
*Ma trận rủi ro*  
- Vượt giới hạn Free Tier: Ảnh hưởng trung bình, xác suất trung bình  
- Lỗi integration giữa các AWS services: Ảnh hưởng cao, xác suất thấp  
- Performance issues với DynamoDB: Ảnh hưởng trung bình, xác suất thấp  
- Security vulnerabilities: Ảnh hưởng cao, xác suất thấp  

*Chiến lược giảm thiểu*  
- Chi phí: Thiết lập CloudWatch billing alerts, monitor usage daily  
- Integration: Thực hiện thorough testing, sử dụng AWS SAM cho local testing  
- Performance: Thiết kế proper DynamoDB indexes, implement caching strategies  
- Security: Follow AWS security best practices, regular security audits  

*Kế hoạch dự phòng*  
- Backup và recovery plan cho DynamoDB data  
- Fallback mechanisms cho critical functions  
- Manual operation procedures nếu hệ thống gặp sự cố  
- Communication plan với stakeholders khi có incidents  

### 8. Kết quả kỳ vọng  
*Cải tiến kỹ thuật*: Hệ thống Coffee Cloud hoàn chỉnh với khả năng xử lý hàng trăm đơn hàng đồng thời, responsive design hoạt động mượt mà trên mọi thiết bị.

*Lợi ích kinh doanh*:  
- Tăng 30% doanh thu nhờ kênh online mới  
- Giảm 50% thời gian xử lý đơn hàng  
- Tăng 25% tỷ lệ khách hàng quay lại nhờ hệ thống tích điểm  
- Cải thiện customer satisfaction score lên 90%  

*Kỹ năng phát triển*:  
- Thành thạo AWS Serverless Architecture  
- Kinh nghiệm phát triển full-stack với ReactJS và .NET  
- Hiểu biết sâu về NoSQL database design  
- Kỹ năng DevOps với CI/CD pipeline  

*Khả năng mở rộng*: Hệ thống có thể dễ dàng scale để phục vụ multiple coffee shops hoặc integrate thêm features như AI recommendation, loyalty program nâng cao.  
*Giá trị dài hạn*: Platform foundation có thể tái sử dụng cho các dự án e-commerce khác, tạo cơ sở cho việc phát triển các ứng dụng kinh doanh tương tự.
