# Origins

For maintainers: the two Skills this one integrates, the research they came from, how the integration reorganized them, and where a predecessor's file or number now lives. Nothing in the Skill depends on this file; [cases.md](cases.md) carries the history in the depth the Skill uses.

## Contents

- [The two predecessor Skills](#the-two-predecessor-skills)
- [The research they came from](#the-research-they-came-from)
- [The integration](#the-integration)
- [From the predecessors' files to this Skill's](#from-the-predecessors-files-to-this-skills)
- [The failure patterns renumbered](#the-failure-patterns-renumbered)
- [Revising](#revising)

## The two predecessor Skills

**The System Design Skill** (`system-design`), first edition 2026-10-09: a methodology for designing, organizing, extending and revising software systems so that each structure answers to something real rather than to the convenience of describing or verifying it. It held nineteen principles (A1 to D6), twenty judgment moves (J1 to J20) with the procedure expand, reorganize, absorb or remove, nineteen failure patterns and the recognizers of excess, the working loop, and the disciplines of writing and working. Its references were `principles.md`, `judgment.md`, `writing-and-working.md`, `cases.md` (the nineteen moves of the history, E1 to E19, and twelve mechanism cases) and `literature.md`. On 2026-10-10 it was revised to join the second Skill: J7 kept its two readings and pointed to M1 for the third; the fates, the problem-side instance of B2, the atomic case under C4, which loop a unit of work is in, and several pointers were added. That revision added and pointed; it removed nothing.

**The Problem Formulation Skill** (`problem-formulation`), first edition 2026-10-10: a methodology for formulating and reformulating the problem a computational system solves, so that the problem's representation can be wrong without the work being lost. It held four understandings, twenty-two moves in four groups (F1 to F7, R1 to R7, M1 to M4, L1 to L4), the reformulation operations in three forms with their tests, fifteen failure patterns, the working loop, and a table of the places where it joined the System Design Skill. Its references were `formulation.md`, `recursion.md`, `reformulation.md`, `cases.md` (the moves of the problem's history, P1 to P18 with P5a and P5b, a reading of the cases together, and the cases recorded after the history by a trial) and `literature.md`.

Both lived in the workspace of the I⁵ project, as .claude/skills/system-design/ and .claude/skills/problem-formulation/, linked at the joins, each with its own `CHANGES.md`. After the integration they were moved, unchanged apart from a closing row in each `CHANGES.md` and three relative links re-pointed for the new location, to the research record of the round that produced them (`docs/research/02-design-principles/skills/` in the I⁵ repository), where they are kept read-only as first editions, so that only this Skill is loaded.

## The research they came from

Both Skills were produced by Round 02 of the I⁵ project, a research round on design principles. I⁵ was established on 2026-10-09 as the successor of I³, a system whose design and construction had run through nineteen research and construction rounds between 2026-09-23 and 2026-10-09 and changed its architecture many times while its direction of reasoning did not change. Before I³ there was a pre-project workspace (2026-09-15 to 2026-09-23) where the problem was first formulated and its recursive solver first framed, and after it I⁵'s own first round, which framed the new system. These are the source history named in [cases.md](cases.md) and [literature.md](literature.md).

The round ran in two phases, each under a brief from the project's owner, recorded verbatim in the round.

**The first phase (2026-10-09)** read the design and revision history of I³ and I⁵'s first round for the reasoning that produced the revisions, not for their conclusions, and asked what of it transfers to the construction of any complex software system. Eleven readers worked in parallel, ten on the history and one on the literature of system design; the lead wrote a working spine and revised it as the reports came in; five writers wrote the study's first three chapters and the System Design Skill against it. One agent applied the Skill, with nothing else about the history, to three design tasks outside its domain (an extensible editor, an over-engineered order system, an observability pipeline); one cross-reader reported twenty-four findings; the lead ruled on all of them, and two fixers applied the rulings in one pass.

**The second phase (2026-10-10)** studied the same history from the problem's side: how the problem the system solves was understood, formulated, recursively expanded and reformulated, and how problem definition and construction changed each other. The sources widened to the pre-project workspace. Eleven readers traced the problem, one of them the literature of formulation and of recursion; the lead wrote a second spine; seven writers wrote three further study chapters, the Problem Formulation Skill and a revision of the System Design Skill made only of additions and pointers. One agent applied the new Skill to three tasks outside the history's domain (a campaign of simulations hunting tipping points, a build system that kept growing special cases, and a rules engine for a claims process); its silences and misleads clustered at three premises the history held and the tasks did not (one owner of meaning; a deterministic meaning with exact answers; a system being formed rather than a live one reformulated part by part), which became the Skill's stated scope. One cross-reader reported fifty-six findings across the study's second part and both Skills; the lead ruled on all of them, and three fixers applied the rulings in one pass.

The study, the round's research deliverable, has six chapters by subject:

| Chapter | Subject |
|---|---|
| Evolution | The nineteen moves of the design history (E1 to E19): why each architecture was proposed, what pressure appeared, why it was revised |
| Principles | The nineteen principles: their derivation, mature statements, kinds (enduring, contextual, objective-bound), the tensions among them, and their relation to the literature |
| Judgment | The twenty judgment moves, the failure patterns, the procedure for expanding, reorganizing, absorbing or removing, the working method, transfers to other kinds of system, and how the methodology revises itself |
| The problem's history | The moves of the problem (P1 to P18, with P5a and P5b): the need, the formulation chosen, what it fixed and left free, what reformulated it and at what cost |
| Formulation | F1 to F7, M1 to M4 and L1 to L4; the fifteen failure patterns of the problem side; the tensions; the literature of formulation |
| Recursion | R1 to R7: what recursed and how it moved out of the runtime into the problem's derivation; identity and sharing; the atomic case; where recursion applies |

The study separates three kinds of statement: a finding reports what a document of the history says, with a locator; a derivation says why the methodology states what it does; a classification marks an example as enduring, contextual or objective-bound. The Skill's cases are short forms of the study's, ending in what each teaches.

The research record (the owner's three briefs, the study, the readers' reports, the spines, the writers' briefs and notes, the trials, the cross-readings and the rulings) belongs to the I⁵ project and is not distributed with this Skill. Nothing in the Skill depends on it. Quotations in the Skill keep their locators (for example "I³ Round 16 `POSITION.md`, 2026-10-07") as provenance, not as links to follow.

## The integration

On 2026-10-10 the owner's third brief asked that the two Skills be integrated into one self-contained Skill ready for public release: the union of the two, losing no method, principle, criterion, case, applicability boundary or reference, adding no new methodology and re-examining no conclusion; naming, structure, phrasing, cross-references and locations free to change to make one organization and remove repetition; no added layers or organizational concepts; no dependency on anything not distributed; the skill-creator's conventions followed, its evaluation loop skipped. A lead planned the work, five writers wrote the files in parallel, and one checker read the result against the two predecessors.

The organizational adjustments:

- **One name and one directory.** `problem-and-system-design`, with one `SKILL.md`, one `CHANGES.md`, a `README.md` for visitors, and nine references.
- **One core.** `SKILL.md` merges the two cores: one description carrying every trigger of both; one stance; both pictures of the result; one working loop, each step once, holding both cores' step texts; then the understandings, principles, moves, operations, failure patterns, writing and working, how the two sides join, which reference to open, and revising.
- **The joins made internal.** The predecessors' links to each other became references inside the Skill, and the phrases "of the Problem Formulation Skill", "of the System Design Skill", "the problem side's" and "the design side's" became the move or principle by name. The section "Working with the System Design Skill" and the design core's pointers to the other Skill were dissolved into the text; the problem core's join table became the section "How the two sides join", kept because it says which moves are twins.
- **The operative references kept whole.** `principles.md`, `judgment.md` and `writing-and-working.md` from the design side, and `formulation.md`, `recursion.md` and `reformulation.md` from the problem side, under their names, with their cross-references made internal and the problem side's attribution convention for quotations adopted in all six.
- **One case file.** `cases.md` tells the one history both Skills were drawn from, in order, with the design-side and problem-side lessons of each event, the mechanism cases, and the cases recorded after the history.
- **One literature register.** `literature.md` merges the two readings of the literature: one register of sources by cluster, each source once with both its uses and both readings' marks; the tensions; the restates, sharpens and departs treatments under the principles and under the move groups; the silences.
- **One list of failure patterns.** Thirty-four entries became twenty-eight in three groups (the problem, the structure, the work); merged entries keep both names and both texts; every pattern is cited by name, never by number, since the predecessors numbered them differently (the table is below).
- **No dependency on the research record.** Links into it and into the project repositories were removed; pointers to the study now go to `cases.md`, and beyond the Skill, here.
- **Project names confined.** The projects are named in `cases.md`, `literature.md`, this file, `README.md` and `CHANGES.md`, and in examples marked as examples; never in a rule of `SKILL.md` or of the six operative references.
- **Names and numbers kept.** A1 to D6, J1 to J20, F1 to F7, R1 to R7, M1 to M4, L1 to L4, E1 to E19 and P1 to P18 (with P5a and P5b) are unchanged.
- **One change record.** `CHANGES.md` carries both predecessors' rows, their citations of the research record turned into provenance text, and a row for the integration.

**What the writers merged, moved, renamed or dropped.**

- *The core.* The working loop has nine steps from the two cores' seven each: the need in its own words; the fixed meaning, the responsibilities and the guarantees; the parts in the world; the concrete object and the fates; expansion; closure; construction read three ways; revision at the premise with a record; and the switch of loops. The frontmatter description was shortened to the Agent Skills specification's cap of 1,024 characters: the two cores' purpose clauses moved into the stance, three trigger phrases were shortened ("modules" for "module structure", "brief" for "a brief for a round of work", "when a difficulty recurs" for "a system or a team keeps meeting the same difficulty"), and every other trigger of both predecessors is present. Four merged failure patterns fold two near-identical sentences into one (the imported frame; the separately granted freedom; the adjacent answer; the closure drive); the check found no idea lost in them. Dropped as repetition: the sentences each core spent pointing at the other, one checklist sentence and one "read the moves first" paragraph that both cores carried, the separate statements of the third reading (now once, in step 7), and the design core's pointer to M4, replaced by the record's own text. The four judgment-move tables gained the heading letter J to sit beside F, R, M and L.
- *The operative references.* Each is within one percent of its source's word count. Only the links, the joins, the pattern numbers, the attribution convention and the pointer to the research record changed; two phrases that named the old Skill ("of the system-design methodology") now say "of this methodology", and one parenthesis after D2 that repeated D2's name was dropped.
- *The cases.* One chronological sequence of thirteen events, each holding the design moves and then the problem moves that record it, with a table placing every E and P number. The context both files carried (the description of the source system, the three kinds of example, the "examples, not rules" sentence, the conventions for the owner and for quotations) is said once. The trial's wording became "this Skill's problem side". The locators and the *Study* pointers at the end of each case are kept as provenance; the intro says what they name.
- *The literature.* One register in seven clusters. Four sources both readings covered (Simon 1962; Alexander 1964 and 1965; Parnas 1972; Brooks 1986) appear once with both readings' marks and uses; both mark scales are kept; the problem side's source table became two lists; the two authors named Jackson carry first names.
- *The change record.* Both predecessors' rows with a column saying which Skill, their citations of the research record turned into provenance text, and a row for the integration.
- *Budgets.* `cases.md` and `literature.md` run about two percent over the plan's word budgets; the overrun is the contents and timeline tables, and no case or source text was condensed.

**What the check found.** One checker diffed the six operative references and the case bodies line by line against their sources and compared the core, the literature register and the change record section by section. Of the predecessors' items (339 counted: principles, moves, understandings, forms, failure patterns, loop steps, statement kinds, joins, premises, worked applications, cases, sources, tensions and change-record sentences) none was missing; 437 links all resolved inside the directory; 1,494 citations of moves, principles and cases were all under existing names; no failure pattern was cited by number; the two em dashes left are inside quotations. It flagged nine small things, all fixed by the lead: the placeholders this section replaced; the two quoted requests "a design" and "an architecture", restored to the description by shortening three other phrases; one sentence under regrowth and the better mechanism that blurred what D4 holds; pattern names that ran into their sentences in `reformulation.md` and `literature.md`; the wording of the separately granted freedom; a note placing E7's question under Round 08; a README sentence that promised more of this file than it holds; and this file's restatement of the revising rule, now a pointer.

## From the predecessors' files to this Skill's

| Predecessor file | In this Skill |
|---|---|
| system-design/SKILL.md and problem-formulation/SKILL.md | [SKILL.md](../SKILL.md), merged section by section as listed above; the problem core's "Working with the System Design Skill" became "How the two sides join" |
| system-design/references/principles.md | [principles.md](principles.md) |
| system-design/references/judgment.md | [judgment.md](judgment.md) |
| system-design/references/writing-and-working.md | [writing-and-working.md](writing-and-working.md) |
| problem-formulation/references/formulation.md | [formulation.md](formulation.md) |
| problem-formulation/references/recursion.md | [recursion.md](recursion.md) |
| problem-formulation/references/reformulation.md | [reformulation.md](reformulation.md) |
| system-design/references/cases.md and problem-formulation/references/cases.md | [cases.md](cases.md) |
| system-design/references/literature.md and problem-formulation/references/literature.md | [literature.md](literature.md) |
| system-design/CHANGES.md and problem-formulation/CHANGES.md | [CHANGES.md](../CHANGES.md) |
| (none) | [README.md](../README.md) and this file |

## The failure patterns renumbered

The design core numbered nineteen failure patterns (SD below) and the problem core fifteen (PF). The merged list has twenty-eight in three groups. Where a predecessor named a pattern differently, its name is given in brackets. The merged numbers are for reading the list in `SKILL.md` only; everywhere else a pattern is cited by name.

| Merged | Name | SD | PF |
|---|---|---|---|
| | *Patterns of the problem* | | |
| 1 | The imported frame | 1 | 1 (the imported problem) |
| 2 | The separately granted freedom | 18 | 2 |
| 3 | The parts list | | 3 |
| 4 | Concepts explaining concepts | 2 | |
| 5 | Procedure before object | 3 | |
| 6 | The closure drive | 4 | 9 (the closure that makes its own problems) |
| 7 | The adjacent answer | 6 | 7 |
| 8 | The convenient requirement and defensive drift | 10 (defensive drift) | 6 (the convenient requirement) |
| 9 | The frozen envelope | | 8 |
| 10 | The recollection as definition | | 11 |
| 11 | Reopening on provenance | 15 | |
| 12 | The level mismatch | | 12 |
| 13 | The channel's premise | | 14 |
| 14 | The question in the structure's vocabulary | | 15 |
| 15 | The lost intent (thinly attested) | | 13 |
| | *Patterns of the structure* | | |
| 16 | The recursion ontology | | 4 |
| 17 | The fused kinds | | 5 |
| 18 | The reification chain | 11 | |
| 19 | Uniformity for its own sake | 7 | |
| 20 | The second axis | 8 | |
| 21 | The manufactured limit | 17 | |
| 22 | Conditional promises | 19 | |
| 23 | Rename as revision | 9 | |
| 24 | Regrowth and the better mechanism | 12 (regrowth) | 10 (the better mechanism) |
| 25 | Over-trimming at the joins | 13 | |
| | *Patterns of the work* | | |
| 26 | The check layer | 5 | |
| 27 | Management for the work | 16 | |
| 28 | Polishing while unstable | 14 | |

## Revising

The rule for revising is the closing section of [SKILL.md](../SKILL.md), "Revising this Skill": what warrants a change, how the methodology is applied to itself, and where the record goes (a later case in [cases.md](cases.md), a row in [CHANGES.md](../CHANGES.md)). One thing holds for maintainers beyond that rule: revising this Skill does not amend the research record of Round 02, which is complete and read-only; where a change comes out of a project's own research or decision record, it is recorded there as well and pointed to from the row.
