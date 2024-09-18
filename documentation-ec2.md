<h1> Deploying a small HTML/CSS/JS website on AWS EC2 </h1>

This document details the deployment of a static website showcasing the 10 EHF Champions League winners on an Amazon EC2 instance.

<h2> Disclaimer </h2>

Many thanks to the guidance offered in the laboratory: https://www.youtube.com/watch?v=ri-Bn5mGcCw

The documentation is customized with the implementation of my own website and how I solved the issues that have appeared along the way.

<h2> Introduction </h2>

This project demonstrates hosting a simple website built with HTML, CSS, and Javascript on an AWS EC2 instance. The website serves information about the 10 handball teams to have won the prestigious EHF Champions League.

<h2> Use cases </h2>

While EC2 offers a robust solution for various web applications, this specific approach is most beneficial for:
- Simple Static Websites: Small websites with limited content updates and functionality are well-suited for EC2 due to its cost-effectiveness compared to more complex services.
- Learning and Experimentation: This deployment process is ideal for individuals or teams new to AWS to gain hands-on experience with EC2 and Linux server management.

**It's important to note that:**
EC2 requires ongoing maintenance for security updates and software installations.

- Scalability for high traffic websites can be challenging with a single EC2 instance.

<h2> Key components of the project </h2>
- AWS EC2: A virtual server instance running a Linux operating system.
- Linux Machine: The operating environment within the EC2 instance, in this case, likely Amazon Linux 2.
- Session Manager: A secure way to connect to the EC2 instance for management and configuration.
- Apache httpd: A web server software that serves the website content.
- wget: A command-line tool for downloading files from the internet (used to download website files from GitHub).
- unzip: A command-line tool for extracting compressed files (used to unzip the downloaded website archive).

<h2> Implementation guide </h2>
1. Setting up the EC2 Instance:

- Launch an EC2 instance with a suitable instance type based on your expected traffic volume. The details of the EC2 are shown below:

<img width="675" alt="Screenshot 2024-08-26 at 09 39 32" src="https://github.com/user-attachments/assets/279cb5d8-0e4f-4e83-8688-e74d8791b152">

- Create a key pair for secure access and download the private key file. 
The below screenshot is taken from SSH client connectivity mode to showcase the creation of the key pair, but for this project I used the session manager.

<img width="677" alt="Screenshot 2024-08-26 at 09 53 24" src="https://github.com/user-attachments/assets/43d7763d-f281-4ba1-994c-39bc332bb9a5">

- Configure a Security Group to allow inbound traffic on port 80 (HTTP).
EC2 instance networking specifications:

![image](https://github.com/user-attachments/assets/194b7469-52fd-49a4-ab50-4cc5c99a2327)

![image](https://github.com/user-attachments/assets/006657cf-13d4-4681-a7e1-bf9debfea712)


We edited the security rules to make sure the public IP of the instance is accessible in the browser:

![image](https://github.com/user-attachments/assets/f55eb871-1136-4053-b12a-f0ed5c15492b)

Health checks of the EC2 to make sure the instance it is good to be used for the deployment:

![image](https://github.com/user-attachments/assets/2b85264b-9380-4d0e-a51a-4dd87ab6dba8)

![image](https://github.com/user-attachments/assets/9248886f-364e-438b-b0b0-894d6e80a698)



2. Connecting with Session Manager:
- Open the AWS Management Console and navigate to the EC2 service.
- Select your instance and choose "Connect" under the "Actions" menu.
- Use Session Manager to connect to the instance using the downloaded private key file.

![image](https://github.com/user-attachments/assets/7da2f6b7-150b-4180-a421-3291450a6ca1)


3. Updating the system and installing packages:
- Gain root privileges using **sudo su -.**
- Update the system packages using **yum update -y.**
- Install the Apache web server using **yum install -y httpd.**
- Verify service status with **systemctl status httpd.**


4. Downloading and deploying the website:
- Create a temporary directory using mkdir temp and navigate to it with **cd temp.**
- Download the website files from a GitHub repository using **wget https://github.com/bogdanapostol97/website-s3/archive/refs/heads/main.zip.**
- Extract the downloaded archive using **unzip main.zip.**
- Navigate to the extracted website directory using **cd website-s3-main.**
- Move all website files to the web server document root with **mv * /var/www/html.**
- Verify file presence in the document root with **ls /var/www/html.**

5. Starting and enabling the web server:
- Start the Apache web server service with **systemctl start httpd.**
- Enable the service to launch automatically on system boot with **systemctl enable httpd.**
- Verify service status again with **systemctl status httpd.**

The sequence of commands I described above and the outcome of each one.

![image](https://github.com/user-attachments/assets/90c59a4e-fcd9-4978-907a-73b3180342b2)

6. Accessing the website:
- Obtain the public IP address of your EC2 instance from the AWS Management Console.
- Open a web browser and enter the public IP address followed by ":80" (e.g., http://<public_ip_address>:80).
- Your handball website should now be accessible.

![image](https://github.com/user-attachments/assets/98979aef-d33c-44cb-8328-7aca590404a7)


<h2> Operational excellence </h2>
- Security: Consider implementing a firewall to further restrict inbound traffic and harden the server configuration with security best practices.
- Reliability: Utilize automated backups and snapshots of your EC2 instance and website files for disaster recovery purposes.
- Performance Efficiency: Monitor server performance and consider scaling up the instance type or optimizing website code for better user experience.
- Cost Optimization: Explore options like Amazon Lightsail for static websites with predictable traffic to potentially reduce costs. Utilize EC2 Scheduled Scaling to automatically adjust resource allocation based on traffic patterns.
- Sustainability: While EC2 offers flexibility, consider serverless options like AWS S3 buckets with static website hosting capabilities for a more energy-efficient approach for simple websites.

<h2> Conclusion </h2>

This project demonstrates a basic method for deploying a static website on AWS EC2. By following the detailed implementation guide and considering the points on operational excellence, you can create a functional website while understanding the trade-offs involved in using EC2 for this


