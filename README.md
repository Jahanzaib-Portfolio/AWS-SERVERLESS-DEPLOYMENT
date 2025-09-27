# ☁️ AWS Serverless Web Application

## 📖 Project Overview
This project demonstrates how to build and deploy a **serverless web application** on AWS.  
The architecture includes the following components:  
- **Amazon S3** for static website hosting  
- **Amazon API Gateway** for exposing RESTful APIs  
- **AWS Lambda** for serverless compute functions  
- **Amazon DynamoDB** for NoSQL database storage  
- **AWS IAM** for access control  
- **Amazon CloudFront** for secure, low-latency content delivery  
# ☁️ AWS Serverless Web Application


---

## 🏗️ Project Layout
![Project Layout](images/screenshot00.png)

---

## 1️⃣ Create DynamoDB
- Create a DynamoDB table.  
- Table name: `student-data`.  

![DynamoDB Table](images/screenshot1.png)

---

## 2️⃣ Create IAM Role
Since we need an IAM role assigned to Lambda functions to access DynamoDB, we will create an IAM role.  

Steps:  
1. Go to **Identity and Access Management (IAM)**.  
2. Click **Create Role**.  

![IAM Console](images/screenshot2.png)  
![Create Role](images/screenshot3.png)  
![IAM Role Setup](images/screenshot4.png)

- Select the service for which we are creating the role. In this case, select **Lambda function**.  

![Select Lambda Service](images/screenshot5.png)

- Add permission to access DynamoDB.  

![Attach DynamoDB Permission](images/screenshot6.png)

- Name the role and click **Create**.  

![Role Created](images/screenshot7.png)

---

## 3️⃣ Create Lambda Functions
We will create two Lambda functions:  
- First → to POST data to DynamoDB  
- Second → to GET data from DynamoDB  

### First Lambda Function (POST)
- Select the IAM role created earlier.  

![Lambda Console](images/screenshot8.png)  
![Select IAM Role](images/screenshot9.png)

- Delete the default code and paste your Lambda code.  

![Insert POST Code](images/screenshot10.png)

### Second Lambda Function (GET)
- Create another Lambda function.  
- Keep everything the same.  

![Create GET Lambda](images/screenshot11.png)  
![Paste GET Code](images/screenshot12.png)  

- Paste the GET Lambda code here.  

![Insert GET Code](images/screenshot13.png)

- Test the function to check if it works properly.  

![Test GET Lambda](images/screenshot14.png)

---

## 4️⃣ Configure API Gateway
Now go to API Gateway to connect the webpage with Lambda functions.  

![API Gateway Console](images/screenshot15.png)  
![Create API](images/screenshot16.png)

- Create two methods: one GET and one POST. Associate them with Lambda functions respectively.  

![Add Methods](images/screenshot17.png)  
![Associate Methods](images/screenshot18.png)  
![Save Methods](images/screenshot19.png)  
![Setup Completed](images/screenshot20.png)  
![Deploy API](images/screenshot21.png)  
![Production Stage](images/screenshot22.png)  
![Deployment Success](images/screenshot23.png)  
![Invoke URL](images/screenshot24.png)  
![Stage Info](images/screenshot25.png)  
![Copy Invoke URL](images/screenshot26.png)

- Give the stage a name (e.g., `production`).  

![Stage Setup](images/screenshot27.png)  
![Stage Deployment](images/screenshot28.png)

- Copy the Invoke URL and paste it into your webpage code that will be uploaded to the S3 bucket.  

![Invoke URL Copied](images/screenshot29.png)

---

## 5️⃣ Create S3 Bucket for Web Hosting
- Create an S3 bucket for web hosting.  

![Create S3 Bucket](images/screenshot30.png)  
![Bucket Created](images/screenshot31.png)

- Upload code into the S3 bucket.  

![Upload Code](images/screenshot32.png)

- Edit static website hosting settings in the S3 bucket to make it publicly accessible.  

![Static Website Hosting](images/screenshot33.png)  
![Hosting Enabled](images/screenshot34.png)

---

## 6️⃣ Create and Apply Bucket Policy
- Create a bucket policy using the Policy Generator.  

![Policy Generator](images/screenshot35.png)

- Copy the generated policy and paste it into the S3 bucket policy editor.  

![Paste Policy](images/screenshot36.png)

- If the bucket is not public, the policy will not be applicable and will give a conflict error. Change the bucket status to **Public**, then reapply the policy.  

Now our page is publicly accessible via S3 web hosting.  

![S3 Website Accessible](images/screenshot37.png)

---

## 7️⃣ API Gateway Triggers Lambda
API Gateway will trigger the Lambda function when requests are made from the webpage.  

---

## 8️⃣ Enter Data and Test Website
- Enter some data on the website and submit.  

![Enter Data](images/screenshot38.png)

- POST successful → now check if the data can be retrieved. Click **View All Students**.  

![POST Success](images/screenshot39.png)

- The posted data is successfully retrieved and displayed.  

---

## 9️⃣ Important Note — S3 Website Is Not Secure
- The website hosted by S3 is **not secure**.  
- URL Example:  
  `http://web-app-for-student-data.s3-website.eu-north-1.amazonaws.com/`  

Since the link uses **HTTP**, it is not secure.  
To make it secure, we will use **CloudFront**, which not only secures the website but also reduces latency.  

---

## 🔟 Create CloudFront Distribution
- Create a CloudFront distribution and add the S3 bucket URL.  

![CloudFront Console](images/screenshot40.png)

- Keep the remaining settings as default.  

![Default Settings](images/screenshot41.png)

- Once created, you will get a new domain name where the same content will be displayed securely.  

![CloudFront Domain](images/screenshot42.png)

### URLs:
- **CloudFront URL:** `https://d11g10oy7djsyh.cloudfront.net/`  
- **S3 Bucket URL:** `http://web-app-for-student-data.s3-website.eu-north-1.amazonaws.com/`

---

## 🎯 Benefits
- **Serverless architecture** → No servers to manage.  
- **Scalable** → Handles traffic spikes easily.  
- **Secure** → CloudFront HTTPS + IAM roles.  
- **Low-cost** → Pay only for what you use.  

---

## 🧠 Key Learnings
- Creating and configuring **DynamoDB tables**.  
- Assigning correct **IAM roles and permissions**.  
- Writing Lambda functions for **CRUD operations**.  
- Exposing Lambda via **API Gateway**.  
- Hosting a static site with **Amazon S3**.  
- Distributing content globally via **CloudFront**.  

---
