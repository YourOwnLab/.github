# Repository agent instructions

## Purpose

This repository provides YourOwnLab organization-wide defaults: contribution, security, support and ownership documents, issue and pull-request templates, and the centrally maintained reusable workflows that Golden Path repositories call.

An agent working here changes every repository in the organization at once. Nothing else in the organization has that reach, and two consequences follow.

**This repository is public.** Its contents, including `profile/README.md`, are visible to anyone. Everything below about disclosure follows from that.

**Its workflows are executed by other repositories.** A change to a reusable workflow is a change to other repositories' CI, made without their review.

## Authority

The YourOwnLab engineering handbook is the authority. This file adds repository-specific expectations and does not restate policy. When information conflicts, use this order:

1. Explicit human instructions in the current task.
2. Repository-local documentation: [`README.md`](README.md), this file, and [`.github/workflows/README.md`](.github/workflows/README.md).
3. The engineering handbook in [`YourOwnLab/platform`](https://github.com/YourOwnLab/platform): [constitution](https://github.com/YourOwnLab/platform/blob/main/handbook/constitution.md), [engineering principles](https://github.com/YourOwnLab/platform/blob/main/handbook/engineering-principles.md), [delivery standard](https://github.com/YourOwnLab/platform/blob/main/handbook/delivery-standard.md), [security baseline](https://github.com/YourOwnLab/platform/blob/main/handbook/security-baseline.md), and [GitHub governance baseline](https://github.com/YourOwnLab/platform/blob/main/handbook/github-governance-baseline.md).
4. Accepted [ADRs](https://github.com/YourOwnLab/platform/blob/main/adr/README.md).
5. Existing implementation.

If implementation conflicts with documentation, treat the documentation as the intended architecture, report the inconsistency, and never silently redesign the system.

## Required reading before changing anything

1. This file.
2. [`README.md`](README.md) and [`.github/workflows/README.md`](.github/workflows/README.md).
3. The [security baseline](https://github.com/YourOwnLab/platform/blob/main/handbook/security-baseline.md) and the [GitHub governance baseline](https://github.com/YourOwnLab/platform/blob/main/handbook/github-governance-baseline.md).
4. The [delivery standard](https://github.com/YourOwnLab/platform/blob/main/handbook/delivery-standard.md), including the Conventional Commits contract for pull-request titles.

## Required workflow

Work on a short-lived `agent/*` branch, never push to `main`, and open a pull request with a Conventional Commits title. Merge authority belongs to an accountable human.

## This repository is public

Assume every change is read by someone outside the organization, because it can be.

- Never add product plans, strategy, roadmaps, internal metrics, incident detail, provider identifiers, environment names, account identifiers, or repository contents that are private elsewhere.
- Never add secrets or credentials. Secret scanning and push protection are enabled here, and neither is a reason to relax attention.
- Community-facing documents describe how to contribute and how to report a problem. They do not describe what is being built.

## Changing a reusable workflow changes other repositories

Caller repositories pin these workflows by immutable commit SHA. That pin is a control, not an inconvenience.

- A change to a reusable workflow reaches a caller only when that caller updates its pin. Do not treat a merge here as a rollout, and do not update callers as a side effect of a change made here.
- State the caller impact in the pull request: which repositories call the workflow, what breaks if they update, and what they must change.
- Pin every third-party action to an immutable commit SHA, never a tag or branch, as the [security baseline](https://github.com/YourOwnLab/platform/blob/main/handbook/security-baseline.md) requires.
- Keep permissions least-privilege and declared. Widening a workflow's `permissions` widens it for every caller.
- Prefer an additive, backward-compatible change. A breaking change to a workflow input or behavior needs an explicit migration note for callers.

## Escalation

Stop and ask for approval before changing reusable workflow behavior, inputs, or permissions, before changing organization-wide policy documents, before changing Dependabot configuration, before adding or upgrading a third-party action, and before publishing anything to `profile/README.md`.

## Definition of done

- The change is correct for every repository that inherits it, not only the one that prompted it.
- Caller impact is stated explicitly, including "none" when that is the answer.
- Third-party actions are SHA-pinned and permissions are least-privilege.
- Nothing private, and nothing that identifies internal systems, has entered a public file.

## AI readiness

Before finishing, ask whether a maintainer of a caller repository could tell, from this change alone, whether it affects them. If not, improve the pull request or the documentation until they could.
