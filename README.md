# NT548 Lab 01 - CloudFormation

## Giới thiệu

Bài lab sử dụng AWS CloudFormation để triển khai hạ tầng mạng và máy chủ trên AWS.

Các thành phần được triển khai:

* VPC
* Public Subnet
* Private Subnet
* Internet Gateway
* NAT Gateway
* Route Tables
* Security Groups
* Public EC2
* Private EC2

---

## Cấu trúc thư mục

```text
network/
├── vpc.yaml
├── subnet.yaml
├── igw.yaml
├── nat.yaml
└── routes.yaml

security/
└── security-group.yaml

compute/
└── ec2.yaml
```

---

## Hướng dẫn triển khai

### Bước 1: Tạo VPC

Upload template:

```text
network/vpc.yaml
```

Ghi lại VpcId trong Outputs.

### Bước 2: Tạo Subnets

Upload:

```text
network/subnet.yaml
```

Sử dụng VpcId từ bước 1.

### Bước 3: Tạo Internet Gateway

Upload:

```text
network/igw.yaml
```

### Bước 4: Tạo NAT Gateway

Upload:

```text
network/nat.yaml
```

Sử dụng PublicSubnetId từ subnet-stack.

### Bước 5: Tạo Route Tables

Upload:

```text
network/routes.yaml
```

### Bước 6: Tạo Security Groups

Upload:

```text
security/security-group.yaml
```

### Bước 7: Tạo EC2

Upload:

```text
compute/ec2.yaml
```

---

## Test Cases

* TC01: Tạo VPC
* TC02: Tạo Public Subnet
* TC03: Tạo Private Subnet
* TC04: Tạo Internet Gateway
* TC05: Tạo NAT Gateway
* TC06: Tạo Route Tables
* TC07: Tạo Security Groups
* TC08: SSH vào Public EC2
* TC09: SSH từ Public EC2 sang Private EC2
* TC10: Private EC2 truy cập Internet thông qua NAT Gateway

---

## Cleanup

Sau khi hoàn thành bài lab:

* Delete ec2-stack
* Delete security-stack
* Delete route-stack
* Delete nat-stack
* Delete igw-stack
* Delete subnet-stack
* Delete lab1

để tránh phát sinh chi phí AWS.

Lab 2 - CodePipeline Auto Trigger Test