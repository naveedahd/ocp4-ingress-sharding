# Project Context: OpenShift 4.18 Ingress Sharding Design

## Objective

Create an architecture and design artifact for using ingress sharding on an OpenShift 4.18 cluster.

## Output Artifact

Primary output is an HTML design document.

Current output file:

- `ingress-sharding-architecture.html`

## Working Rules

- Treat this Markdown file as internal project memory.
- Do not write this file as end-user documentation.
- Use this file to preserve project intent, assumptions, open questions, and decisions.
- Keep architectural assumptions explicit.
- Keep unresolved decisions visible.
- Prefer official Red Hat OpenShift 4.18 documentation for product behavior.
- Validate OpenShift API examples against OpenShift 4.18 before publishing them.
- Keep the HTML output self-contained where practical.
- Update this file when the project scope, assumptions, decisions, or output structure changes.

## Known Scope

- IngressController sharding.
- Route and namespace selector strategy.
- DNS and wildcard domain implications.
- Router placement and scaling.
- Operational ownership.
- Certificate and domain ownership implications.
- Observability and troubleshooting expectations.
- Rollout, validation, and rollback planning.
- Migration guidance from open source ingress-nginx to OpenShift Routes and sharded Ingress Controllers.
- Risks, limitations, and decision tradeoffs.

## Current Design Bias

- Use ingress sharding to create intentional routing boundaries, not just extra router replicas.
- Prefer selector-driven route admission over informal naming conventions.
- Keep shard ownership clear enough that platform, application, DNS, and certificate responsibilities do not blur.
- Design for operational clarity: teams should be able to explain why a route landed on a given shard.
- Avoid assuming that every shard needs a unique domain until the target model is chosen.

## Open Questions

- What shard model are we designing for: environment, tenant, workload class, exposure tier, compliance boundary, or another boundary?
- Are custom router domains required per shard?
- Will shards use dedicated nodes or share worker capacity?
- What DNS provider and process will manage wildcard records?
- What route admission policy should the default ingress controller use?
- Will shard membership be based on namespace labels, route labels, or both?
- Are there externally managed load balancers in front of router services?
- Are certificates managed by the OpenShift ingress operator, a cluster certificate process, or an external certificate workflow?
- What observability signals are required to prove traffic is reaching the intended shard?
- What validation steps are required before moving production routes?
- Which existing ingress-nginx annotations are in use, and which ones require redesign instead of direct translation?
- Should migrated applications standardize on OpenShift Routes, or should some Kubernetes Ingress resources remain for compatibility?

## Decision Log

No project decisions have been finalized yet.

Use this format when decisions are made:

```text
YYYY-MM-DD - Decision title
Decision:
Rationale:
Impact:
Follow-up:
```

## Source Notes

- OpenShift 4.18 documentation is the authority for IngressController behavior.
- Verify ingress sharding behavior against the Red Hat OpenShift 4.18 docs before finalizing the HTML artifact.
- Use official OpenShift route annotation documentation when translating ingress-nginx behavior.
- Use ingress-nginx upstream documentation to identify source annotation intent before mapping it to OpenShift.
- Treat implementation examples as illustrative until tested against an OpenShift 4.18 cluster or verified API schema.

## HTML Artifact Expectations

- The HTML document should be readable as a standalone architecture/design artifact.
- It should include the necessary context, diagrams, assumptions, and decision points.
- It should distinguish confirmed design decisions from placeholders.
- It should include practical implementation examples only when they are version-appropriate.
- It should avoid becoming a generic OpenShift tutorial.

## Diagram Inventory

Expected diagrams may include:

- Baseline ingress path before sharding.
- Target ingress sharding traffic flow.
- Route admission using namespace selectors and route selectors.
- DNS and wildcard domain relationship to router shards.
- Operational responsibility model.
- Rollout sequence from default ingress to shard-specific ingress.
- Migration flow from ingress-nginx Ingress resources to OpenShift Routes and shard admission.

## Validation Checklist

- Confirm OpenShift 4.18 API fields used in examples.
- Confirm selector behavior and route admission implications.
- Confirm DNS requirements for any shard-specific domains.
- Confirm certificate behavior for shard domains.
- Confirm default ingress behavior when additional shards are introduced.
- Confirm rollback path for moving routes between shards.
- Confirm observability and troubleshooting commands.
- Confirm migrated route behavior against the source ingress-nginx behavior, especially rewrites, redirects, TLS, allow lists, and timeouts.
