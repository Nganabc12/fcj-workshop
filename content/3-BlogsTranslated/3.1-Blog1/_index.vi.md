---
title: "Blog 1: Machine Learning Pipelines"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Understanding Machine Learning Pipelines: The Journey to Bring AI Models into Reality

## Thông tin bài viết

| Mục | Nội dung |
|-----|----------|
| **Tiêu đề bài viết** | Machine Learning Pipelines |
| **Tác giả** | Accenture |
| **Ngày xuất bản** | 27/07/2022 |
| **Nguồn bài viết** | https://docs.aws.amazon.com/whitepapers/latest/accenture-ai-scaling-ml-and-deep-learning-models/machine-learning-pipelines.html |
| **Người dịch** | Nguyễn Hoàng Sơn |
| **Ngày đăng bản dịch** | 09/06/2026 |
| **Bài viết đã dịch** | https://www.facebook.com/share/p/18qaf9Rky8/ |

---

## Giới thiệu

Trong quá trình tìm hiểu về AI/ML trên AWS, tôi đã đọc một tài liệu kỹ thuật (AWS Whitepaper) trình bày về cách xây dựng và triển khai các mô hình Machine Learning ở quy mô doanh nghiệp. Điều khiến tôi ấn tượng không phải là các thuật toán Machine Learning phức tạp mà là một câu hỏi rất thực tế:

**Làm thế nào để đưa một mô hình AI từ máy tính cá nhân lên môi trường Production để có thể phục vụ hàng triệu người dùng?**

Trước đây, khi nhắc đến AI, tôi thường nghĩ rằng chỉ cần thu thập dữ liệu, huấn luyện mô hình bằng Python hoặc Jupyter Notebook là đã hoàn thành. Tuy nhiên, tài liệu của AWS chỉ ra rằng việc xây dựng mô hình chỉ là một phần nhỏ của toàn bộ quá trình. Phần lớn công việc còn lại nằm ở việc xây dựng hạ tầng, tự động hóa quy trình, giám sát và vận hành hệ thống để mô hình có thể hoạt động ổn định trong môi trường thực tế.

Chính vì vậy, **Machine Learning Pipeline** được xem là một thành phần quan trọng trong MLOps, giúp tự động hóa toàn bộ vòng đời của mô hình Machine Learning, từ thu thập dữ liệu, xử lý dữ liệu, huấn luyện, triển khai cho đến theo dõi và cập nhật mô hình.

---

> **Lưu ý:** Bài viết này được dịch và tổng hợp từ **AWS Whitepaper – Accenture Enterprise AI: Scaling Machine Learning and Deep Learning Models** nhằm phục vụ mục đích học tập và nghiên cứu. Mọi bản quyền nội dung thuộc về **Amazon Web Services (AWS)** và **Accenture**. :contentReference[oaicite:0]{index=0}


Đó là lý do khái niệm **Machine Learning Pipelines** (Đường ống học máy) ra đời.

---

## Kiến trúc Machine Learning Pipeline giải quyết vấn đề gì?

Theo bài viết, để một mô hình AI hoạt động trơn tru trong thực tế, nó cần đi qua một dây chuyền tự động hóa (pipeline). Thay vì phải chạy bằng tay từng bước, một Pipeline tốt sẽ liên kết tất cả các tác vụ này lại với nhau thành một vòng lặp hoàn toàn tự động.

**Các bước cốt lõi trong Pipeline bao gồm:**

- **Thu thập dữ liệu (Data Ingestion):** Tự động kéo dữ liệu thô mới nhất từ các kho lưu trữ khổng lồ.
- **Tiền xử lý (Data Preprocessing):** Làm sạch, chuẩn hóa định dạng và trích xuất đặc trưng (Feature Engineering) cho dữ liệu.
- **Huấn luyện (Training & Tuning):** Cho AI học lại từ dữ liệu mới để thông minh hơn, đồng thời tự động tối ưu hóa siêu tham số (Hyperparameter tuning).
- **Triển khai (Deployment):** Đưa mô hình AI đã học xong lên máy chủ thành các Endpoint (điểm cuối) để phục vụ người dùng theo thời gian thực hoặc xử lý hàng loạt.

