#Deploying a small HTML/CSS/JS website on AWS EC2
This document details the deployment of a static website showcasing the 10 EHF Champions League winners on an Amazon EC2 instance.

**Introduction**

This project demonstrates hosting a simple website built with HTML, CSS, and Javascript on an AWS EC2 instance. The website serves information about the 10 handball teams to have won the prestigious EHF Champions League.

Use cases
While EC2 offers a robust solution for various web applications, this specific approach is most beneficial for:
Simple Static Websites: Small websites with limited content updates and functionality are well-suited for EC2 due to its cost-effectiveness compared to more complex services.
Learning and Experimentation: This deployment process is ideal for individuals or teams new to AWS to gain hands-on experience with EC2 and Linux server management.
It's important to note that:
EC2 requires ongoing maintenance for security updates and software installations.
Scalability for high traffic websites can be challenging with a single EC2 instance.

Key components of the project
AWS EC2: A virtual server instance running a Linux operating system.
Linux Machine: The operating environment within the EC2 instance, in this case, likely Amazon Linux 2.
Session Manager: A secure way to connect to the EC2 instance for management and configuration.
Apache httpd: A web server software that serves the website content.
wget: A command-line tool for downloading files from the internet (used to download website files from GitHub).
unzip: A command-line tool for extracting compressed files (used to unzip the downloaded website archive).

Implementation guide
1. Setting up the EC2 Instance:
Launch an EC2 instance with a suitable instance type based on your expected traffic volume. The details of the EC2 are shown below:


Create a key pair for secure access and download the private key file. 
The below screenshot is taken from SSH client connectivity mode to showcase the creation of the key pair, but for this project I used the session manager.

Configure a Security Group to allow inbound traffic on port 80 (HTTP).
EC2 instance networking specifications:
	


We edited the security rules to make sure the public IP of the instance is accessible in the browser:



Health checks of the EC2 to make sure the instance it is good to be used for the deployment:





2. Connecting with Session Manager:
Open the AWS Management Console and navigate to the EC2 service.
Select your instance and choose "Connect" under the "Actions" menu.
Use Session Manager to connect to the instance using the downloaded private key file.

3. Updating the System and Installing Packages:
Gain root privileges using sudo su -.
Update the system packages using yum update -y.
Install the Apache web server using yum install -y httpd.
Verify service status with systemctl status httpd.
4. Downloading and Deploying the Website:
Create a temporary directory using mkdir temp and navigate to it with cd temp.
Download the website files from a GitHub repository using wget https://github.com/bogdanapostol97/website-s3/archive/refs/heads/main.zip.
Extract the downloaded archive using unzip main.zip.
Navigate to the extracted website directory using cd website-s3-main.
Move all website files to the web server document root with mv * /var/www/html.
Verify file presence in the document root with ls /var/www/html.
5. Starting and Enabling the Web Server:
Start the Apache web server service with systemctl start httpd.
Enable the service to launch automatically on system boot with systemctl enable httpd.
Verify service status again with systemctl status httpd.

The sequence of commands I described above and the outcome of each one.

6. Accessing the Website:
Obtain the public IP address of your EC2 instance from the AWS Management Console.
Open a web browser and enter the public IP address followed by ":80" (e.g., http://<public_ip_address>:80).
Your handball website should now be accessible.



Operational excellence
Security: Consider implementing a firewall to further restrict inbound traffic and harden the server configuration with security best practices.
Reliability: Utilize automated backups and snapshots of your EC2 instance and website files for disaster recovery purposes.
Performance Efficiency: Monitor server performance and consider scaling up the instance type or optimizing website code for better user experience.
Cost Optimization: Explore options like Amazon Lightsail for static websites with predictable traffic to potentially reduce costs. Utilize EC2 Scheduled Scaling to automatically adjust resource allocation based on traffic patterns.
Sustainability: While EC2 offers flexibility, consider serverless options like AWS S3 buckets with static website hosting capabilities for a more energy-efficient approach for simple websites.

Conclusion
This project demonstrates a basic method for deploying a static website on AWS EC2. By following the detailed implementation guide and considering the points on operational excellence, you can create a functional website while understanding the trade-offs involved in using EC2 for this


