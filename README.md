![Alt text](/Host_a_Static_Website_on_AWS.png).

---
# Host-a-static-website-on-aws
Host-a-static-website-on-aws
Here's the updated README file for your project that includes the necessary information about your AWS setup and the deployment script:

---

# Host a Static Website on AWS

## Overview
This project demonstrates how to host a static HTML web application on Amazon Web Services (AWS). The infrastructure is designed with best practices for scalability, security, and fault tolerance. The project utilizes AWS resources such as EC2, VPC, Auto Scaling, Load Balancer, Route 53, and more. All relevant scripts, architecture diagrams, and configuration files are available in this repository.

## Project Architecture
The infrastructure setup includes the following AWS components:
1. **Virtual Private Cloud (VPC)** with public and private subnets across two different availability zones for enhanced fault tolerance.
2. **Internet Gateway** to provide connectivity between the instances in the VPC and the broader internet.
3. **Security Groups** to control inbound and outbound traffic to EC2 instances and other resources.
4. **Public Subnets** for infrastructure components like the NAT Gateway and Application Load Balancer (ALB).
5. **EC2 Instances** in **Private Subnets** to enhance security and isolate web servers from direct exposure to the internet.
6. **Application Load Balancer (ALB)** for distributing traffic evenly to EC2 instances across multiple Availability Zones.
7. **Auto Scaling Group** to manage the EC2 instances automatically, ensuring scalability, availability, and elasticity.
8. **Route 53** for DNS management, allowing you to map a custom domain to your web application.

## Key Features
1. Hosted a static HTML website on EC2 instances.
2. Set up an **Application Load Balancer** to distribute traffic to multiple EC2 instances in different Availability Zones.
3. Implemented **Auto Scaling** to automatically scale EC2 instances based on demand.
4. Secured the application using **AWS Certificate Manager** for SSL/TLS encryption.
5. Configured **SNS (Simple Notification Service)** to receive alerts regarding scaling activities within the Auto Scaling Group.
6. Registered a custom domain and set up DNS records using **Route 53**.

## Deployment Script

The following script automates the process of setting up Apache, installing dependencies, cloning the project repository from GitHub, and serving the static website on an EC2 instance.

### Script: `deploy.sh`

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
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### How to Run the Script
1. **Upload the script to your EC2 instance**: You can use SCP, SFTP, or any other method to transfer the script to your EC2 instance.
2. **Make the script executable**: Change the file permissions to make the script executable.

   ```bash
   chmod +x deploy.sh
   ```

3. **Run the script**: Execute the script to install Apache, clone the repository, and start serving the static website.

   ```bash
   ./deploy.sh
   ```

After running the script, the static website will be live and can be accessed via the public IP of your EC2 instance or the custom domain (if configured with Route 53).

## Project Files
The GitHub repository contains the following resources:
- **VPC and Networking Configuration**: Scripts and configurations to set up the VPC, subnets, and routing.
- **EC2 Configuration**: Scripts to launch EC2 instances with necessary security groups.
- **Auto Scaling and Load Balancer**: Configurations for setting up Auto Scaling and Application Load Balancer.
- **SSL Configuration**: Instructions and scripts to secure communication using SSL/TLS certificates with AWS Certificate Manager.
- **Route 53 DNS Setup**: Configuration files for DNS setup using Route 53.
- **Deployment Scripts**: Automating the deployment of the static web app.

## Resources and Costs
The following AWS resources are used in this project:
- **EC2 instances**: Cost based on the instance type and number of instances running.
- **VPC**: Costs related to the NAT Gateway, Internet Gateway, and data transfer.
- **Elastic Load Balancer (ELB)**: Charges for load balancing traffic.
- **Auto Scaling**: Costs for the instances launched in the Auto Scaling Group.
- **Route 53**: Domain registration and DNS query fees.
- **SNS**: Charges for sending notifications.

Use **AWS Cost Explorer** to monitor your expenses and optimize resource utilization.

## Conclusion
This project illustrates how to host a scalable, secure, and fault-tolerant static website on AWS. By utilizing services such as EC2, VPC, Auto Scaling, and Route 53, the website can handle high traffic while maintaining high availability and security.
