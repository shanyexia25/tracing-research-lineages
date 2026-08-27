# tracing-research-lineages

> A Codex Skill for analyzing academic papers and tracing their research lineages.

中文版本：[README.md](README.md)

## Feature Overview

`tracing-research-lineages` analyzes a paper's research problem, core arguments, experimental validation, and development lineage. It treats a paper as a research artifact that presents arguments rather than an isolated citation node, helping users answer the following questions:

| Capability | Description |
| --- | --- |
| Paper analysis | Extract the research problem, core arguments, methods, and experimental setup |
| Argument–experiment mapping | Connect major arguments to data, models, baselines, metrics, and results |
| Narrow-direction definition | Define a searchable direction as “object + mechanism/phenomenon + purpose,” with synonyms and exclusions |
| Lineage search | Combine concept search with backward and forward citation tracing to find possible predecessors and follow-up work |
| Core/adjacent screening | Separate papers that form the actual research line from papers that are only topically similar |
| Timeline reconstruction | Order work by its earliest verifiable public date and merge preprint, conference, journal, and revision versions |
| Innovation comparison | Explain the inherited basis, prior limitation, new increment, and relationship type for each core paper |
| Uncertainty reporting | Distinguish direct evidence, analytical inference, and unsupported assumptions instead of asserting unqualified completeness |

## Analysis Workflow

1. Classify the evidence level from the available full text, abstracts, and metadata: `A`, `B`, or `C`.
2. Extract the focal paper's research problem, core arguments, and argument-to-experiment mapping.
3. Build a narrow-direction abstraction with the object, mechanism/phenomenon, purpose, synonyms, and exclusions.
4. Search by concept first, then expand the candidate set through backward and forward citation tracing.
5. Screen the candidate papers, keeping lineage-relevant work in the core timeline and moving broad, similar, survey, benchmark, or application work to adjacent work.
6. Reconstruct the timeline by earliest verifiable public date while recording formal publication separately.
7. Compare each lineage node by its inherited basis, prior limitation, and new increment over earlier work.
8. Produce a structured report with evidence grades, citations, analytical inferences, cutoff date, and limitations.

## Output Structure

The final report is organized into the following nine sections, matching `references/output-template.md`:

1. `Paper Metadata`
2. `One-Sentence Synthesis`
3. `Research Problem and Core Claims`
4. `Claim-Experiment Validation Matrix`
5. `Narrow Direction`
6. `Search Scope`
7. `Core Timeline`
8. `Adjacent Work`
9. `Development Lineage`

## Usage

After installation, invoke the Skill in Codex by name:

```text
$tracing-research-lineages
```

Recommended request format:

```text
Use $tracing-research-lineages to analyze this paper and trace its research lineage.

Paper: <paper title, URL, uploaded file, or identifier>
Focus: <optional research direction, method, dataset, or argument>
Cutoff: <optional search cutoff date>
```

You can also describe the paper, research direction, or comparison scope directly. Providing the full text, reliable metadata, and accessible citation information generally produces a more defensible lineage analysis.

## Deployment Guide

### Option 1: Ask Codex to Install It (Recommended)

Send the following request in Codex:

```text
Use `$skill-installer` to install this Skill from the following GitHub repository:
https://github.com/shanyexia25/tracing-research-lineages
```

After installation, start a new Codex session and invoke `$tracing-research-lineages`.

### Option 2: Install Locally Manually (Optional)

#### PowerShell

Run the following from the repository root:

```powershell
$skillRoot = if ($env:CODEX_HOME) {
  Join-Path $env:CODEX_HOME 'skills'
} else {
  Join-Path $env:USERPROFILE '.codex\skills'
}
$targetDir = Join-Path $skillRoot 'tracing-research-lineages'

New-Item -ItemType Directory -Force -Path $targetDir | Out-Null
Copy-Item -Path .\SKILL.md, .\README.md, .\README.en.md, .\agents, .\references `
  -Destination $targetDir -Recurse -Force
```

#### macOS / Linux

Run the following from the repository root:

```bash
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
target_dir="$skill_root/tracing-research-lineages"

mkdir -p "$target_dir"
cp SKILL.md README.md README.en.md "$target_dir/"
cp -R agents references "$target_dir/"
```

Restart Codex or start a new session after installation so that the Skill is discovered again. Check the key files with:

```powershell
Test-Path (Join-Path $targetDir 'SKILL.md')
Test-Path (Join-Path $targetDir 'references\research-protocol.md')
Test-Path (Join-Path $targetDir 'references\output-template.md')
```

On macOS / Linux, use:

```bash
test -f "$target_dir/SKILL.md"
test -f "$target_dir/references/research-protocol.md"
test -f "$target_dir/references/output-template.md"
```

Then invoke `$tracing-research-lineages` in Codex.

#### Updating a Local Installation

After pulling or switching to a new version, rerun the copy command for your platform from the repository root. Keep the following layout intact, especially the `references` directory:

```text
tracing-research-lineages/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── research-protocol.md
    └── output-template.md
```

## Project Structure

```text
tracing-research-lineages/
├── SKILL.md                         # Skill instructions and analysis workflow
├── agents/
│   └── openai.yaml                  # Codex UI metadata and default prompt
├── references/
│   ├── research-protocol.md         # Evidence, search, screening, and timeline protocol
│   └── output-template.md           # Structured report template
├── README.md                        # Chinese documentation
└── README.en.md                     # English documentation
```

## Evidence and Limitations

- Prefer full text and verified metadata. When only an abstract or secondary source is available, reduce the strength of the arguments and state the downgrade explicitly.
- A research lineage is not simply a list of similar papers. Use strong labels such as `direct` or `continuation` only when primary records show a citation, explicit motivation, reused setup, or documented continuation.
- Order the timeline by the earliest verifiable public version and list formal publication separately. Mark unresolved date conflicts explicitly.
- “No predecessor found” does not mean “no predecessor exists.” Results are limited by full-text availability, search sources, query terms, and the cutoff date.
- If external search or citation-chain analysis cannot be completed, state the degraded mode and coverage boundary in the report.
