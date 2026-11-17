# OPS Helm charts

```sh
helm repo add ops https://ops-plane.github.io/Helm-charts
helm install ops ops-plane/ops -f my-values.yaml
# or, as an OCI artifact:
helm install ops oci://ghcr.io/ops-plane/charts/ops -f my-values.yaml
```

| Chart | Description |
|---|---|
| [ops](charts/ops) | OPS app + runners ([docs](https://github.com/ops-plane/ops)) |

## Development

- CI (`.github/workflows/charts.yml`) runs `ct lint`, kubeconform and `ct install` on kind (with a throwaway Postgres) for every PR, using each chart's `ci/*-values.yaml`.
- Bump `version` in `Chart.yaml` on every chart change (CI enforces it on PRs). A merge to `main` publishes new versions as GitHub releases and updates `index.yaml` on the `gh-pages` branch, and pushes them to `oci://ghcr.io/ops-plane/charts`.

Locally: `ct lint --config ct.yaml --all` and `ct install --config ct.yaml --all` against a kind cluster.
