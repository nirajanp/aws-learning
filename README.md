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

_________________________________________________________________________

## EC2 Section

### What is Amazon EC2?

  * __EC2__ is one of the most popular of AWS' offering.
  * __EC2__ = Elastic Compute Cloud = This is the way to do infrastructure as a Service in AWS.
  * __EC2__ is not just one service. It is composed of many things at a high level, such as:
    * Renting virtual machines (EC2 instances)
    * Storing data on virtual drive (EBS volumes)
    * Distributing load across machines (ELB: Elastic Load Balancer)
    * Scaling the services using an auto-scaling group (ASG)
  * Knowing EC2 is fundamental to understand how the Cloud works.

### Sizing & configuration option to create EC2 instances

  * Operating System (OS): Linux(most popular), Windows, or even Mac OS
  * How much compute power and cores (CPU)
  * How much random-access memory (RAM)
  * How much storage space:
    * Network-attached (EBS & EFS)
    * Hardware (EC2 Instance Store)
  * Network card: speed of the card, Public IP address
  * Bootstrap script(configure at first launch): which is called EC2 User Data

  ### EC2 User Data

  * It is possible to bootstrap our instances using an __EC2 User Data__ script.
  * _bootstraping_ means launching commands when a machine starts
  * That script is _only run once_ at the instance _first start_
  * __EC2 User data__ has a very specific purpose, it is used to automate boot tasks such as:
    * Installing updates
    * Install software
    * Downloading common files from the internet
    * Anything you can think of, however the more you add into your __User Data script__ the more your instant has to do at boot time. 
    * The __EC2 User Data Script__ runs with the root user so any command you have will have pseudo rights.

### EC2 instance types: example
  __t2.micro instance is part of the AWS free tier (up to 750 hours per month), used in this course__

## Hands-On: Launching an EC2 Instance running Linux

  * We'll br launching our first virtual server using AWS Console
  * This will allow us to get high-level approach to understanding some parameters for the configuration of your EC2 instances. 
  * Then we will use EC2 user data script to configure our web server.
  * We will learn how to start/stop/terminate our instance.

  ### Create an EC2 Instance with EC2 User Data to have a website

    1. Search for EC2 service and open EC2 console
    2. Click __Instances__ on left hand side.
    3. __Launch Instances__
    4. __Choose Amazon Machine Image__, 'free-tier eligible' in my case, & next to instance type.
    5. Choose an __Instance type__, t2.micro in my case, & next to configure instance.
    6. In __Configure Instance__ Left everything default in my case except __User Data__. Wrote a script to display some
    message in web browser after running the instance, & next to add storage
    7. __Add storage__, default in my case, & next to tags
    8. You can give name to your instance in __Add Tags__, or name of department, team, & next
    9. In __Configure Security Group__. 
    10. __Review and Launch__
    
## EC2 Instance Types Basics

