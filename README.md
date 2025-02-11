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

Deploy
3️⃣ Create an API Gateway
📌 API Gateway allows your frontend to communicate with Lambda.

Go to the API Gateway Console
Click "Create API" → Choose "HTTP API"
Click "Add Integration" → Select "Lambda Function"
Choose PowerCalculationFunction
Click "Next" → Deploy API
Copy the Invoke URL (e.g., https://xyz.execute-api.us-east-1.amazonaws.com/dev)
4️⃣ Create a DynamoDB Table
📌 DynamoDB stores the calculations.

Go to the DynamoDB Console
Click "Create Table"
Table name: PowerOfMathTable
Primary Key: ID (String)
Click "Create Table"
5️⃣ Attach IAM Permissions to Lambda
📌 IAM allows Lambda to write to DynamoDB.

Go to the IAM Console
Click Roles → Find your Lambda function role
Click Attach Policies → Search for "AmazonDynamoDBFullAccess"
Click Attach Policy
6️⃣ Update AWS Lambda to Store Data in DynamoDB
📌 Modify Lambda to save calculations in DynamoDB.

Open your Lambda function (PowerCalculationFunction)
Replace the code with:
python
Copy
Edit
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
Deploy
7️⃣ Connect Frontend to API Gateway
📌 Modify your index.html to use the API Gateway URL.

Open index.html
Replace the fetch URL with your API Gateway Invoke URL:
javascript
Copy
Edit
fetch("https://YOUR_API_GATEWAY_URL/dev", requestOptions);
Save and reload the page.
🌎 Running Locally
📌 Clone the project and run it on your local machine.

sh
Copy
Edit
git clone https://github.com/YOUR_GITHUB_USERNAME/PowerOfMath.git
cd PowerOfMath
open index.html
✅ Testing Your Project
Open your Amplify website (if hosted)
Enter numbers and click "Calculate"
Open DynamoDB Table → Check if results are stored
Open API Gateway Logs → Check if API is being called
💡 Future Enhancements
✅ Add a history feature to view past calculations
✅ Improve UI/UX for a better experience
✅ Deploy with AWS Amplify for public access

❌ Deleting AWS Resources (To Avoid Charges)
📌 If you don’t want to be charged for AWS services, delete these resources:

DynamoDB Table: PowerOfMathTable
Lambda Function: PowerCalculationFunction
API Gateway: PowerOfMathAPI
**Amplify App (if hosted)`
📜 License
This project is licensed under the MIT License.
Feel free to use and modify it! 🚀

📢 Questions?
For issues, open a GitHub issue or reach out! 🚀

vbnet
Copy
Edit

✅ **Now, you can copy and paste this into your `README.md` file on GitHub.**  
Let me know if you need any modifications! 🚀

