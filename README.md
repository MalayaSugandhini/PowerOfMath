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
6. Replace the default code with:

```python
import json
import math

def lambda_handler(event, context):
    base = int(event["base"])
    exponent = int(event["exponent"])
    result = math.pow(base, exponent)

    return {
        'statusCode': 200,
        'body': json.dumps({'result': result})
    }

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
2. Replace the code with:

```python
import json
import math
import boto3
import uuid
from time import gmtime, strftime

# Initialize DynamoDB
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('PowerOfMathTable')

def lambda_handler(event, context):
    base = int(event["base"])
    exponent = int(event["exponent"])
    result = math.pow(base, exponent)
    calculation_id = str(uuid.uuid4())
    now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())

    # Store result in DynamoDB
    table.put_item(
        Item={
            'ID': calculation_id,
            'base': base,
            'exponent': exponent,
            'result': result,
            'timestamp': now
        }
    )

    return {
        'statusCode': 200,
        'body': json.dumps({'ID': calculation_id, 'result': result})
    }
