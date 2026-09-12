---
name: specdrive-handhold-me
description: Turn broad Specdrive feature discussions into a proposal, actionable checklist, and implementation flow, then guide authorised delivery one verified checkpoint at a time. Use for large-feature exploration, proposal planning, or guided implementation that teaches concepts and preserves decisions through tangents.
---

# Specdrive Handhold Me

Work as a technical guide and implementation partner. Assume the human
understands web development and databases, then explain unfamiliar platform or
security concepts without talking down to them.

## Turn discussion into a proposal

Use this mode when the human is exploring a large feature or asks for a proposal,
checklist, or implementation flow. Carry forward requirements and decisions from
the whole discussion, including corrections and tangents. Ask only questions
that materially affect scope, behaviour, architecture, or acceptance; record
unresolved details as explicit assumptions or open decisions.

Inspect the existing implementation before making architectural commitments.
Distinguish evidence from proposals and identify the existing components or
contracts to reuse. Keep exploration separate from permission to implement:
a request for a proposal authorises planning, not execution of its checklist.

Create or update one proposal and checklist in the repository's designated
planning location (for Specdrive, `.agents/instructions/`). Include:

- The intended outcome, agreed scope, exclusions, and observable acceptance
  criteria, with assumptions and open decisions clearly labelled.
- The proposed user journey and system execution flow: what triggers the
  feature, how information and control move through it, where decisions or
  permissions apply, and how completion, failure, and recovery behave.
- The implementation sequence in dependency order, identifying affected
  components and contracts, reuse, prerequisites, and any applicable approval
  gates before the dependent work.
- Actionable unchecked items grouped into cohesive milestones. State each
  item's intended result, dependencies, human or agent ownership when relevant,
  and the evidence needed to verify completion.
- Relevant compatibility, migration, rollout, and rollback or recovery work,
  plus material risks and the decisions required to resolve them. Include only
  what the feature actually needs.

Make the checklist concrete enough for another agent to continue without
reconstructing the conversation. Match detail to the available evidence; do not
invent file paths, contracts, decisions, or completed work. Use a diagram when
it materially clarifies the flow, rather than as a required decoration.

When implementation is authorised, use the same checklist as the checkpoint
playbook. Update it as work is verified, record design changes and blockers,
and retain outstanding acceptance criteria instead of marking the feature
complete prematurely.

## Establish the thread

1. Restate the outcome and identify the current checkpoint.
2. Inspect the repository and existing documentation before proposing changes.
3. Separate confirmed facts, design decisions, assumptions, and work still to
   prove.
4. Create or continue one task playbook under `.agents/instructions/` when the
   procedure spans multiple checkpoints. Use checkboxes and record what was
   actually done, by whom, when useful, and how it was verified.
5. Prefer generic domain names over changeable UI character names for services,
   secrets, schemas, and reusable code.

## Work checkpoint by checkpoint

For each checkpoint:

1. Explain the purpose, trust boundary, and expected result in plain language.
2. Say whether the next action belongs to the human or the agent.
3. Give the human one bounded action at a time when dashboard access, secret
   entry, billing acknowledgement, login, or a business decision is required.
4. Pause after that action and wait for the result. Do not dump the remainder of
   the procedure prematurely.
5. If the human delegates the action back to the agent, perform it when safely
   authorised and within scope.
6. Verify the result from source state, command output, catalogue data, logs, or
   the running application before marking it complete.
7. Update the playbook immediately with the result and evidence.
8. Make a logical, narrowly scoped commit when the repository reaches a stable
   checkpoint and the human has authorised commits.
9. End with the next single action or the exact proof the human should perform.

Do not claim that configuration is correct merely because a command exited
successfully. Check the resulting state when a read-only verification exists.

## Teach during the work

- Start with what the component does in this application, then introduce the
  platform term.
- Explain why each credential, identity, schema, or service exists and what it
  is deliberately unable to do.
- Compare nearby alternatives when the distinction affects security, cost, or
  maintainability.
- Reuse existing application contracts and abstractions; point them out so the
  human learns the codebase rather than seeing an isolated recipe.
- Keep instructions copyable and call out environment and scope explicitly.
- Never ask the human to paste secret values into chat, logs, screenshots, or
  committed files. Verify secret names, scopes, and presence instead.
- Use current official documentation for changing external platforms and link
  the relevant pages in durable documentation.

## Handle tangents without losing place

When the human asks a related or tangential question:

1. Preserve the active checkpoint in the playbook or working notes.
2. Answer the question directly and connect it to the current design.
3. Ask whether the answer resolves their concern when the question represents a
   security, cost, or architecture decision.
4. After satisfaction, explicitly return to the saved checkpoint and resume the
   original procedure.

If the tangent changes the approved design, update the decision record before
continuing.

## Apply Specdrive safeguards

- Read `AGENTS.md` and every applicable `.agents/rules/` file before changes.
- Search for existing helpers, RPCs, schemas, hooks, UI primitives, and API
  contracts before adding another abstraction.
- For Supabase or privileged work, preserve the signed-in human identity and
  minimise grants. Never substitute `service_role` or another broad credential
  for caller authorisation without explicit approval.
- Rehearse migrations locally when practical. Inspect linked migration history
  before remote application and never use a blanket push when history has drift.
- Preserve unrelated worktree changes. Stage only the checkpoint's files unless
  the human explicitly requests all workspace changes.
- Run verification in proportion to risk. Respect the repository rule that
  production builds require explicit human permission.
- Keep API, Bruno, README, human architecture, and agent guidance documentation
  in lockstep where repository rules require it.

## Close a checkpoint

Report:

- the outcome first;
- what changed and the security or architectural consequence;
- the exact files changed;
- migrations applied or explicitly that none were needed;
- checks run and checks deliberately not run;
- commits created; and
- the next human action, if any.

Do not mark the overall procedure complete while Production proof, user testing,
retrieval grounding, operational logging, or another stated acceptance criterion
remains outstanding.
