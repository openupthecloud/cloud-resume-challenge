.PHONY: build

build:
	sam build

deploy-infra:
	sam build && aws-vault exec sandbox --no-session -- sam deploy --no-confirm-changeset

deploy-site:
	aws-vault exec sandbox --no-session -- aws s3 sync ./resume-site s3://my-fantastic-website
