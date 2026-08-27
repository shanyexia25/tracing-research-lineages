# Output Template

Use the following sections in this exact order. Place citations beside every supported claim, and label any analytical inference explicitly, for example `Inference:` or `Analytical inference:`.

## 1. Paper Metadata

Include original paper title, authors, venue, first public date, formal publication, links or identifiers, and evidence access grade.

## 2. One-Sentence Synthesis

Summarize the paper's main contribution and role in the lineage in one sentence with citation support when available.

## 3. Research Problem and Core Claims

State the research problem, then list the focal paper's core claims with citations.

## 4. Claim-Experiment Validation Matrix

| ID | Claim | Experimental design | Data/models | Baselines | Metrics | Main result | Support strength |
| --- | --- | --- | --- | --- | --- | --- | --- |

Each row must place an evidence citation in its `Support strength` or `Main result` cell; no row may leave both cells uncited.

## 5. Narrow Direction

Define the exact narrow-direction abstraction as `object + mechanism/phenomenon + purpose`, then include `Parent field`, `Synonyms`, `Scope`, and `Exclusions` as explicit fields.

## 6. Search Scope

Report these explicit fields: `Sources used`, `Concept queries`, `Backward citation tracing status`, `Forward citation tracing status`, `Screening criteria`, `Round 1 outcome`, `Round 2 outcome`, `Saturation status`, `Cutoff`, and `Limitations`. Mark `Saturation status: saturated` only after two consecutive rounds produce no new high-relevance core papers; if either round was not run, mark `Saturation status: unsaturated` and identify the unrun round.

## 7. Core Timeline

| No. | Paper | First public date | Formal publication | Stage role | Core innovation | Increment over predecessor | Relationship | Evidence grade |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

Required per-row comparative note: `Inherited basis: ...; Prior limitation: ...; New increment: ...; Relationship: ...`.

Use labels containing `direct` or `continuation` only when primary records show a citation, stated motivation, reused setup, or documented continuation; otherwise use `candidate predecessor`, `mechanistic analogue`, `parallel branch`, or `analytical inference` and state that the citation edge is unverified. Place an evidence citation beside every relationship label, especially labels containing `direct` or `continuation`.

## 8. Adjacent Work

List excluded but relevant papers with concise exclusion reasons.

## 9. Development Lineage

Organize the narrative using these elements when supported by evidence:

- origin
- validation
- method formation
- extensions
- applications
- attacks/defenses
- corrections
- focal-paper positioning
- evidence gaps
