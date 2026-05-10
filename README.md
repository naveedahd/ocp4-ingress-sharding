# OpenShift 4.18 Ingress Sharding Design

This repository contains a living architecture and design artifact for planning ingress sharding on an OpenShift Container Platform 4.18 cluster.

The primary document is:

- [`ingress-sharding-architecture.html`](./ingress-sharding-architecture.html)

Open the HTML file in a browser to review the design narrative, diagrams, assumptions, implementation examples, migration guidance, validation checklist, risks, and unresolved decisions.

## Project Scope

The design artifact covers:

- OpenShift `IngressController` sharding.
- Namespace and route selector strategy.
- DNS and wildcard domain implications.
- Router placement, scaling, and operational ownership.
- Certificate and domain ownership considerations.
- Observability, troubleshooting, rollout, validation, and rollback planning.
- Migration guidance from open source `ingress-nginx` to OpenShift Routes and sharded Ingress Controllers.

## How To Use This Repository

Use the HTML document as the main source of context and discussion. It is intended to be read directly in a browser rather than consumed as raw markdown.

Recommended review flow:

1. Open [`ingress-sharding-architecture.html`](./ingress-sharding-architecture.html).
2. Review the current target architecture and sharding model.
3. Work through the decision placeholders.
4. Validate the implementation examples against your OpenShift 4.18 cluster and organization-specific DNS, certificate, and load-balancing model.
5. Update the artifact as design decisions become final.

## Status

This is a draft design artifact. Implementation examples are illustrative until validated against a target OpenShift 4.18 cluster.

## Disclaimer

This content was generated with the assistance of AI. Review and validate all architecture recommendations, OpenShift API examples, operational procedures, and migration guidance before using them in a production environment.
