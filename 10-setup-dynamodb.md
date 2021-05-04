
## Dynamo

- NoSQL DB
- Dynamo is good for high availability
- Simple to get started with, but deceptive!
- Mastering DDB is an art
- https://www.dynamodbbook.com/ (Alex Debrie)
- Rick Houlihan AWS Re:Invent

```yaml
  DynamoDBTable:
    Type: AWS::DynamoDB::Table
    Properties:
      TableName: cloud-resume-challenge
      BillingMode: PAY_PER_REQUEST
      AttributeDefinitions:
        - AttributeName: "ID"
          AttributeType: "S"
      KeySchema:
        - AttributeName: "ID"
          KeyType: "HASH"
```
