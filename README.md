# 🚀 Coolify Deploy GitHub Action

Reusable GitHub Action for:
- Validating Coolify env vars
- Triggering deployment via Coolify API
- Sending success/failure notifications via [ntfy.sh](https://ntfy.sh)

## 📥 Inputs

| Name          | Required | Description                              |
|---------------|----------|------------------------------------------|
| docker_image  | ✅ Yes   | Docker image tag to display              |
| ntfy_topic    | ❌ No    | Topic name on ntfy.sh to send messages   |
| ntfy_token    | ❌ No    | Token for private ntfy topics (optional) |

## 🌍 Required Environment Variables (set as `env:` or `secrets:`)

- `COOLIFY_URL`
- `COOLIFY_RESOURCE_ID`
- `COOLIFY_API_TOKEN`

## 🧪 Example

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    env:
      COOLIFY_URL: ${{ secrets.COOLIFY_URL }}
      COOLIFY_RESOURCE_ID: ${{ secrets.COOLIFY_RESOURCE_ID }}
      COOLIFY_API_TOKEN: ${{ secrets.COOLIFY_API_TOKEN }}

    steps:
      - uses: actions/checkout@v4

      - uses: nasrdev/coolify-deploy@v1
        with:
          docker_image: "myapp:latest"
          ntfy_topic: "nasr-deploys"
          ntfy_token: ${{ secrets.NTFY_TOKEN }}
