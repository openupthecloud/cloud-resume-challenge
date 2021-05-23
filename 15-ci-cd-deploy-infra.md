
## CI/CD - Tests

1. Add secrets to your pipeline -> https://github.com/openupthecloud/cloud-resume-challenge/settings/secrets/actions
2. How to do dependent jobs in Github Actions

```yaml
deploy-infra:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-python@v2
      - uses: aws-actions/setup-sam@v1
      - uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1
      - run: sam build
        working-directory: cloud-resume-challenge
      - run: sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
        working-directory: cloud-resume-challenge
```
