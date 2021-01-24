
## Setting up S3

- What is S3?
- What is AWS SAM?
    - Will create us an AWS Lambda (but we can ignore for now)
- Setup the SAM CLI (https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-command-reference.html)
    - `sam init`
    - `sam build`
- Add IAM permissions for SAM
    - CloudFormation
    - IAM
    - Lambda
    - API Gateway
- Deploy SAM
    - `aws-vault exec my-user --no-session -- sam deploy --guided`
- Add S3
    - https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket.html
    - `aws-vault exec my-user -- aws s3 ls`

```
  MyWebsite:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: my-fantastic-website
```
