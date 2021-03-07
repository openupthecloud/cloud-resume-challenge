
# Push to S3

- Update our bucket to be a website
- Allow public access
- Deploy an index.html to our bucket

## Set your S3 bucket as a website

```bash
sam build && aws-vault exec my-user --no-session -- sam deploy
```

```yaml
  MyWebsite:
    Type: AWS::S3::Bucket
    Properties:
      AccessControl: PublicRead
      WebsiteConfiguration:
        IndexDocument: index.html
      BucketName: my-fantastic-website

  BucketPolicy:
    Type: AWS::S3::BucketPolicy
    Properties:
      PolicyDocument:
        Id: MyPolicy
        Version: 2012-10-17
        Statement:
          - Sid: PublicReadForGetBucketObjects
            Effect: Allow
            Principal: "*"
            Action: "s3:GetObject"
            Resource: !Join
              - ""
              - - "arn:aws:s3:::"
                - !Ref MyWebsite
                - /*
      Bucket: !Ref MyWebsite
```

## Update the Makefile

```makefile
.PHONY: build

build:
	sam build

deploy-infra:
	sam build && aws-vault exec my-user --no-session -- sam deploy

deploy-site:
	aws-vault exec my-user --no-session -- aws s3 sync ./resume-site s3://my-fantastic-website
```

## Upload an index.html

```
make deploy-site
```

## Add CSS

```html
<head>
    <style>
        p {
            color: red;
        }
    </style>
</head>
```
