# AWS SAM Project

![Alt text](assets/images/architecture.png?raw=true "Architecture")

This project contains source code and supporting files for a basic CRUD serverless application that you can deploy with the AWS Serverless Application Model (AWS SAM) command line interface (CLI). It includes the following files and folders:

- `src` - Code for the application's Lambda function.
- `events` - Invocation events that you can use to invoke the function.
- `__tests__` - Unit tests for the application code.
- `template.yaml` - A template that defines the application's AWS resources.

The application uses several AWS resources, including Lambda functions, an API Gateway API, and Amazon DynamoDB tables. These resources are defined in the `template.yaml` file in this project. You can update the template to add AWS resources through the same deployment process that updates your application code.

The application also uses AWS Cognito as the authorizer for API Gateway, therby restricting unauthorized access to the Lambda functions. Only Authenticated users will be able to invoke the API Gateway Rest APis.

## How to Generate Users and User token using Cognito CLI

- Register a user : [Cognito IDP signup documentation](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/sign-up.html)
- Confirm user registration: [Confirm Signup](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/admin-confirm-sign-up.html)
- Authenticate : [Initate auth](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/admin-initiate-auth.html)

## Deploy the sample application

The AWS SAM CLI is an extension of the AWS CLI that adds functionality for building and testing Lambda applications. It uses Docker to run your functions in an Amazon Linux environment that matches Lambda. It can also emulate your application's build environment and API.

To use the AWS SAM CLI, you need the following tools:

- AWS SAM CLI - [Install the AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html).
- Node.js - [Install Node.js 18](https://nodejs.org/en/), including the npm package management tool.
- Docker - [Install Docker community edition](https://hub.docker.com/search/?type=edition&offering=community).

To build and deploy your application for the first time, run the following in your shell:

```bash
sam build
sam deploy --guided
```

## AWS SAM Pipeline

The application has also been configured with the SAM pipeline using AWS Code pipeline. You can choose other CI/CD systems of your choice. In this project I have configured it using the AWS Code pipeline CI/CD system.

- sam pipeline init --bootstrap
- Commit pipeline changes to git repo
- Connect Git repo with CI/CD system sam deploy -t codepipeline.yaml --stack-name <pipeline-stack-name> --capabilities=CAPABILITY_IAM
- If you are using GitHub or Bitbucket, after running the sam deploy command previously, complete the connection by following the steps under To complete a connection found on the Update a pending connection topic in the Developer Tools console user guide. In addition, store a copy of the CodeStarConnectionArn from the output of the sam deploy command, because you will need it if you want to use AWS CodePipeline with another branch than main.

## Resources

For an introduction to the AWS SAM specification, the AWS SAM CLI, and serverless application concepts, see the [AWS SAM Developer Guide](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-sam.html).

For AWS SAM pipeline using AWS Codepipeline as the CI/CD system, see the [Generating starter pipeline for AWS CodePipeline in AWS SAM](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-generating-example-ci-cd-codepipeline.html)

For Cognito IDP, see the [Cognito IDP Documentation](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/)
