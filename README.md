# AWS

## AWS Cloud Overview - Regions & AZ
### How to choose AWS Region

__Compliance__ with data governance and legal requirements: data never leaves a region without your explicit permission.

__Proximity__ to customers: reduces latency

__Available services__ withing a Region: new services and features aren't available in every Region

__Pricing__: pricing varies from region to region. Details available in service pricing page.

### AWS Availability Zones

Each region has many availability zones (usually 3, min 2, max 6). For Example: AWS Region in Sydney has 3 Regions i.e

  1. ap-southeast-2a
  2. ap-southeast-2b
  3. ap-southeast-2c

Each availability zone (AZ) is one or more discreet data centers with redundant power, networking, and connectivity. 

These are seperate from each other, so that they're isolated from disasters.

They are connected with high bandwidth, untra-low latency networking, and therefore all together they form a Region.

### AWS Points of Presence (Edge Locations)

  * Amazon has 216 Points of Presence (205 Edge         Locations & 11 Regional Caches) in 84 cities across 42 countries.

  * Content is delivered to end users with lower latency.

### Tour of the AWS Console
__AWS has Global Services:__
  * Identity and Access Management (IAM)
  * Route 53 (DNS service)
  * CloudFront (Content Delivery Network)
  * WAF (Web Application Firewall)

__Most AWS services are Region-scoped:__
  * Amazon EC2 (Infrastructure as a Service)
  * Elastic Beanstalk (Platform as a Service)
  * Lambda (Function as a Service)
  * Rekognition (Software as a Service)

## IAM Introduction: Users, Group, Policies

### IAM: Users & Groups
  * __IAM__: Identity and Access Management, is Global service because in IAM, we are going to create our users and assign them to group.
  * __Root account__: When we created AWS account we created root account. It has been created by default. This is the root user of our accounts. And the only things you should use it for is to set up your account.
  * __Users__ are people within your organization, and can be grouped. 
  * __Groups__ can only contain users, not other groups.
  * __Users__ don't have to belong to a group, and user can belong to multiple group. 

### IAM: Permissions
#### Why do we create users and why do we create groups?
Because we wwant to allow them to use our AWS accounts and to allow them to do so, we have to give them permissions. So users or groups can be assigned.

  * __Users or Groups__ can be assigned JSON documents called IAM policies.
  * These policies define the permissions of the users
  * In AWS you apply the __least privilege principle__: don't give more permissions that a user needs. 

