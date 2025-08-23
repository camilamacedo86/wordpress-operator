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

1. **Generate manifests/code:** `make manifests generate`
2. **Static checks:** `make fmt vet lint`
3. **Build:** `make build` → builds `bin/manager`
4. **Unit tests:** `make setup-envtest` then `make test`
5. **E2E tests:** `make test-e2e`
6. **Cluster deploy:** `make install deploy`
7. **Cluster cleanup:** `make undeploy uninstall`
8. **Dependencies:** `go mod tidy`
9. **Images:** `make docker-build` then `make docker-push`

---
## Project Layout
- `/api` — CRD types & deepcopy files
- `/controllers` — Reconciliation logic
- `/webhooks` — Admission webhooks
- `/cmd` — Main entrypoint
- `/config` — Kustomize manifests, CRDs, RBAC
- `/test` — E2E tests and helpers
- `Makefile` — Build automation
- `PROJECT` — Auto-generated config file. DO NOT EDIT MANUALLY.

---
## Copilot Code Review Rules

:robot: AI-generated (may contain mistakes).

### File classification
- **[GENERATED]** `api/**/zz_generated.*.go`, `config/crd/bases/*.yaml`, `config/rbac/*.yaml`, `PROJECT`
- **[SOURCE]** All other files (`api/*_types.go`, `controllers/**`, `webhooks/**`, etc.)

### For [GENERATED]
- DO NOT recommend manual edits. Instead, suggest fixing the source file (`api/*_types.go`, `internal/controller`, etc.) and running `make generate` or `make manifests`.
- After code is changed, always suggest `make fmt vet lint-fix`.

### For [SOURCE]
- Provide 1-3 short bullets for what to keep, edit, or remove.
- Mention imports or API updates if needed.
- If `go.mod`/`go.sum` changed, suggest `go mod tidy`.
