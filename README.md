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

---

## 🏗️ Project Layout
The following diagram represents the complete application flow:  

![Project Layout](images/screenshot00.png)

---

## 🚀 Implementation Steps

### 1. Create DynamoDB Table
- Open the **DynamoDB Console** and select **Create Table**.  
- Table name: `student-data`  
- Partition key: `studentID` (String).  

![DynamoDB Console](images/screenshot1.png)  
![Create DynamoDB Table](images/screenshot2.png)

---

### 2. Create IAM Role for Lambda
- Navigate to **IAM → Roles → Create Role**.  
- Select **AWS Service → Lambda** as trusted entity.  
- Attach the **AmazonDynamoDBFullAccess** policy.  
- Name the role `Lambda-DynamoDB-Access` and create it.  

![IAM Console](images/screenshot3.png)  
![Select Lambda Service](images/screenshot4.png)  
![Attach DynamoDB Policy](images/screenshot5.png)

---

### 3. Create Lambda Functions
We need two Lambda functions:  
- **POST Lambda** → Inserts student data into DynamoDB.  
- **GET Lambda** → Retrieves student data from DynamoDB.  

Steps:  
- Go to **Lambda Console → Create Function**.  
- Choose runtime: **Python 3.x**.  
- Assign the IAM role created earlier.  
- Write code for POST and GET separately.  
- Deploy and test with sample payloads.  

![Lambda Console](images/screenshot6.png)  
![Create POST Lambda](images/screenshot7.png)  
![Assign IAM Role](images/screenshot8.png)  
![Insert POST Lambda Code](images/screenshot9.png)  
![Test POST Lambda](images/screenshot10.png)

---

### 4. Configure API Gateway
- Open **API Gateway Console** → **Create API**.  
- Add two methods:  
  - **POST** → linked to POST Lambda.  
  - **GET** → linked to GET Lambda.  
- Deploy the API to a stage (e.g., `production`).  
- Copy the **Invoke URL**.  

![API Gateway Console](images/screenshot11.png)  
![Create New API](images/screenshot12.png)  
![Add POST Method](images/screenshot13.png)  
![Add GET Method](images/screenshot14.png)  
![Invoke URL](images/screenshot15.png)

---

### 5. Host Web Content on S3
- Create a new **S3 bucket**.  
- Uncheck “Block all public access”.  
- Enable **Static Website Hosting**.  
- Upload `index.html`, `error.html`, and other web files.  
- Note down the S3 Website Endpoint.  

![Create S3 Bucket](images/screenshot16.png)  
![Upload Files](images/screenshot17.png)  
![Enable Static Hosting](images/screenshot18.png)  
![S3 Website Endpoint](images/screenshot19.png)

---

### 6. Configure S3 Bucket Policy
- Go to **Permissions → Bucket Policy**.  
- Use the AWS Policy Generator to create a policy.  
- Allow `s3:GetObject` for `*` on the bucket ARN.  
- Apply the policy to make files publicly readable.  

![Open Bucket Policy](images/screenshot20.png)  
![Policy Generator](images/screenshot21.png)  
![Apply Policy](images/screenshot22.png)

---

### 7. Connect Frontend to Backend
- Edit your `index.html` file.  
- Replace the placeholder API URLs with the **API Gateway Invoke URL**.  
- Upload updated files to S3.  

![Update HTML](images/screenshot23.png)  
![Upload Updated Files](images/screenshot24.png)  
![Confirm API Connection](images/screenshot25.png)

---

### 8. Test the Application
- Open the **S3 Website Endpoint** in your browser.  
- Enter student details and submit the form (POST request).  
- Check **DynamoDB** to confirm data insertion.  
- Retrieve student data via GET request to verify retrieval.  

![Open S3 Website](images/screenshot26.png)  
![Enter Student Data](images/screenshot27.png)  
![Submit Form](images/screenshot28.png)  
![Lambda Processes Data](images/screenshot29.png)  
![Check DynamoDB Records](images/screenshot30.png)  
![Execute GET Request](images/screenshot31.png)  
![Data Displayed](images/screenshot32.png)

---

### 9. Secure Website with CloudFront
- Go to **CloudFront Console → Create Distribution**.  
- Choose your **S3 bucket** as the origin.  
- Enable **Redirect HTTP to HTTPS**.  
- Copy the CloudFront distribution domain.  
- Now your app is served securely via HTTPS with low latency.  

![CloudFront Console](images/screenshot33.png)  
![Create Distribution](images/screenshot34.png)  
![Select S3 as Origin](images/screenshot35.png)  
![CloudFront Settings](images/screenshot36.png)  
![Deploy Distribution](images/screenshot37.png)  
![CloudFront Domain URL](images/screenshot38.png)  
![Access via CloudFront](images/screenshot39.png)

---

### 🔒 Final Verification
- Compare **S3 Endpoint (HTTP)** and **CloudFront URL (HTTPS)**.  
- Ensure both index and error pages are working.  

![Compare URLs](images/screenshot40.png)  
![S3 Endpoint](images/screenshot41.png)  
![CloudFront Endpoint](images/screenshot42.png)

---

## 🔗 Final URLs
- **CloudFront Secure URL**: `https://<your-distribution-id>.cloudfront.net/`  
- **S3 Website URL**: `http://<your-bucket-name>.s3-website.<region>.amazonaws.com/`

---

## 🎯 Benefits
- **Serverless architecture** → No servers to manage.  
- **Scalable**
