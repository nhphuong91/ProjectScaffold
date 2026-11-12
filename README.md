# Project Scaffold

A scaffold for writing a design specification with an AI assistant, one stage at a time. The AI drafts the documents and recommends; a human Owner makes every decision; and every rule comes with Pass and Fail examples, so engineers can build and test against the specification directly. Each stage is frozen before the next one builds on it.

The scaffold is a fill-in prompt, a set of blank document templates and a guideline that explains every part. It is designed for Claude Projects: the prompt goes into the project instructions and the stage documents into project knowledge.

## Principles

- **The Owner decides; the AI recommends.** Every open question becomes an Open item with lettered options, their trade-offs and a recommendation. The AI then stops and waits for an answer such as "O1: A".
- **Every rule is testable.** Each rule has an R-number and at least one Pass and one Fail example, all built on one shared fixture.
- **What binds is kept apart from what explains.** Each stage has a normative document and a non-normative Supplement. Where they disagree, the normative document wins.
- **Frozen stages change only in the open.** A change to a frozen stage is proposed with its exact new text and logged as a decision.
- **Nothing gets lost.** Deferred items name the stage they go to, rejected alternatives keep their reason, and IDs are never reused.

## What's inside

```text
ProjectScaffold_Guideline.md     Why and how: principles, section specs, IDs, protocols
Skeleton/                        Blank files to copy into a new project
├── Project_Prompt.md            Project instructions in 11 XML-tagged blocks
├── Stage0_PolicyDefinition.md   Stage 0 normative doc: decisions, rules, schemas
├── Stage0_SupplementInfo.md     Stage 0 Supplement: terminology, decision log, evidence
├── StageN_Name.md               Normative doc for each later stage (copy and rename)
├── StageN_SupplementInfo.md     Supplement for each later stage
├── SeedData.json                Seed data with a schema id and per-row provenance
└── SampleFile/                  Your raw corpus files (git-ignored)
```

Where the guideline and a skeleton file disagree, the skeleton file governs.

## How it works

Each stage produces two files:

| File | Role | Contains |
|---|---|---|
| `Stage<n>_<Name>.md` | Normative: binding | Decisions (policy, scope, accepted limits) · Steps · Rules with Pass/Fail examples · Schemas · Open items |
| `Stage<n>_SupplementInfo.md` | Non-normative: explains | Terminology · Architecture history · Decision log · Rejected alternatives · Corpus evidence · Deferred material · Walkthrough · References |

Stage 0 holds the policy that binds every later stage; it has no Steps table and no Walkthrough. Each later stage is one transformation that produces one named output record.

A stage moves forward in working rounds:

1. You send the `<task>` block with the stage number.
2. The AI returns both files and its Open items, then stops.
3. You answer each Open item.
4. The AI logs each answer as a `D-##` row in the Supplement's Decision log, applies it to the documents and re-runs the checks listed in `<task>`.

A stage is **frozen** when its Open items section reads "None", every check in `<task>` passes and the Owner signs off.

## Quick start

1. **Copy** `Skeleton/` into a new project folder.
2. **Fill in `Project_Prompt.md`.** Start with `<context>`: the situation, a `Why:` line naming the constraints that pull against each other, and one easily misread term pinned down. List your stages in `<stages>`, write 3–5 measurable end-to-end properties in `<success_criteria>`, and give one canonical `<example>` of 1–3 lines using placeholders only. Replace every `{{…}}` placeholder; `{{Owner}}` is the person who makes the decisions.
3. **Add your evidence.** Put the raw corpus files in `SampleFile/`: the original files, never converted copies. Put seed data in a JSON file modelled on `SeedData.json`.
4. **Set up a Claude Project.** Paste `Project_Prompt.md` into the project instructions, and upload the Stage 0 pair and your seed data file to project knowledge. Leave each `<document>` body in the prompt empty when its file is in project knowledge; otherwise paste the file's contents inside the tag.
5. **Run Stage 0** in working rounds until it can be frozen.
6. **Add later stages** by copying the `StageN_` pair and renaming it for each stage (for example `Stage1_<Name>.md` and `Stage1_SupplementInfo.md`), then run each one the same way. Before you freeze a stage, run a prototype against its rule examples and the corpus, and record the method and date in its Supplement. A small project can keep to the Stage 0 pair until it needs a transformation stage.

## IDs at a glance

| ID | Names | Scope and reuse |
|---|---|---|
| `§n.m` | Section | Per document; stable once frozen |
| `S<stage>.<k>` | Step | Per stage; never reused |
| `R<n>` | Rule | Continuous across all stages; never reused, and a withdrawn rule keeps its number |
| `(a)`, `(b)`… | Accepted limit | Per §0; cited as §0.x (a) |
| `O<n>` | Open item | Restarts at O1 once the Open items section reads "None" |
| `D-<nn>` | Decision | Per Supplement; never reused, and a replaced decision stays, marked "superseded by D-##" |
| `[W<n>]` | External reference | Per Supplement |
| `[VAR]` | Variant marker, e.g. `[DOCX]` | On headings, steps, rules and fields that apply to one variant only |

## Reading the guideline

[ProjectScaffold_Guideline.md](ProjectScaffold_Guideline.md) explains every part of the scaffold. Its examples come from PseudoTool, the project the scaffold was derived from.

| Section | Covers |
|---|---|
| A · Logic brief | The nine principles behind the scaffold |
| B · Layer 1 | What to write in each block of the prompt |
| N, U · Layer 2 | The sections of the normative doc and of the Supplement |
| E · IDs | Numbering and cross-reference style |
| G · Writing conventions | Tables first, placeholders only, "None" instead of an empty section |
| F · Protocols | From question to decision, from draft to frozen, one working round |
| H · Applying the scaffold | Setting up a new project, step by step |
| C · Counterarguments | The scaffold's known costs and how it mitigates them |
| X · External benchmark | How it compares with Anthropic's prompting guidance and with spec-writing practice: W3C, RFCs, ADRs, PEPs, Example Mapping |
| P, D, W | The guideline's pending decisions, decision log and references |
