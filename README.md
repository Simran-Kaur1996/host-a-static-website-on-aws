# Host a Static Website on AWS

## Overview
This project demonstrates how to host a static HTML web app on AWS using EC2 instances, VPC, Load Balancer, Auto Scaling, and other AWS services. The setup is designed to be highly available, scalable, and fault-tolerant, leveraging AWS infrastructure.

## Architecture
The architecture includes:
1. **Virtual Private Cloud (VPC)**: Configured with public and private subnets across two Availability Zones for fault tolerance.
2. **Internet Gateway**: Provides connectivity between VPC instances and the internet.
3. **Security Groups**: Acts as a firewall to control access to the EC2 instances.
4. **EC2 Instances**: Deployed within private subnets for security.
5. **NAT Gateway**: Allows instances in private subnets to access the internet.
6. **Application Load Balancer (ALB)**: Distributes incoming web traffic across EC2 instances.
7. **Auto Scaling Group**: Automatically manages EC2 instances to ensure availability and scalability.
8. **AWS Certificate Manager (ACM)**: Secures the application with SSL/TLS.
9. **Amazon Route 53**: Manages the DNS records for the domain.
10. **SNS Notifications**: Alerts about Auto Scaling activities.

## Resources Used
- **Amazon EC2**: For web server hosting.
- **Amazon VPC**: For network setup.
- **Amazon Route 53**: For DNS management.
- **Amazon Elastic Load Balancer (ELB)**: For traffic distribution.
- **Amazon Auto Scaling**: For automatic scaling of web servers.
- **Amazon Certificate Manager (ACM)**: For SSL certificates.
- **Amazon SNS**: For notifications.

## Deployment Steps

1. **Configure VPC and Subnets**: Set up both public and private subnets across two availability zones to ensure high availability and fault tolerance.
2. **Create and Attach Internet Gateway**: This enables instances in public subnets to access the internet.
3. **Set Up Security Groups**: Define rules to control the access to instances (e.g., allow HTTP/HTTPS access to web servers).
4. **Launch EC2 Instances**: Deploy web servers in private subnets and set up Application Load Balancer for distributing traffic.
5. **Enable EC2 Instance Connect**: For secure SSH access to instances in private subnets.
6. **Configure NAT Gateway**: Allow instances in private subnets to access the internet.
7. **Deploy Application**: Host a static HTML web app by cloning the GitHub repository to the EC2 instance.

## Steps to Host the Static Website

### EC2 Instance Setup Script:
```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/Simran-Kaur1996/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Key Steps:
1. **Install Apache HTTP Server**: This is done using `yum install httpd` to set up a web server on your EC2 instance.
2. **Clone the GitHub Repository**: The script clones your GitHub repository which contains the static HTML files.
3. **Copy Files to Web Root**: The files from the repository are copied to the Apache web root directory (`/var/www/html`) for Apache to serve.
4. **Start the Web Server**: The Apache HTTP server is enabled and started to begin serving the website.

## Additional Configuration
- **Auto Scaling Group**: Automatically scales the number of EC2 instances based on web traffic.
- **Application Load Balancer**: Ensures traffic is distributed evenly across instances.
- **SNS Notifications**: Set up notifications for scaling events.

## Domain and DNS Configuration
- **Amazon Route 53**: Register your domain and set up a DNS record to point to the Load Balancer's endpoint.

## Conclusion
This setup provides a scalable, fault-tolerant, and secure environment to host a static website on AWS. The architecture leverages multiple AWS services to ensure the website remains available under varying traffic loads, while maintaining security and performance.

---

### How to Use This Project:
1. **Clone the Repository**: 
   ```bash
   git clone https://github.com/Simran-Kaur1996/host-a-static-website-on-aws.git
   ```
2. **Deploy Resources on AWS**:
   Follow the steps in the project to set up your VPC, EC2 instances, Auto Scaling Group, and other AWS services.

3. **Monitor Your Website**:
   Use the SNS alerts to monitor the scaling activities and health of the website.


