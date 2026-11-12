# Project Scaffold — Guideline

**Non-normative.** How to set up a stage-gated specification project in which an AI drafts the design documents, the Owner decides, and every rule is testable. Derived from PseudoTool (user, September 2026). Blank files → `Skeleton/`; where this guideline and a skeleton file disagree, the skeleton governs.

**Src:** 📖 PseudoTool — P = project instructions (`PseudoTool_Prompt.md`) · S0, S1 = Stage 0 / 1 normative docs · S0s, S1s = their Supplements · 🌐 [W#] = external source (§W) · 🧠 = synthesis
**Mark:** ✅ matched · 🟡 partially matched · ⚠️ risk or conflict · ✏️ changed or added vs the source project · 🔖 pending decision (§P)

| File | Role |
|---|---|
| `ProjectScaffold_Guideline.md` | This guideline: why and how |
| `Skeleton/Project_Prompt.md` | Project-instructions template; paste into the new Project's instructions |
| `Skeleton/Stage0_PolicyDefinition.md` · `Skeleton/Stage0_SupplementInfo.md` | Stage 0 pair |
| `Skeleton/StageN_Name.md` · `Skeleton/StageN_SupplementInfo.md` | Pair for each later stage; copy and rename per stage |
| `Skeleton/SeedData.json` | Seed-data file with schema header |
| `Skeleton/SampleFile/` | Raw corpus files |

---

## A · Logic brief

| ID | Principle | Mechanism | Example (PseudoTool) | Src |
|---|---|---|---|---|
| A1 | Keep what binds apart from what explains | Two files per stage; if they disagree, the normative one wins | `Stage0_PolicyDefinition.md` ↔ `Stage0_SupplementInfo.md` | 📖 P·S0s ✅ |
| A2 | Keep stances apart from behaviour | §0 Decisions cannot be tested; Rules can, and carry R-numbers | S0 §0.3 "Matching is case-sensitive" → R1 example: `JANE ROE` stays unchanged | 📖 S0 ✅ |
| A3 | Say each thing once | One R-rule per behaviour; everything else cites § or R-number | S1 §0.2: "Policy: Stage 0 §0.3 · R1" | 📖 P·S1 ✅ |
| A4 | Frozen stages change only openly | An amendment Open item carries the exact new text; once decided it becomes a D-## row in the frozen stage's Supplement | S1 O2 → S0 D-59 → S0 §0.3 updated | 📖 P·S0s·S1s ✅ |
| A5 | The Owner decides; the AI recommends | Each Open item lists options, trade-offs and a recommendation; then the AI stops | S1 O5: options A/B/C, recommends A | 📖 P·S1 ✅ |
| A6 | Every rule can be tested | At least one Pass and one Fail example per rule, all on one shared fixture | R12: runs `John D`·`oe` → `John Doe`. Fail: two strings | 📖 P·S1 ✅ |
| A7 | Nothing gets lost | A deferred item names the stage it goes to, and that stage's history records the answer; rejected ideas keep their reason | S0s §6 "Mapping R1 spans… → Stage 1" answered in S1s §2 by R13 | 📖 S0s·S1s ✅ |
| A8 | Evidence comes before decisions | Each observation names the rule it informs; measurements are dated | "2,734 runs in 151 paragraphs" → R12 | 📖 S1s ✅ |
| A9 | One example, reused everywhere | The prompt example is also the rule-example fixture and the walkthrough sample | "Party B: ABC LLC…" in P, S0 §3 and S1s §7 | 📖 P·S0·S1s ✅ |

---

## B · Layer 1 — Project instructions

**B0 · How the layers fit** 🧠

```
LAYER 1  Project instructions ─ how the AI works
         governing_documents · role · context · governing_rules · stages ·
         stage_doc_spec · open_items_protocol · edit_proposal_format ·
         success_criteria · example · task
            │ governs
            ▼
LAYER 2  Stage docs ─ 2 files per stage
         Stage0 normative ──binds──► Stage1 normative ──binds──► Stage n …
            │ explained by              │ explained by
         Stage0 Supplement           Stage1 Supplement        (normative wins)
            └─ Deferred material ──hand-off──► next stage's Architecture history
            ▲ informs
LAYER 3  Evidence & data
         SampleFile/ raw corpus · *.json seed data (schema id · row provenance) · *.md mirrors
```

| ID | Block | What to write | Example | Src |
|---|---|---|---|---|
| B1 | `<governing_documents>` | One tag per file, data files included. Status = normative or non-normative, plus draft or frozen | `Vault.json` → "non-normative, draft" | 📖 P ✅ |
| B2 | `<role>` | Seniority, three specialisms, and one sentence setting the quality bar | "…specifications that engineers can build and test against directly" | 📖 P ✅ |
| B3 | `<context>` | The situation, a `Why:` line naming the competing constraints, a pointer to the terminology, and one easily misread term pinned down | "Encrypt/decrypt is NOT cryptographic" | 📖 P ✅ |
| B4 | `<governing_rules>` | Stage 0 binds all stages; cite by § and R-number; how to amend a frozen stage; deferred items belong to the stage they name; work from the normative docs and open Supplements only when needed; when a stage is frozen | An amendment gives: reason · triggering stage · affected § · exact text | 📖 P ✅ ✏️ D-03, D-08 |
| B5 | `<stages>` | One line per stage: its status, or scope keywords including items deferred to it. Then the build order and the variant marker | Stage 2 line: "R7 source pre-scan, image classification, URL path-suffix rule", all deferred from S0s §6 | 📖 P·S0s ✅ |
| B6 | `<stage_doc_spec>` | The two files, their section lists, and the ~30-word rule | See N and U | 📖 P ✅ ✏️ |
| B7 | `<open_items_protocol>` | Options lettered A, B, C…; an Open item becomes a D-## row once decided; OI numbers restart at O1 once the section is cleared; "None" when empty | `O# \| Question \| Options \| Recommendation` | 📖 P ✅ ✏️ D-06, D-09 |
| B8 | `<edit_proposal_format>` | File, location, ADDS or REPLACES, then the exact text in a code block | "after heading ### 0.3" | 📖 P ✅ |
| B9 | `<success_criteria>` | 3–5 measurable end-to-end properties, plus "every rule is testable from its examples" | "decrypt(encrypt(doc)) … reproduces the source exactly, except IMG markers" | 📖 P ✅ |
| B10 | `<example>` | Fixture, input, output, what must NOT change, and what is only illustrative | "LLC", "Mr.", "Director" are never keys | 📖 P ✅ |
| B11 | `<task>` | `{{N}}`, the word "only", optional focus, deliverables, stop-and-wait, language, and a 5-point self-check | "…then stop and wait for the user's decisions" | 📖 P ✅ ✏️ D-07 |

**B12 · Template** → `Skeleton/Project_Prompt.md`. It is word-for-word P except the `{{…}}` placeholders and these changes:

| # | Change | Block | Basis |
|---|---|---|---|
| 1 | Header and Purpose bullet | `<stage_doc_spec>` item 1 | 📖 S1 header · ✏️ 🔖 V6 |
| 2 | Stage 0 has no Steps table and no Walkthrough | `<stage_doc_spec>` item 1 | 📖 S0 · S0s D-50 · ✏️ 🔖 V6 |
| 3 | Withdrawn items under "Dissolved without a decision" | `<stage_doc_spec>` item 2 | 📖 S0s §3 · ✏️ 🔖 V6 |
| 4 | Proposals not adopted kept as dated subsections | `<stage_doc_spec>` item 2 | 📖 S1s §6.1–6.2 · ✏️ 🔖 V6 |
| 5 | Walkthrough = canonical example plus real corpus quirks | `<stage_doc_spec>` item 2 | 📖 S1s §7 · ✏️ 🔖 V6 |
| 6 | References section | `<stage_doc_spec>` item 2 | 📖 S1s §8 · ✏️ 🔖 V6 |
| 7 | Open items numbered per round, restarting at O1 once cleared; each D-## names its OI | `<open_items_protocol>` | ✏️ D-06 (supersedes D-01) |
| 8 | Accepted limits lettered | `<stage_doc_spec>` item 1 | ✏️ D-02 |
| 9 | When a stage is frozen | `<governing_rules>` | ✏️ D-03 |
| 10 | R-, S- and D-numbers never reused; "withdrawn" and "superseded by D-##" markers | `<stage_doc_spec>` IDs line | ✏️ D-06 |
| 11 | Check 5: Supplement sections updated with each new D-## | `<task>` | ✏️ D-07 |
| 12 | Work from the normative docs; open Supplements only when needed | `<governing_rules>` | ✏️ D-08 |
| 13 | Options lettered A, B, C… | `<open_items_protocol>` | ✏️ D-09 |
| 14 | Rules are plain statements; every rule is mandatory | `<stage_doc_spec>` item 1 | ✏️ D-10 |

If the files are uploaded as Project knowledge, leave each `<document>` body empty. Otherwise paste the file contents inside the tag.

---

## N · Layer 2 — Normative doc `Stage<n>_<Name>.md`

| ID | Section | What goes in it | Table columns | Example | Src |
|---|---|---|---|---|---|
| N0 | Header | Status, which stages it binds, what governs it, a pointer to the Supplement, the variant legend, and a Purpose (what it produces, what it does not do) | prose, ≤5 lines | "Stage 1 detects nothing and writes nothing." | 📖 S1 ✏️ 🔖 V6 |
| N1 | §0 Decisions | Only statements no test can falsify. Topic subsections, with Accepted limits last | `Item \| Value`, bold stance first. Limits: `# \| Limit`, lettered (a), (b)… | S1 §0.3 (f), whitespace variants | 📖 P·S1 ✅ ✏️ D-02 |
| N2 | §1 Steps | One transformation per row; `[VAR]` if it applies to one variant only | `Step \| Input \| Action items \| Output` | "S1.3 Run-join [DOCX]" | 📖 P·S1 ✅ |
| N3 | §2 Rules | One behaviour per rule: a bold one-line rule, then the precise detail, written as a plain statement (every rule is mandatory; no "should" or "may"). Long definitions get their own §2.x subsection | `ID \| Rule`, where ID = `R<n> — Name [VAR]` | Stage 1's R11–R18 follow Stage 0's R1–R10 | 📖 P·S1 ✅ ✏️ D-10 |
| N4 | §2.x Rule examples | At least one Pass and one Fail per rule. Declare the fixture once; one row per case | `Rule \| Pass \| Fail` | "R11 — hidden text: a `w:vanish` run is extracted \| Fail: it is skipped" | 📖 S0·S1 ✅ |
| N5 | §3 Schemas | One subsection per record, stating its invariants | `Field \| Definition` | S1 §3.1: "deterministic (same source bytes, same record)" | 📖 S1 ✅ |
| N6 | §4 Open items | Only decisions that belong to the Owner, with options lettered A, B, C…; or "None" | `O# \| Question \| Options (with trade-offs) \| Recommendation` | S1 O5 | 📖 P·S1 ✅ ✏️ D-09 |
| N7 | Stage 0 differences | No Steps table and no Walkthrough. Domain sections sit between §0 and Rules | — | S0 §1 Target items, §2 Surrogate scheme | 📖 S0·S0s D-50 ✅ |

---

## U · Layer 2 — Supplement `Stage<n>_SupplementInfo.md`

| ID | Section | What goes in it | Table columns | Example | Src |
|---|---|---|---|---|---|
| U0 | Header | "Non-normative": the normative doc governs, Stage 0 terminology applies, and `[W#]` points to References | prose | S1s header | 📖 S1s ✏️ 🔖 V6 |
| U1 | §1 Terminology | Only terms this stage introduces; record what each was formerly called | `Term \| Meaning in this project \| Formerly` | Encrypted asset, formerly "token" | 📖 S0s·S1s ✅ |
| U2 | §2 Architecture history | Stage 0 records what was removed and why. Later stages answer each deferral they inherited | `Removed \| Replaced by \| Why` · `Deferral (source) \| Stage n answer` | "Mapping R1 spans…" → "Unit map + atom map (R13)" | 📖 S0s·S1s ✅ |
| U3 | §3 Decision log | D-## numbers are local to the stage and never reused; each row names the OI it closes; a replaced decision stays, marked "superseded by D-##"; the freeze is a row; amendments to a frozen stage are logged in both stages; no separate amendments section | `# \| Question \| Decision \| Lands in`, plus `Item \| Status` for dissolved items | S1 D-02 ↔ S0 D-59 | 📖 S0s D-45·S1s ✅ ✏️ D-03, D-06 |
| U4 | §4 Rejected alternatives | One line saying why not, citing a D-##, an R-number or evidence | `Alternative \| Rejected because` | "Match run by run": 3 of 18 key occurrences span 2–11 runs | 📖 S1s ✅ |
| U5 | §5 Corpus evidence | Each observation and what it informs; corpus status; measurements with method, result and date | `Observation \| Where \| Informs` · `# \| Measure \| Method \| Result` | M2 near-miss rate, re-run 2026-09-26 | 📖 S0s·S1s ✅ |
| U6 | §6 Deferred material | Every parked item names where it goes. Proposals not adopted get a §6.x subsection with date, reason, and a logic-plus-example table | `Item \| To` · `ID \| Logic \| Example` | S1s §6.1: "Not adopted: too complicated for now (user)" | 📖 S1s ✅ |
| U7 | §7 Walkthrough | The canonical example plus real quirks, traced through every step. Add a hand-off table and say how it was verified | `Step \| Definition \| Decision \| Action \| Output` | S1.4: `e`+U+0301 → `é` | 📖 P·S1s ✅ |
| U8 | §8 References | External sources, cited as `[W#]` | `ID \| Source \| Used for` | W4 UAX #15 → NFC | 📖 S1s ✏️ 🔖 V6 |

---

## E · IDs and cross-references

| ID | Item | Pattern | Scope and reuse | Example | Src |
|---|---|---|---|---|---|
| E1 | Section | `§n` · `§n.m` | Per doc; stable once frozen | Stage 0 §0.3 | 📖 ✅ |
| E2 | Step | `S<stage>.<k>` | Per stage; never reused | S1.8 Assemble | 📖 S1 ✅ ✏️ D-06 |
| E3 | Rule | `R<n> — Name` | Project-wide, continuous across stages, never reused; a withdrawn rule keeps its number, marked "withdrawn". Renumber only while the stage is draft and no other doc cites it | Stage 1 starts at R11. S0s D-13 restarted numbering at R1 while draft | 📖 S0s·S1 ✏️ D-06 |
| E4 | Accepted limit | `(a)`, `(b)`… | Per §0 | Stage 1 §0.3 (f) | 📖 S1 ✅ ✏️ D-02 |
| E5 | Open item | `O<n>` | Per round: restarts at O1 once Open items reads "None". Each D-## names its OI; the D-## is the permanent reference | O5 | 📖 P·S0s ✅ ✏️ D-06 |
| E6 | Decision | `D-<nn>` | Local to each Supplement, never reused; a replaced decision is marked "superseded by D-##". Name the file when citing across stages | "`Stage0_SupplementInfo.md` D-59" | 📖 S1s ✅ ✏️ D-06 |
| E7 | External reference | `[W<n>]` | Per Supplement | [W16] | 📖 S1s ✅ |
| E8 | Variant marker | `[DOCX]` | On headings, steps, rules and fields | "R14 — Hyperlink targets [DOCX]" | 📖 S1 ✅ |
| E9 | Data file | `schema: <stage>-<name>/<ver>`, `encoding`; rows may carry `source` | Per file. Bump the version on a breaking change 🧠 | `stage0-vault/1`; `source: corpus \| proposed` | 📖 JSON ✅ |
| E10 | Cross-reference style | `Stage 0 §0.3 · R1` · `(R13)` · `Supplement §5.3` | `·` joins several references | S1 §0.2, NFC row | 📖 S1 ✅ |

---

## G · Writing conventions

| ID | Rule | Example | Src |
|---|---|---|---|
| G1 | Use tables first. Put the binding sentence in bold, then the detail | S0 §0.3: "**L1 only.** Literal exact match…" | 📖 S0 ✅ |
| G2 | A definition over ~30 words gets a one-line summary plus its own subsection | S1 §2.3 Normalisation unit | 📖 P·S1 ✅ |
| G3 | State the edges: what the stage does not do and what is out of scope | S1 §0.1 "Out of scope — later phase" | 📖 S1 ✅ |
| G4 | Use placeholders only. Declare one fixture once and let later stages reuse it | S1 §2.4: "Placeholders and vault as in Stage 0 §3" | 📖 S0·S1 ✅ |
| G5 | Removed design leaves the normative doc; the Supplement keeps one line about it | S0s §2: "Superseded wholesale" | 📖 S0s ✅ |
| G6 | Stay in scope: anything beyond the task becomes an Open item or a deferred proposal, never a silent addition | S1s §6.2: K1–K4 recorded but not adopted | 📖 P·S1s ✅ |
| G7 | Write "None" rather than leaving a section empty | S0 §5: "None" | 📖 P·S0 ✅ |
| G8 | Write rules as plain statements; every rule is mandatory. Optional behaviour goes to §0 or Deferred material, never into a rule with "should" or "may" | R18: "A document holding any tracked-revision element… is refused at intake" | 📖 S1 ✅ ✏️ D-10 |

---

## F · Protocols

**F1 · From question to decision** (📖 P·S0s·S1s)

```
gap / question
 └► O# in normative "Open items"   (options · trade-offs · recommendation)
     │  AI stops → Owner decides
     ├─ adopt ────────► D-## in Supplement log ──► text applied where "Lands in" points
     ├─ not now ──────► D-## + Deferred material (dated proposal §6.x, reason)
     └─ hits FROZEN ──► amendment OI: reason · triggering stage · affected § · exact text
                         └► D-## in BOTH Supplements ──► text applied to the frozen doc
```

Real cases: **adopt** — S1 O3 → D-03 → §0.3 · **not now** — S1 O1 → D-01 → R18 plus §6.1 · **hits a frozen stage** — S1 O2 → S1 D-02 and S0 D-59 → S0 §0.3.

**F2 · From draft to frozen** (✏️ D-03)

```
DRAFT ──[Open items "None" · <task> checks pass · Owner sign-off]──► FROZEN ──[amendment OI only]──► FROZEN
```

Log the freeze as a D-## row in the stage's Supplement, and change its status in both `<governing_documents>` and `<stages>`.

**F3 · One working round** (📖 P · 🧠)

1. Send `<task>` with the stage number.
2. The AI returns both files plus Open items, then stops.
3. The Owner answers each Open item.
4. The AI logs the D-##, applies the text (B8 format for edits), and re-runs the checks.

---

## H · Applying the scaffold to a new project

| ID | Step | Do | Example (PseudoTool) | Src |
|---|---|---|---|---|
| H0 | Copy the skeleton | Copy `Skeleton/` into the new project folder. Paste `Project_Prompt.md` into the Project's instructions; upload the Stage 0 pair to Project knowledge | — | 🧠 |
| H1 | Frame the problem | Write `<context>` first: the situation, a `Why:` line with the tension, and one misreadable term pinned down | "the LLM provider must never see real identities, yet the LLM must still understand roles and relationships" | 📖 P |
| H2 | Split into stages | Stage 0 is policy. Each later stage is one transformation producing one named output record. A small project runs Stage 0 only (one pair) until a transformation stage appears | Stage 1 turns a DOCX into an extraction record; it "detects nothing and writes nothing" | 📖 P·S1 ✏️ D-05 |
| H3 | Build the canonical example | 1–3 lines, placeholders only. Cover the main entity types, one variant, and the scaffolding that must survive | `JOHN DOE` → `PSN00001` (a variant); "LLC" untouched | 📖 P |
| H4 | Set success criteria | 3–5 measurable end-to-end properties | Round trip; every key replaced and nothing else; nothing silently kept; rules testable | 📖 P |
| H5 | Collect the corpus and seed data | Keep the raw files, never converted copies. Seed data as JSON with a schema id and per-row provenance, plus an optional `.md` mirror | The Markdown copy of the DOCX dropped the header, so the raw file is used (S1s §5.1) | 📖 S1s·JSON |
| H6 | Write and freeze Stage 0 | §0 decisions → domain scheme → R1…Rn with Pass/Fail → schemas → Open items. Repeat until Open items is "None", then freeze (F2) | R1–R10; D-01…D-59 | 📖 S0·S0s ✏️ D-03 |
| H7 | Run each later stage | Fill in `<task>` and start from the deferred material it inherits. The AI returns two files and Open items, then stops | Stage 1 began from 5 Stage 0 deferrals | 📖 P·S1s §2 |
| H8 | Decide and apply | Answer each Open item. The AI logs the D-##, applies the text and re-runs the checks; freeze per F2 | S1 D-01…D-03 | 📖 S1s ✏️ D-03 |
| H9 | Test before freezing | Run a prototype on the rule examples and the corpus, and record the method and date | "passes every R11–R18 example (25 checks)"; M1 and M2 dated | 📖 S1s §5, §7 |

---

## C · Counterarguments

| ID | Risk | When it bites | Mitigation | Src | Decision |
|---|---|---|---|---|---|
| C1 | It's heavy: two files per stage, 11 prompt blocks, 6+ ID series | One owner, two stages or fewer, short-lived work | Stage-0-only mode: one pair until a transformation stage appears | 🧠 | D-05 |
| C2 | Freezing early forces amendments | A later stage finds a gap upstream | The amendment protocol keeps it cheap: the first downstream stage already needed one (S1 O2 → S0 D-59) | 📖 S0s | None needed |
| C3 | Project-wide R-numbers are rigid | Rules merged or withdrawn after freezing | R-, S- and D-numbers are never reused; mark them withdrawn or superseded, as RFC and ADR practice do [W6, W7]. Renumber only while draft (S0s D-13). OI numbers restart after each cleared round | 📖 S0s · 🌐 | D-06 |
| C4 | Pass/Fail examples don't give test coverage | Rules with many edge cases | The examples fix what a rule means; implementation tests must go further | 🧠 | None needed |
| C5 | Supplements drift out of date | Decisions applied to the normative doc only | Check 5 in `<task>`: update the Supplement sections a new D-## touches in the same delivery | 📖 P · 🧠 | D-07 |
| C6 | Context grows with every stage | Governing docs were ≈102 KB at Stage 1 of the source project. RAG turns on as a project nears the context window, and then only the most relevant parts are retrieved [W3, W12] | Work from the normative docs; open a Supplement only for further context, plus the Deferred material rows that name the current stage. This saves context only when Supplements are read on demand; if they sit in fully loaded Project knowledge, the rule sets priority only | 📖 · 🌐 · 🧠 | D-08 |
| C7 | "The AI must not decide" slows things down | Many small Open items | Letter the options (A, B, C…) so the Owner answers "O5: A", as S1 O5 does | 📖 S1 · 🧠 | D-09 |

---

## X · External benchmark

| ID | Scaffold element | External practice | Mark | Note |
|---|---|---|---|---|
| X1 | XML-tagged prompt blocks (B1–B11) | "XML tags help Claude parse complex prompts unambiguously"; consistent, descriptive tag names; nest tags [W1] | ✅ | — |
| X2 | Reference material first (`<governing_documents>`), `<task>` last | "Put longform data at the top… Queries at the end can improve response quality by up to 30 percent" [W1] | ✅ | Doc metadata as `name`/`status` attributes, where W1 uses `<source>` subtags: equivalent |
| X3 | `<role>` | "Setting a role in the system prompt focuses Claude's behavior and tone… Even a single sentence makes a difference" [W1] | ✅ | — |
| X4 | `Why:` line in `<context>` | "Providing context or motivation behind your instructions… can help Claude better understand your goals" [W1] | ✅ | — |
| X5 | One canonical `<example>` | "Include 3–5 examples for best results"; relevant, diverse, wrapped in `<example>` tags [W1] | 🟡 | Diversity comes from the Pass/Fail tables once docs exist; while Stage 0 is drafted the prompt holds one example only. No change proposed |
| X6 | `<success_criteria>` | Specific · Measurable · Achievable · Relevant [W2] | ✅ | — |
| X7 | Normative vs non-normative files with status labels | Label content normative or informative (Good Practice 2) [W4]; mixing reference and explanation is "bad for the reference… bad for the explanation too" [W11] | ✅ | — |
| X8 | Terms a rule depends on are defined in the normative doc (G2); Supplement §1 is the glossary | "Define the terms used in the normative parts" (Requirement 5) [W4] | ✅ | Holds only while every term a rule depends on is defined in the normative doc |
| X9 | Rule wording is declarative ("is refused") | BCP 14 key words MUST, SHOULD, MAY…, with special meaning "only when they are in all capitals" [W5] | 🟡 | Kept declarative, every rule mandatory; optional behaviour stays out of Rules (D-10) |
| X10 | Frozen docs amended in place, traced by D-## | "Once an RFC is published, it is never changed"; errata, or new RFCs that update or obsolete it [W6]. PEPs "are no longer substantially modified" after Final [W8] | 🟡 | Deliberate: the AI always reads one current text; file version history keeps the old text. No change proposed |
| X11 | Decision log D-## | ADR: Title · Context · Decision · Status · Consequences; "Numbers will not be reused"; a reversed decision is kept and "marked as superseded" [W7] | 🟡 | No Status field; a replaced decision stays, marked "superseded by D-##" (D-06), as S0s D-12 and D-40 already do inline |
| X12 | Rejected alternatives | "Those rejected ideas should be recorded along with the reasoning as to why they were rejected" [W8]; "Rationale and alternatives" [W9] | ✅ | — |
| X13 | Open items | "Open Issues" [W8]; "Unresolved questions" [W9]; Example Mapping: "capture those on a red card and move on with the conversation" [W10] | ✅ | The scaffold adds options and a recommendation |
| X14 | Deferred material | PEP status "Deferred" [W8]; "Future possibilities" [W9] | ✅ | — |
| X15 | Rules with Pass/Fail examples | Example Mapping: rules on blue cards, examples on green [W10]; "Provide examples" (Good Practice 6) [W4] | ✅ | — |
| X16 | Governing docs held in Project knowledge | RAG "automatically activates when your project approaches or exceeds the context window limits", then retrieves "only the most relevant information" [W3]; window 200K–1M tokens by model [W12] | ⚠️ | Past that point, binding docs may be read only in part. D-08 keeps the working set to the normative docs |

---

## P · Pending decisions

Answer as "V6: A". Accepted items move to §D; the skeleton follows.

| ID | Question | Options (with trade-offs) | Recommendation |
|---|---|---|---|
| V6 | Keep the six practice-derived additions (B12 rows 1–6)? They are in `Skeleton/` meanwhile | **A — Keep all.** The skeleton matches how the docs are really written · **B — Drop some** (name them). Shorter spec, but the skeleton drifts from practice | A |

---

## D · Decision log

| # | Question | Decision | Lands in |
|---|---|---|---|
| D-01 | Open-item numbering (V2) | OI numbers are unique within a stage and never reused; each D-## row names the OI it closes. **Superseded by D-06** | — |
| D-02 | Accepted-limit format (V4) | Lettered `# \| Limit` everywhere, Stage 0 included; cited as §0.x (a) | N1 · E4 · `Project_Prompt.md` `<stage_doc_spec>` · stage skeletons §0 |
| D-03 | When a stage is frozen (V5) | Open items "None", every `<task>` check passes, and the Owner signs off; the freeze is a D-## row; status changed in `<governing_documents>` and `<stages>` | B4 · F2 · U3 · `Project_Prompt.md` `<governing_rules>` |
| D-04 | Scope of this guideline | The scaffold only; improvements to PseudoTool are out of scope (V1, V3, T4 dropped) | whole document |
| D-05 | Overhead for small projects (C1) | Stage-0-only mode: a small project runs one pair (policy, rules, Open items) until a transformation stage appears. No new file | H2 · C1 |
| D-06 | ID policy (C3); supersedes D-01 | R-, S- and D-numbers are never reused: a withdrawn rule keeps its number, marked "withdrawn"; a replaced decision stays, marked "superseded by D-##"; renumber only while a stage is draft and no other doc cites it. Open items are numbered O1, O2… per round and restart at O1 once the section reads "None"; each D-## row names the OI it closes | B7 · E2 · E3 · E5 · E6 · U3 · C3 · `Project_Prompt.md` `<stage_doc_spec>`, `<open_items_protocol>` · Supplement skeletons §3 |
| D-07 | Keeping Supplements up to date (C5) | Check 5 in `<task>`: Supplement sections touched by new D-## rows (Terminology, Architecture history, Deferred material) are updated in the same delivery | B11 · C5 · `Project_Prompt.md` `<task>` |
| D-08 | Context budget (C6) | Work from the normative docs; open a Supplement only when further context is needed, and always read the Deferred material rows that name the current stage | B4 · C6 · X16 · `Project_Prompt.md` `<governing_rules>` |
| D-09 | Faster answers from the Owner (C7) | Open-item options are lettered A, B, C…; the Owner answers "On: A" | B7 · N6 · C7 · `Project_Prompt.md` `<open_items_protocol>` |
| D-10 | Wording of rules (X9) | Plain statements of fact; every rule is mandatory; optional behaviour goes to §0 or Deferred material, never into a rule with "should" or "may" | N3 · G8 · X9 · `Project_Prompt.md` `<stage_doc_spec>` |

---

## W · References

| ID | Source | Used for |
|---|---|---|
| W1 | Anthropic, [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) | XML tags · role · examples (3–5) · long documents first, query last (up to 30 %) · context and motivation |
| W2 | Anthropic, [Define success criteria and build evaluations](https://platform.claude.com/docs/en/test-and-evaluate/develop-tests) | Specific · Measurable · Achievable · Relevant |
| W3 | Anthropic Help Center, [Retrieval augmented generation (RAG) for projects](https://support.claude.com/en/articles/11473015-retrieval-augmented-generation-rag-for-projects) | RAG near the context limit; retrieval instead of full load |
| W4 | W3C, [QA Framework: Specification Guidelines](https://www.w3.org/TR/qaframe-spec/) (2005-08-17) | Good Practice 2 normative vs informative · Good Practice 6 examples · Requirement 5 terms |
| W5 | IETF, [RFC 8174](https://www.rfc-editor.org/rfc/rfc8174) (May 2017) | BCP 14 key words; meaning only in capitals |
| W6 | IETF, [About RFCs](https://www.ietf.org/process/rfcs/) | Published RFCs never changed; errata; updated or obsoleted by new RFCs |
| W7 | M. Nygard, [Documenting Architecture Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions) (2011-11-15) | ADR sections; numbers not reused; superseded decisions kept |
| W8 | Python, [PEP 1](https://peps.python.org/pep-0001/) | Statuses; Rejected Ideas; Open Issues; no substantial change after Final |
| W9 | Rust, [RFC template](https://github.com/rust-lang/rfcs/blob/master/0000-template.md) | Rationale and alternatives; Unresolved questions; Future possibilities |
| W10 | M. Wynne, [Introducing Example Mapping](https://cucumber.io/blog/bdd/example-mapping-introduction/) (2015-12-08) | Rules, examples and questions as separate cards |
| W11 | Diátaxis, [Reference and explanation](https://diataxis.fr/reference-explanation/) | Keep reference and explanation apart |
| W12 | Anthropic Help Center, [How large is the context window on paid Claude plans?](https://support.claude.com/en/articles/8606394-how-large-is-the-context-window-on-paid-claude-plans) | 200K, 500K or 1M tokens depending on model |
