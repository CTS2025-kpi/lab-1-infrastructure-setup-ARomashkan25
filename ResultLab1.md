
# Results Lab 1
---

**Description** 
```
This lab is dedicated to setting up infra for your future project. 
U can select cloud provider at will (GCP gives 300 bucks, while AWS has a generous free tier and also gives credits if u ask for those).
Those who don’t have credit card can reach out to lecturer to receive IAM user.
```


---
## Task 1 : 
Set-up account. Register in a cloud provider. Now you have a root account. (1 point) 

<img width="1917" height="952" alt="CreateRootAccount" src="https://github.com/user-attachments/assets/5b83449e-fef4-48b6-a778-970e0d9b95da" />


---
## Task 2 : 
Now perform one of the following (you need to select only one action):
  - [ ] Create an IaM user and attach FullAdmin policy. Use it for all future interactions with the system. (1 point)
  - [x] Create an IaM Identity center account (or analog for you cloud provider). Also make it full admin. (2 points)

Створення нового юзера в IaM Identity з назвою `RootUser`
<img width="1918" height="949" alt="image" src="https://github.com/user-attachments/assets/91b348db-9a05-46f4-b7d9-a964ad9d5a12" />
Створення нового дозволу `AdministratorAccess`
<img width="1917" height="950" alt="image" src="https://github.com/user-attachments/assets/f0feed56-e6a4-4532-a311-2e83effa82a6" />

Прив'язання AWS account до RootUser з full admin permisions 
<img width="1919" height="953" alt="image" src="https://github.com/user-attachments/assets/24fea86c-b0b5-4133-952c-a7199e61f39a" />

**Перевірка** 
<img width="1919" height="949" alt="image" src="https://github.com/user-attachments/assets/38598e49-e402-4161-86cc-c3aa2ee7a2aa" />


---
## Task 3 : (Optional)
Create an Organisation docs.aws.amazon.com/organizations/latest/userguide/orgs_tutorials_basic.html and user for it. 
**All next labs are to be performed within it. (2 points)**

<img width="1919" height="946" alt="image" src="https://github.com/user-attachments/assets/036d9600-33f2-45bd-b159-9b6e9fde6c04" />


---
## Task 4 : 
 Create one more user. Create an IaM policy that allows ONLY to view resources (no write access). (1 point)

Створив нового юзера з userName = `ViewOnly`
<img width="1914" height="949" alt="image" src="https://github.com/user-attachments/assets/24900ecd-199d-4d46-a2a7-15ea30b44946" />
Створив окремий доступ 
<img width="1919" height="951" alt="image" src="https://github.com/user-attachments/assets/25a8b6d1-b143-4768-b09a-e3b2db76262d" />
Назначив до юзера 
<img width="1920" height="951" alt="image" src="https://github.com/user-attachments/assets/3de70a72-2185-4140-ade0-603ed4a481b0" />

Перевірка: 
<img width="1919" height="949" alt="CheckViewOnly" src="https://github.com/user-attachments/assets/7d58bcc7-f90d-4e53-b19c-1cb4fc4b2e95" />

---
## Task 5 : 
Create a Role that has this policy attached and can be assumed by user from p3. (1 point)
Створив нову роль з назвою `RoleForLabs` де з дозволів, присутній лише перегляд та  
<img width="1919" height="948" alt="image" src="https://github.com/user-attachments/assets/7a3b792e-e151-4dcb-b698-9fdf4f621809" />

Окремо налаштування ролі, де вказаний дозвіл `OnlyReadEC2`
<img width="1917" height="948" alt="image" src="https://github.com/user-attachments/assets/450fef11-2e99-424f-987f-c08b53acb691" />


---
## Task 6 : (Optional)
Create a Cloudformation (or Terraform, OpenTofu, whatever) template describing your policy and role. (1 point)

