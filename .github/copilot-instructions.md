# Copilot Repository Instructions

These are repository-wide instructions for a **Kubebuilder-style Kubernetes Operator** written in Go.

---

## Project Overview
- **Type:** Kubernetes Operator (Kubebuilder scaffold)
- **Language:** Go (version pinned in `go.mod`)
- **Key libs:** `sigs.k8s.io/controller-runtime`, `k8s.io/*`
- **Tools:** `sigs.k8s.io/controller-tools` (`controller-gen`), kustomize, envtest, golangci-lint, kind (for e2e)

---

## Project Layout
- `/api` — CRD types & deepcopy files
- `/controllers` — Reconciliation logic
- `/webhooks` — Admission webhooks
- `/cmd` — Main entrypoint
- `/config` — Kustomize manifests, CRDs, RBAC
- `/test` — E2E tests and helpers
- `Makefile` — Build automation
- `PROJECT` — Kubebuilder project config (**auto-generated**, do not edit)

**Generated files include:**
- `api/**/zz_generated.*.go`
- `config/crd/bases/*.yaml`
- `config/rbac/*.yaml`
- `PROJECT`

All other files are considered **source**.

---

## Copilot Code Review Rules

:robot: AI-generated (may contain mistakes).

### For [GENERATED]
- DO NOT recommend manual edits.
- Suggest fixing the relevant source file (e.g. `api/*_types.go`, `internal/controller`, `internal/webhooks`) and rerunning:
    - `make generate`
    - `make manifests`
- Always follow with: `make fmt vet lint-fix`
