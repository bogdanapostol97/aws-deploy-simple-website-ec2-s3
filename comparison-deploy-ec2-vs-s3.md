<h1>  Comparison of EC2 and S3 Deployment </h1>

<h2> EC2 Deployment </h2>

**Key commands**

- Connecting to EC2 instance:

  aws ssm start-session --target <instance-id>
  
- Updating system and installing packages:

  - sudo su -
  - yum update -y
  - yum install -y httpd
  - systemctl status httpd

- Downloading and deploying website:

  - mkdir temp
  - cd temp
  - wget https://github.com/bogdanapostol97/website-s3/archive/refs/heads/main.zip
  - unzip main.zip
  - cd website-s3-main
  - mv * /var/www/html
  - ls /var/www/html
  
- Starting and enabling web server:

  - systemctl start httpd
  - systemctl enable httpd
  - systemctl status httpd

<h2> S3 Deployment </h2>

**Key components:**

- GitHub repository: Create a repository and push your game code.
- AWS CodePipeline: Create a pipeline with source, build (optional), and deploy stages.
- AWS S3 bucket: Create a bucket, configure static website hosting, and grant public read access.

**Key Commands:** 

- Creating S3 bucket:

  aws s3 mb s3://your-bucket-name

- Configuring static website hosting:

  aws s3 website put-bucket-website --bucket s3://your-bucket-name --index-document index.html

- Granting public read access:

  aws s3acl put-bucket-acl --bucket s3://your-bucket-name --acl public-read
  
<h2> Comparison </h2>

**Feature**

1. EC2:

   - Deployment method is manual.
   - It requires ongoing maintenance (security updates, software installation)
   - It can be scaled manually or using auto-scaling groups.
   - The cost can be more expensive for high-traffic applications.
   - The setup and management are more complex.

2. S3:

   - Deployment method is automated through AWS Codepipeline.
   - It requires minimal maintenance (CodePipeline handles updates).
   - It scales automatically based on traffic.
   - It can be more cost-effective for static content.
   - The setup and management are simpler with AWS CodePipeline.
     

**Choosing the right method:**

- EC2: Suitable for complex applications requiring flexibility and control.
- S3: Ideal for simple websites and applications with static content, offering automated deployments and cost-effectiveness.

**Additional considerations:**

- Security: Implement appropriate security measures for both methods, including IAM roles, firewalls, and encryption.
- Performance: Optimize your website or application for performance, especially if using EC2. Consider using CDNs for S3 to improve load times.
- Cost optimization: Explore options like reserved instances, spot instances, and S3 storage classes to optimize costs.

**Note:** By understanding these key aspects and commands, you can make an informed decision about which deployment method is best suited for your specific project.


