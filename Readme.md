# Budget Setup
    - cost budget 
    - recurring budget 
    - enter your budget amount
    - configure alerts
        - actual Costs
        - threshold 
        - provide email
    - confirm buget

# AWS Regions
    - Region is cluster of data centeres, they are all over the world.
    - Most of the services are region-scoped.
    - Each region can have many AZ's (availability zones)
    - Each region has AZ's Usually 3 , min 2 , max 6 , indicated by a,b,c,d,e,f.
    - EC2 is called regional service.

# AZ 
    - AZ's is seperate data center's connected to each other.
    - They have networking and connectivity with high bandwidth, ultra-low latency networking.
    
# IAM
    - It's a global service linked to AWS account
    - Identity Access Manager, Users,Groups and Roles.
    - Root is the first time you create your AWS Account.
    - IAM is at the center of AWS
    - Policies are written in JSON
    - Users-> related to physical person
    - Group -> Users are grouped together based on functionality
        - ex: Developer,Tester,Architect, Admin
    - Roles-> These are given to machines
    - Permissions are governed by Policies written in JSON.
    - Always give the least privilege to get the job done.
    - One IAM user per physical person.
    - One IAM Role per applicaiton.
    - Never use Root IAM credentials except during the setup.
    - Never,ever,ever write IAM credentials in Code or commit to github.

# IAM Federation
    - Used by large or enterprise companies to integrate with Active Directory using SAML

# EC2 
    - Renting Virtual Machines (EC2)
    - Storing Data on virtual drives (EBS)
    - Distributing load across machines (ELB)
    - Scaling the services using an auto-scaling group (ASG)
    - Ability to start the machine and use immediately
    - AMI (Amazon Machine image) is software which is opearating system that would be launced upon based on your selection.
    - Type indicates how powerful you wanted the instance to be.
    - There is a default VPC when you are trying to create a instance
    - No Subnet preference , subnet indicates which AZ you choose to place your instance (AZ- data center).
    - Default EBS Volume is 8GB, SSD (GP2)
    - Tags allow to classify or identify the instance
    - A security group is a set of firewall rules that control the traffic for your instance. 

# SSH 
    - Works for MAc, Linux and Windows >=10
    - Windows<10 use putty 
    - Another alternative EC2 connect directly on the browser
    - SSH allows you to connect and control the remote machine using the command line with port 22.
    - ssh ec2-user@IP -i path of your PEM File.
    - ``` ssh ec2-user@13.229.183.124 -i ~/Downloads/my-first-instance-feb12-learning.pem ```
    - How to fix bad permission issue when loading the key for SSH
    - chmod 0400 pemfilepath
    - Windows
        - Download putty 
        - Use Putty gen to convert the key (PEM) file to PPK format.
        - Save ppk to respective location.
        - Open Putty enter public IP address(ec2-user@IP) of EC2 machine.
        - Under SSH, under Auth choose under Private Key fileand browse.
        - If Windows>=10 use powershell where you can use SSH directly.
        - Right click on PEM file and goto Advanced Security , ensure the owner is you, remove all other Owner's , disable inheritance and click on apply.
    - SSH Wizard does not work for EC2 Connect on the browser if the port is not open in Security Groups.
    - EC2 connect on browser works only for AMI.


# Security Groups.

    - A security group is a set of firewall rules that control the traffic for your instance.
    - They control in and out traffice for the EC2 Machines.
    - By default no rules, by default outbound is allowed.
    - Inbound rule is the control for incoming traffic.
    - Add Custom TCP Rule/HTTP/SSH  based on your needs
    - Can be attached to multiple instances
    - An instance can attach multiple SG's.
    - Locked down to region / VPC combination.
    - If your app is not accessible (timeout issue) it's a security group issue.
    - By default all inbound is blocked.

# Public vs Private IP
    - IPV4 allows for 3.7 billon different address
    - Public allows the instance to be accessed globally.
    - Private IP allows the communication only with the network.
    - Not two machines can have same public IP.
    - Machines connect to WWW using a IGW.
    - Elastic IP , fixed IP for a instance does not change when you stop and start a instance.
    - Limited to 5 instances , each instance have only one Elastic IP it's not shared.
    - Better to random public IP, register a DNS name to it.
    - You can also use LB avoid public IP.

# EC2 User Data
    - It's possible to bootstrap our instance using an EC2 User data script.
    - Bootstrapping  means launch commands when machine starts.
    - It's run only once at the instane first start.
    - It's used for
        - Installing Softwares
        - Installing Updates
        - Downloading common files from the internet
        - 

