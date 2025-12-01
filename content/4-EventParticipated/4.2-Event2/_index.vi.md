---
title: "Sự kiện 2"
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Báo cáo Tóm tắt: "Hội thảo AI/ML trên AWS"

### Chi tiết Sự kiện
- **Ngày**: Thứ Bảy, 15 tháng 11, 2025
- **Thời gian**: 8:30 AM - 12:00 PM  
- **Địa điểm**: Văn phòng AWS Việt Nam
- **Loại sự kiện**: Hội thảo Kỹ thuật và Đào tạo

### Mục tiêu Sự kiện

- Cung cấp tổng quan toàn diện về AI/ML landscape tại Việt Nam
- Demo các dịch vụ và khả năng AWS AI/ML
- Trải nghiệm thực hành với Amazon SageMaker và Amazon Bedrock
- Học về triển khai Generative AI và best practices
- Networking với các chuyên gia AI/ML và AWS

### Lịch trình Chi tiết

#### Chào mừng & Giới thiệu (8:30 - 9:00 AM)
- Đăng ký tham gia và networking
- Tổng quan workshop và mục tiêu học tập
- Hoạt động làm quen
- Giới thiệu về AI/ML landscape tại Việt Nam

#### Tổng quan Dịch vụ AWS AI/ML (9:00 - 10:30 AM)
- **Amazon SageMaker** - Nền tảng ML end-to-end
  - Chuẩn bị và labeling dữ liệu
  - Model training, tuning, và deployment
  - Khả năng MLOps tích hợp
- **Live Demo**: Walkthrough SageMaker Studio

#### Generative AI với Amazon Bedrock (10:45 AM - 12:00 PM)
- **Foundation Models**: So sánh và hướng dẫn lựa chọn Claude, Llama, Titan
- **Prompt Engineering**: Techniques, Chain-of-Thought reasoning, Few-shot learning
- **Retrieval-Augmented Generation (RAG)**: Architecture và tích hợp Knowledge Base
- **Bedrock Agents**: Multi-step workflows và tool integrations
- **Guardrails**: Safety và content filtering
- **Live Demo**: Xây dựng Generative AI chatbot sử dụng Bedrock

### Nội Dung Nổi Bật

#### Đưa ra các ảnh hưởng tiêu cực của kiến trúc ứng dụng cũ

- Thời gian release sản phẩm lâu → Mất doanh thu/bỏ lỡ cơ hội
- Hoạt động kém hiệu quả → Mất năng suất, tốn kém chi phí
- Không tuân thủ các quy định về bảo mật → Mất an ninh, uy tín

#### Chuyển đổi sang kiến trúc ứng dụng mới - Microservice Architecture

Chuyển đổi thành hệ thống modular – từng chức năng là một **dịch vụ độc lập** giao tiếp với nhau qua **sự kiện** với 3 trụ cột cốt lõi:

- **Queue Management**: Xử lý tác vụ bất đồng bộ
- **Caching Strategy:** Tối ưu performance
- **Message Handling:** Giao tiếp linh hoạt giữa services

#### Domain-Driven Design (DDD)

- **Phương pháp 4 bước**: Xác định domain events → sắp xếp timeline → identify actors → xác định bounded contexts
- **Case study bookstore**: Minh họa cách áp dụng DDD thực tế
- **Context mapping**: 7 patterns tích hợp bounded contexts

#### Event-Driven Architecture

- **3 patterns tích hợp**: Publish/Subscribe, Point-to-point, Streaming
- **Lợi ích**: Loose coupling, scalability, resilience
- **So sánh sync vs async**: Hiểu rõ trade-offs (sự đánh đổi)

#### Compute Evolution

- **Shared Responsibility Model**: Từ EC2 → ECS → Fargate → Lambda
- **Serverless benefits**: No server management, auto-scaling, pay-for-value
- **Functions vs Containers**: Criteria lựa chọn phù hợp

#### Amazon Q Developer

- **SDLC automation**: Từ planning đến maintenance
- **Code transformation**: Java upgrade, .NET modernization
- **AWS Transform agents**: VMware, Mainframe, .NET migration

### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Business-first approach**: Luôn bắt đầu từ business domain, không phải technology
- **Ubiquitous language**: Importance của common vocabulary giữa business và tech teams
- **Bounded contexts**: Cách identify và manage complexity trong large systems

#### Kiến Trúc Kỹ Thuật

- **Event storming technique**: Phương pháp thực tế để mô hình hóa quy trình kinh doanh
- Sử dụng **Event-driven communication** thay vì synchronous calls
- **Integration patterns**: Hiểu khi nào dùng sync, async, pub/sub, streaming
- **Compute spectrum**: Criteria chọn từ VM → containers → serverless

#### Chiến Lược Hiện Đại Hóa

- **Phased approach**: Không rush, phải có roadmap rõ ràng
- **7Rs framework**: Nhiều con đường khác nhau tùy thuộc vào đặc điểm của mỗi ứng dụng
- **ROI measurement**: Cost reduction + business agility

### Ứng Dụng Vào Công Việc

- **Áp dụng DDD** cho project hiện tại: Event storming sessions với business team
- **Refactor microservices**: Sử dụng bounded contexts để identify service boundaries
- **Implement event-driven patterns**: Thay thế một số sync calls bằng async messaging
- **Serverless adoption**: Pilot AWS Lambda cho một số use cases phù hợp
- **Try Amazon Q Developer**: Integrate vào development workflow để boost productivity

### Trải nghiệm Sự kiện

Tham gia hội thảo **"AI/ML trên AWS"** là một trải nghiệm học tập chuyên sâu về trí tuệ nhân tạo và machine learning trên nền tảng AWS. Các trải nghiệm nổi bật bao gồm:

#### Hành trình Học tập AI/ML Toàn diện
- **Phiên sáng** xây dựng nền tảng vững chắc về SageMaker và MLOps pipeline
- **Demo thực hành** cung cấp kinh nghiệm trực tiếp với SageMaker Studio và model training
- **Phiên Bedrock** mở ra thế giới Generative AI với foundation models và RAG architecture
- **Case studies thực tế** minh họa cách triển khai AI/ML trong production environments

#### Phát triển Kỹ năng ML Engineering
- **Thực hành SageMaker**: Từ data preparation đến model deployment và monitoring
- **Foundation Models mastery**: Hiểu cách lựa chọn và fine-tune Claude, Llama, Titan
- **Prompt Engineering**: Kỹ thuật tối ưu hóa prompts cho kết quả AI chất lượng cao
- **RAG Implementation**: Architecture và best practices cho Retrieval-Augmented Generation
- **MLOps Pipeline**: Automated training, testing, và deployment workflows

#### Hiểu biết Generative AI sâu sắc
- **Bedrock ecosystem**: Khám phá khả năng của các foundation models khác nhau
- **Agent development**: Xây dựng AI agents với multi-step reasoning và tool integration
- **Safety và Ethics**: Guardrails và content filtering cho responsible AI
- **Business applications**: Cách áp dụng GenAI vào các use cases thực tế

#### Networking với Cộng đồng AI/ML
- **Kết nối với AWS experts**: Học từ các solution architects và technical specialists
- **Trao đổi với practitioners**: Chia sẻ kinh nghiệm và challenges trong AI/ML projects
- **Community building**: Tham gia AWS AI/ML community tại Việt Nam
- **Future collaboration**: Xây dựng mối quan hệ cho các dự án AI/ML tương lai

#### Bài học Chiến lược
- **AI/ML strategy**: Phương pháp tiếp cận từng bước để triển khai AI trong doanh nghiệp
- **Cost optimization**: Cách quản lý chi phí ML workloads hiệu quả trên AWS
- **Scalability planning**: Thiết kế architecture có thể scale cho millions of users
- **Ethics và Compliance**: Đảm bảo AI systems tuân thủ regulations và ethical guidelines

#### Một số hình ảnh hội thảo
*Thêm hình ảnh AI/ML workshop của bạn tại đây*

> Tổng thể, hội thảo AI/ML này không chỉ cung cấp kiến thức kỹ thuật sâu rộng mà còn mở ra tầm nhìn về tương lai của AI/ML, giúp tôi định hướng rõ ràng hơn trong việc phát triển kỹ năng và ứng dụng AI vào các dự án thực tế.
