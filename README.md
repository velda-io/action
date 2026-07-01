# Velda RunTask Action

This action submits a task to Velda.

## Features

- Uses API token auth input.
- Supports custom API server host (default: `velda.cloud`).
- Supports two execution modes:
  - Script mode: wraps script with `sh -c`.
- Supports targeting by `instance-id` or `instance-name`.
- Exposes `task-id`, `instance-id`, and raw response outputs.

## Inputs

- `api-token` (required): Velda API token.
- `api-server` (optional): API host without scheme. Default `velda.cloud`.
- `pool` (required): Target pool.
- `instance-id` (optional): Numeric target instance id.
- `instance-name` (optional): Target instance name.
- `script` (optional): Script body to run through `sh -c`.
- `login-user` (optional): Workload `login_user`.
- `stdin` (optional): Non-streaming stdin payload. The action base64-encodes it for the proto bytes field.
- `dry-run` (optional): If `true`, prints payload without sending request.

## Outputs

- `task-id`: Created task id.
- `instance-id`: Returned instance id.
- `response-json`: Raw JSON response.

## Usage

### Script Mode (wrapped with sh -c)

```yaml
name: Example Script Mode
on: [workflow_dispatch]

jobs:
  run-task:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Submit task
        uses: ./
        with:
          api-token: ${{ secrets.VELDA_API_TOKEN }}
          pool: shell
          instance-name: my-instance
          login-user: root
          script: |
            echo "hello from script mode"
```
