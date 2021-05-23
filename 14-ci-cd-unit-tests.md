
## CI/CD - Tests

1. Setup a simple workflow, no secrets, just tests here
2. If you're using another language, don't worry, the process should be similar
3. Free for 2000 minutes a month (not bad!) -> https://github.com/pricing

```yaml
  build-infra:
    runs-on: ubuntu-latest
    timeout-minutes: 2
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-go@v2.1.3
        with:
          go-version: ${{ env.GO_VERSION }}
      - name: test get-function
        run: cd cloud-resume-challenge/get-function && go test -v ./ && cd ../../
      - name: test put-function
        run: cd cloud-resume-challenge/put-function && go test -v ./ && cd ../../
```
