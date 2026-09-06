---
name: infrastructure
group: Ship and run
description: >-
  Write Terraform, Pulumi or CloudFormation and automate provisioning, state and drift detection.
  Use when writing Terraform, OpenTofu, Pulumi, or cloud IaC manifests.
---

# Infrastructure

Infrastructure code has a different failure mode than application code: a mistake doesn't just break a test, it can provision the wrong resources, leave something publicly exposed, or rack up unexpected cloud spend. Be conservative by default and explicit about anything that costs money or opens network access.

## Deciding which tool fits

- **Dockerfile / docker-compose** — for containerizing a single app or a small multi-service local dev setup. This is almost always the right starting point even if the user's end goal is Kubernetes — a working Dockerfile is a prerequisite either way.
- **Terraform** — for provisioning cloud resources themselves (VMs, managed databases, networking, IAM) rather than what runs on top of them. Use when the user is standing up infra, not just packaging an app.
- **Kubernetes manifests / Helm** — for orchestrating already-containerized apps at a scale or complexity where docker-compose stops being enough (multiple replicas, rolling updates, service discovery across many services). Don't reach for K8s by default for a simple app — it's meaningfully more operational overhead, and it's worth saying so if the user's actual need looks like it fits in docker-compose.

## Dockerfile principles

1. **Multi-stage builds** for compiled/bundled languages — build in one stage, copy only the artifact into a slim runtime image. This keeps the final image small and avoids shipping build tools into production.
2. **Pin base image versions** (`node:20-slim`, not `node:latest`) — floating tags mean the same Dockerfile can produce a different image next month, which is exactly the kind of surprise IaC is supposed to prevent.
3. **Order layers by change frequency** — copy dependency manifests and install dependencies before copying application source, so Docker's layer cache isn't invalidated by every code change.
4. **Run as a non-root user** in the final image unless there's a specific reason not to — flag this explicitly if generating a Dockerfile that doesn't do it, since running as root is a common and avoidable security gap.

## Terraform principles

1. **State matters more than the config itself.** Always ask (or check for existing config) whether remote state (S3+DynamoDB, Terraform Cloud, etc.) is set up before writing resources — local state is fine for a quick experiment but is a real risk for anything touching shared infrastructure.
2. **Never hardcode secrets or credentials** in `.tf` files — use variables sourced from environment variables or a secrets manager, and remind the user `.tfvars` files with real secrets shouldn't be committed.
3. **Default to least-privilege IAM** — don't write a wildcard `*` resource/action policy just because it's simpler; scope permissions to what the specific resource actually needs.
4. **Flag anything that costs money or opens public access** before presenting it — e.g. "this creates an RDS instance, which has an ongoing cost" or "this security group rule opens port 22 to 0.0.0.0/0, which exposes SSH to the entire internet — did you mean to scope this to your IP instead?"

## Kubernetes principles

1. **Set resource requests/limits** on every container — an unbounded pod can starve its neighbors on the same node, and this is one of the most common things people forget when hand-writing manifests.
2. **Use a Deployment, not a bare Pod**, for anything that should self-heal or scale — bare Pods don't restart if they crash.
3. **Liveness/readiness probes** should be included for anything serving traffic, so Kubernetes actually knows when a pod is unhealthy rather than routing traffic to a broken instance.
4. **Namespace scoping** — don't default everything to the `default` namespace for a real (non-toy) deployment; ask or infer an appropriate namespace.

## Anti-Patterns & Constraints

- Don't provision real cloud resources yourself (i.e. don't run `terraform apply` or `kubectl apply` against a live cluster) unless the user has explicitly asked you to and confirmed they understand what will be created and its cost — writing the config and applying it are different levels of consequence, treat them that way.
- Don't silently choose a cloud provider or region — ask if it's not stated or inferable from existing config.

## Output format

Provide the complete file(s), ready to save at the conventional path (`Dockerfile`, `docker-compose.yml`, `main.tf`, `deployment.yaml`), with inline comments on anything non-obvious or anything that costs money/opens access. Follow with a short plain-language summary of what it provisions and any cost or security flags — before the user applies it, not after.

See `references/dockerfile-patterns.md` and `references/terraform-k8s-patterns.md` for fuller examples per stack.

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.
