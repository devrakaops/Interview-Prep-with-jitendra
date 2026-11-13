# 30 AWS Questions by Subtopic

Each subtopic has basic questions to check your fundamentals and scenario questions to check how you apply them. Scenario questions are marked "(Scenario)".

---

## 1. Cloud Concepts and AWS Architecture (3)

**Q1. What is cloud computing, and why do companies move to AWS?**
> Cloud computing means renting servers, storage and databases over the internet and paying only for usage. Companies move for lower upfront cost, fast provisioning, easy scaling and global reach.

**Q2. What are a Region and an Availability Zone?**
> A Region is a geographic location such as Mumbai. An AZ is an isolated data center inside that region. Spreading resources across AZs keeps the app running if one AZ fails.

**Q3. (Scenario) Your application must stay online even if one data center fails. How will you design it?**
> Deploy EC2 instances in two or more AZs behind a load balancer, use an Auto Scaling Group to replace failed instances, and run the database as RDS Multi-AZ. This removes the single point of failure.

---

## 2. EC2 (5)

**Q4. What is EC2, and what is an AMI?**
> EC2 is a virtual server in the cloud. An AMI is the template (OS plus software) used to launch an instance.

**Q5. What is the difference between stopping and terminating an instance?**
> Stop keeps the EBS volume and data, and you can start it again (you pay only for storage). Terminate deletes the instance permanently, and the root volume is deleted by default.

**Q6. What are the EC2 pricing models?**
> On-Demand (pay as you go), Reserved (1 or 3 year commitment, cheaper), and Spot (spare capacity, cheapest, but AWS can reclaim it).

**Q7. (Scenario) You launched an EC2 instance, but you cannot SSH into it. What will you check?**
> The Security Group allows port 22 from your IP, the instance is running and has a public IP, the subnet has a route to the Internet Gateway, the NACL allows traffic, the `.pem` key has `chmod 400`, and you are using the correct username (`ec2-user` or `ubuntu`).

**Q8. (Scenario) You stopped and started an instance, and its public IP changed, breaking your application. How do you fix it?**
> Attach an Elastic IP, which is a static public IP that stays the same across restarts. For production, put the instance behind a load balancer and use DNS names instead of raw IPs.

---

## 3. S3 (4)

**Q9. What is S3, and what are buckets and objects?**
> S3 is object storage for files. A bucket is a container with a globally unique name, and an object is a file plus its metadata. Buckets are private by default.

**Q10. What are the S3 storage classes?**
> Standard (frequent access), Standard-IA (infrequent access), Glacier (cheap archive, slow retrieval), and Intelligent-Tiering (moves data automatically).

**Q11. (Scenario) Someone accidentally deleted an important file in S3. How could you have protected against this?**
> Enable versioning, so a deleted file can be restored from a previous version. You can also enable MFA Delete and restrict delete permissions through IAM and bucket policies.

**Q12. (Scenario) Logs in your S3 bucket keep growing and costs are rising. What will you do?**
> Create a lifecycle policy: move logs to Standard-IA after 30 days, to Glacier after 90 days, and delete after a retention period. This cuts storage cost automatically.

---

## 4. IAM (4)

**Q13. What is IAM, and what are users, groups, roles and policies?**
> IAM controls who can access AWS and what they can do. A user is a person or app, a group is a set of users, a role is a temporary identity for a user or service, and a policy is a JSON document defining permissions.

**Q14. What is the principle of least privilege?**
> Give only the minimum permissions required for a task, for example read-only access to one bucket instead of full S3 or admin access.

**Q15. (Scenario) An application on EC2 needs to read files from S3. How do you give it access securely?**
> Create an IAM role with a policy allowing `s3:GetObject` on that bucket, and attach it to the EC2 instance. The app gets temporary credentials automatically, so no access keys are stored in code or on the server.

