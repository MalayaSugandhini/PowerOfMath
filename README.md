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
---
