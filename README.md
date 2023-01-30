# AWS Microservice Demo

This microservice architecture demo is built on the AWS platform, using Lambda (Python), Dynamo DB and API Gateway.

Highly flexible, reliable and scalable microservice architecture using AWS Lambda, Dynamo DB, and API Gateway. 

This demo will demonstrate how to use Microservice architecture components together to create a robust solution while minimizing complexity.

## Step 1: Creating a role for Lambda function with read only permissions to DynamoDB

### Use the below policy for the role

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

## Step 2: Creating Lambda function using the Python 3.7 runtime.

### Use the below code

```

from __future__ import print_function

import boto3
import json

print('Loading function')


def lambda_handler(event, context):
    '''Provide an event that contains the following keys:

      - operation: one of the operations in the operations dict below
      - tableName: required for operations that interact with DynamoDB
      - payload: a parameter to pass to the operation being performed
    '''
    #print("Received event: " + json.dumps(event, indent=2))

    operation = event['operation']

    if 'tableName' in event:
        dynamo = boto3.resource('dynamodb').Table(event['tableName'])

    operations = {
        'create': lambda x: dynamo.put_item(**x),
        'read': lambda x: dynamo.get_item(**x),
        'update': lambda x: dynamo.update_item(**x),
        'delete': lambda x: dynamo.delete_item(**x),
        'list': lambda x: dynamo.scan(**x),
        'echo': lambda x: x,
        'ping': lambda x: 'pong'
    }

    if operation in operations:
        return operations[operation](event.get('payload'))
    else:
        raise ValueError('Unrecognized operation "{}"'.format(operation))

```        

## Step 3: Create a DynamoDB table
## Step 4: Create API Gateway
## Step 5: Deploy and Test the API