**Q16. (Scenario) You find that an access key was accidentally pushed to GitHub. What do you do?**
> Immediately deactivate and delete the key, create a new one if needed, review CloudTrail for any misuse, and remove it from the repository history. Going forward, use IAM roles and Secrets Manager instead of hardcoded keys.

---

## 5. VPC, Subnets, Routing and Security Groups (5)

**Q17. What is a VPC, and what is a subnet?**
> A VPC is your isolated private network in AWS, defined by a CIDR range such as 10.0.0.0/16. A subnet is a smaller section of it, located in one AZ.

**Q18. What makes a subnet public or private?**
> A subnet is public if its route table has a route to an Internet Gateway (destination `0.0.0.0/0`, target the IGW). A private subnet has no such route.

**Q19. What is the difference between a Security Group and a NACL?**
> A Security Group works at the instance level, is stateful and allow-only. A NACL works at the subnet level, is stateless, and supports both allow and deny rules.

**Q20. (Scenario) Your private-subnet instances need to download OS updates from the internet but must not be reachable from it. How?**
> Place a NAT Gateway in a public subnet and add a route in the private subnet's route table (destination `0.0.0.0/0`, target the NAT Gateway). Outbound traffic works, and inbound connections from the internet are blocked.

**Q21. (Scenario) Your web server and database are in the same VPC. How should the Security Groups be set up?**
> The web server allows ports 80 and 443 from the internet. The database Security Group allows the DB port (3306 or 5432) only from the web server's Security Group, never from `0.0.0.0/0`.

---

## 6. RDS (3)

**Q22. What is RDS, and why use it instead of installing a database on EC2?**
> RDS is a managed database service. AWS handles backups, patching, monitoring and failover, so you spend less time on administration.

**Q23. What is the difference between Multi-AZ and a Read Replica?**
> Multi-AZ keeps a standby copy in another AZ for high availability with automatic failover. A Read Replica serves read traffic to improve performance.

**Q24. (Scenario) Your database is slow because of too many read queries. What do you do?**
> Add one or more Read Replicas and send read traffic to them, while writes go to the primary. You could also consider caching or a bigger instance size.

---

## 7. CloudWatch and Monitoring (3)

**Q25. What is CloudWatch, and what do metrics, logs and alarms do?**
> CloudWatch is AWS's monitoring service. Metrics are numeric data (such as CPU), logs are text records of events, and alarms send a notification or trigger an action when a threshold is crossed.

**Q26. What is the difference between CloudWatch and CloudTrail?**
> CloudWatch shows what is happening (performance and logs). CloudTrail records who did what (API calls and account activity) for auditing.

**Q27. (Scenario) You want to be notified when an EC2 instance's CPU goes above 80%. How do you set that up?**
> Create a CloudWatch alarm on the CPUUtilization metric (threshold 80% for a few periods) and connect it to an SNS topic that emails you. For memory and disk metrics, install the CloudWatch Agent.

---

## 8. Cloud Security and Overall Scenarios (3)

**Q28. What is the Shared Responsibility Model?**
> AWS secures the cloud itself (hardware, data centers, the virtualization layer). The customer secures what they put in it (data, IAM, Security Group rules, OS patching, encryption choices).

**Q29. (Scenario) Your S3 bucket was found to be publicly accessible by mistake. What will you do?**
> Turn on Block Public Access immediately, review and fix the bucket policy and ACLs, check access logs and CloudTrail for what was accessed, and enable encryption and monitoring. Then add checks to prevent it recurring.

**Q30. (Scenario) Design a simple, secure setup to host a small web application on AWS.**
> A VPC with public and private subnets across two AZs. An ALB in the public subnets, EC2 instances in an Auto Scaling Group, and RDS Multi-AZ in private subnets. Security Groups chained from ALB to app to database, an IAM role on the instances for S3 access, S3 for static files, and CloudWatch for monitoring and alarms.

---

Every answer now uses the same `>` quote style as your first three. Do you want this as a Claude Doc, or shall we start the mock interview with the scenario questions?
