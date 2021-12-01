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
  13. After creating a user you can review their permissions, groups, tags under USER. You can also set alias (in Dashboard) for User because AWS generates a number which can be hard to remember. 

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

## IAM - Password Policy
After creating users and groups, we need to protect users and groups. For this there are two defense mechanish:
### First One - Strong Password
  * __Strong password__: stronger pw you create higher security for your account.
  * In __AWS__, you can setup a password policy with different options
    * Set a minimum password length
    * Require specific characters types:
      * including uppercase
      * lowercase letters
      * numbers
      * non-alphanumeric characters
    * Allow all IAM users to change their own passwords
    * Require users to change password after some time (password expiration)
    * Prevent password re-use

### Second One - Multi Factor Authentication - MFA
  * Users have access to your account and can possibly change configurations or delete resources in your AWS account.
  * You absolutely want to protect your __Root Accounts__ and hopefully all __IAM__ users.
  * __MFA__ = password you know + security device you own.
  * Main benefit of MFA:
    <u>if a password is stolen or hacked, the account is not comprimised</u>

### MFA devices options in AWS - __IMPORTANT FOR EXAM__

#### Virtual MFA device
  * Google Authenticator (phone only)
  * Authy (multi-device), ex: phone and computer
    * For Authy have support for multiple tokens on a single device.

#### Universal 2nd Factor (U2F) Security Key
  * Supports for multiple root and IAM users using a single security key
  * YubiKey by Yubico (Third-party)

#### Hardware Key Fob MFA Device
  * Provided by Gemalto (Third-party)

#### Hardware Key Fob MFA Device for AWS GovCloud(US)
  * Provided by SurePassID (Third-party)

### IAM MFA Hands On
We are going to at first setup password policy for out account. 

* First we are going to change password policy
  1. IAM service 
  2. Accounts Settings 
  3. Change password policy 

* Second we are going to do is setup MFA for _root account_
  1. Go to your root account
  2. Click on _username_ 
  3. Security credentials 
  4. MFA 
  5. __Activate MFA__ 
  6. Use app you like for 2FA 
  7. Scan the QR code on AWS root account from your phone 
  8. It will add the account 
  9. Get two codes consecutively and plug into AWS root account. 

## AWS Access Keys, CLI and SDK

* To Access AWS, there are three different ways
  1. AWS Management Console (protected by username, password + MFA)
  2. AWS Command Line Interface (CLI): protected by access keys. 
    Access keys are credentials that will allows us to use AWS from _terminal_
  3. AWS Software Development Kit (SDK) - for code: protected by access keys
    It is used whenever you want to call APIs from AWS from within your application code.

### How to generate __Access Keys__?
  * __Access keys__ are generated through the AWS Console.
  * Users manage their own access keys.
  * __Access keys are secret, just like a password. Don't share them__
    * __Access Key ID__ ~= _username_
    * __Secret Access Key__ ~= _password_

### What's the AWS CLI?
  * A tool that enables you to interact with AWS services using commands in your command-line shell.
  * With this CLI you get direct access to the public APIs of AWS services.
  * Using the CLI you can develop scripts to manage your resources and automate some of your tasks.
  * It's open source [AWS_CLI_Repo](https://github.com/aws/aws-cli)

### What's the AWS SDK?
  * AWS Software Development Kit (AWS SDK)
  * Language-specific APIs (set of libraries)
  * It will allow you to access and manage AWS services programmatically.
  * It is not something you use in terminal, it is something you embed within your application.
  * Supports many programming language
    * SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
    * Mobile SDKs (Android, iOS, ..)
    * IoT Device SDKs (Embedded C, Arduino, ..)
  * Example: AWS CLI is built on AWS SDK for Python

## AWS CLI Hands On 

### How to create Access Keys?
  1. login to AWS Console using IAM user. __Do not use root account to create security credentials__
  2. Go to IAM service
  3. Go to Users
  4. Select Users
  5. Select __Security credentials__
  6. __Create access key__ under Access key.
  7. You may download __.csv file__ for your usage, never share. 

