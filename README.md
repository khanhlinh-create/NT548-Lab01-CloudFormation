# NT548 - Nhóm 9 - Lab 1 & Lab 2 CloudFormation

## Giới thiệu

Repository này chứa mã nguồn thực hiện Lab 1 và Lab 2 môn NT548 - Điện toán đám mây.

Mục tiêu của bài lab:

* Triển khai hạ tầng AWS bằng CloudFormation.
* Thiết kế hạ tầng theo mô hình module hóa.
* Tự động kiểm tra CloudFormation templates bằng AWS CodeBuild.
* Tích hợp cfn-lint và Taskcat.
* Tự động hóa quy trình CI bằng AWS CodePipeline và AWS CodeCommit.

---

## Kiến trúc hệ thống

Các thành phần được triển khai:

* VPC
* Public Subnet
* Private Subnet
* Internet Gateway
* NAT Gateway
* Route Tables
* Security Groups
* Public EC2 Instance
* Private EC2 Instance

AWS Region:

```text
ap-southeast-2 (Sydney)
```

Key Pair:

```text
nt548-lab1-key
```

---

## Cấu trúc thư mục

```text
NT548-Nhom9-Lab1-2-CloudFormation

├── network
│   ├── vpc.yaml
│   ├── subnet.yaml
│   ├── igw.yaml
│   ├── nat.yaml
│   └── routes.yaml
│
├── security
│   └── security-group.yaml
│
├── compute
│   └── ec2.yaml
│
├── buildspec.yml
├── .taskcat.yml
└── README.md
```

---

## Yêu cầu môi trường

* AWS Account
* AWS CLI v2
* Git
* AWS CloudFormation
* AWS CodeCommit
* AWS CodeBuild
* AWS CodePipeline

---

## Hướng dẫn triển khai Lab 1

### Bước 1: Triển khai VPC

Template:

```text
network/vpc.yaml
```

Lưu lại giá trị:

```text
VpcId
```

---

### Bước 2: Triển khai Subnet

Template:

```text
network/subnet.yaml
```

Tham số:

```text
VpcId
```

Lưu lại:

```text
PublicSubnetId
PrivateSubnetId
```

---

### Bước 3: Triển khai Internet Gateway

Template:

```text
network/igw.yaml
```

Tham số:

```text
VpcId
```

Lưu lại:

```text
InternetGatewayId
```

---

### Bước 4: Triển khai NAT Gateway

Template:

```text
network/nat.yaml
```

Tham số:

```text
PublicSubnetId
```

Lưu lại:

```text
NatGatewayId
```

---

### Bước 5: Triển khai Route Tables

Template:

```text
network/routes.yaml
```

Tham số:

```text
VpcId
PublicSubnetId
PrivateSubnetId
InternetGatewayId
NatGatewayId
```

---

### Bước 6: Triển khai Security Groups

Template:

```text
security/security-group.yaml
```

Tham số:

```text
VpcId
```

Lưu lại:

```text
PublicSGId
PrivateSGId
```

---

### Bước 7: Triển khai EC2 Instances

Template:

```text
compute/ec2.yaml
```

Tham số:

```text
PublicSubnetId
PrivateSubnetId
PublicSGId
PrivateSGId
```

---

## Hướng dẫn triển khai Lab 2

### AWS CodeCommit

* Tạo repository CodeCommit.
* Push source code từ GitHub lên CodeCommit.

### AWS CodeBuild

Build project được cấu hình để:

* Cài đặt cfn-lint.
* Cài đặt Taskcat.
* Kiểm tra CloudFormation templates.

### AWS CodePipeline

Pipeline bao gồm:

```text
Source (CodeCommit)
        ↓
Build (CodeBuild)
```

Pipeline được cấu hình tự động kích hoạt khi mã nguồn thay đổi trên CodeCommit.

---

## Kiểm tra kết quả

### Test Case 01

Tạo VPC thành công.

### Test Case 02

Tạo Public Subnet thành công.

### Test Case 03

Tạo Private Subnet thành công.

### Test Case 04

Tạo Internet Gateway thành công.

### Test Case 05

Tạo NAT Gateway thành công.

### Test Case 06

Tạo Route Tables thành công.

### Test Case 07

Tạo Security Groups thành công.

### Test Case 08

SSH từ máy cá nhân vào Public EC2 thành công.

### Test Case 09

SSH từ Public EC2 vào Private EC2 thành công.

### Test Case 10

Private EC2 truy cập Internet thông qua NAT Gateway thành công.

### Test Case 11

AWS CodeBuild thực hiện kiểm tra CloudFormation templates thành công.

### Test Case 12

AWS CodePipeline tự động kích hoạt khi có thay đổi trên CodeCommit.

---

## Cleanup

Để tránh phát sinh chi phí AWS, thực hiện xóa tài nguyên theo thứ tự:

```text
ec2-stack
security-stack
route-stack
nat-stack
igw-stack
subnet-stack
vpc-stack
```

Sau đó:

* Xóa CodeBuild Project.
* Xóa CodePipeline.
* Xóa CodeCommit Repository (nếu không còn sử dụng).
* Xóa các tài nguyên AWS còn tồn tại.

```
```
