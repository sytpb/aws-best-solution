# aws-best-solution
Best practice and solution for AWS cloud



## Web Design 


**1**<br>
A company has a web application that is hosted in an Auto Scaling group of EC2 instances behind an Application Load Balancer and is deployed across multiple AWS regions. The users can be found all around the globe, but the majority are from Japan and Sweden. Because of the compliance requirements in these two locations, you want the Japanese users to connect to the servers in the *ap-northeast-1* Asia Pacific (Tokyo) region, while the Swedish users should be connected to the servers in the *eu-west-1* EU (Ireland) region.

How should you to easily fulfill this requirement?


**Geolocation routing
