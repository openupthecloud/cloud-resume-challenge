SHELL:=/bin/bash

.PHONY: build
.SILENT: integration-test

build:
	sam build

create-json-config:
	HOSTED_ZONE=$$(aws-vault exec acloudguru-sandbox --no-session -- aws route53 list-hosted-zones | jq .HostedZones[0].Id | cut -d "\"" -f 2 | cut -d "/" -f3); \
	DOMAIN_NAME=$$(aws-vault exec acloudguru-sandbox --no-session -- \
		aws route53 list-resource-record-sets \
				--hosted-zone $$HOSTED_ZONE | \
				jq '.ResourceRecordSets[] | select(.Type == "NS") | .Name ' | \
				cut -d "\"" -f2 \
				| sed 's/.$$//'); \
	echo "{ \"HOSTED_ZONE\": \"$$HOSTED_ZONE\", \"DOMAIN_NAME\": \"$$DOMAIN_NAME\"  }" > config.json

integration-test:
	DOMAIN_NAME=$$(cat config.json | jq .DOMAIN_NAME -r); \
	FIRST=$$(curl -s "https://api.$$DOMAIN_NAME/get" | jq ".count| tonumber"); \
	curl -s "https://api.$$DOMAIN_NAME/put"; \
	SECOND=$$(curl -s "https://api.$$DOMAIN_NAME/get" | jq ".count| tonumber"); \
	echo "Comparing if first count ($$FIRST) is less than (<) second count ($$SECOND)"; \
	if [[ $$FIRST -le $$SECOND ]]; then echo "PASS"; else echo "FAIL";  fi

end-to-end-test:
	node end-to-end-test/index.js

deploy-infra:
	HOSTED_ZONE=$$(cat config.json | jq .HOSTED_ZONE -r); \
	DOMAIN_NAME=$$(cat config.json | jq .DOMAIN_NAME -r); \
	make build; \
	aws-vault exec acloudguru-sandbox --no-session -- \
		sam deploy \
			--no-confirm-changeset \
			--parameter-overrides HostedZoneParameter=$$HOSTED_ZONE DomainNameParameter=$$DOMAIN_NAME

deploy-site:
	DOMAIN_NAME=$$(cat config.json | jq .DOMAIN_NAME -r); \
	sed -i '' "s/.cmcloudlab.*\.info/.$$DOMAIN_NAME/" resume-site/index.html; \
	aws-vault exec acloudguru-sandbox --no-session -- aws s3 sync ./resume-site s3://open-up-the-cloud-site

hostedzone:
	aws-vault exec acloudguru-sandbox --no-session -- aws route53 list-hosted-zones | jq .HostedZones[0].Id | cut -d "\"" -f 2 | cut -d "/" -f3

invoke-get:
	sam build && aws-vault exec acloudguru-sandbox --no-session -- sam local invoke GetFunction

invoke-put:
	sam build && aws-vault exec acloudguru-sandbox --no-session -- sam local invoke PutFunction
