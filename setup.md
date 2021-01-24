
Consider: Using the ACloudGuru sandbox.

Setup your AWS account:

1. Create an AWS account (https://aws.amazon.com/resources/create-account/)
2. Setup MFA for your root account (https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable.html)
3. Create an IAM user (IAM)
    * Create new user
    * Assign permissions
4. Setup vault (https://github.com/99designs/aws-vault)
    * `aws-vault add my-user`
    * `aws-vault exec my-user -- aws s3 ls`
