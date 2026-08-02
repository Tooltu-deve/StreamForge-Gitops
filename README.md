# streamforge-gitops

GitOps source of truth for **StreamForge**. ArgoCD (installed by Terraform in the app repo)
watches this repo and syncs every workload onto EKS.

- `charts/` — Helm charts copied from the app repo (ADR-0002).
- `values/`  — per-service values. Seeded from Terraform outputs by `scripts/seed-gitops-values.sh`
  in the app repo on each provision. Only `image.tag` changes afterwards, and only via CI.
- `apps/`   — one ArgoCD `Application` per workload (managed by the root app-of-apps).

Do not `kubectl apply` here — change state by committing to this repo.