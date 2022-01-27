# Cloud.gov CloudFoundry CLI Configuration Setup
This action performs the following steps in order:

1. Installs the CloudFoundry CLI
2. Runs the `cf api` command to set the CLI to target the cloud.gov API
(https://api.fr.cloud.gov).
3. Authenticates to the cloud.gov CLI using the provided user/pass.
4. Targets one of 'dev', 'test', or 'prod' spaces. Note: the action will
determine the space to target based on the github environment. Pushes to
`main` target 'dev', tags will target 'test', and GitHub releases will
target 'prod'.

# Usage
```yaml
- uses: 18F/identity-idva-cf-setup@v2
  with:
    cf-username: ${{ secrets.CF_USER }}
    cf-password: ${{ secrets.CF_PASS }}
    cf-org: ${{ secrets.CF_ORG }}

    # Optional
    space-suffix: "-closed"
```

## Outputs

| Output | Description |
| --- | --- |
| `target-environment` | One of `dev`, `test`, or `prod` depending on the GitHub environment at the time of execution |
| `target-environment-upper` | The upper-case variant of `target-environment` |
| `target-space` | The name of the cf space that was targeted by the action. This will be the concatenation of the `target-environment` output and `space-suffix` parameter |

### Using the action output
```yaml
jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: Cloud Foundry Job
    steps:
      - uses: actions/checkout@v2

      - uses: 18F/identity-idva-cf-setup@v2
        id: cf-setup
        with:
          cf-username: ${{ secrets.CF_USER }}
          cf-password: ${{ secrets.CF_PASS }}
          cf-org: ${{ secrets.CF_ORG }}

      - run: echo "Environment target was ${{ steps.cf-setup.outputs.target-environment }}
        shell: bash

      - run: echo "Upper-case target was ${{ steps.cf-setup.outputs.target-environment-upper }}
        shell: bash
```
