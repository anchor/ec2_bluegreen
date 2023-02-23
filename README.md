# Ec2 (In-place) Deployment via AWS CodePipeline

Here are the steps:

    1. Launch an Ec2 Instance with below specifications:
        * AMI - Amazon Linux 2 AMI (HVM)
        * Instance Type - t2.micro
        * Security group - allow inbound traffic on 8080 port number from 0.0.0.0/0
        * Storage - 8 GiB
        * Instance Profile - Ec2SSMRole
    
    2.  Create an Application and Deployment group in AWS CodeDeploy.
        * Compute Platform - EC2/On-premises
        * Service Role - CodeDeploy Role with permission to deploy an application in EC2.
        * Deployment Type - In-place
        * Environment Configuration - Amazon EC2 instances. Provide same tags which are attached to Ec2.
        * CodeDeploy Agent Configuration - Now and schedule updates
        * Uncheck the "Enable load balancing".

    3. Setup AWS CodePipeline with 2 Stages (Source=GitHub 2, Deploy=AWS CodeDeploy).
        * Service Role - CodePipeline Role with CodeDeploy permissions.
        * Source Provider - GitHub (Version 2)
            NOTE: Make sure you have already established the GitHub connection with your AWS Account.
        * Select the repository and branch "master".
        * Skip the build stage.
        * Deploy Provider: AWS CodeDeploy.
