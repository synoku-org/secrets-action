# Synoku Secrets Action

Securely sync secrets between Synoku and GitHub Actions workflows.

This Action supports two modes:

- **`load`** (default): fetch secrets from Synoku and expose them as environment variables.
- **`upload`**: push selected environment variables to Synoku for later use.

[![Tests](https://github.com/synoku-org/secrets-action/actions/workflows/test.yml/badge.svg)](https://github.com/synoku-org/secrets-action/actions/workflows/test.yml)

## Upload secrets

Useful for the first load to Synoku. Pass all secrets and vars starting with `SYNOKU_`. Example:

```yaml
- name: Upload secrets to Synoku
  uses: synoku-org/secrets-action@v1
  with:
    mode: upload
    token: ${{ secrets.SYNOKU_API_TOKEN }}
    application: ${{ github.event.repository.name }}
    environment: ci
  env:
    SYNOKU_SECRET_A: ${{ secrets.SECRET_A }}
    SYNOKU_SECRET_B: ${{ secrets.SECRET_B }}
    SYNOKU_VARIABLE_A: ${{ vars.VARIABLE_A }}
    SYNOKU_VARIABLE_B: This is manual variable B
```

## Load secrets

```yaml
- name: Load Synoku secrets
  uses: synoku-org/secrets-action@v1
  with:
    token: ${{ secrets.SYNOKU_API_TOKEN }}
    application: ${{ github.event.repository.name }}
    environment: ci
```

## Action inputs

| Name              | Required | Description                                                                 |
|-------------------|----------|-----------------------------------------------------------------------------|
| `token`           | ✅ Yes   | Synoku API token (User token, App token or Env token).                      |
| `application`     | ✅ Yes   | Application name (slug).                                                   |
| `environment`     | No       | Environment name (default: `ci`).                                           |
| `mode`            | No       | `load` (default) or `upload`. Use `upload` to push secrets from env.       |
| `allowEmptyUpload`| No       | Allow uploads with no variables. Emits warning instead of failing.         |
| `debug`           | No       | Enable debug messages (default: `false`).                                  |

## Action outputs

_This Action does not currently expose outputs._

## License

This repository and its contents are proprietary and confidential.

All rights reserved © 2025 Synoku.

Use of this software is strictly limited to authorized Synoku clients under explicit written agreement.

Any unauthorized use, distribution or modification is prohibited.

For licensing inquiries, contact legal@synoku.com.
