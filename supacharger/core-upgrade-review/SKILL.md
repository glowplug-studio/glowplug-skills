---
name: core-upgrade-review
description: Compare a Supacharger consumer's installed Core revision with a proposed immutable revision, inspect actual consumer usage, and report evidenced compatibility, migration and deployment risks before an update. Use when reviewing whether a Core change will break an application or planning a guarded Core upgrade.
---

# Core Upgrade Review

Review compatibility before changing the consumer. The review is read-only unless the human separately authorises an update or remediation.

## Establish the comparison

1. Read the consumer's `AGENTS.md`, `.agents/supacharger/guidance.md`, project instructions, `.supacharger/managed-files.json` and `.supacharger/core-lock.json`.
2. Record the consumer path, installed immutable Core commit, proposed immutable commit or tag, CLI version and relevant repository state. Resolve `latest` to an immutable commit before drawing conclusions.
3. If the installed baseline, proposed source or ownership manifest cannot be verified, report that limitation. Do not infer a baseline from filenames, package versions or the working tree.
4. Inspect the Core commit history and complete diff between the installed and proposed revisions. Treat `supacharger doctor --ref` as supporting evidence only; verify important findings against source and the consumer.

## Inspect compatibility surfaces

Follow changed dependencies into their callers. Review only surfaces implicated by the diff, including:

- ownership classes, added or removed paths and collisions with existing developer files;
- exported modules, adapters, component props and reusable public APIs;
- `SupachargerConfig` names, types, defaults and semantic meaning;
- environment variables, package requirements, scripts and build assumptions;
- public, protected, authenticated and verified routes, redirects, cookies and session behaviour;
- Supabase schemas, migrations, RPC signatures, grants, RLS, Edge Functions, generated types, OpenAPI and Bruno documentation;
- authentication, authorisation, billing and privileged service boundaries;
- deployment order, external service configuration and recovery requirements; and
- agent guidance or developer-owned seams whose expected behaviour changed.

Search the consumer's developer-owned code and configuration for each changed contract, symbol, route, key or assumption. When the requested scope includes several consumers, inspect each separately; do not assume identical usage.

## Classify findings

Classify every material finding as one of:

- **Confirmed breakage:** the consumer demonstrably depends on removed or incompatible behaviour.
- **Likely incompatibility:** evidence shows a material risk, but runtime or external-state verification is still needed.
- **Compatible change:** the affected consumer usage has been inspected and no required adaptation was found.
- **Insufficient evidence:** the relevant baseline, usage or runtime state could not be established.

For each finding, cite the changed Core file and symbol or contract, affected consumer files, evidence, required action, migration or deployment order, verification and recovery. Distinguish source facts from inference. Static review cannot guarantee that every behavioural break has been found.

## Apply Supacharger gates

Use the existing protection gate in `.agents/supacharger/guidance.md`; do not invent another approval system. Before proposing edits to protected contracts, report affected files, ownership, consumers, intended result and migration, compatibility, deployment and data risk. A review does not authorise `coreupdate`, file changes, migrations, deployment, commits or pushes.

Do not create or extend CLI regression tests during Core or consumer work unless the human explicitly requests them. Preserve developer-owned changes and installation records. Treat `.supacharger/backups/` as recovery copies, not proof of rollback.

## Deliver the report

Lead with the upgrade recommendation: proceed, proceed after named adaptations, or block pending named evidence or fixes. Include:

- installed and proposed immutable revisions;
- a concise contract-change inventory;
- findings ordered by severity;
- exact consumer adaptations and responsible owner;
- database, service and deployment sequencing;
- verification and recovery steps; and
- unresolved evidence and the applicable protection gate.

Keep the report in the project's normal planning or review location. Do not place a general upgrade review in `docs/reports/sc-install/`, which is reserved for active installation records.
