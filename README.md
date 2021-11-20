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
Because we want to allow them to use our AWS accounts and to allow them to do so, we have to give them permissions. So users or groups can be assigned.

  * __Users or Groups__ can be assigned JSON documents called IAM policies.
  * These policies define the permissions of the users
  * In AWS you apply the __least privilege principle__: don't give more permissions that a user needs. 

### Why do we want to create a IAM user? 
Because root user have all the permission you want in your account. You can do anything you want, therefore it can be dangerous account to use. Better way is to create administrator account. 

## IAM hands on
### How to create a IAM admin user?
IAM users and groups are created in a global fashion. IAM does not require region selection. 
  1. Search for IAM and GOTO IAM dashboard.
  2. Click Users.
  3. Click on Add Users
  4. Fill username feild.
  5. For AWS access type, select __Password - AWS Management Console Access__
  6. We don't require password reset.
 Now we need to add a user to group. 
  7. So create a group. 
  8. Name the group.
  9. For admin group select group policy __Administrator Access__
  In AWS there are Tags everywhere, they are information, that can help you track, organize or controll access for users.
  10. Next and Review
  11. Review and Create User
  12. Download the CSV if you auto-gen the pw. OR, you can also send email to a particular user if you are creating USER for someone else. 
  13. After creating a user you can review their permissions, groups, tags under USER. You can also set alias for User because AWS generates a number which can be hard to remember. 

## IAM Policies inheritance
Let's imagine we have three developers Alice, Bob, and Charles, and we attach a policy at group level. In that case policy will get applied to all the members of the groups. 

### IAM Policies Structure
  * Consists of 
    * __Version__: policy language version, always include "2012-10-17"
    * __Id__: an identifier for the policy(optional)
    * __Statement__: one of more individual statements(required) 
  * __Statements__ consists of
    * __Sid__: identifier for the statement(optinal)
    * __Effect__: whether the statement allows or denies access(Allow, Deny)
    * __Principal__: account/user/role to which policy applied to.
    * __Condition__: conditions for when this policy is in effect(optional)

We can add or remove policies to the user or user groups from policies tab on left hand side. 



