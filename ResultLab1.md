
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

Створення нового юзера 


---
## Task 2 : 
Now perform one of the following (you need to select only one action):
  - Create an IaM user and attach FullAdmin policy. Use it for all future interactions with the system. (1 point)
  - Create an IaM Identity center account (or analog for you cloud provider). Also make it full admin. (2 points)


---
## Task 3 : (Optional)
Create an Organisation docs.aws.amazon.com/organizations/latest/userguide/orgs_tutorials_basic.html and user for it. 
**All next labs are to be performed within it. (2 points) **


---
## Task 4 : 
 Create one more user. Create an IaM policy that allows ONLY to view resources (no write access). (1 point)


---
## Task 5 : 
Create a Role that has this policy attached and can be assumed by user from p3. (1 point)


---
## Task 6 : (Optional)
Create a Cloudformation (or Terraform, OpenTofu, whatever) template describing your policy and role. (1 point)


---
## Task 7 : (Optional)
Create a network (VPC for your resources). There should be private and public subnets. Public one has IGW, private ones are for internal access only. (3 points)


---
## Task 8 : 
Create IaC stack holding hour network resources. (2 points)

---
## Task 9 : 
Calculate monthly budget for lab 2, assuming there will be only 2 shards. (2 point) 

---


Control questions*aaS :  
 - Compare cloud models. When to use which.Regions, Availability zones, etc.Define IaC and it’s value.
 - Difference between using roles and usergroups for assigning policies to the users.
 - VPC. 
 - CIDR, block calculationsHow to arrange public and private subnets. How does it work.When to use allow and deny policies.

