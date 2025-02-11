# 📌 Power of Math Project

## 🎯 Overview
This project is a simple web application that calculates the power of a given base number raised to an exponent. The backend is powered by AWS services, including **AWS Lambda**, **DynamoDB**, and **API Gateway**, while the frontend is built with **HTML, JavaScript, and CSS**.

## 🛠️ Tech Stack
- **Frontend:** HTML, CSS, JavaScript
- **Backend:** Python (AWS Lambda)
- **Database:** AWS DynamoDB
- **API Management:** AWS API Gateway
- **Hosting:** AWS Amplify (Optional)

## ⚡ Features
- ✅ Take user input for base and exponent values  
- ✅ Compute the power using an AWS Lambda function  
- ✅ Store and retrieve results from DynamoDB  
- ✅ Display results in a web-based interface  
- ✅ Hosted via AWS Amplify (Optional)  

---

## 🚀 How to Set Up AWS Services
Follow these steps to deploy this project on AWS.

### **1️⃣ Create an AWS Lambda Function**
1. Go to the [AWS Lambda Console](https://console.aws.amazon.com/lambda/)
2. Click **Create Function** → Choose **Author from scratch**
3. Enter **Function name:** `PowerCalculationFunction`
4. Select **Runtime:** `Python 3.x`
5. Click **Create Function**
6. Replace the function code with:

### **🔹 Lambda Code Before Adding DynamoDB**
```python
import json
import math

def lambda_handler(event, context):
    base = int(event["base"])
    exponent = int(event["exponent"])
    result = math.pow(base, exponent)
    return {
        'statusCode': 200,
        'body': json.dumps(f'Your result is {result}')
    }
