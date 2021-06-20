.PHONY: build

build:
	sam build

deploy-infra:
	HOSTED_ZONE=$$(aws-vault exec acloudguru-sandbox --no-session -- aws route53 list-hosted-zones | jq .HostedZones[0].Id | cut -d "\"" -f 2 | cut -d "/" -f3); \
    DOMAIN_NAME=$$(aws-vault exec acloudguru-sandbox --no-session -- \
		aws route53 list-resource-record-sets \
				--hosted-zone $$HOSTED_ZONE | \
				jq '.ResourceRecordSets[] | select(.Type == "NS") | .Name ' | \
				cut -d "\"" -f2 \
				| sed 's/.$$//'); \
	make build; \
	aws-vault exec acloudguru-sandbox --no-session -- \
		sam deploy \
			--no-confirm-changeset \
			--parameter-overrides HostedZoneParameter=$$HOSTED_ZONE DomainNameParameter=$$DOMAIN_NAME

deploy-site:
	aws-vault exec acloudguru-sandbox --no-session -- aws s3 sync ./resume-site s3://open-up-the-cloud-website

hostedzone:
	aws-vault exec acloudguru-sandbox --no-session -- aws route53 list-hosted-zones | jq .HostedZones[0].Id | cut -d "\"" -f 2 | cut -d "/" -f3

invoke-get:
	sam build && aws-vault exec acloudguru-sandbox --no-session -- sam local invoke GetFunction

invoke-put:
	sam build && aws-vault exec acloudguru-sandbox --no-session -- sam local invoke PutFunction
