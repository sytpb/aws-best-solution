# aws-best-solution
Best practice and solution for AWS cloud



## Web Application deploy with AWS

**#1**.A company has a web application that is hosted in an Auto Scaling group of EC2 instances behind an Application Load Balancer and is deployed across multiple AWS regions. The users can be found all around the globe, but the majority are from Japan and Sweden. Because of the compliance requirements in these two locations, you want the Japanese users to connect to the servers in the *ap-northeast-1* Asia Pacific (Tokyo) region, while the Swedish users should be connected to the servers in the *eu-west-1* EU (Ireland) region.

How should you to easily fulfill this requirement?


**Geolocation routing**<br>
*Key word: global user, low latency access*<br>
[Geolocation routing](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-geo.html/)    


**#2**.A tech company are building their mobile forex trading application. You are hired to set up their cloud architecture in AWS and to implement a highly available, fault tolerant system. For their database, they are using DynamoDB and for authentication, they have chosen to use Cognito. Since the mobile application contains confidential financial transactions, there is a requirement to add a second authentication method that doesn't rely solely on user name and password.   

How can you implement this in AWS?

**Add multi-factor authentication (MFA) to a user pool to protect the identity of your users.**<br>
*Key word: authentication, not only user name and password, Cognito*


## EC2 
**#1**.A company has a web application hosted in AWS cloud where the application logs are sent to Amazon CloudWatch. Lately, the web application has recently been encountering some errors which can be resolved simply by restarting the instance.

What will you do to automatically restart the EC2 instances whenever the same application error occurs?

**look at the existing CloudWatch logs for keywords related to the application error to create a custom metric. Then, create a CloudWatch alarm for that custom metric which invokes an action to restart the EC2 instance.**<br>
*Key word: error, restart*<br>
[Create alarms to stop, terminate, reboot, or recover an EC2 instance](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/UsingAlarmActions.html/)


**#2**.A company has a UAT and production EC2 instances running on AWS. They want to ensure that employees who are responsible for the UAT instances don't have access to work on the production instances to minimize security risks.

Which of the following would be the best way to achieve this?

**Define the tags on the UAT and production servers and add a condition to the IAM policy which allows access to specific tags.**<br>
*Key word: security access of Development resource , TAG for UAT PRD, IAM policy*


## Resource Provisioning, Security compliance
**#1**.A company has a group of developers who manage their own resources on AWS cloud. These developers employ IAM user access keys to automate their resource provisioning and application testing processes within AWS. To maintain proper security compliance, the security team aims to automate the deactivation and deletion of any IAM user access key that is older than 90 days.

Which solution will meet these requirements with the LEAST operational effort?

**Use the AWS Config managed rule to check if the IAM user access keys are not rotated within 90 days. Create an Amazon EventBridge (Amazon CloudWatch Events) rule for the non-compliant keys, and define a target to invoke a custom Lambda function to deactivate and delete the keys.**<br>
*Key word: AWS Config, developer provisioning, compliance*<br>

**#2**.A new company policy requires IAM users to change their passwords’ minimum length to 12 characters. After a random inspection, you found out that there are still employees who do not follow the policy.

How can you automatically check and evaluate whether the current password policy for an account complies with the company password policy?

**Configure AWS Config to trigger an evaluation that will check the compliance for a user’s password periodically.**<br>
*Key word: AWS Config, Compliance for password policy*<br>


## Architecture for internet access

**#1**.A Solutions Architect is designing the cloud architecture for the enterprise application suite of the company. Both the web and application tiers need to access the Internet to fetch data from public APIs. However, these servers should be inaccessible from the Internet.

Which of the following steps should the Architect implement to meet the above requirements?

**deploy a NAT gateway in the public subnet and add a route to it from the private subnet where the web and application tiers are hosted.**<br>
*Key word: Nat gateway, Route, Subnet*

## Failover && High availibility

**#1**.A company is running a web application on AWS. The application is made up of an Auto-Scaling group that sits behind an Application Load Balancer and an Amazon DynamoDB table where user data is stored. The solutions architect must design the application to remain available in the event of a regional failure. A solution to automatically monitor the status of your workloads across your AWS account, conduct architectural reviews and check for AWS best practices.

Which configuration meets the requirement with the least amount of downtime possible?

**In a secondary region, create a global table of the DynamoDB table and replicate the auto-scaling group and application load balancer. Use Route 53 DNS failover to automatically route traffic to the resources in the secondary region. Set up the AWS Well-Architected Tool to easily get recommendations for improving your workloads based on the AWS best practices**<br>
*Key word: Region failover, Route53 failover, Well-Architected Tool, DynamoDB global table*

## Auto scaling
**#1**.An Auto Scaling group (ASG) of Linux EC2 instances has an Amazon FSx for OpenZFS file system with basic monitoring enabled in CloudWatch. The Solutions Architect noticed that the legacy web application hosted in the ASG takes a long time to load. After checking the instances, the Architect noticed that the ASG is not launching more instances as it should be, even though the servers already have high memory usage.

