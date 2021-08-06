# GIVE CloudFoundry CLI Configuration Setup
This action installs the CloudFoundry CLI within a GitHub action run and will
optionally authenticate to the cloud.gov CLI and target one of the give 'dev',
'test', or 'prod' environments if given a user/pass/org.

# Usage
```yaml
- uses: 18F/identity-give-cf-action@v1
  with:
    cf-username: ${{ secrets.CF_USER }}
    cf-password: ${{ secrets.CF_PASS }}
    cf-org: ${{ secrets.CF_ORG }}
```

## Outputs
The action outputs a single value that can be used to determine the targeted
environment. The `target-environment` output will be one of `dev`, `test`, or
`prod`.

### Using the action output
```yaml
jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: Cloud Foundry Job
    steps:
      - uses: actions/checkout@v2
      - id: cf-setup
        uses: 18F/identity-give-cf-action@v1
        with:
          cf-username: ${{ secrets.CF_USER }}
          cf-password: ${{ secrets.CF_PASS }}
          cf-org: ${{ secrets.CF_ORG }}
      - run: echo "Environment target was ${{ steps.cf-setup.outputs.target-environment }}
        shell: bash
```
