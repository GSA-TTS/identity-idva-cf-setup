# Cloud Foundry Service Setup
This action performs the service checks and procurement for cloud foundry apps.

# Usage
```yaml
- uses: GSA-TTS/identity-idva-cf-setup/service-setup@{version}
  with:
    require-redis: "true" # Each 'require-<x>' parameter is optional
    require-postgres: "true"
    require-elasticsearch: "true" 
```

A `services.json` file is required in the root directory of the cloud foundry app to specify the service names and specifications.

```json
{
    "db": {
        "name": "mydb",
        "service": "aws-rds",
        "plan": {
            "dev": "micro-psql",
            "test": "micro-psql",
            "prod": "micro-psql"
        }
    }
}
```