# AWS Microservice Demo

This microservice architecture demo is built on the AWS platform, using Lambda (Python), Dynamo DB and API Gateway.

Highly flexible, reliable and scalable microservice architecture using AWS Lambda, Dynamo DB, and API Gateway. 

This demo will demonstrate how to use Microservice architecture components together to create a robust solution while minimizing complexity.

## Step 1: Creating a role for Lambda function with read only permissions to DynamoDB

#### Use the below policy for the role

```

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "lambda:InvokeFunction"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "dynamodb:DescribeStream",
                "dynamodb:GetRecords",
                "dynamodb:GetShardIterator",
                "dynamodb:ListStreams"
            ],
            "Resource": "*"
        }
    ]
}

```

## Step 2: Creating Lambda function usin Python runtime.
## Step 3: 
