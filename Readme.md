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
