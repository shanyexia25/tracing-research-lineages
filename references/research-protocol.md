# Research Protocol

## Evidence Access

- `A`: inspected full text plus verified metadata.
- `B`: reliable abstract plus metadata.
- `C`: secondary-only lead.

Use `A` whenever possible. If forced into `B` or `C`, state the downgrade, limit claim strength, and avoid overconfident lineage assertions.

## Direction Abstraction

Represent the narrow direction as `object + mechanism/phenomenon + purpose`.

- Parent field: the broader area that contains the direction.
- Synonyms: alternate names, task labels, or neighboring terminology worth searching.
- Exclusions: nearby topics, benchmark-only work, or application-only variants that should not be treated as core lineage without stronger evidence.

## Search Expansion

Build query families from the focal paper's problem, method terms, object, mechanism, purpose, synonyms, and cited baselines. Expand through backward citation tracing and forward citation tracing from high-relevance papers. Surveys only discover candidates; they do not establish lineage facts by themselves.

## Screening

Screen papers for these roles:

- origins
- new evidence
- method formation
- generalization
- operationalization
- attack/defense
- correction/challenge

Move broad, similar, survey, benchmark, and weak papers to adjacent work with reasons.

## Dates, Versions, and Deduplication

Use the earliest verifiable public version for timeline ordering. Record formal publication separately. Merge preprint, conference, journal, and revision versions of the same work into one timeline entry, and mark unresolved metadata conflicts explicitly. Before reporting, run a final monotonic chronology check: normalize dates as `exact`, `month`, `unknown`, or `inferred`, sort by earliest verifiable public date, and mark conflicts. Never let a later paper challenge or correct an earlier paper in reverse temporal order. Direct, continuation, challenge, and correction labels must respect both temporal direction and evidentiary direction.

## Comparative Innovation

For each core paper, record:

- inherited basis
- prior limitation
- new increment
- relationship type

Reserve labels containing `direct` or `continuation` for explicit evidence visible in primary records: a citation, stated motivation, reused setup, or documented continuation. When only mechanism similarity or concept search supports the link, label it `candidate predecessor`, `mechanistic analogue`, `parallel branch`, or `analytical inference`, and state that the citation edge is unverified.

## Saturation and Reporting

Treat the search as saturated only after two consecutive rounds with no new high-relevance core papers. Record the cutoff date, sources searched, query families used, backward/forward tracing status, screening criteria, and limitations.

## Degraded Modes

- abstract-only: use cautious claim summaries, weaker support labels, and explicit uncertainty.
- An abstract without verified metadata must not receive plain `B`; use `B-degraded` (`abstract-only; metadata unavailable`) and state the missing metadata.
- no web: rely on provided files and local metadata only; state that citation chaining could not be completed externally.
- ambiguous direction: present candidate abstractions, explain the ambiguity, and avoid over-pruning.
- no supported predecessor: report that no supported predecessor was found yet, distinguish absence of evidence from evidence of absence, and keep adjacent candidates visible.