![Quy trình Machine Learning](/images/3-BlogsTranslated/blog1-1.png)

---

## Lựa chọn công nghệ cho từng giai đoạn Pipeline

Khi áp dụng mô hình này lên AWS, chúng ta cần map (ánh xạ) các bước trên với các dịch vụ Cloud tương ứng. Dưới đây là bảng tổng hợp các công nghệ thường được xem xét:

| Giai đoạn Pipeline (Pipeline Stage) | Các dịch vụ AWS cốt lõi (AWS Services) | Chức năng chính trong hệ thống |
| ----------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Lưu trữ & Kéo dữ liệu** | Amazon S3, AWS Lake Formation, Amazon RDS | Cung cấp Data Lake tập trung, lưu trữ dữ liệu thô (raw data) và dữ liệu đã xử lý. |
| **Tiền xử lý dữ liệu** | AWS Glue, Amazon SageMaker Data Wrangler | Chạy các job ETL (Extract, Transform, Load) để làm sạch dữ liệu ở quy mô lớn. |
| **Huấn luyện mô hình** | Amazon SageMaker Training Instances, EC2 | Cấp phát các cụm máy chủ có GPU mạnh mẽ để train AI, sau đó tự động tắt khi train xong. |
| **Triển khai & Suy luận** | Amazon SageMaker Endpoints, API Gateway, AWS Lambda | Đóng gói mô hình thành REST API để Frontend/Backend của ứng dụng gọi tới. |

![Kiến trúc Machine Learning Engineering](/images/3-BlogsTranslated/blog1-2.png)

---

## Phân rã các thành phần trong hệ thống MLOps

Giống như việc chia nhỏ một ứng dụng thành các Microservices, một hệ thống AI trên Production cũng được chia thành các phân hệ kết hợp rời rạc (loosely coupled):

### 1. Data Storage Hub (Kho lưu trữ tập trung)
Thay vì dùng database quan hệ thông thường, hệ thống AI sử dụng **Amazon S3** làm nền tảng.
- Lưu trữ hàng TB dữ liệu hình ảnh, văn bản, file CSV không cấu trúc.
- Lưu trữ các artifact (file trọng số `.tar.gz` của mô hình) sau khi quá trình huấn luyện hoàn tất.

### 2. Orchestration Layer (Lớp điều phối)
Để các bước (Ingestion -> Processing -> Training) chạy tự động, chúng ta cần một công cụ điều phối như **AWS Step Functions** hoặc **SageMaker Pipelines**. 
- Hệ thống này hoạt động theo mô hình *event-driven* (hướng sự kiện). Ví dụ: Khi có 1 file dữ liệu mới được upload lên S3, nó sẽ tự động kích hoạt Lambda để khởi chạy toàn bộ quy trình huấn luyện lại mô hình.

> *Chỉ cho phép ứng dụng bên ngoài gọi đến mô hình AI thông qua một điểm cuối duy nhất (API Gateway) → Đảm bảo khả năng kiểm soát lưu lượng và bảo mật.*

---

## Tính năng tự động hóa và Infrastructure as Code

Để quản lý hạ tầng AI, các kỹ sư Cloud thường sử dụng mã hóa hạ tầng (IaC) để định nghĩa Pipeline. Dưới đây là một ví dụ về cấu hình tự động tạo S3 Bucket để chứa dữ liệu Training bằng **AWS CloudFormation**:

```yaml
Resources:
  MLTrainingDataBucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: !Sub '${AWS::StackName}-ml-training-data'
      VersioningConfiguration:
        Status: Enabled
      LifecycleConfiguration:
        Rules:
          - Id: TransitionToGlacier
            Status: Enabled
            Transitions:
              - TransitionInDays: 90
                StorageClass: GLACIER
Outputs:
  TrainingBucketName:
    Value: !Ref MLTrainingDataBucket
    Export:
      Name: !Sub '${AWS::StackName}-TrainingBucket'