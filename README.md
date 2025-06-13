# 1P Rails Credentials Heroku Buildpack

This is a Heroku buildpack for injecting Rails credencials from 1Passwod Vault in deploy to avoid putting the credentials file into the repository.

## Setup

Add the following variables in the application:

| Variable                 | Value                                   |
|--------------------------|-----------------------------------------|
| CREDENTIALS_PATH         | op://CLI_STAGING/YOUR_APP/CREDENTIALS   |
| CREDENTIALS_ENVIRONMENT  | production                              |
| OP_SERVICE_ACCOUNT_TOKEN | your-service-token                      |

The service account token must have permission to read the vault in the path.

Example:

```bash
heroku config:add CREDENTIALS_PATH=op://CLI_STAGING/YOUR_APP/CREDENTIALS CREDENTIALS_ENVIRONMENT= staging OP_SERVICE_ACCOUNT_TOKEN=your-service-token -a heroku-app
```

## Usage

Add the buildpack to your application.

```bash
heroku buildpacks:add https://github.com/universokobana/heroku-buildpack-op-rails-credentials.git -a my_app
```

## Output

This will save the content from 1Password to `./config/credentials/{environment}.yml.enc` whene environment is the value of environment variable `CREDENTIALS_ENVIRONMENT`.