---
name: tracing-research-lineages
description: Use when a user supplies, uploads, links, or identifies an academic paper and asks about its research question, claims, experimental validation, related-paper timeline, comparative innovations, research lineage, or historical development.
---

# Tracing Research Lineages

## Core Principle

Trace a paper as a claim-bearing research artifact, not as an isolated citation node. Prefer full text over abstract-only evidence, preserve original paper titles, and write the final answer in the user's language. Read [references/research-protocol.md](references/research-protocol.md) before searching or screening, and read [references/output-template.md](references/output-template.md) before drafting the response.

## Workflow

1. Classify evidence access using the protocol and state any degraded mode up front.
2. Extract the focal paper's research problem, core claims, and claim-to-experiment mapping from the fullest available text.
3. Build a narrow direction abstraction: object + mechanism or phenomenon + purpose, with explicit scope, synonyms, and exclusions.
4. Search by concept, then expand with backward and forward citation chaining. Use surveys only to discover candidates, then verify core facts from primary sources.
5. Separate core papers from adjacent work. Keep only lineage-relevant papers in the core timeline and move broad or merely similar work to adjacent with reasons.
6. Order core papers by first verifiable public date, while listing formal publication separately. Merge duplicate versions and mark unresolved date conflicts.
7. For each core step, explain the inherited basis, prior limitation, new increment, and relationship label. Claim direct inheritance only with explicit evidence.
8. Mark analytical inference explicitly, state uncertainty where evidence is partial, and never claim complete coverage without qualification.

| Need | Minimum action |
| --- | --- |
| Best evidence | Prefer full text and verified metadata |
| Validation | Map each major claim to supporting experiments |
| Search | Concept queries plus backward/forward citation tracing |
| Scope | Separate core lineage from adjacent work |
| Chronology | Use first public date; list formal publication separately |
| Reporting | Label relationships, cite support, expose uncertainty |

Example: For a multimodal jailbreak paper, identify its exact attack mechanism, map each claim to experiments, trace predecessor attack formulations and later defenses by citation chaining, then place benchmarks or loosely related safety work in adjacent rather than core lineage.

Common mistakes: treating surveys as evidence, using only publication venue dates, collapsing adjacent work into the core chain, inferring direct inheritance without proof, or implying exhaustive coverage despite missing full text or limited search access.

## Quality Gates

- Both reference files were read and followed for this run.
- When drafting, copy all required output-template section names and table columns verbatim; do not abbreviate or rename them.
- Every supported claim has a citation, and every inference is labeled as analysis.
- Claim-to-experiment mapping is explicit for the focal paper.
- The narrow direction excludes nearby but non-core lines.
- Core timeline dates use earliest verifiable public versions, with conflicts noted.
- The answer states saturation status, uncertainty, cutoff limits, and no unqualified completeness claim.
