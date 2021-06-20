
## Deploy Site S3

- Use AWS CLI to upload to S3

```yaml
deploy-site:
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v2
    - uses: jakejarvis/s3-sync-action@master
      with:
        args: --delete
      env:
        AWS_S3_BUCKET: open-up-the-cloud-website
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        SOURCE_DIR: cloud-resume-challenge/resume-site
```
