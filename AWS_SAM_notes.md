# AWS SAM Notes

SAM provides a shorthand syntax to express functions, APIs, databases, and event source mappings. And, it will have `Transform` header that indicates it's a SAM template.

## Installing AWS SAM

- Need permissions to call AWS services.
- To test this locally, you need to install the Docker containers for SAM.
- You must install AWS SAM CLI first before you can proceed.

## How It Works

1. SAM pushes your code/yaml to S3.
2. It then transforms them into a Lambda function/DynamoDB/API Gateway based on the instructions of the YAML file. Similar to CloudFormation.

## Commands

You run `sam package` and `sam deploy` to run the package and deploy using AWS SAM.

**Note: The template must be a YAML formatted document even with the aws cloudformation CLI commands.
**
