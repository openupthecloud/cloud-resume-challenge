

```yml
  MyRoute53Record:
    Type: "AWS::Route53::RecordSetGroup"
    Properties:
      HostedZoneId: Z06245993R6DDL18APSF6 # TODO: Don't hardcode me
      RecordSets:
        - Name: website.cmcloudlab515.info # TODO: Don't hardcode me
          Type: A
          AliasTarget:
            HostedZoneId: Z2FDTNDATAQYW2
            DNSName: !GetAtt MyDistribution.DomainName
```
