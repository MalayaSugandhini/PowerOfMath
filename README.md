# 📌 Power of Math Project

## 🎯 Overview
This project is a simple web application that calculates the power of a given base number raised to an exponent. The backend is powered by AWS services, including **AWS Lambda**, **DynamoDB**, and **API Gateway**, while the frontend is built with **HTML, JavaScript, and CSS**.

---

## 🛠️ Tech Stack
- **Frontend:** HTML, CSS, JavaScript
- **Backend:** Python (AWS Lambda)
- **Database:** AWS DynamoDB
- **API Management:** AWS API Gateway
- **Hosting:** AWS Amplify 

---

## 🚀 Step-by-Step Setup Guide

### **1️⃣ Set Up AWS Amplify**
📌 **Amplify is used for hosting the frontend (index.html).**

1. Go to the **[AWS Amplify Console](https://console.aws.amazon.com/amplify)**
2. Click **"New App" → "Host a Web App"**
3. Connect your **GitHub Repository** (PowerOfMath)
4. Click **Next** → Configure Build Settings  
5. Deploy the frontend site
6. Get the **Amplify URL** (e.g., `https://yourproject.amplifyapp.com`)

---

### **2️⃣ Create an AWS Lambda Function**
📌 **This function will compute the power of numbers.**

1. Go to the **[AWS Lambda Console](https://console.aws.amazon.com/lambda)**
2. Click **"Create Function"**
3. **Function name:** `PowerCalculationFunction`
4. **Runtime:** Python 3.x
5. Click **"Create Function"**
6. Replace the default code with the power calculation logic.
7. **Deploy**

---

# 📌 Power of Math Project - Deployment Guide

## 3️⃣ Create an API Gateway
📌 **API Gateway allows your frontend to communicate with Lambda.**

1. Go to the **[API Gateway Console](https://console.aws.amazon.com/apigateway)**
2. Click **"Create API"** → Choose **"HTTP API"**
3. Click **"Add Integration"** → Select **"Lambda Function"**
4. Choose **PowerCalculationFunction**
5. Click **"Next"** → Deploy API
6. **Copy the Invoke URL** (e.g., `https://xyz.execute-api.us-east-1.amazonaws.com/dev`)

---

## 4️⃣ Create a DynamoDB Table
📌 **DynamoDB stores the calculations.**

1. Go to the **[DynamoDB Console](https://console.aws.amazon.com/dynamodb)**
2. Click **"Create Table"**
3. **Table name:** `PowerOfMathTable`
4. **Primary Key:** `ID` (String)
5. Click **"Create Table"**

---

## 5️⃣ Attach IAM Permissions to Lambda
📌 **IAM allows Lambda to write to DynamoDB.**

1. Go to the **[IAM Console](https://console.aws.amazon.com/iam)**
2. Click **Roles** → Find your Lambda function role
3. Click **Attach Policies** → Search for `"AmazonDynamoDBFullAccess"`
4. Click **Attach Policy**

---

## 6️⃣ Update AWS Lambda to Store Data in DynamoDB
📌 **Modify Lambda to save calculations in DynamoDB.**

1. Open your Lambda function (`PowerCalculationFunction`)
2. Replace the existing function with one that stores data in DynamoDB.
3. **Deploy**

---

## 7️⃣ Connect Frontend to API Gateway
📌 **Modify your `index.html` to use the API Gateway URL.**

1. Open `index.html`
2. Replace the fetch URL with your API Gateway Invoke URL.
3. Save and reload the page.

---

## 🌎 Running Locally
1. Clone the project:

```sh
git clone https://github.com/YOUR_GITHUB_USERNAME/PowerOfMath.git
cd PowerOfMath
