<h1> Meme matching game deployment on AWS S3 via CodePipeline </h1>

<h2> Disclaimer </h2>

Many thanks to the guidance offered in this laboratory: https://www.youtube.com/watch?v=biYVW1TMYAU&list=PLwyXYwu8kL0wMalR9iXJIPfiMYWNFWQzx&index=8

This guide is customized with the implementation of my own website and how I solved the issues that have appeared along the way.

<h2> Introduction </h2>

This document outlines the deployment of a HTML, CSS, and JavaScript-based meme matching game to an AWS S3 bucket using AWS CodePipeline. The game presents users with ten image pairs and challenges them to find matching pairs within a minimum number of attempts.

<h2> Use cases </h2>

This deployment strategy is particularly suitable for:
**- Simple Web Applications:** Games or applications with static content that require frequent updates are ideal candidates for this setup. <br />
**- Rapid Deployment:** The automated pipeline ensures swift deployment of code changes, enabling quick iterations and updates. <br />
**- Cost-Effective Hosting:** S3 is a cost-efficient solution for static content, especially when considering low to moderate traffic. <br />

<h2> Key components of the project </h2>
- GitHub: Version control repository for the game code.
- AWS CodePipeline: Automation service to build, test, and deploy the game.
- AWS S3: Object storage for hosting the game files.

<h2> Implementation guide </h2>
1. Game Development:

- Create the game logic using HTML, CSS, and JavaScript.
- Ensure the game's core functionality is implemented, including:
  
  - Displaying ten random image pairs.
  - Implementing click event handlers for image selection.
  - Comparing selected images for matches.
  - Removing matched pairs from the screen.
  - Tracking the number of attempts.
  - Providing game over or win conditions.

**Note:** The initial application that is running locally:

![image](https://github.com/user-attachments/assets/13f6d88c-900a-440f-9b2c-7d4f150dd5fa)

2. GitHub Repository:
   
- Create a GitHub repository to store the game code.
- Commit and push the code to the main branch.
  
3. AWS S3 Bucket Setup:
   
- Create an S3 bucket in the desired AWS region.

![image](https://github.com/user-attachments/assets/02518d36-86e7-44d3-8406-3c4669d1b7a7)

- Upload all the necessary resources to the S3 bucket.

![image](https://github.com/user-attachments/assets/98cba298-b111-4458-a692-a552f5e6765e)

- Configure the bucket for static website hosting.

**Steps:** Buckets -> Properties -> Static website hosting -> Use this bucket to host a website -> Static website hosting -> 

- Grant public read access to the bucket (adjust permissions based on security requirements of the project).

**Note:** I have unlocked public access from ACL.

![image](https://github.com/user-attachments/assets/33dc4a4a-f012-485a-85a7-4848505d4be1)
  
4. AWS CodePipeline Setup:
   
- Create a new CodePipeline.

![image](https://github.com/user-attachments/assets/01efc54c-a776-43d0-ac24-db8ad109ea15)

- Configure the source stage to point to your GitHub repository and main branch.

![image](https://github.com/user-attachments/assets/8b2be68c-f9e4-42a3-88ab-e4d37b0db9fe)

![image](https://github.com/user-attachments/assets/f610483b-5e89-47c7-9794-239cb12eac1c)

![image](https://github.com/user-attachments/assets/df2fa848-868c-40a6-a3bc-24684c809044)

- Configure the deploy stage to point to the S3 bucket.

![image](https://github.com/user-attachments/assets/eb928d04-e689-4725-9f70-7587f2c7171b)

5. Deployment and Testing:
   
- Push code changes to the GitHub repository.

![image](https://github.com/user-attachments/assets/961130b2-56b0-4a22-a248-62a1dd9aefd8)

- Monitor the CodePipeline for successful execution.
- Access the game in the S3 bucket's website endpoint.
- Test the game's functionality and performance.

**Note:** The updated application that is running in the AWS S3 Bucket after the commit in the main branch:

![image](https://github.com/user-attachments/assets/d02329e7-0aea-45d7-a16b-32f4346d4c21)
  
<h2> Operational Excellence </h2>

- Security: Implement appropriate S3 bucket permissions to control access to the game files. Consider using AWS Identity and Access Management (IAM) roles for fine-grained control.
- Reliability: Regularly test the CodePipeline to ensure reliable deployments. Implement error handling and notifications for pipeline failures.
- Performance Efficiency: Optimize game code for performance. Consider using content delivery networks (CDNs) for improved load times.
- Cost Optimization: Analyze S3 storage and transfer costs. Implement lifecycle policies to manage object expiration. Explore S3 Intelligent-Tiering for cost-effective storage.
- Sustainability: Consider using renewable energy options for AWS resources. Optimize game code for energy efficiency.

<h2> Conclusion </h2>

Deploying a simple game like meme matching to AWS S3 using CodePipeline offers a rapid and cost-effective solution. By following the outlined steps and considering the operational excellence factors, you can create a reliable and scalable game deployment process.
