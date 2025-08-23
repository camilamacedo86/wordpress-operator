# Copilot Repository Instructions

:robot: AI-generated (may contain mistakes).

These are repository-wide instructions for a **Kubebuilder-style Kubernetes Operator** written in Go.

---
## Project Overview
- **Type:** Kubernetes Operator (Kubebuilder scaffold)
- **Language:** Go (version pinned in `go.mod`)
- **Key libs:** `sigs.k8s.io/controller-runtime`, `k8s.io/*`
- **Tools:** controller-gen, kustomize, envtest, golangci-lint, kind (for e2e)
- **Images:** built with `${CONTAINER_TOOL}` (default: docker) and tagged via `IMG` (default: controller:latest)

---
## Build / Test / Validate Flow
Always use the Makefile targets in this order:

1. **Generate manifests and code** `make manifests generate`
   *Use this after modifying API types (`*_types.go`) or adding markers.*

2. **Static checks** `make fmt vet`
   `make lint` or `make lint-fix`

3. **Build / Run** `make build` → builds binary (`bin/manager`)

4. **Unit tests (with envtest)** `make setup-envtest`
   `make test`

5. **End-to-end tests (with kind)** `make test-e2e`

6. **Cluster operations** - Install CRDs: `make install`
    - Deploy controller: `make deploy`
    - Remove controller: `make undeploy`
    - Remove CRDs: `make uninstall`

7. **Dependencies** If `go.mod` or `go.sum` changed → run `go mod tidy`

8. **Images** - `make docker-build IMG=<registry/repo:tag>`
    - `make docker-push IMG=<...>`

---
## Project Layout
- `/api` — CRD type definitions & generated deepcopy files
- `/controllers` — Reconciliation logic
- `/webhooks` — Admission webhooks
- `/cmd/main.go` — Entrypoint
- `/config` — kustomize configs, CRDs, RBAC, deployments
- `/test` — e2e and helpers
- `Makefile` — authoritative for build, test, and deployment tasks
- `PROJECT` — Auto-generated file that tracks all project configuration. This file should never be manually edited.

---
## Copilot Code Review Rules

**Always start reviews with this line:**

:robot: AI-generated (may contain mistakes).

### File classification
- **[GENERATED]** - `api/**/zz_generated.*.go`
    - `config/crd/bases/*.yaml`
    - `config/rbac/*.yaml`
- **[SOURCE]** Everything else (`api/*_types.go`, `controllers/**`, `webhooks/**`, `cmd/**`, `test/**`, configs, etc.).

### For [GENERATED]
- Never recommend manual edits.
- Instead:
    - `zz_generated.*.go` → run `make generate`
    - CRDs → fix types in `api/*_types.go` then run `make generate manifests`
    - RBAC → fix markers in `internal/controller` or `internal/webhooks` then run `make manifests`
- Then: `run: make fmt vet lint-fix`
- If CRDs or webhooks changed: add `validate with: make install`

### For [SOURCE]
- Give 1–3 short bullets: what to keep, edit, remove.
- Mention imports or API updates if needed.
- If `go.mod`/`go.sum` changed: suggest `go mod tidy`.