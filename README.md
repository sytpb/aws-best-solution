# aws-best-solution
Best practice and solution for AWS cloud



## Web Design 

**1**.A company has a web application that is hosted in an Auto Scaling group of EC2 instances behind an Application Load Balancer and is deployed across multiple AWS regions. The users can be found all around the globe, but the majority are from Japan and Sweden. Because of the compliance requirements in these two locations, you want the Japanese users to connect to the servers in the *ap-northeast-1* Asia Pacific (Tokyo) region, while the Swedish users should be connected to the servers in the *eu-west-1* EU (Ireland) region.

How should you to easily fulfill this requirement?


**Geolocation routing**<br>
*Key word: global user, low latency access*<br>
[AWS Document](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-geo.html/)    


**2**.A tech company are building their mobile forex trading application. You are hired to set up their cloud architecture in AWS and to implement a highly available, fault tolerant system. For their database, they are using DynamoDB and for authentication, they have chosen to use Cognito. Since the mobile application contains confidential financial transactions, there is a requirement to add a second authentication method that doesn't rely solely on user name and password.   

How can you implement this in AWS?

**Add multi-factor authentication (MFA) to a user pool to protect the identity of your users.**<br>
*Key word: authentication, not only user name and password, Cognito*