### EC2 Instance Types Overview
  * You can use different types of EC2 instances that are optimised for different use cases [here](https://aws.amazon.com/ec2/instance-types/)
  * For now there are seven different types of EC2 instances
    1. General Purpose
    2. Compute Optimized
    3. Memory Optimized
    4. Accelerated Computing
    5. Storage Optimized
    6. Instance Features
    7. Measuring Instance Performance
  * For each type of instance there are different families. 
  
  * Naming convention of instances, for example: __m5.2xlarge__
    * m: instance class - this is going to be General Purpose
    * 5: generation (AWS improves them over time)
    * 2xlarge: size within the instance class

### EC2 Instance Types - General Purpose
  * Great for a diversity of workloads such as web servers or code repositories.
  * They will have a good balance between:
    * Compute
    * Memory
    * Networking

### EC2 Instance Types - Compute Optimized
  * Great for compute-intensive tasks that require high performance processors:
    * Batch processing workloads
    * Media transcoding
    * High performance web servers
    * High performance computing (HPC)
    * Scientific modeling & machine learning
    * Dedicated gaming servers

### EC2 Instance Types - Memory Optimized
  * Fast performance for workloads that process large data sets in memory
  * Use cases: 
    * High performance, relational/non-relational databases
    * Distributed web scale cache stores
    * In-memory databases optimized for BI(Business Intelligence)
    * Application performing real-time processing of big unstructured data

### EC2 Instance Types - Storage Optimized
  * Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage.
  * Use cases:
    * High frequency online transaction processing(OLTP) systens
    * Relational & NoSQL databases
    * Cache for in-memory databases (for example, Redis)
    * Data warehousing applications
    * Distributed file systems

## Security Groups and Classic Ports Overview

### Introduction to Security Groups
  * __Security Groups__ are the fundamental of network security in AWS
  * They control how traffic is allowed into or out of our EC2 instances
  
  * Security groups only contains _allow_ rules.
  * Security groups rules can reference by IP or by security group

  For example: 
    We are on computer on our internet i.e. (www) and we are trying to access an EC2 instance from our computer. We are going to create a security group around EC2 instance and then this security group is going to have rules. These rules are going to say weather or not some inbound traffic (traffic coming from your computer to EC2 instance) from outside into the EC2 instance is allowed. And also if the EC2 instance can perfrom outbound traffic (to talk from EC2 into the internet).

### Security Groups
### Deeper Dive
  * Security groups are acting as a "firewall" on EC2 instances
  * They regulate:
    * Access to Ports
    * Authorised IP ranges - IPv4 and IPv6
    * Control of inbound network (from outside to the instance)
    * Control of outbound network (from the instance to other)

### Security Groups, Good to Know
  * Can be attached to multiple instances
  * Locked down to a region/VPC combination
  * Does live "outside" the EC2 - if the traffic is blocked the EC2 instance won't see it
  * __It's good to maintain one seperate security group for SSH access__
  * If your application is not accessible(time out), then it's a security group issue
  * If your application gives a "connection refused" error, then it's an application error or it's not launched
  * All inbound traffic is __blocked__ by default
  * All outbound traffic is __authorized__ by default

### Classic Ports to know
  * 22 = SSH (Secure Shell) - log into a Linux instance
  * 21 = FTP (File Transfer Protocol) - upload files into file share
  * 22 = SFTP (Secure File Transfer Protocol) - upload files using SSH
  * 80 = HTTP - access unsecured websites
  * 443 = HTTPS - access secured websites
  * 3839 = RDP (Remote Desktop Protocol) - log into a Windows instance

### NOTE
As a general rule, when you get time out in AWS when you connect to EC2 instance this has to be Security Group issue. 

## SSH Summary Table
### How do you connect inside of your server to perform some maintenance or action?
  * SSH is a command line utility that can be used on Mac, Linux, and Windows 10 or greater to perform some maintenance or action. 
  * For any version of Windows we could use Putty to do SSH.
  * EC2 instance connect is going to use web browser to connect to EC2 instance. It is valid for all Linux, Mac and Windows.

## How to SSH into your EC2 Instance Linux/Mac OS X?
  * We will learn how to SSH into your EC2 instance using Linux/Mac
  * SSH is one of the most inportant function. It allows you to control as remote machine, all using the command line.

  1. Make sure port 22 is allowed in security group of instance you are trying to access. 
  2. Use command in terminal `ssh ec2-user@public_IPv4_address`
  3. It will ask for confrimation? If you want to connect say __yes__ 

  _opps_ failed. It is because we do not want anyone to access to our machine. In order to access to our EC2 instance we need key file that was generated. 

  4. Find where you have saved your EC2.pem file.
  5. Use following command `ssh -i ~/aws-documents/EC2Tutorial.pem ec2-user@3.12.107.67`
  6. After this you will get __!!WARNING!! UNPROTECTED PRIVATE FILE__. You will get _bad permessions_ and won't allow to access SSH.
  When you first download a file the permission is 0644 and thats too open. Basically private key can leak because the private key could be accessed by other.  
  7. To fix this we use following command `chmod 0400 keyName.pem`, this gives owner to read.
  8. Use same command `ssh -i ~/aws-documents/EC2Tutorial.pem ec2-user@3.12.107.67`
  9. :tada: You are connected to EC2 instance.

## EC2 Instance Roles Demo using SSH

  * Amazon Linux 2 comes with AWS CLI. If we use `aws --version`, it will shoud AWS CLI version. 
  * You could use AWS command here such as `aws iam list-users`, but you will need to configure credentials. 
  * `aws configure` can be used to configure but it is a __NO NO__. The reason is if we run `aws configure` and enter our personal details onto this EC2 instance then anyone else in our account could again connect to our EC2 instance, for example using __EC2 Instance Connect__ and retrieve the value of these credentials in our instance.
  * As a rule of thumb never enter your IAM access keys ID, and Secred Access Key into EC2 instance. 

  __Instead__ what we have to do is use __IAM Roles__. We have created __IAM Roles__ in IAM service >> Roles, which is DemoRoleForEC2.
  * IAMReadOnlyAccess policy is attached to DemoRoleForEC2.

### We are going to attach this DemoRoleForEC2 onto our EC2 instance to provide it with credentials. 

### How do we do this?
  1. Go to DemoRoleForEC2 in IAM >> Roles
  2. If you check in you EC2 instance under security there, IAM role is empty. 
  3. Go to our instances. 
  4. Click on __Action__
  5. Click on __Security__
  6. And __Modify IAM Role__
  7. There you could _Choose IAM Role_
  8. Select the IAM role, DemoRoleForEC2 in my case. 
  9. Click on save to attach this IAM role to the instance. 
  10. Result of this is, if you now run `aws iam list-users` in your EC2 instance in which you attached role, you will be able to view users. 

  * You are seeing results because IAMReadOnlyAccess policy is attached to DemoRoleForEC2 instance IAM Role. If this is policy is detached then you won't be able to view users in EC2 instance. 

## EC2 Instances Purchasing Options
We have seen EC2 instances and virtual servers on cloud, so far we are using:
  * __On-Demand Instances__: short workload, predictable pricing

Sometime we might know we will need servers for longer time, then we can get cost savings by saying that to AWS. First option is to use
  * __Reserved Instance__ (Minimum 1 year)
  Its types are:
    * Reserved Instances: long workloads (think of a database)
    * Convertible Reserved Instances: long workloads with flexible instances (You want to change types of instances over time)
    * Scheduled Reserved Instances: example every Thursday between 3 and 6 pm
  * __Spot Instances__: short work loads, cheap, can loose instances(less reliable)
  * __Dedicated Hosts__: book an entire physical server, control instance placement

__Exam is going to ask question on choose best EC2 instance based maximum amount of cost saving or to comply with some rule__

### EC2 On Demand Instance
  * Pay for what you use:
    * Linux or Windows - billing per second, after first minute
    * All other OS - billing per hour
  * Has the highest cost but no upfront payment
  * No long-term commitment

  * Recommended for __short-term__ and __un-interrupted workloads__, where you can't predict how the application will behave

### EC2 Reserved Instance
  * Up to 75% discount compared to On-demand
  * Reservation period: 1 year = you get discount discount | 3 years = you get even bigger discount
  * Purchasing options: no upfront | partial upfront = some more discount | All upfront = even more discount
  * Reserve a specific instance type, for example you will have to specify t2.micro, c5.xlarge
  * Recommended for steady-state usage applications. For example database, if you know you will need database for next 3 years - reserving that instance will bring huge cost savings.

  #### Convertible Reserved Instance
    * Can chance the EC2 instance type
    * Upto 54% discount.

  ### Scheduled Reserved Instances
    * launch within time window you reserve
    * when you require a fraction of day / week / month
    * Still need commitment over 1 to 3 years

### EC2 Spot Instance
  * Can get a discount up to 90% compared to On-demand
  * Instances that you can "lose" at any point of time if your max price is less that the current spot price. 
  * The MOST cost-efficient instances in AWS

  * Useful for workloads that are relilient to failure
    * Batch jobs
    * Data analysis
    * Image processing
    * Any distributed workloads: if workload is distributed among two servers, and if one fails other still know how to work without any affect of terminated server
    * Workloads with a flexible start and end time

  * Not suitable for critical jobs or databases.

### EC2 Dedicated Hosts

  * An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts can help you address __complicance requirements__ and reduce cost by allowing you to use your __existing server-bound software licences__.
  * Allocated for your account for a 3 year period reservation
  * More expensive
  
  * Useful for software that have complicated licencing model (BYOL - Bring Your Own Licence)
  * Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
  * Instances running on hardware that's dedicated to you
  * May share hardware with other instances in same account
  * No control over instance placement (can move hardware after Stop/ Start)