### After this on _Terminal_ we need to configure aws CLI
  1. Enter command `aws configure`
  2. Enter your AWS Access Key ID from __.csv file__
  3. Enter your AWS Secret Key from __.csv file__
  4. Write your region i.e. us-east-1
  5. For Default output format, press enter
  Now AWS CLI is configured.

### To list users
  Use command `aws iam list-users` to list all your users 

## AWS CloudShell

  * AWS __CloudShell__ is not available in all the regions. It does same work as AWS CLI. To check if your region is available or not check out [here](https://docs.aws.amazon.com/general/latest/gr/cloudshell.html)
  * By default __CloudShell__ will use the IAM user you are in, you will not have to configure it like you did in _Terminal_
  * You can also create files or directories in your __CloudShell__ like in your _Terminal_
  * You could also upload or download the files that you have in your __CloudShell__, create multiple __CloudShell__ tabs.

## IAM Roles for AWS Services

  * Some AWS services will need to perform actions on our, i.e. IAM user's, behalf on our account.
  * For this to do action, user's will need some kind of permission. So we to assign permession to AWS services, and we can achieve that by creating an IAM roles. So these IAM role will be just like a user, but they are intended to be used not by physical people, but instead they will be used by AWS services. 
    * For example, we are going to create a EC2 instance. An EC2 instance is just like a virtual server. So, this EC2 instance may want to perform some actions on AWS and to do so, we need to give permissions to our EC2 instance. We can do that by creating IAM roles and together they will make one entity. And together, once the EC2 instance is trying to access some information from AWS, then it will use the IAM Role. And if the permission assigned to the IAM role is correct then we are going to get access to the call we're trying to make. 
  * Common Roles includes:
      * EC2 instance roles
      * Lambda Function Roles
      * Roles for CloudFormation

## IAM Roles Hands On
  * When you go to your IAM user and use IAM service, on left hand side you can see __Roles__
    1. Click on __Roles__
    2. Create role
    3. Select __AWS service__
    4. Select role you want to create, for example __EC2__
    5. Click button __Next Permissions__
    6. Attach any permission policies you want to give to this role.
    7. Click button __Next Tags__ 
    8. Add tags info, if you like.
    9. Click button __Next Review__ 
    10. Give name to this role and __Create Role__

## IAM Security Tools

### __IAM Credentials Report (account-level)__
  * This report will contain list of all your account's user and the status of their various credentials.

### __IAM Access Advisor (user-level)__
  * Access advisor shows the service permissions granted to a user and when those services were last accessed. 
  * Using this tool we are able to see which permission are not used and reduce the permission the user can get to be inlined with the principle of least-privilege.

## IAM Security Tools Hands on

### __IAM Credentials Report (account-level)__
  1. On the bottom left of IAM service click on __Credential Report__.
  2. Click __Download Report__ which will be a .csv file.

### __IAM Access Advisor (user-level)__
  1. On IAM service click on __Users__
  2. Click on user you want to find out what permission user has, for example _nirajan_ in my case.
  3. Click on Access Advisor. This is going to show me services I have used. 
  4. This will show AWS services this user is using. If you want inline with the principle of least-privilege, then maybe it makes sense to remove the AWS services the user has not accessed. 

## IAM Guidelines and Best Practices

  * Don't use the root account except for AWS account setup.
  * One physical user = One AWS user. For ex, if a friend of yours want to use AWS - do not give them root account instead create another user for them.
  * __Assign users to groups__ and assign permissions to groups to make sure that security is managed at group level. 
  * Create a __strong password policy__.
  * Use and enforce the use of __Multi Factor Authentication (MFA)__ to make your account safer from hackers.
  * Create and use __Roles__ for giving permission to AWS services. 
  * Use Access Keys for Programmatic Access (CLI/SDK)
  * To audit permission of your account use IAM __Credentials Report__ and __IAM Access Analyzer__
  * __Never Share IAM users & Access Keys__