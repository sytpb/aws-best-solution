# aws-best-solution
Best practice and solution for AWS cloud



## Web Design 

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

*Key word: Nat gateway, Route, Subnet



