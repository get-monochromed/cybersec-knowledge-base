---
title: Container Security
aliases: [Docker Security, Kubernetes Security, K8s Security]
category: domain
tags: [domain/cloud, containers]
status: solid
up: "[[Domains MOC]]"
created: 2026-10-23
updated: 2026-10-23
sources: []
---

# Container Security

## Summary

A container is a process with namespaces and cgroups — not a security boundary in the way a VM is. Security comes from image provenance, runtime isolation, and the cluster's admission control.

## Layers

1. **Image** — minimal base (distroless/alpine), no secrets baked in, pinned digests, scanned for CVEs, non-root `USER`, no unnecessary setuid binaries.
2. **Build** — reproducible, signed (cosign/Sigstore), SBOM generated, provenance attested ([[Supply Chain Attack]]).
3. **Registry** — private, immutable tags, admission only from trusted registries.
4. **Runtime** — read-only root filesystem, dropped capabilities, seccomp/AppArmor, no `--privileged`, no docker socket mount, user namespaces.
5. **Orchestrator** — RBAC least privilege, network policies (default deny), Pod Security Standards, secrets from a vault, admission controllers (OPA/Gatekeeper, Kyverno).
6. **Host** — the real boundary. Patch it, isolate it, and prefer dedicated nodes for sensitive workloads. gVisor/Kata/Firecracker for stronger isolation.

## Common failures

- `privileged: true`, `hostPath` mounts, `hostNetwork` — container escape in one line.
- Cluster admin bound to a service account used by CI.
- Kubernetes API server exposed to the internet without authn/authz hardening.
- Secrets as base64 in manifests — encoding is not encryption.
- Image tags like `:latest` with no digest pinning → silent supply-chain change.

## Detection

- Runtime: unexpected process execution in a pod, shell spawned in a distroless image, crypto-mining CPU patterns, outbound connections to mining pools.
- Control plane audit logs: `exec` into pods, RBAC changes, secret reads, new cluster-admin bindings.
- Image scanning on admission, alerting on unsigned images.

## Related

- [[Cloud Security]]
- [[Application Security]]
- [[Supply Chain Attack]]
- [[Network Segmentation]]
- [[Domains MOC]]
