# Project Tarius: AWS Serverlsss Real Time Data Load to DynamoDB

The user / producer uploads a csv source file to the landing zone S3 bucket. A Lambda function is triggered using S3 event notification and loads it to a DynamoDB table. The entire stack is created using AWS SAM template. The SNS, S3 Bucket and DynamoDB tables are encrypted using Customer Managed KMS Key.

## Description

This sample project demonstrate the capability of loading a .csv file into a DynamoDB table using a Lambda function. The Lambda function is triggered using an Event Source Notification created in the S3 bucket. Once the data loads successfully into the table a SNS notification is published and end users are notified via email subscriibed to the SNS Topic. CloudWatch Alarms are created to demonstrate the different metrics on the Lambda function. The S3 Bucket, SNS Topic and the DynamoDB tables are encrypted using Customer Managed KMS Key. The entire stack (excluding the KMS Key is created using AWS SAM - Serverless Application Model).

![Project Tauris - Design Diagram](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0001-tarius/tarius-architecture-diagram.png)

![Project Tauris - Services Used](https://subhamay-projects-repository-us-east-1.s3.amazonaws.com/0001-tarius/tarius-services-used-sam.png)

## Getting Started

### Dependencies

* Create a Customer Managed KMS Key in the region where you want to create the stack..
* Modify the KMS Key Policy to let the IAM user encrypt / decrypt using any resource using the created KMS Key.
* Setup AWS CLI with an user having appropriate access to create the required resources.

### Installing

* Clone the repository https://github.com/subhamay-cloudworks/0001-tarius-cft (the nested and cross stacks are available in this repo).
* Create a S3 bucket for code repository.
* Create the folders - tarius/cft/nested-stacks, tarius/cft/cross-stacks, tarius/code
* Upload the following YAML templates to tarius/cft/nested-stacks
    * cloudwatch-stack.yaml
    * dynamodb-stack.yaml
    * iam-role-stack.yaml
    * s3-stack.yaml
    * sns-stack.yaml
    * sqs-stack.yaml
* Upload the following YAML templates to tarius/cft/cross-stacks
    * custom-resource-lambda-stack.yaml
* Upload the following YAML templates to tarius/cft/
    * tarius-root-stack.yaml
* Zip and Upload the Python file  to tarius/cft/code
* Create the cross-stack using the template custom-resource-lambda-stack.yaml by using the S3 url and pass the appropriate parameters.
* Create the entire stack in two steps.
    * sam build
    * sam deploy --guided --capabilities "CAPABILITY_NAMED_IAM"
### Executing program

* Upload the sample products.csv file to the landing zone folder of the S3 bucket either using S3 console or CLI
* Step-by-step bullets
```
aws s3 cp products.csv <s3 bucket uri>/data/
```

## Help

Post message in my blog (https://subhamay.blog)


## Authors

Contributors names and contact info

Subhamay Bhattacharyya  - [subhamoyb@yahoo.com](https://subhamay.blog)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under Subhamay Bhattacharyya. All Rights Reserved.

## Acknowledgments

Inspiration, code snippets, etc.
* [Stephane Maarek ](https://www.linkedin.com/in/stephanemaarek/)
* [Neal Davis](https://www.linkedin.com/in/nealkdavis/)
* [Adrian Cantrill](https://www.linkedin.com/in/adriancantrill/)