Результат створеного template, що створю дозвіл та роль
<img width="1920" height="950" alt="image" src="https://github.com/user-attachments/assets/a3f4251c-e288-4b22-8e60-e43b92fdbae6" />
Окремо відображення створеної ролі та дозволу
<img width="1919" height="948" alt="image" src="https://github.com/user-attachments/assets/8e1d35c1-1e5b-490b-8967-9005753b2316" />


Скрипт що використовувася: 
```
AWSTemplateFormatVersion: "2010-09-09"
Description: >
  Lab1 - IAM Role and Policy for ViewOnly_CloudFormation user (EC2 read-only)

Resources:
  OnlyReadEC2Policy:
    Type: AWS::IAM::Policy
    Properties:
      PolicyName: OnlyReadEC2_CloudFormation
      PolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: Allow
            Action:
              - "ec2:Describe*"
            Resource: "*"
      Roles:
        - !Ref RoleForLabsCloudFormation

  RoleForLabsCloudFormation:
    Type: AWS::IAM::Role
    Properties:
      RoleName: RoleForLabsCloudFormation
      AssumeRolePolicyDocument:
        Version: "2012-10-17"
        Statement:
          - Effect: Allow
            Principal:
              AWS: arn:aws:iam::247430386033:user/ReadOnlyUser
            Action: "sts:AssumeRole"
      Path: "/"

```

---
## Task 7 : (Optional)
Create a network (VPC for your resources). There should be private and public subnets. Public one has IGW, private ones are for internal access only. (3 points)

Створення VPC 
<img width="3200" height="1080" alt="image" src="https://github.com/user-attachments/assets/0178a319-b182-4ae9-a8fb-976310a4ecd5" />
Створення приватної та публічної підмережі 
<img width="1918" height="952" alt="image" src="https://github.com/user-attachments/assets/ed2635e8-653f-45e8-aaf8-2135fd4b804a" />
Створення IGW
<img width="1917" height="947" alt="image" src="https://github.com/user-attachments/assets/5d7f7409-3d94-46b1-aafa-8f707fb81fc9" />
Створення таблиці маршрутів для публічної підмережі та підключення до VPC та IGW 
<img width="1916" height="950" alt="image" src="https://github.com/user-attachments/assets/3d4a62b4-aeea-4d00-8be8-055f89204db7" />

Resource map: 
<img width="1917" height="951" alt="image" src="https://github.com/user-attachments/assets/7f1e7c3c-f2d7-4524-8d25-15d928864da3" />

Перевірка роботи через створення EC2 та використання команди ping на публічну IP4 адресу 
Публічної підмережа:
<img width="1917" height="955" alt="image" src="https://github.com/user-attachments/assets/bb846a79-43b7-4548-abf8-902e1ba69b4b" />
На пінг отримуємо позитивку
Приватна підмережа: 
<img width="1916" height="953" alt="image" src="https://github.com/user-attachments/assets/cecf3d8f-aef6-4118-b01c-2edb8bffd5be" />
На пінг отримуємо time-out


---
## Task 8 : 
Calculate monthly budget for lab 2, assuming there will be only 2 shards. (2 point) 

Було використано офіційний сайт для підрахунку [AWS калькулятор](https://calculator.aws/#/estimate)

Розрахунок місячного бюджету (Регіон: Europe – Stockholm)

| Service Name | Monthly Cost (USD) | Config Summary |
|--------------|--------------------|----------------|
| Amazon EC2 | 3.65 |	Linux, t4g.micro 1 instance 730 hours/month | 
| Amazon API Gateway | 0.00 | HTTP API |
| Amazon Elastic Block Store (EBS) | 16.14 | 1 volume, 125 GB, 730 hours/month, 2 snapshots/day |

Загальний місячний бюджет: ≈ 19.79 USD

---


Control questions*aaS :  
 - Compare cloud models. When to use which.Regions, Availability zones, etc.Define IaC and it’s value.
 - Difference between using roles and usergroups for assigning policies to the users.
 - VPC. 
 - CIDR, block calculationsHow to arrange public and private subnets. How does it work.When to use allow and deny policies.

