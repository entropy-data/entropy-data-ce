# AWS CloudFormation Template

The cloud formation template for the AWS infrastructure is available in `template.yaml` and in a public S3 bucket: https://entropy-data-ce.s3.us-east-1.amazonaws.com/template.yaml.

It uses the Docker Image hosted on AWS Public ECR: `public.ecr.aws/s4e5k7s9/entropy-data-ce:latest` (see more on https://gallery.ecr.aws/s4e5k7s9/entropy-data-ce).

[Quick-Create Link](https://eu-central-1.console.aws.amazon.com/cloudformation/home?region=eu-central-1#/stacks/create/review?templateURL=https://entropy-data-ce.s3.us-east-1.amazonaws.com/template.yaml)

## Constraints

Using a public image from Docker Hub in AWS AppRunner comes with many constraints on AWS.

- AppRunner does not support public images from Docker Hub, only from ECR Public.
- AppRunner does not support automated deployment from images on ECR Public.

The alternative requires a private ECR repository, which either gets the image pushed or configures a pull-through cache.
The pull-through cache always requires credentials configured in the AWS Secrets Manager, even for public docker images on Docker Hub.

Because of that, the CloudFormation template uses `public.ecr.aws/s4e5k7s9/entropy-data-ce:latest` from ECR Public. But be aware that it does not automatically upgrade to newer versions of the Entropy Data!

## Running the CloudFormation Template from CLI

```
aws cloudformation create-stack \
  --stack-name entropy-data \
  --template-body file://./template.yaml \
  --parameters \
    ParameterKey=ImageIdentifier,ParameterValue=public.ecr.aws/s4e5k7s9/entropy-data-ce:latest \
    ParameterKey=DBInstanceIdentifier,ParameterValue=entropy-data-postgres \
    ParameterKey=DBName,ParameterValue=postgres \
    ParameterKey=SuperAdmins,ParameterValue= \
    ParameterKey=SMTPHost,ParameterValue=email-smtp.eu-central-1.amazonaws.com \
    ParameterKey=SMTPPort,ParameterValue=587 \
    ParameterKey=SMTPUsername,ParameterValue=xxx \
    ParameterKey=SMTPPassword,ParameterValue=xxx \
    ParameterKey=MailFrom,ParameterValue=support@example.com \  
  --region eu-central-1
```

## Testing the CloudFormation Template

This is done automatically via GitHub Actions to ensure that the cloud formation template still works.


### Running Taskcat

```bash
# requires AWS credentials via environment variables
uvx taskcat test run
```