# EC2 Instance Launch Types
    - On Demand Instances : short workload , predictable pricing
    - Reserved (Min 1 year) 
        - reserved instances - long workloads
        - Convertible Reserved Instances - based on long workloads with flexible instances
        - Schedule Reserved Instances 
    - Spot Instances - short workloads , for cheap, can lose instances (not reliable)
    - Dedicated Instances - no other customers will share your hardware
    - Dedicated Host - book an entire physical server,control instance placement

    # EC2 OnDemand
        - Pay for what you use (billing per second after first minute)
        - Has the highest cost, but no upfront payment
        - No long term commitment
        - Recommended for short-term and uninterrupted workloads,where you can't predict how the application will behave.
    
    # EC2 Reserved Instances
        - Up to 75% discount compared to On Demand
        - Pay upfront for what you use, long term commitment.
        - Reservation period min 1 or 3 years.
        - Reserve a specific instance type.
        - Recommended for steady state usage applications (ex: Database,RDS)
        - Convertible Reserved Instance ,little bit expensive
            - upto 54% discount

    # EC2 Scheduled Reserved Instances
        - launch within time window you reserve
        - When you require a fraction a day/week/month
    # EC2 Spot Instances
        - Upto 90% discount, can loose at anytime.
        - Most effecient cost instances in AWS.
        - 2 minutes grace spot price>max pirce.
        - Spot Block, block instance for 1 to 6 hours without interruptions.
        - Can loose instance if max prices is less than current spot price.
        -  Useful for
            - Batch jobs
            -   Data Analysis
            - Image processing
            - Not good for critical jobs
        - Two types of request
            - one time
            - persistent valid from , valid until
        - maximum price, desired no of instances
        - To termiante the spot instance cancel the spot request and then terminate the instance.
        - To cancel spot instance they have to be active/open/disabed state.
        - Spot Fleets = set of Spot Instances + Optional OnDemand Instances.
        - Try to meet target capacity  with price constraints.
        - Stategies to allocate Spot Instances:
            - lowestPrice: from the pool with the lowest price.
            - diversified: distributed across all pools (great for availability),long work loads.
        - Spot Fleets allows us to automatically request spot instance with request price.

    # EC2 Dedicated Host
        - Physical dedicated EC2 server for you use.
        - Full control of EC2 instance placement.
        - Visibility for underlying sockets/cores of the instance.
        - 3 year period reservation, more expensive
        - Bring your own license model.
        - Strong Regulatory or complaince needs.
    # EC2 Dedicated Instances.
        - Instances running on hardware that's dedicated to you.
        - May share hardware with other instances in same account.
        - No control over instance placement (can move hardware after Stop/Start).
    
    # EC2 Instance Types - Main Ones

        - R applications that needs lot of RAM  - In memory caches, In memory databases.
        - C applications that needs good CPU - Compute databases,Big Data.
        - M applications that are balanced (think "medium") general webapp.
        - I applications that need good local I/O (instance storage) databases.
        - G applications that needs a GPU - video rendering/machine learning.
        - T2/T3: burstable instances (up to a capactiy).
        - https://instances.vantage.sh/?filter=m4&cost_duration=annually&reserved_term=yrTerm1.allUpfront
        - burst is boost of power, if the credits are gone,CPU gets terrible.
        - use cloudwatch the credit usage.
        - T2/T3 Unlimited burst credit balance.

# AMI
    - Amazon Machine Image, these can be customised at runtime using EC2 User Data.
    - AMI's can be used for Linux/Windows.
        - Faster Boost time.
        - Pre installed packages.
        - Control of Maintenacne and update
        - Security concerns - control over the machines in the network.
        - Machine comes configured with monotoring / enterprise software.
        - Installing your app ahead of time (for faster deploys when auto-scaling)
        - Using someone's else's AMI that is optimised for running an app,DB,etc.
    - Public AMIS can be found on Amazon Marketplace.
    - Your AMI take space and they live in S3.
    - By default AMI's are private and locked for your account , specific region.
    - You get charged for the actual space in takes in Amazon S3.
    - Make sure to remove the AMIs you don't use.
    - Sharing an AMI does not affec the ownership of the AMI.
    - You can share AMI to another account.
    - You can't copy an AMI with associated billingProduct code that was shared to  you from another account.If you want to copy,create a EC2 instance , launch it and then make a AMI from this.
    - If they do copy AMI to another region they become the owner of the AMI.
    - To avoid copy of AMI, you don't grant S3 or EBS permission.
    - If they make an AMI from this shared AMI, they have the AMI. 
    
# Placement Groups
    - To control the EC2 instances placement strategy in AWS infrastructure.
    - Three Strategies:
        - Cluster - low latency group, High Performance , High Risk. 
            -  Same Rack,Same AZ.
            - If Rack fails, all instances fail at the same time.
            - Greate network,useful for big data job,extreme low latency, high bandwidth.
        - Spread - spreads instances across underlying hardware ( max 7 per AZ) - critical apps.
            - Minimise the risk, located in different hardware.
            - Reduce risk of hardware failure.
            - Applications maximise of high availability.
            - Critical applications , isolate from failure.
        - Partition - spreads instances across many different paritions, they rely on different set of racks. Scales to 100 of EC2 instances in group.
            - Each partition different types of instances.
            - across the partition no failure.
            - They are placed in single rack.
            - Upto 7 partitions per AZ
            - Upto 100 EC2 instances.
            - Partition failure will affect many instances in that partition.
            - Distributed Big Data applciations such as HDFS,HBase,Cassandra,Kafka usecases.
            - The instance in partition don't share racks with the another instance in other partition.

