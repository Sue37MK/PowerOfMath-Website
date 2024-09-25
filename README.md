![Alt text](ArchitectDiagram.png)

---
# AWS Web Application Project

## Project Overview
This project demonstrates an end-to-end web application built using five different AWS services: Amplify, Lambda, IAM, API Gateway, and DynamoDB. The application performs basic math operations and stores the results in DynamoDB.

## Services Used
1. **AWS Amplify**: Hosts the frontend (HTML page).
2. **AWS Lambda**: Executes backend logic to perform math operations.
3. **AWS IAM**: Provides the necessary permissions for Lambda to interact with DynamoDB.
4. **API Gateway**: Acts as a RESTful interface to invoke Lambda functions.
5. **DynamoDB**: Stores the results of the math operations.

## Project Setup and Workflow

### 1. Host Webpage on AWS Amplify
- Create an `index.html` file for the web application’s frontend. Please refer to index-Original.html for code.
- Use AWS Amplify to host the webpage.

  ![Alt text](Amplify-app.png)
  ![Alt text](Appdeploy.png)
  
- Ensure that the Amplify service successfully deploys the page and check the URL to confirm the webpage is live and functional.
  ![Alt text](Webapp1.png)
  
### 2. Create Lambda Function for Math Operations
- Create an AWS Lambda function to perform basic math (e.g., addition, subtraction, multiplication).
  ![Alt text](Lamdafuction1.png)
- Test the Lambda function by creating a test event in the Lambda console to ensure the math logic is correctly implemented.
   ![Alt text](Lamdatestevent.png)
   ![Alt text](LamdaTest.png)
  
### 3. Use API Gateway to Invoke Lambda
- Set up a REST API in AWS API Gateway to trigger the Lambda function.
   ![Alt text](RestAPI.png)
- Use the **POST** method and enable **CORS** to allow the frontend to make requests to the API.
  ![Alt text](APImethod.png)
  ![Alt text](APIMethod1.png)
  ![Alt text](PostMethod.png)
  ![Alt text](EnableCORS.png)
  ![Alt text](EnbleCORS.png)
   ![Alt text](CORS.png)
  
- Test the API Gateway by invoking the Lambda function through it.
  ![Alt text](TestAPI.png)

### 4. Store Math Results in DynamoDB
- Create a DynamoDB table with a partition key (e.g., `ID`) to store the math results.
  ![Alt text](Dynamodbtable.png)
  ![Alt text](DBTable.png)
- Design the table to store operation results with a unique identifier.
  ![Alt text](Savedata.png)

### 5. Grant Lambda Permission to Access DynamoDB
- Assign a JSON policy to the Lambda function’s execution role to allow it to write results to DynamoDB.
  ![Alt text](Executionrole.png)
- Attach below policy to the Lambda execution role in AWS IAM.
```json
{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "YOUR-TABLE-ARN"
    }
    ]
}
  ```
![Alt text](PermissionPolicy.png)
![Alt text](Policy.png)

### 6. Update Lambda Function to Save Results in DynamoDB
- Modify the Lambda function code to save the results of the math operation in DynamoDB.
- Please refer to file name PowerOfMathFuction-Lamda-Final.txt for code.
  
- Re-test the function and verify that the results are stored correctly in the DynamoDB table.
  ![Alt text](LamdaTestresult.png)

### 7. Update Frontend (index.html)
- Edit the `index.html` file to include CSS styles for improved user interface.
- Add an input field where users can type the numbers for the math operation.
- Implement a script to invoke the API Gateway from the frontend, making a request to the Lambda function to perform the operation and return the result.
- Please refer to file name index.html for code.

  
## Running the Project

1. **Deploy the Webpage**:
   - Use AWS Amplify to host your `index.html` page and get the live URL.
2. **Test the Lambda Function**:
   - Test the Lambda function locally using the Lambda console or AWS CLI.
3. **Test the API Gateway**:
   - Use a REST client (e.g., Postman) to invoke the API Gateway and ensure it triggers the Lambda function correctly.
4. **Check DynamoDB Results**:
   - Verify that the math results are saved in DynamoDB.
   
![Alt text](PowerofMathWeb.png)

## Conclusion
This project showcases how to integrate AWS services like Amplify, Lambda, API Gateway, IAM, and DynamoDB to build a functional web application from scratch. The application performs basic math operations, stores the results in a NoSQL database, and presents an interactive UI hosted on AWS.