Which of the following options should the Architect implement to solve this issue?

**Install the CloudWatch unified agent to the EC2 instances. Set up a custom parameter in AWS Systems Manager Parameter Store with the CloudWatch agent configuration to create an aggregated metric on memory usage percentage. Scale the Auto Scaling group based on the aggregated metric**<br>
*Key word: CloudWatch unified agent, Manager Parameter Store, metric of memory usage*<br>
*[explanation]*<br>
CloudWatch doesn't monitor memory usage but only the CPU utilization, Network utilization, Disk performance, and Disk Reads/Writes.Therefore you should use  CloudWatch unified agent to collect the memory usage.  

## Encryption
**#1**.A multinational bank is storing its confidential files in an S3 bucket. The security team recently performed an audit, and the report shows that multiple files have been uploaded without 256-bit Advanced Encryption Standard (AES) server-side encryption. For added protection, the encryption key must be automatically rotated every year. The solutions architect must ensure that there would be no other unencrypted files uploaded in the S3 bucket in the future.

Which of the following will meet these requirements with the LEAST operational overhead?

**Create an S3 bucket policy that denies permissions to upload an object unless the request includes the s3:x-amz-server-side-encryption": "AES256" header. Enable server-side encryption with Amazon S3-managed encryption keys (SSE-S3) and rely on the built-in key rotation feature of the SSE-S3 encryption keys.**<br>
*Key word: automatically rotated every year(built-in), SSE-S3, s3:x-amz-server-side-encryption": "AES256" header*<br>

**#2**.A company is looking to store their confidential financial files in AWS which are accessed every week. The Architect was instructed to set up the storage system which uses envelope encryption and automates key rotation. It should also provide an audit trail that shows who used the encryption key and by whom for security purposes.

Which combination of actions should the Architect implement to satisfy the requirement in the most cost-effective way? (Select TWO.)

**using Amazon S3 to store the data and configuring Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS)**
*Key word: envelope encryption, automates key rotation, audit trail that shows who used, SSE-KMS*<br>

**SSE-s3 vs SSE-KMS**

SSE-KMS = Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS)

Server-Side Encryption with Customer Master Keys (CMKs) Stored in AWS Key Management Service (SSE-KMS) – *Similar to SSE-S3*, but with some additional benefits and *charges for using* this service. There are separate permissions for the use of a CMK that provides added protection against unauthorized access of your objects in Amazon S3. SSE-KMS also provides you with an *audit trail that shows when your CMK was used and by whom*. Additionally, you can create and manage customer-managed CMKs or use AWS managed CMKs that are unique to you, your service, and your Region.

**#3**.A health organization is using a large Dedicated EC2 instance with multiple EBS volumes to host its health records web application. The EBS volumes must be encrypted due to the confidentiality of the data that they are handling and also to comply with the HIPAA (Health Insurance Portability and Accountability Act) standard.

In EBS encryption, what service does AWS use to secure the volume's data at rest? (TWO CHOICES)

**using your own keys in AWS Key Management Service (KMS)**<br>
**using Amazon-managed keys in AWS Key Management Service (KMS).**<br>
*Key word: EBS volumes's encryption, own keys + KMS, aws-managed key + KMS*

## Storage
**#1**.A company has both on-premises data center as well as AWS cloud infrastructure. They store their graphics, audios, videos, and other multimedia assets primarily in their on-premises storage server and use an S3 Standard storage class bucket as a backup. Their data is heavily used for only a week (7 days) but after that period, it will only be infrequently used by their customers. The Solutions Architect is instructed to save storage costs in AWS yet maintain the ability to fetch a subset of their media assets in a matter of minutes for a surprise annual data audit, which will be conducted on their cloud storage.

Which of the following are valid options that the Solutions Architect can implement to meet the above requirement? 

**Set a lifecycle policy in the bucket to transition the data from Standard storage class to Glacier after one week (7 days).**<br>
**Set a lifecycle policy in the bucket to transition to S3 - Standard IA after 30 days.**<br>
*Key word: S3, Glacier, Standard IA, 30 days limitation*

[take note]there is a constraint in S3 that objects must be stored at least *30 days* in the current storage class before you can transition them to *STANDARD_IA or ONEZONE_IA*.


## Database migration, high availibility, security

**#1**.A leading media company has recently adopted a hybrid cloud architecture which requires them to migrate their application servers and databases in AWS. One of their applications requires a heterogeneous database migration in which you need to transform your on-premises Oracle database to PostgreSQL in AWS. This entails a schema and code transformation before the proper data migration starts.   

Which of the following options is the most suitable approach to migrate the database in AWS? <br>

**First use the AWS Schema Conversion Tool to convert the source schema and code to match that of the target database, and then use the AWS Database Migration Service to migrate data from the source database to the target database.**<br>
*Key word: migration, oracle->postgre in AWS, schema and code transformation *

