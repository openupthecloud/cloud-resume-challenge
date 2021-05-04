
## Put into DynamoDB

1. You'll need to use AWS SDK
2. We'll write unit-tests later
3. Update makefile with local invoke
4. Docker installed for SAM local command
5. AWS credentials with exec (local permissions for Dynamo)
6. Need to give lambda permissions for Dynamo to be accessed

### Makefile updates

```shell
invoke-put:
	sam build && aws-vault exec acloudguru-sandbox --no-session -- sam local invoke PutFunction
```

### Policy updates

```yaml
    Policies:
      - DynamoDBCrudPolicy:
          TableName: cloud-resume-challenge
```
