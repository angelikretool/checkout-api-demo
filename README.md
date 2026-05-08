# checkout-api-demo

Demo target for the PyCon on-call agent talk. The on-call agent triggers these workflows via `workflow_dispatch` from a Retool dispatcher when an operator clicks an action button in Slack.

## Workflows

- `rollback.yml` — Reverts `checkout-api` from one version to another. Logs each step (drain, deploy, verify) so the audience sees a real CI run streaming.

## Triggering from Retool

```
POST https://api.github.com/repos/angelikretool/checkout-api-demo/actions/workflows/rollback.yml/dispatches
Authorization: Bearer <PAT with repo + workflow scopes>

{
  "ref": "main",
  "inputs": {
    "from_version": "v2.84.1",
    "to_version": "v2.84.0",
    "incident_id": "Q2NPD8VSAJWR5V",
    "initiated_by": "angelik"
  }
}
```

GitHub returns 204 No Content on success.
