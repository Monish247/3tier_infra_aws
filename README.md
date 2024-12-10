AWS 3-Tier Infrastructure Project


Description:

This project demonstrates a hands-on implementation of a three-tier web architecture using AWS. The primary purposes of this project are to achieve high availability, enhanced security through SSM Session Manager, and fault tolerance. We manually created the necessary network, security, application, and database components to run this architecture in an available and scalable manner.

Architecture Overview

In this architecture, a public-facing Application Load Balancer (ALB) forwards client traffic to our web tier EC2 instances. The web tier runs Nginx web servers configured to serve a React.jswebsite and redirect API calls to the application tier’s internal-facing load balancer. The internal-facing load balancer then forwards traffic to the application tier, which is built using Node.js.The application tier manipulates data in an Aurora MySQL multi-AZ database and returns it to the web tier. Load balancing, health checks, and auto-scaling groups are created at each layer to maintain the availability of this architecture.

Key Purposes:

High Availability: Ensured through the use of multi-AZ deployments, load balancing, and auto-scaling.
Enhanced Security: Achieved through Security Groups, IAM roles, and SSM Session Manager for secure access.
Fault Tolerance: Implemented with redundant components and multi-AZ setups to handle failures gracefully.

Project Steps

Creating 3-Tier Architecture & Integrating Other AWS Resources
Step 1: Download Code from GitHub to Your Local System

Step 2: Create Two S3 Buckets

Create one S3 bucket for storing web-server and app-server code.
Upload the code to your S3 bucket from your local system.

Create another S3 bucket for VPC flow logs.

Step 3: Create IAM Role with Policies
S3 read-only access.

SSM managed instance core.

Step 4: Create VPC, Subnets, IGW, NAT-GW, and Route Tables
Enable auto-assign public IP for web-tier public subnets.

Create flow logs for VPC and use the S3 bucket created above.

Step 5: Create Security Groups
External Load Balancer SG: HTTP (80) - Allow from 0.0.0.0/0.

Web-Tier SG: Allow HTTP from the External Load Balancer SG.

Internal Load Balancer SG: Allow HTTP from the Web-Tier SG.

App-Tier SG: Allow Port 4000 from the Internal Load Balancer SG.

DB-Tier SG: Allow MySQL (3306) from the App-Tier SG.

Step 6: Create DB Subnet Group & RDS
Create a DB subnet group.

Create an RDS instance with Multi-AZ setup.

Place them in the DB subnet group created above.

Step 7: Create Test App Server, Install Packages, Test Connections
Use the Test App-Server Commands.

Create an AMI from the test app server.

Create a launch template using the AMI.

Create a target group for the app servers.

Create an internal load balancer.

Create an auto-scaling group for the app servers.

Edit the nginx.conf file locally by adding the Internal-LB-DNS and upload the file to S3.

Step 8: Create Test Web Server, Install Packages (Nginx, Node.js(React)), Test Connections
Use the Test Web-Server Commands.

Create an AMI from the test web server.

Create a launch template using the AMI.

Create a target group for the web servers.

Create an external load balancer.

Create an auto-scaling group for the web servers.

Step 9: Add External ALB DNS Record in Route 53
Step 10: Create CloudWatch Alarms Along with SNS
Step 11: Enable CloudTrail
Step 12: Deleting the Entire Infrastructure
Delete CloudFront.

Delete CloudWatch alarms.

Delete records from Route 53.

Delete load balancers, target groups, ASG, and launch templates.

Delete security groups.

Delete NAT gateway (it will take 5 mins).

Release elastic IP.

Delete VPC.

Delete RDS subnet group and RDS instance.
