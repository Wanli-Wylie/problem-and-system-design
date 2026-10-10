# Cases

The cases the methodology was drawn from: one system's history, told in order as one sequence of events, with the design moves E1 to E19 and the problem moves P1 to P18 (with P5a and P5b) that record it; twelve mechanisms whose lifecycle ran across several moves; and the cases recorded after the history, when the methodology was first applied to tasks outside it. They are examples, not rules: read a case to see a principle or a move under pressure, and do not import its answer.

This file is the history, and it names the projects of that history: I³, its successor I⁵, and axle, the workspace that preceded I³. The names are historical labels. The Skill depends on nothing outside its own directory, and in its rules and operative references these projects appear, if at all, as marked examples.

**How a case is told.** A design move (E) gives the situation and the form the design took, the pressure on it and the revision, and ends in what it teaches, named by the principle in [principles.md](principles.md) and the judgment move in [judgment.md](judgment.md) it supports. A problem move (P) gives the need at the time, the formulation chosen, the pressure that bore on it, the reformulation and its form, and the lesson by the move or two it teaches best, among F1 to F7 ([formulation.md](formulation.md)), R1 to R7 ([recursion.md](recursion.md)) and M1 to M4 and L1 to L4 ([reformulation.md](reformulation.md)). A field with nothing to report is left out. Where E-moves and P-moves concern one event or period, they stand together under one heading for it, the design moves first; an event that only one side recorded stands alone. Failure patterns are cited by name, as the failure-pattern list in `SKILL.md` names them.

**Two vocabularies recur.** A reformulation takes one of three forms: a *re-rendering* asks the same thing in a form that changes the cost of solving (tested by equivalence of what is asked); a *replacement* solves a different problem in the original's service (tested by whether the answer transfers back); a *change of what is asked* moves the ends, the claim or the level (tested only by whether those who rely on the answer accept it). Each case ends in the kind of the example: *enduring* (it would hold for any system), *contextual* (it depends on a technology) or *objective-bound* (it follows from what the system was for and could change with it).

**Sources.** "The owner" is the person who held the system's meaning. Quotations are the owner's unless marked as agents' or the lead's text. The cases stand on their own. Their locators point into the research record of the project named: I³'s are relative to the research directory of the I³ repository, and axle's to `axle/`, whose documents carry few dates and are cited by round. The *Study* pointer at the end of each case names the section of the research study under which the case is told in full, with its locators and the dead ends this file condenses. That record, the study included, is described in [origins.md](origins.md) and is not distributed with the Skill.

## Contents

- [What I³ was](#what-i³-was)
- [Where each move sits](#where-each-move-sits)
- [The history](#the-history)
  - [Before I³: the axle workspace (about 15 to 23 September 2026)](#before-i³-the-axle-workspace-about-15-to-23-september-2026)
  - [I³ Round 01: the blueprint (2026-09-23)](#i³-round-01-the-blueprint-2026-09-23)
  - [Rounds 02 to 04: the problem space and four rulings (2026-09-23 and 2026-09-24)](#rounds-02-to-04-the-problem-space-and-four-rulings-2026-09-23-and-2026-09-24)
  - [Rounds 05 and 06: from the generic model to the concrete object (2026-09-24 to 2026-09-26)](#rounds-05-and-06-from-the-generic-model-to-the-concrete-object-2026-09-24-to-2026-09-26)
  - [Round 07: constructive contact and the fates (2026-09-26)](#round-07-constructive-contact-and-the-fates-2026-09-26)
  - [Round 08: runs as processes, and where computations come from (2026-09-26)](#round-08-runs-as-processes-and-where-computations-come-from-2026-09-26)
  - [Round 09: workers and drivers (2026-09-27)](#round-09-workers-and-drivers-2026-09-27)
  - [Round 10: the baseline (about 2026-09-28)](#round-10-the-baseline-about-2026-09-28)
  - [Round 11: the skeleton (2026-09-28)](#round-11-the-skeleton-2026-09-28)
  - [Rounds 12 and 13: the canonical division, and computation against execution (2026-09-29 to 2026-10-01)](#rounds-12-and-13-the-canonical-division-and-computation-against-execution-2026-09-29-to-2026-10-01)
  - [Round 14: the closed design (2026-10-01)](#round-14-the-closed-design-2026-10-01)
  - [Rounds 15 to 19: construction, the runtime ontology and commitment trimming (2026-10-02 to 2026-10-09)](#rounds-15-to-19-construction-the-runtime-ontology-and-commitment-trimming-2026-10-02-to-2026-10-09)
  - [I⁵ Round 01: three to five (2026-10-09)](#i⁵-round-01-three-to-five-2026-10-09)
- [Reading the cases together](#reading-the-cases-together)
- [Mechanism cases](#mechanism-cases)
  - [Run endings](#run-endings)
  - [The Commit and the frontier](#the-commit-and-the-frontier)
  - [Instruction kinds](#instruction-kinds)
  - [Outcomes](#outcomes)
  - [Knowledge delivery](#knowledge-delivery)
  - [Qualification](#qualification)
  - [Capability](#capability)
  - [Drivers](#drivers)
  - [Hosts, formations and their lifecycles](#hosts-formations-and-their-lifecycles)
  - [Descriptions](#descriptions)
  - [Accounting and bounds](#accounting-and-bounds)
  - [Check layers](#check-layers)
- [Cases recorded after the history: the trial](#cases-recorded-after-the-history-the-trial)

## What I³ was

I³ (Infrastructure, Interpreter, Intelligence) was a distributed runtime for tensor computation on scientific clusters, designed and partly built from 23 September to 9 October 2026. A computation was a *Program*: an immutable set of tensor equations in a small language, *Tensor IR*, which fixed what is computed and said nothing about how. A *Run* executed one Program. One *Interpreter* process at a time held the Run under a lease in etcd (the *agreement service*), decided how to decompose, place and implement the work, and sent *Instructions* (units of work with fixed content: Apply, Transfer, Load, Store and others) to *Infrastructure*: a *node control* process per node, which started *native hosts* (child processes owning CUDA, PJRT, MPI or Python state) for *places* on the node, and *formations* where native state spanned nodes. Progress was made durable as a *chain* of create-once commit records in an object store, so a lost Interpreter could be replaced and the Run resumed. *Intelligence* was the work of producers outside any Run: implementations, decision methods and *knowledge sets*.

One owner, who held the system's meaning, worked it out with teams of AI agents through nineteen research rounds in seventeen days. Each round kept the owner's direction verbatim, the agents' briefs, reports and rulings, and a deliverable. Design rounds alternated with construction rounds in which agents built the Rust code in goal cycles, and construction was read back as evidence about the design. The design grew to about 316,000 words (Round 14), was reshaped by asking which of its nouns had to exist in running software (Round 16), and was trimmed by asking which of its commitments it needed at all (Round 18). On 9 October 2026 the owner retired it for a successor, I⁵, which keeps I³'s fixed meaning and floor and makes the strategy for carrying out a computation a program that is produced, hosted and improved. Almost all of its architecture was revised. The substantive revisions moved one way, and where a ruling went the other way the owner later reversed it with a reason in the same direction; that direction is what the methodology records.

Before I³, a workspace called axle (about 15 to 23 September 2026) framed the same need, first as a recursive execution model written by the owner and then as a control kernel over a declarative tensor language.

## Where each move sits

Each row is one event or period of the history, in order, with the moves told under it; each number links to its move. Rounds are I³'s unless marked.

| Event | Dates | Design moves | Problem moves |
|---|---|---|---|
| [Before I³: the axle workspace](#before-i³-the-axle-workspace-about-15-to-23-september-2026) | about 15 to 23 September 2026 | none | [P1](#p1--the-declarative-restriction), [P2](#p2--from-a-scheduler-to-an-execution-model), [P3](#p3--the-recursive-worker), [P4](#p4--the-framework-replaced), [P5a](#p5a--cursor), [P5b](#p5b--policy-and-handoff), [P6](#p6--two-machines) |
| [I³ Round 01: the blueprint](#i³-round-01-the-blueprint-2026-09-23) | 2026-09-23 | [E1](#e1--the-blueprint) | [P7](#p7--three-responsibilities) |
| [Rounds 02 to 04: the problem space and four rulings](#rounds-02-to-04-the-problem-space-and-four-rulings-2026-09-23-and-2026-09-24) | 2026-09-23 and 2026-09-24 | [E2](#e2--removing-the-database-frame), [E3](#e3--indexing-without-designing) | [P8](#p8--the-problem-space), [P9](#p9--four-rulings) |
| [Rounds 05 and 06: from the generic model to the concrete object](#rounds-05-and-06-from-the-generic-model-to-the-concrete-object-2026-09-24-to-2026-09-26) | 2026-09-24 to 2026-09-26 | [E4](#e4--the-generic-model-closed), [E5](#e5--the-concrete-object) | [P10](#p10--the-map-not-the-specification) |
| [Round 07: constructive contact and the fates](#round-07-constructive-contact-and-the-fates-2026-09-26) | 2026-09-26 | [E6](#e6--constructive-contact-and-flow-pressure) | [P11](#p11--the-fates) |
| [Round 08: runs as processes, and where computations come from](#round-08-runs-as-processes-and-where-computations-come-from-2026-09-26) | 2026-09-26 | [E7](#e7--runs-as-processes-no-mini-os) | [P12](#p12--where-computations-come-from) |
| [Round 09: workers and drivers](#round-09-workers-and-drivers-2026-09-27) | 2026-09-27 | [E8](#e8--the-driver-axis-removed) | [P13](#p13--flat-types-recursive-ownership) |
| [Round 10: the baseline](#round-10-the-baseline-about-2026-09-28) | about 2026-09-28 | [E9](#e9--unfolding-and-closing-layers) | none |
| [Round 11: the skeleton](#round-11-the-skeleton-2026-09-28) | 2026-09-28 | [E10](#e10--the-skeletons-checks-removed) | none |
| [Rounds 12 and 13: the canonical division, and computation against execution](#rounds-12-and-13-the-canonical-division-and-computation-against-execution-2026-09-29-to-2026-10-01) | 2026-09-29 to 2026-10-01 | [E11](#e11--the-canonical-division-and-the-lifecycle-repository), [E12](#e12--authority-into-the-rounds-computation-versus-execution) | [P14](#p14--mechanical-composition-not-a-second-solver-computation-against-execution) |
| [Round 14: the closed design](#round-14-the-closed-design-2026-10-01) | 2026-10-01 | [E13](#e13--the-closed-self-explaining-design) | [P15](#p15--five-structures-three-recursions) |
| [Rounds 15 to 19: construction, the runtime ontology and commitment trimming](#rounds-15-to-19-construction-the-runtime-ontology-and-commitment-trimming-2026-10-02-to-2026-10-09) | 2026-10-02 to 2026-10-09 | [E14](#e14--construction-and-the-check-layer), [E15](#e15--the-runtime-ontology), [E16](#e16--behaviour-decides-not-names), [E17](#e17--commitment-trimming), [E18](#e18--tests-are-not-the-frontier) | [P16](#p16--the-decision-is-a-function), [P17](#p17--construction-as-evidence-about-the-problem) |
| [I⁵ Round 01: three to five](#i⁵-round-01-three-to-five-2026-10-09) | 2026-10-09 | [E19](#e19--from-three-to-five) | [P18](#p18--three-to-five) |

## The history

### Before I³: the axle workspace (about 15 to 23 September 2026)

The problem's history begins before I³, in the workspace that framed the need first; only problem moves record this period.

#### P1 · The declarative restriction

**Need.** Scientific simulation codes, such as an Earth-system land-surface model and a coupled atmosphere and land model of about 12,700 and 448,000 lines: populations of entities, relations among them, time at several rates, opaque numerical kernels. The owner never stated the need in his own words in the workspace; it is visible through the codes an axle usage survey read (Round 09) and through the language built for them.

**Formulation.** The need became a computational problem by a choice of representation. The owner's framing (`IDEA.md`, undated, read 2026-09-15): a declarative model is "to deliberately restrict the expressive freedom of a program so that information such as computation structure, data dependencies, local computation, and communication requirements becomes explicitly exposed. These restrictions, in turn, create greater implementation freedom". The model fixed logical structure when a program was formed ("A **structural change** is a **different program**", agents' text, axle Round 09) and left placement, scheduling, movement and storage free. The same round gave every matter one of three homes: the declaration, the runtime when it finds the machine, the runtime as the run goes (agents' text).

**Pressure.** The usage survey found that declarations with no consequence for lowering had zero real uses in about 460,000 lines, and named two structures the model did not obviously cover. The static-formation law excluded adaptive refinement and changing populations. The language's own assumption list, written "so that a later round can tell a failed assumption from a failed detail" (agents' text, axle Round 06), predicted where it would later be questioned: I⁵ Round 01's open questions on non-tensor data and streams land on its items.

**Reformulation.** The restriction was revised rarely and on stated evidence: mostly by narrowing or by relocating a matter to the party that could act on it (P12, P14, P16), and once by admitting three operations a performance criterion showed the solver had to see (P14). In every stage the language was two lists, what it fixed and what it left free; only the line moved. *Form:* the founding formulation; its later revisions were re-renderings, each stated as a revision of the fixed meaning.

**Lesson.** F1 The fixed meaning: a formulation is two lists, and a restriction earns its place by what the solver derives from it ("Nothing else earns a body", agents' text, axle Round 06, of the language's built-in operations). The assumption list as a forecast of failure is F6's practice.

*Kind:* the cut is enduring in its general form (fixed by the formulation; bound when the environment is known; decided during operation), and its form here (fixed at formation, decided at opening, decided as the run goes) is objective-bound; the tensor language, its grain and its line are objective-bound. *Study:* P1 · The declarative restriction.

#### P2 · From a scheduler to an execution model

**Need.** The same need, now asked of the runtime. Two earlier tensor runtimes existed in the owner's line.

**Formulation.** `IDEA.md` opens: "My current understanding of the runtime has gradually shifted from that of a scheduler designed for a particular class of tensor programs toward a much more general execution model." The question, "can there exist a relatively generic runtime model that progressively realizes this logical computation as actual execution through a unified mechanism?", is followed at once by "I currently believe that such a runtime can be built around a recursive worker hierarchy."

**Pressure.** None recorded. "Gradually shifted" names a process, not an event, and no failure of the scheduler is cited. The reformulations of the origin cite a conflation or a wrong object, never insufficient capability.

**Reformulation.** Widened: "no longer merely a high-performance scheduler for tensor computation, but a more general organizational principle". The scheduler's problem survived as one instance ("a complex distributed JAX computation can be treated in exactly the same way as a single kernel"). *Form:* replacement; its test, whether the answer transfers back to the original, was met by keeping the tensor case as an instance. Its cost appeared as a negative finding: axle's knowledge rounds found the earlier systems supplied "no precedent for four things SYSTEM.md commits to" (lead's text), which marked where the new formulation was newest and least tested.

**Lesson.** The question already carried the shape of the mechanism expected to answer it: a uniform mechanism at every level. This is the tension of the question shaped by its mechanism (F1 against R1): state the restriction separately from the expectation of a uniform mechanism, so that the history of the mechanism can revise the expectation without touching the restriction.

*Kind:* the widening is objective-bound; that a question can carry its mechanism is enduring. *Study:* P2 · From a scheduler to an execution model.

#### P3 · The recursive worker

**Need.** A runtime that realizes a declared computation through one mechanism at every level, with no central scheduler "possessing complete knowledge of the entire system".

**Formulation.** A worker "is first and foremost a logical unit of execution responsibility" holding "some amount of resource capacity"; it observes, decides and acts, refining its responsibility into sub-workers of the same kind or realizing it through an opaque mechanism. Realizations may be reopened downward, and a stable recurring subtree lifted upward into a new instruction, which the owner called "recursive closure" and "one of the most important properties of the runtime model". Intelligence is "a producer of runtime abstractions, not a replacement for runtime authority". The tree "represents responsibility, delegation, and resource ownership rather than the complete dependency structure", and "A worker is not a synonym for a thread, process, or node" (all `IDEA.md`).

**Pressure.** The framing did not say how a portion of responsibility is named; a sub-problem had only a place in the tree. Later forms supplied identity each time from the representation every party shares (anchors in a DAG, then restrictions of the IR "divided and reassembled by the IR's own algebra"), never from the tree. The history had no precedent for recursive capacity delegation, and "No reviewed generation supported discovering a recurring subtree and re-encapsulating it" (agents' text, axle Round 02, RS-37).

**Reformulation.** Not one event. Over P4 to P16 what recursed moved from a holder (a worker with capacity) to a decider and then to a derivation; capacity left the kernel (P5a); lifting was never built and not restated, with no reason recorded. What survived was recursion as logical, not physical, and Intelligence outside authority, which I⁵ recovered at a higher level (P18).

**Lesson.** R2 Identity by description, by its counter-case: a sub-problem named by its position cannot be named by a second party. The fused kinds: responsibility and capacity were one hierarchy because both recurse.

*Kind:* the worker tree is objective-bound to the first framing; the lessons are enduring. *Study:* P3 · The recursive worker.

#### P4 · The framework replaced

**Need.** A software system to be built, not only a runtime idea.

**Formulation.** `SYSTEM.md` opens: "Axle aims to treat “how a logical computation should be realized” as a control problem that is continuously solved, rather than first fixing a decomposition into tasks and then scheduling those tasks for execution." A decision chooses region, assignee, implementation, resources and conditions together: "These choices are coupled." The owner limited his own mechanism: "Recursion is a way to organize and solve a coupled problem, not an assumption that all subproblems are naturally independent." The program's graph, the responsibility structure and physical execution have "no unique structural isomorphism" (§§IV, VI).

**Pressure.** Before the replacement, the archived line under `IDEA.md` had specified its way down to a Rust architecture with no implementation, and one of its rounds was reduced: "The earlier five-component framing mixed execution objects with conditions of valid execution. It is superseded as the core model, not discarded as research" (lead's text, axle archived Round 02). Its five components had come from a deletion test asking which failure each concept's absence allows, so conditions of safe execution had become the model's objects. Why `SYSTEM.md` replaced `IDEA.md` is not recorded, and the study does not invent a reason.

**Reformulation.** Replacement of the framework, and inside it separations of what was fused: the model from its validity conditions, responsibility from dependency. Reopening, lifting and capacity delegation were not restated. An amendment of 2026-09-22 recorded that the worker tree is "formed by rule outputs (effect, delegation, handoff, termination) rather than kept as separate structures". *Form:* replacement of the frame, with re-renderings by separation. The separations relocated weight rather than removing it: "The model describes organization, not a complete specification of a valid Axle execution" (lead's text), and validity became a premise someone had to supply.

**Lesson.** M2 The operation: separate what was fused, and name the owner that now carries what moved. R7 Coupled or independent: the coupling is stated, never assumed away.

*Kind:* enduring; the joint decision as the unit is objective-bound. *Study:* P4 · The framework replaced.

#### P5a · Cursor

**Need.** The control kernel that axle Round 03 had left "a black box with four named commitments" (joint decision, a tree of delegated responsibility, recursive capacity, reopening and lifting), with capacity accounting assigned to the kernel as "the generic mechanism of the worker tree; no precedent" (agents' text).

**Formulation.** Axle Round 04 (revised with Round 05 on 2026-09-17): "Axle owns one thing: **event-driven recursive advancement of a bounded dependency structure the runtime describes**" (agents' text). The unit was a cursor with a fixed region, obligations, inherited conditions, rules, a lifecycle and a mailbox, running one six-step turn; "Recursion is the same control mechanism applied across scopes of responsibility; there is no second kind of controller and no level at which the loop changes" (agents' text). The cursor was both the concept and a resident runtime object.

**Pressure.** The owner's guidance, preserved only as the agents rendered it, came in two passes. The second removed an agreement primitive, a decision stream and properties that a distributed-systems model would need. The third moved feasibility, applicability and capacity out of the kernel: "The kernel accounts no resource: no budget, no capacity, no dimension, no reservation, no ceiling" (agents' text, specification §14.6).

**Reformulation.** Narrowed by removing an imported frame (a re-rendering), and capacity moved to another owner, the runtime's rules (a change of what is asked). The first framing's "responsibility and capacity travel together" lost its second half. The cost arrived later: once control became a one-off activation (P5b), eleven of the cursor specification's twenty-five invariants "have no object left to hold of" (agents' text, axle Round 13).

**Lesson.** The recursion ontology: the problem's recursion was given a resident object with state. F3 Intrinsic or attached gains the round's basis test: an element exists "because of custody, lifetime, invariant enforcement, mutation authority, a crossing, or an explicit obligation it discharges, never because a duty can be named" (agents' text).

*Kind:* the cursor is objective-bound; the basis test and the lesson about residence are enduring. *Study:* P5a · Cursor.

#### P5b · Policy and handoff

**Need.** A concrete architecture for the tensor runtime, asked in eight charges within one round (axle Round 12, 2026-09-18 to 09-20, with Rounds 13, 15 and 16).

**Formulation and pressure.** Three forms were each rejected by a charge that named an imported assumption. A plan formed outside the kernel: "`PlanCore`, `MemberPlan`, and the associated mechanisms have created an independent planning and execution decision system outside of Axle." One kernel per member of a distributed job: "Distribution is an operational environment, not a principle of program organization that Axle must adhere to." Sessions emerging over a node service, rejected by the fourth charge: "An "Axle" should be understood as a one-off, stateless decision activation, rather than a persistent session, agent, or control process." The lead's audit found that sessions, nested controls, hosting and their patches "exist only because a control object persisted". The sixth charge widened what recursed: "I want recursion to organize decision-making responsibilities and expertise, not merely to decompose computational problems." Policies of declared scope designated one another, and a delegation became "a joint transition of three things: responsibility ..., authority ..., and knowledge" (agents' text). The seventh barred "a new permanent center that must understand, aggregate, and trim the entire world" (all axle Round 12 `commission.md`). A measurement of the built persistent control, attached to Round 12's evidence after the fourth charge, found its per-turn cost "grows super-linearly above about 800 units", dominated by copying the control's state each turn; it confirmed the removal of residence rather than triggering it.

**Reformulation.** Residence removed (a re-rendering: structure dissolved, not answered); the referent of recursion widened from computation to decision responsibility (a change of what is asked). A region was named once in the global space and held as a different problem value by each policy; the handoff was the only conversion. Six of the seven reformulating charges named something to remove before saying what to build; the positive arrived with a unifying noun, "data, and transformations applied to data".

**Lesson.** R3 Derived, not stored: a resident object manufactured structure, and "recursion is not runtime structure", stated in Round 04, was violated twice through distribution until the owner's reading, not the principle, removed each violation. R7 gains its hard limit: a block-local run over more than one exchange interval is not convex, so parts that exchange while running are "a **joint execution**" (agents' text).

*Kind:* recursion of decision authority is objective-bound (the literature has no counterpart); the convexity limit is contextual; removing residence is enduring. *Study:* P5b · Policy and handoff.

#### P6 · Two machines

**Need.** How host memory under the distributed communication library reaches GPU computation, which opened the question of what the runtime's world is (axle Round 21, about 2026-09-23).

**Formulation.** "Recursion is the control side's way to break down problem complexity. ... Recursive levels correspond to problem decomposition, not node, process, MPI-rank, resource-pool, or authorization-tree levels" (agents' text, `21-vm/01-system-model.md`). A control machine and a distributed tensor machine were found to be "two independent objects" (agents' text); "node runtimes do not know about recursive Rules" (agents' text). The owner's words are not in the workspace: the record says "the user explicitly chose two crates".

**Pressure.** Not recorded.

**Reformulation.** The two machines were separated (a re-rendering), and a guarantee was dropped: the round removed "recursively allocate capacity and rely on the entire control tree to guarantee global plan feasibility" from the core (a change of what is asked). Local admission against current facts remained.

**Lesson.** R4: a level of the problem is not a node, a process, a rank, a pool or an authority. R7: a global feasibility proof over the tree is a manufactured requirement; the coupling is carried as facts at admission.

*Kind:* the two-crate split is objective-bound; separating the problem's recursion from the resource hierarchy is enduring. *Study:* P6 · Two machines.

### I³ Round 01: the blueprint (2026-09-23)

#### E1 · The blueprint

**Situation and form.** Round 01 (2026-09-23) set the system out from the owner's conversation as three kinds of responsibility: realizing what has already been chosen, advancing the current problem, and making better decisions in the future. The round insisted the cut was by responsibility, not package: "their number is not dictated by the three initials" (round text, `01-system-model/docs/01-system-model.md`). Packages, processes and directories were to follow real dependencies, not the number three. Proposing a method was kept apart from the authority to change a running computation.

**What happened to it.** The blueprint was never amended; later rounds re-cut its interior. A day later the boundary between Interpreter and Infrastructure was redrawn (E2); Round 18 restated the three responsibilities with new contents and added a second triple for the whole system: control of real resources, correctness of results, persistence of progress.

**Lesson.** A design starts from the few things it is answerable for and lets packages and processes follow real dependencies: A1 · Responsibilities before mechanisms and C2 · Boundaries from responsibility, not symmetry. The round's test of a responsibility (its problems can be named separately, each in an existing field's vocabulary) is an early form of J1 The responsibility question.

*Kind:* the responsibility cut is enduring; I³'s three responsibilities are objective-bound. *Study:* E1 · The blueprint.

#### P7 · Three responsibilities

Same event as [E1 · The blueprint](#e1--the-blueprint), seen from the problem's side.

**Need.** A starting point for I³ (Round 01, 2026-09-23), formed from a conversation with the owner.

**Formulation.** The system's three layers answer "how to realize what has already been chosen, how to advance the current problem, and how to make better decisions in the future"; "Maturity means the problems can be named separately", each part in an existing field's vocabulary, and "Existing systems are implementation references for these problems, not the architectural substance itself"; "Recursion is the decomposition of a logical problem, not a tree for allocating nodes, processes, or resources" (round text, `01-system-model/docs/`). The evaluator's work was split into what fixed semantic operations derive and what improvable knowledge chooses.

**Pressure.** The round's open boundaries carried two frames it did not mark: a "prior authorization" within which a local executor may arrange things, and a request-processing vocabulary of repeated submissions and replay. Both were removed a day later (P9).

**Reformulation.** The problem was restated at a higher level, as three questions with owners instead of a runtime with a mechanism. *Form:* change of what is asked.

**Lesson.** F4 Named in the world: a problem is mature when its parts can be named in existing fields, and a named part is asked of the world first. R6 Fixed derivation, free choice (the control test), in its first form.

*Kind:* the cut by responsibility is enduring; the three responsibilities are objective-bound. *Study:* P7 · Three responsibilities.

### Rounds 02 to 04: the problem space and four rulings (2026-09-23 and 2026-09-24)

#### E2 · Removing the database frame

**Situation.** Round 02 turned the blueprint into a problem space of 79 problems before any design. Much of it came from distributed-systems habit: request identities so a resubmission is safe, deduplication scopes, quarantine for effects in limbo, exactly-once classes, and a "pre-authorized latitude contract" granting Infrastructure a policed freedom inside each request, ranked first among the load-bearing problems.

**Revision.** On 2026-09-24 the owner issued four rulings (`02-subsystem-problems/appendices/A-premises.md` §D). D-1: "I³ does not adopt a database-style mental model of transactions, rollback, or retry. The system's own semantics are that reality progresses forward in one direction"; a repetition is a new decision over a newly observed state, and "no mechanism for these concepts is to be designed." D-2: admitted implementations are equivalent by default. D-3: a hard boundary between decision and execution, where an instruction's freedom "is defined by the semantics of that abstraction or instruction itself, not granted by a vague, independently existing principle of 'execution latitude'". D-4: a capability absent from the first build is not prohibited, and a possible future need is no reason to embed complexity now. Retired questions got nothing designed in their place. What survived D-1 was the observation half: stable identities, "what happened to this request", unknown as a state of knowledge. Round 18 later narrowed D-1 by its own reason, keeping no-resend only where a repeat is a second real effect.

**Lesson.** The imported frame, removed as a family. Keep the observation, drop the guarantee (B5 · One path for loss), and narrow a discipline by its reason, not by counting exceptions. D-3 is the sharpest form of A3 · Fix meaning, free execution: latitude belongs to the definition of what it applies to, and a separately granted freedom (the failure pattern of that name) has an edge someone must police; one ruling dissolved the top-ranked problem. D-4 is C4's rule on absences.

*Kind:* forward-only recovery without compensation is objective-bound (it suits computations whose loss is cheaper than a coordination layer); one loss story and latitude as definition are enduring. *Study:* E2 · Removing the database frame.

#### E3 · Indexing without designing

**Situation and form.** Rounds 03 and 04 indexed about two million words of earlier research onto Round 02's problems, under strict rules: no design, no argument; record a gap rather than fill it from general knowledge; an owner ruling is only the owner's own words.

**Pressure.** A review checked the entries marked "settled by ruling" against the rulings' words. Of 18, four settled cleanly, five cited a real ruling that answered a neighbouring question, and nine cited no owner ruling at all. And the problem the map ranked first, on which four of five independent cuts agreed, was dissolved a day later by D-3.

**Revision.** The amendment after the rulings used "settled" for 8 of 332 sub-questions, only where a ruling's words answered the sub-question's words directly.

**Lesson.** The adjacent answer: a filled schema or a label of settlement is taken for understanding. Convergence on where a problem lies does not show it is a problem. The list a design is tested against is itself a representation, open to the responsibility question at the next level (D4 · Revise at the level of premises). The remedies the history found later are J18 The fates (re-ask an inherited problem of the present object instead of trusting its standing) and J20 Comparators (convergence on where a problem lies is a claim with a stated confidence, not a verdict).

*Kind:* enduring, a point of method. *Study:* E3 · Indexing without designing.

#### P8 · The problem space

Same events as [E3 · Indexing without designing](#e3--indexing-without-designing) and the problem space of [E2](#e2--removing-the-database-frame), seen from the problem's side.

**Need.** A statement of what must be solved to build two subsystems, before any design (Round 02, 2026-09-23; Rounds 03 and 04, 2026-09-24).

**Formulation.** Seventy-nine leaves in twenty-six families. A leaf was a question with a space of candidate answers, constraints and, at a boundary, an owner ("who decides, who is constrained"). It was formed by seven extraction memos, five independent cuts and five tests per leaf: local workability, layer assignment, openness ("at least two materially different answers"), grounding and no leakage; about sixty rewrites turned disguised solutions into the questions they would have settled. "Four of the five cuts ranked the same three boundary problems highest", the round's strongest evidence that its structure was not one vantage point's artefact. It stated its own blind spots, first "The premise set itself", and said "leaves are meant to be reformulated" (lead's text, `02-subsystem-problems/docs/`).

**Pressure.** The indices that filed two million words under the leaves tested the leaves' claims against history and found a premise "the history did not converge on" (lead's text). A review of the eighteen rows marked settled by an owner ruling found four settled by the ruling's words; the rest cited a ruling that answered a neighbouring question, or none. The next day's rulings (P9) fell on the premise register, which the per-leaf tests could not reach.

**Lesson.** F6 The map: tests run inside a register cannot test the register, and convergence of independent cuts says where a problem is, not that it is one; the register's standing changed later without its text (P9, P10). F3: openness, grounding and no leakage are its tests at the scale of a leaf.

*Kind:* enduring as method; the counts are objective-bound. *Study:* P8 · The problem space.

#### P9 · Four rulings

Same event as [E2 · Removing the database frame](#e2--removing-the-database-frame).

**Need.** A problem space that had absorbed frames from neighbouring domains.

**Formulation and pressure.** The owner's rulings of 2026-09-24 (`02-subsystem-problems/appendices/A-premises.md` §D) named four. D-1: "I³ does not adopt a database-style mental model of transactions, rollback, or retry", and "The residual influence of database mental models such as transaction, rollback, retry, and exactly-once is to be removed from the problem space; no mechanism for these concepts is to be designed." D-2: numerical equivalence of admitted implementations is Intelligence's question, not the core's. D-3: an instruction's freedom "is defined by the semantics of that abstraction or instruction itself, not granted by a vague, independently existing principle of "execution latitude"". D-4: "The absence of a capability from the first implementation must not be misrepresented as an architectural prohibition."

**Reformulation.** Of 332 sub-questions, 77 changed: 28 narrowed, 22 reinterpreted, 9 retired, 10 moved outside, 8 settled. The problem ranked first, the latitude contract, was retired a day after it was ranked; its tension had been "independently rediscovered at least three times under different vocabularies" (agents' text) and was dissolved without being answered. All four frames had entered through the premise register or inherited open boundaries. D-1 kept the observation (identity, "what happened to this request", unknown as a state of knowledge) and dropped the guarantee. *Forms:* D-3 relocated a definition (re-rendering); D-1, D-2 and D-4 changed what is asked, by dropping a guarantee and by moving questions to another owner. Two costs were recorded: a destination such as "to Intelligence" was a label nobody checked could receive the question, and the dissolution left a prohibition ("No hidden planner ...") where a test was wanted.

**Lesson.** M3 The signs: a tension rediscovered under several vocabularies, a ranking contradicted within a day, one word naming two problems ("deduplication"). F7 Decided absences, from D-4.

*Kind:* forward-only recovery is objective-bound; latitude as part of a definition and "keep the observation, drop the guarantee" are enduring. *Study:* P9 · Four rulings.

### Rounds 05 and 06: from the generic model to the concrete object (2026-09-24 to 2026-09-26)

#### E4 · The generic model closed

**Situation and form.** Round 05 (2026-09-24/25) set out to close the whole problem space into one self-consistent model. Each of 461 question rows got one disposition; accepted conclusions became premises in an append-only ledger; a coordinator ran cycles of planners, workers, synthesizers and a recorder; the goal's verification surface was a script that checked form. It produced a fifteen-chapter model of about 60,000 words, each chapter marked stable with its assumptions reading "None."

**Pressure.** The round's own closure showed the form check passing while the model's carriage of the rows stood at zero; its guarantees held only under named conditions no party had committed to. The owner's diagnosis: the model was so generic that many problems "could therefore only be closed by continuing to add abstractions", giving its answers "a circular or self-justifying character" (2026-09-26, `06-software-structure/POSITION.md` Part IV).

**Revision.** The owner closed the round without a pass. It "did not fail", but its model became a reference map and "an instrument for scrutiny", no longer a construction specification: "But concepts do not thereby acquire an automatic right to exist in the software" (2026-09-25, same file, Part I). The same text barred the over-corrections: the ontology rewritten as Rust typestate, or an architecture grown out of a pilot.

**Lesson.** The failure patterns concepts explaining concepts, procedure before object, conditional promises and the check layer (in its first form). The principle is D1 · A concrete object early, with the first statement of B2 · A concept is not an object; the ledger and form check fall under D3 · No second specification.

*Kind:* enduring. *Study:* E4 · The generic model closed.

#### E5 · The concrete object

**Situation.** Round 06 (2026-09-25/26) went through four configurations in two days. The first asked a coordinator to derive the structure from the crossings between the selected software stacks; the second to develop the owner's runtime premise (a master and heterogeneous workers, "very similar to nginx") chapter by chapter; the third to apply change requests in cycles to an imported model.

**Pressure.** Before the second charter wrote a chapter, a rough concrete model formed outside the repository: processes, who starts them and what state each owns; messages with fields; states and transitions; flow steps with actors. Parts were split by what runs and holds state, a separate agent wrote flows to find gaps, and one review found five faults "at the joints between parts, not missing parts" (agents' review).

**Revision.** The owner promoted the model to candidate on 2026-09-26 and named what the charters shared: "the research lacked a sufficiently concrete software object", so questions explained one another inside abstract models and new abstractions closed problems produced by earlier ones (`06-software-structure/POSITION.md` Part IV). Candidate meant coordinate system, not finished design.

**Lesson.** D1 · A concrete object early at its clearest: a procedure cannot supply the object it operates on. B1 · Design inside the existing world: the object is made of real things that already have semantics. J15 Drawn and forced (each element drawn with an owner and a lifetime, forced by a real fact; "it was in the old model" is not one) and J6 The world question.

*Kind:* enduring; the nginx-like runtime form is objective-bound, the stacks contextual. *Study:* E5 · The concrete object.

#### P10 · The map, not the specification

Same events as [E4](#e4--the-generic-model-closed) and [E5](#e5--the-concrete-object).

**Need.** One self-consistent system closing every question of the problem space (Round 05, 2026-09-24 to 09-25).

**Formulation.** The unit of closure was the question row: 461 rows, each with one disposition (397 answered, 57 absorbed, 5 outside, 1 nothing carried, 1 dissolved, 0 the owner's). Fifteen chapters stood "stable", each with assumptions reading "None.", and none of the rows had been carried into the model by a recorded carrier.

**Pressure.** The owner judged the kind of object, not a failed check. On 2026-09-25: "Round 05 itself did not fail. ... That value should be preserved", and "But concepts do not thereby acquire an automatic right to exist in the software. ... The new point of departure must be the software stacks that actually exist" (`06-software-structure/POSITION.md` Part I). On 2026-09-26 he named the cause: answers with "a circular or self-justifying character", because "the research lacked a sufficiently concrete software object" (Part IV).

**Reformulation.** Demoted from specification to map, its standing changed and its text untouched (a re-rendering). The owner then supplied the runtime form ("This runtime structure is the design premise I am now providing", Part II; a change of what is asked), re-levelled twenty-nine provider, version and deployment decisions that had been set at the level of architecture, and named three recursions: "No structural isomorphism should be established among these three forms of recursion" (Part III). Guards barred the over-corrections: the ontology rewritten as types, the system as "the old model minus the capabilities already supplied", a pilot grown into an architecture.

**Lesson.** F6 at its sharpest: a closure procedure certifies relations among answers, not that the set's ontology is the solution's. F4: for a computational world, the world is the existing stacks, and "the real boundaries and coordination mechanisms created between them are often precisely the things this system must own".

*Kind:* enduring; the runtime form is objective-bound and the stacks contextual. *Study:* P10 · The map, not the specification.

### Round 07: constructive contact and the fates (2026-09-26)

#### E6 · Constructive contact and flow pressure

**Situation and form.** Round 07 (2026-09-26) had to use Round 05's problems without letting its ontology return. The owner reversed the question: not how Round 05's concepts map onto the candidate, but "in what concrete form does the problem ... actually exist?" there. Each recovered problem met one fate: dissolved by the world; carried by an existing element; expanding the design with a constructed mechanism; not arising, because the old ontology made it; the owner's; outside. "The old ontology has no right of inheritance" (2026-09-26, `07-software-design/POSITION.md` Part I). Of 416 entries, 228 were carried, 106 expanded, 29 did not arise, 22 dissolved.

**Pressure and revision.** The first session left 28 owner questions, most of them engineering. The owner set the criterion for escalation as "semantic consequence, not implementation difficulty", with a list of what changes a long-term definition: the responsibility boundary, where authority lives, failure semantics, the sharing model between runs, a public contract, a new core abstraction (same file, Part II). The open set fell to one. Flows became a design tool to force untouched contracts into contact; where a flow stops, the design changes. "When two concrete mechanisms differ, do not instinctively invent a new generic layer above them." Resolutions went into the design, one row each beside it, not into a parallel body of resolved answers.

**Lesson.** J18 The fates, J13 Flow pressure and J10 The escalation criterion, under D2 · Construction is evidence and D6 · Escalate by semantic consequence; the no-generic-layer rule is C2. The same direction barred polishing while unstable.

*Kind:* enduring; the list of long-term definitions is objective-bound in content. *Study:* E6 · Constructive contact and flow pressure.

#### P11 · The fates

Same event as [E6 · Constructive contact and flow pressure](#e6--constructive-contact-and-flow-pressure).

**Need.** Use the closed model's problems without letting its ontology return (Round 07, 2026-09-26).

**Formulation.** The owner reversed the question: "In the current candidate software system, in what concrete form does the problem that Round 05 was trying to address actually exist?" and "The old ontology has no right of inheritance", with a diagnostic rule: if an old problem can be answered in its original form only by reintroducing a generic abstraction, "first examine whether the problem itself was created by the old ontology" (`07-software-design/POSITION.md` Part I). Each problem was recovered in plain words and recorded in six fields: as posed; where it exists; fate; answer; goes to; open.

**Pressure.** Of 416 problems, 228 were carried by an existing element, 106 expanded the design, 29 did not arise, 22 were dissolved by the world, 19 were outside, 12 were the owner's. The catalogue told where a difficulty lay: in the formulation's ontology (29), with an existing supplier or another owner (41), or in the object under construction (334). Nine of the 29 non-arising problems rested on one structural fact, one decider per run. A dissolved problem created a reliance stated in one sentence; a non-arising one created a condition under which it would arise ("Several eval threads would reopen it", agents' text). The round's first session left 28 owner questions, most of them engineering; under the owner's criterion, "semantic consequence, not implementation difficulty" (Part II), 26 of 28 closed.

**Reformulation.** Each inherited problem was re-asked of a concrete object, and the channel through which problems reached the owner was given a criterion. *Form:* change of what is asked, at two scales.

**Lesson.** F5 The concrete form, and its precondition, an object. M1: the fates are the readings recorded and counted, and three findings stay apart: the world answers it; another owner holds it; the formulation produced it.

*Kind:* the fates are enduring; the counts are objective-bound, and the share of non-arising problems measures the owner's premises, not the problem. *Study:* P11 · The fates.

### Round 08: runs as processes, and where computations come from (2026-09-26)

The question E7 records was raised in Round 07; the ruling that answers it, and P12, belong to Round 08, so both sit here.

#### E7 · Runs as processes, no mini-OS

**Situation.** Round 07's one genuine owner question was how runs are isolated and share a node.

**Revision.** The owner on 2026-09-26: "My intention is to avoid reimplementing a mini-OS in user space; I do not require I³ to build its own universal per-run quotas, fine-grained resource virtualization, or allocation ledgers" (`08-inputs-and-drivers/POSITION.md` Part I §IV). Runs were isolated by OS process boundaries; where a hard constraint was needed, the mechanism that provides it was to be named. In the same round the owner moved applicability (shapes, specializations, devices) out of Tensor IR into each implementation's mechanism, refused a global registry, plugin manager or dynamic discovery as the answer to extensibility, and kept live objects from crossing the core boundary. Ledgers returned later by other routes; see [Accounting and bounds](#accounting-and-bounds).

**Lesson.** B1 · Design inside the existing world and J6 The world question: let the OS carry isolation, design the contact. A3 · Fix meaning, free execution: the language fixes computation, realizations carry their own applicability. C4 refuses a registry before any need.

*Kind:* delegating isolation to the OS is enduring as a move; the Linux mechanisms are contextual; the Run as the boundary of live coordination is objective-bound. *Study:* E7 · Runs as processes, no mini-OS.

#### P12 · Where computations come from

Same event as [E7 · Runs as processes, no mini-OS](#e7--runs-as-processes-no-mini-os).

**Need.** The input end of a runtime whose execution end was fixed: "My primary concern is understanding exactly where computations in the current system originate and the process by which they transform into objects that the runtime can comprehend and execute" (2026-09-26, `08-inputs-and-drivers/POSITION.md` Part I).

**Formulation.** A first proposal took an artifact as the unit that crosses the boundary and made an "implementation valid for any box" the foundation, with a "box class" problem at its centre.

**Pressure.** The owner had warned: "my recollections or explanations from previous conversations cannot simply be treated as finalized definitions" (Part I). His review: "You must determine whether "box class" should truly be a formal concept within the I³ core or merely local information utilized by specific backends or providers", and "do not continue to assume that Tensor IR is the system's sole input object" (Part II). The agents' reconstruction found "box class" nowhere in the earlier research; it had entered with concrete-shape artifacts of a compiler toolchain, and thirty-one passages carried it.

**Reformulation.** Applicability moved to the implementation and its driver (a re-rendering by relocating a line), and the input became several objects with their own identities, classed persistent, reconstructible or live. "Being usable by the system" was separated from "being serializable into a portable artifact".

**Lesson.** F3 gains two tests: the membership question (a formal concept of the core, or local information?) and the provenance test (a term with no earlier provenance marks an imported frame). F1's first guard: nothing of a solution's facts flows up into the fixed meaning.

*Kind:* the box class is contextual; the provenance test is enduring. *Study:* P12 · Where computations come from.

### Round 09: workers and drivers (2026-09-27)

#### E8 · The driver axis removed

**Situation and form.** Round 08 answered extension with a "driver line": a driver per class of implementation, half compiled into the interpreter and half in a worker, seven closed questions the core could ask it, a static table closed by the build. It had heeded the owner's warning against registries.

**Pressure.** The next day the owner read the design as holding workers and drivers as "two partially overlapping classification systems", forcing the system to track both and their combinations (2026-09-27, `09-workers-drivers/worker-driver.md`). The operating-system analogy did not carry: an OS needs drivers to expose devices to many independent programs, while I³'s master and workers already severed programs from devices.

**Revision.** The axis was removed; what a worker needs to interface with a stack went into the worker definition; definitions stayed flat while runtime ownership stayed recursive. The owner guarded against "a generic 'provider interface' that differs in name only": shared abstraction stems "solely from genuine, recurring system invariants" the system must understand, not from code reuse, formal uniformity or provider symmetry. In the same round the owner asked the software to "evolve like a miniature Linux" (stable core, compile-time extensions, content arriving without a rebuild), embedded in module boundaries and builds; the agents held each shared contract element against other ecosystems' documentation and found almost none documented beyond the NVIDIA path.

**Lesson.** The second axis. C2 · Boundaries from responsibility, not symmetry: a type space may be flat while ownership is recursive. C4 and J14 The expansion test with its generality test: a shared abstraction is held against each instance, not judged by a neutral name. Asking whether an analogy's reason holds here is the habit of J20 Comparators.

*Kind:* removing a second axis is enduring; the flat worker space is contextual (it rests on a statically linked, single-team build); the OS-driver argument is contextual. *Study:* E8 · The driver axis removed. The structure that outlived the axis is told under [Drivers](#drivers).

#### P13 · Flat types, recursive ownership

Same event as [E8 · The driver axis removed](#e8--the-driver-axis-removed).

**Need.** "We must determine what constitutes the basic unit of extension for interfacing with external software systems within I³" (2026-09-27, `09-workers-drivers/worker-driver.md`).

**Formulation.** Two classifications, workers and drivers, overlapped. The owner removed one: "The goal here is not merely to rename the driver, but to remove an unnecessary layer of architectural classification." And he separated what recursed: "while the worker type space can remain flat, the actual runtime ownership graph can be recursive and hierarchical", a structure that "should not be conflated with the Interpreter's decision-making recursion" (`09-workers-drivers/POSITION.md`).

**Pressure.** The worker of this round fused four roles: an execution unit, a build unit, a node of ownership and lifetime, and the boundary of integration. The owner's coupling sentence, "the unit of extension influences the evolution boundaries, the evolution boundaries influence the level of abstraction", predicted the split: a unit tied to several rates of change is divided when the rates are observed. Round 12 divided it into a build-time definition, a long-lived service and the scope of one accepted instruction.

**Reformulation.** Separation of three things that recurse or classify (types, ownership, decisions), and a merge of two axes. *Form:* re-rendering.

**Lesson.** R4: whether a recursion is a tree or a graph follows from the relation it carries; ownership gives a tree, demand a graph with shared nodes. The fused kinds, in the worker's four roles.

*Kind:* the worker is objective-bound; the pattern is enduring. *Study:* P13 · Flat types, recursive ownership.

### Round 10: the baseline (about 2026-09-28)

#### E9 · Unfolding and closing layers

**Situation and form.** By Round 10 (about 2026-09-28) the design existed as five sets of material from shifting perspectives. The owner's prompt: "I view complex system design as a process of unfolding and closing layers" (`10-system-design-baseline/prompt.txt`). At each scale, subsystems with defined relations form a closed system that becomes a component of a larger one; the system is "not ... a single hierarchical tree"; views correspond without being forced one-to-one; source layout is a deeper level of implementation, not a way to define the concepts above it. The baseline carried no provenance, and what the material did not settle was marked unresolved.

**Result.** Thirteen views and scales, each with its parts, the relationship that closes it and its link to a larger system; a table pairing each valid correspondence with the invalid equation it must not become (a worker definition is not a live worker singleton); three recursions related by lowering, not isomorphism; and five kinds of limit kept apart: not yet designed, absent from this build, an accepted limitation, not reached by any probe, a release gate.

**Lesson.** C1 · Closure at each scale: views are related by elaboration, and the layout is not the design. The five kinds of limit are C4's rule that an absence states its kind and nothing is closed by an invented default. D5 · The design explains itself without its history.

*Kind:* enduring; the thirteen rows are objective-bound. *Study:* E9 · Unfolding and closing layers.

### Round 11: the skeleton (2026-09-28)

#### E10 · The skeleton's checks removed

**Situation and form.** Round 11 (2026-09-28) migrated the baseline into a repository skeleton of hundreds of files, guarded by a script and five registers checking coverage, package identities, the import graph, hashes, links and reachability. The check's own contract warned that link direction was "only a mechanical proxy" (agents' text).

**Revision.** The owner removed the global checks the same day: useful for the migration, they were not to be acceptance gates. "We must especially guard against letting easily satisfied automated checks become proxy goals for the AI's workflow; doing so creates a false sense of completion and obscures unresolved design issues" (`11-project-skeleton/docs/development/direction.md`). Checks were to emerge from semantic contracts, inside the boundary that owns them. Each element got a standing instead of a completeness score: committed, a specification decision with its alternatives and what each blocks, or to be established by qualification. Agents were assigned by responsibility, not by directory, and integration readers comparing both sides of each boundary found contradictions the script had passed.

**Lesson.** The check layer, and D3 · No second specification: the tool's own warning did not prevent it, because the pressure was on what agents optimize. C4's standings replace completeness as the measure.

*Kind:* enduring; the tooling is contextual. *Study:* E10 · The skeleton's checks removed.

### Rounds 12 and 13: the canonical division, and computation against execution (2026-09-29 to 2026-10-01)

#### E11 · The canonical division and the lifecycle repository

**Situation and form.** Round 12 (2026-09-29/30) was eight sessions with an external model in about 26 hours, each taking the last output and opening one question. The v6.0 prompt kept the simplification that had rejected forcing all capabilities into "a single generic `worker` runtime", and barred the opposite extreme, a coordinator calling stateless capability functions, because native capabilities have state of their own. What is unified is the responsibility long-lived entities carry, "not their internal shape"; recursion in Infrastructure is "mechanical execution composition, not a second solver or planner"; and "Do not allow a cleaner abstraction to merely hide" the hard issues (`12-gpt-6-pro-rounds/05-system-design-v6/prompts/prompt-en.txt`). The round's canonical design had divided the system by what each part carries: "The compiler carries local continuation. The Interpreter carries semantic continuation. Infrastructure carries accepted execution responsibility. Native owners carry physical obligations. The durable chain carries recoverable progress." (design text, `12-gpt-6-pro-rounds/04-canonical-design/outputs/I3-Canonical-Design.md`, overview).

**Pressure and revision.** The first software system, SS1, organized the repository by responsibility (18 top-level regions, 124 directories) and asked for closure in two directions, from responsibility down to repository location and back. Within hours SS2 changed the axis to the software's lifecycle (development, build, delivery, deployment, release): nine regions, each SS1 directory and decision given a disposition, responsibilities kept as private modules. Responsibility governed ownership inside the code; lifecycle governed repository, build and package.

**Lesson.** C2 · Boundaries from responsibility, not symmetry: the axis of a layout is chosen by what changes together and when, the same criterion yields different structures at different scales, and the axis may change without reopening semantics. The prompt pairs each prohibition with its opposite danger, the form each principle takes.

*Kind:* the lifecycle axis is objective-bound (a product of Rust and native stacks with a release process); the principle is enduring. *Study:* E11 · The canonical division and the lifecycle repository.

#### E12 · Authority into the rounds; computation versus execution

**Situation.** Round 13 (2026-09-30 and 2026-10-01) formed a baseline from Round 12's outputs. The root agent guide carried design principles across rounds, a first decision surface reopened decisions for lacking explicit owner approval, and Tensor IR entries mandated runtime checks, numerical details and tiling contracts.

**Revision.** "Authority for system design must derive from explicit round deliverables rather than being permanently codified in a global design document that spans multiple rounds" (`13-baseline-synthesis/POSITION.md` Part I). Completed rounds stayed read-only. Questions whose only basis was provenance or missing approval were removed as "a mechanical audit of owner text". Tensor IR fixes computation semantics and leaves execution free; a decision that leaves the Interpreter no meaningful choice is re-examined; the IR carries no validation added only to make behaviour mechanically checkable, and removing a validation does not delete a computation's preconditions. The semantic space is kept small, but what matters for high-performance realization is visible in it.

**Lesson.** A3 · Fix meaning, free execution; A2 · Effectiveness over completeness (small, but bounded by performance, not by minimalism); B4 · Facts by construction, checks at boundaries (validation leaves, preconditions stay); D5 (the record of why lives beside the design, read-only). Reopening on provenance.

*Kind:* the particular IR line and the performance criterion are objective-bound; authority in the rounds and the computation/execution split are enduring. *Study:* E12 · Authority into the rounds; computation versus execution.

#### P14 · Mechanical composition, not a second solver; computation against execution

Same events as [E11](#e11--the-canonical-division-and-the-lifecycle-repository) and [E12](#e12--authority-into-the-rounds-computation-versus-execution).

**Need.** A place for native state that outlives one instruction, and a language whose meaning is closed.

**Formulation.** The owner recovered "the valid intuition that existed behind the earlier notion of a 'recursive worker,' without restoring `worker` as a universal foundational entity": "this recursion is **mechanical execution composition**, not a second solver or planner" (2026-09-29/30, `12-gpt-6-pro-rounds/05-system-design-v6/prompts/prompt-en.txt`). In the same days a closure pass pinned numerical behaviour, strict index checking and restriction obligations on Kernels into the language.

**Pressure.** The agents found that native defaults "often do not conform" to the pinned numerics, so each body, type, operator and substrate would need conformance work. On 2026-10-01 the owner: "If a decision effectively dictates *how* a computation is executed—to the extent that the Interpreter no longer has meaningful choices regarding realization, decomposition, or execution—then that decision should be re-examined", and prerequisites should not become runtime semantics "simply because they *can* be checked" (`13-baseline-synthesis/POSITION.md` Part III). Part V: "A Kernel is an atomic computation", and "Keep the semantic space small", bounded by performance: a computation stays visible "when doing so is materially useful for high-performance realization".

**Reformulation.** Numerical realization moved to the realization and Intelligence; Kernel tiling moved to Intelligence, which may decompose a Kernel only by producing a new Program; conversion, a base for scatter and a fill constant were admitted by the performance criterion while empty intervals stayed out. The owner's decision surface fell from thirty-four entries to twenty to seven. *Form:* re-rendering by relocating the line, with narrowing.

**Lesson.** F1's second guard: nothing of the fixed meaning flows down to remove a solver's meaningful choice; the first guard (P12) did not imply it, and legality does not depend on what can execute today. R5: the atomic case is a decision, and moving it is a new representation.

*Kind:* the tensor content is objective-bound; the two guards and smallness bounded by use are enduring. *Study:* P14 · Mechanical composition, not a second solver; computation against execution.

### Round 14: the closed design (2026-10-01)

#### E13 · The closed, self-explaining design

**Situation and form.** Round 14 (2026-10-01) wrote one design. The owner: "Each layer should be closed at its own conceptual scale"; lower layers elaborate and do not define retroactively. The truncation test: "If all design layers below a given layer were temporarily removed, would the higher-level design still constitute a complete and correct system description, only at a more abstract level?" The deletion test: an agent given only this design continues the work without earlier rounds. "Do not use historical accounts of 'who decided what' as the reason why the design holds" (`14-system-design/POSITION.md` Part I). The result was five layers on one line of elaboration and two views beside it, with placement tests: what two parties rely on is a contract, what one owner relies on is mechanism; if a lower layer needs what the upper one lacks, the upper one is fixed.

**Pressure.** The closure phase treated 127 listed gaps as design tasks and stopped only when "an implementer can build each part from it without inventing semantics" (agents' brief). It added a history marker, an ended record kept in two places, profiles, qualification records and node capability statements; the design grew from about 206,000 to 316,000 words. Rounds 16 and 18 removed most of what closure added. Keeping technology names out of upper layers also forced technology-free stand-ins, several later withdrawn.

**Lesson.** C1 · Closure at each scale, J8 The truncation and deletion tests and D5 · The design explains itself held. The closure drive: "complete enough to implement from" has no stopping point inside itself, since each closed gap adds an object whose edges must be closed; the stopping criterion is J4 The failure question. C1's caution: name a technology where it is the selection, and ask whether the argument above would survive another selection.

*Kind:* the layering and the two tests are enduring; the seven-part cut is objective-bound; the proxies were a contextual cost. *Study:* E13 · The closed, self-explaining design.

#### P15 · Five structures, three recursions

Same event as [E13 · The closed, self-explaining design](#e13--the-closed-self-explaining-design).

**Need.** A complete design closed at each scale (Round 14, 2026-10-01), under the owner's instruction: "Different layers may contain different forms of recursion, composition, and internal closure. Do not force them into a single abstraction merely for the sake of formal uniformity" (`14-system-design/POSITION.md` Part I).

**Formulation.** "**Demand recursion.** A goal requests child goals through interests. Equal obligations share one goal, so demand is a finite graph, checked for cycles as interests are added. It solves semantic obligations" (agents' text). A goal's key "contains exactly the fields that change the obligation, never its scheduling history". Mechanical recursion and native nesting were distinguished from it, and "No structure is inferred from another's shape".

**Pressure.** The goal graph was at once the statement of what is owed and a structure the owner kept. Construction chose "one future per goal" with a task map, a dependency graph between tasks and an executor budget (agents' reading of the code, Round 16): the problem's recursion had become the runtime's. The key held the unsatisfied remainder, so partial progress minted a successor goal and migrated every interest. The demand graph was reformulated in P16.

**Lesson.** R2's content test (the key holds only what changes the obligation) was right and was not enough: it said what enters an identity, not who can compute it. R4 at its fullest.

*Kind:* the content is objective-bound; the form is enduring. *Study:* P15 · Five structures, three recursions.

### Rounds 15 to 19: construction, the runtime ontology and commitment trimming (2026-10-02 to 2026-10-09)

Construction rounds (15, 17, 19) alternated with design rounds (16, 18). The design moves tell the period round by round; P16 reads Rounds 16 and 18 from the problem's side, and P17 reads the whole period.

#### E14 · Construction and the check layer

**Situation and form.** Round 15 (2026-10-02) began construction in goal cycles of plan, execute and synthesize. The design was read-only, the repository the only record of progress; no plans, backlogs or ledgers were kept. Each cycle took from the frontier (designed parts not yet built whose prerequisites work) the large coherent transition that made the most of the system real; no pilots, placeholders or mocks. Test-driven development was barred out of "a desire to avoid creating a second specification" (`15-construction/POSITION.md` Part III).

**Pressure.** Within seventeen cycles a `tools/check` tree had grown beside the product, with operand files and product entry points that accepted facts their owners should have established; commit messages narrated hashes and passing runs.

**Revision.** On 2026-10-03 the owner ruled that the design text and the product code "constitute the sole sources of the system's meaning and implementation; no alternative 'source of truth'—capable of defining, simulating, proving, or explaining system behavior—should be allowed to emerge outside of these" (same file, consolidation). The test was whether a component had begun to define what the system is or what counts as valid. Capability the harness held went back to its owners; about 11,000 lines were deleted. The owner barred the swing the other way: "do not shift the objective to running an end-to-end computation case as quickly as possible".

**Lesson.** D3 · No second specification; the check layer and management for the work; C4's construction in large coherent steps; progress measured as capability in the product, not as counts.

*Kind:* enduring for construction; the blanket bar on test-driven development is objective-bound and was narrowed (E18). *Study:* E14 · Construction and the check layer.

#### E15 · The runtime ontology

**Situation.** Round 16 (2026-10-06/07) read the Round 15 software as a nearly literal realization of the design and asked which named things had to exist in running code. "A concept being useful for design reasoning does not imply that it must exist as a software object" (`16-runtime-ontology/POSITION.md`). The owner listed signals of reverse pressure (fields added to complete an abstract object, a second lifecycle over a native one, a local relation promoted to an entity) and allowed the conclusion that the specification was over-abstracted.

**Form.** A threshold for runtime identity (shared by independent actors, exchanged across processes, re-identified across time, durable, recognized after recovery, or externally observable); the boundary test, "Which unavoidable software boundary does it correspond to?"; the chain by which a known fact is re-described as an object, given identity, copied, validated and reconfirmed; and "Every additional independent representation creates an additional consistency obligation by construction" (same file, 2026-10-07). About ninety rulings followed, each in four parts: what stays, what goes, what carries it now, what is lost.

**Revision and regrowth.** The frontier fact, chain incarnation, the complete object description, Run modes, goals and interests went; the Commit left the Instructions; place and host were separated. Judges forced back what a behaviour list needed, such as each object's logical tag. The owner barred the swing: not "anti-formalization", not "the more native, the better", not a "better ontology". Cross-reading found regrowth in the rewrite: the host back as a public object, a per-call read set kept under three names.

**Lesson.** B2 · A concept is not an object; B3 · One fact, one owner; D2 · Construction is evidence; D4's four-part rulings and its watch for regrowth. J2 The boundary test, J3 The owner test, J7 The two readings of pressure, J11 The reification chain, J16 What reads it?; the reification chain, and regrowth and the better mechanism. This round asked which objects must exist; Round 18 asked which commitments must: J2 and J1 are one question at two levels.

*Kind:* the threshold and test are enduring; the list of seven boundaries is close to enduring but phrased for distributed software. *Study:* E15 · The runtime ontology.

#### E16 · Behaviour decides, not names

**Situation and form.** Round 17 (2026-10-07) moved construction to Round 16's design while the tree held code built to Round 14's. "The deciding factor is always software behavior and the assignment of responsibility, not lexical differences" (`17-construction-shift/POSITION.md`). No compatibility layers keeping two ontologies alive, no dual representations kept in step by checks, no migration plan in advance. In the round's rules, a rename that leaves behaviour and ownership where they were is not a transition.

**Pressure.** The owner's Round 16 critique of how bounds were measured (encoded JSON length does not correspond to the cost of the real state) was answered in construction by typed allocation accounting and then a cycle of "memory-charge accounting", whose code had to avoid an admission waiting on its own reservation. A critique of how a mechanism worked had produced a better mechanism. Meanwhile four answered construction questions each extended an apparatus the next round withdrew.

**Revision.** The owner's next direction moved the question up a level (E17); the accounting cycle was stashed as "no longer a valid direction", and construction later restarted from the cycle before it.

**Lesson.** Rename as revision. D4 · Revise at the level of premises: a critique of how invites a better how, where the question wanted was whether, and a prohibition stated once does not hold against a premise that keeps generating the mechanism. J10 The escalation criterion with its premise step: before answering a question, ask whether what it assumes should exist.

*Kind:* enduring. *Study:* E16 · Behaviour decides, not names.

#### E17 · Commitment trimming

**Situation.** Round 18 (2026-10-08/09). The owner: earlier refactoring had asked how to implement semantics concisely, not whether they were needed; "Should the constraint it attempts to satisfy be a design requirement for I³ at all?"; the pursuit of "boundedness, determinism, defensiveness, and formal completeness" may have imported requirements of hard real-time and safety-critical systems; "Do not first establish a fact and then build additional mechanisms to verify that the fact continues to hold" (`18-commitment-trimming/POSITION.md` §1, §2). In the same text: "avoid trimming for the sake of trimming", and no old mechanism replaced by one of the same function in a more elegant form.

**Form.** Readers classified each commitment as essential, already carried by the world, or excess; judges worked at the level of premises, since "a premise change that removes ten mechanisms is worth more than ten separate trims" (judges' brief); each relinquished commitment came with what a user would notice.

**Revision.** Three responsibilities, seven principles (among them: loss is the answer to failure; the release is the trust boundary; safety strict, liveness ordinary; distinctions as fine as their consumers), nine guarantees in their users' words, 33 commitments withdrawn, and a design rewritten from the premises with each sentence's kind marked. A weakened guarantee was named as weakened. The cross-review then found the trim had passed the joins with real resources: device memory outside the retry rules, exclusions forgotten when a Run ended, node control as the likeliest OOM victim. Each was closed by a native mechanism or the operator's tool, not by runtime coordination.

**Lesson.** J1 The responsibility question, J4 The failure question, J5 The consumer test, J12 The premise lever, J20 Comparators and J9 The carrier rule, under A1 (name each relinquished commitment and its cost) and D4. The convenient requirement and defensive drift, and over-trimming at the joins; B4's safety claims are the floor. D5's statement kinds exist because a design that is the construction authority turns explanations into conditions, and conditions into code.

*Kind:* the method is enduring; the withdrawals are objective-bound; the release as trust boundary is contextual, resting on an objective-bound assumption (one team builds every process; a trusted single-tenant site). *Study:* E17 · Commitment trimming.

#### E18 · Tests are not the frontier

**Situation and revision.** Round 19 (2026-10-09) configured construction on the trimmed design. The owner: the project's own tests "should not be treated as a 'construction frontier'", progress is not measured by their coverage or number, and they confirm the implementation without being "a secondary source of semantic authority"; the conformance runner and the site acceptance kit "represent product capabilities intended for actual use" and are built (`19-construction/POSITION.md`, on testing). The round's rules added that a withdrawn thing leaves inside the cycle that builds its owner, not as a separate sweep; that nothing becomes a commitment because the tree already has it; and that a withdrawn responsibility is not rebuilt under another name, smaller, or as a better mechanism. The first cycle's removals each named what carries the behaviour now, or that nothing does.

**Lesson.** D3 · No second specification, with its line: what a verification is for decides its standing. Confirming an implementation is subordinate and sets no goal; delivering a capability to a user is product; a check at a real boundary is design. J9 The carrier rule governs each removal.

*Kind:* enduring; where the line between product and project verification falls is objective-bound. *Study:* E18 · Tests are not the frontier.

#### P16 · The decision is a function

Same events as [E15](#e15--the-runtime-ontology) and [E17](#e17--commitment-trimming), seen from the problem's side.

**Need.** The interior of the Interpreter, read through the code built from it.

**Formulation and pressure.** The owner on 2026-10-06: "**Have concepts, objects, and classifications introduced during the design process in order to make the problem understandable, decomposable, and reason-able been unnecessarily carried into the I³ software system itself, and further turned into an ontology that the runtime must maintain?**" and "**A concept being useful for design reasoning does not imply that it must exist as a software object.**" On 2026-10-07: "Does remaining computation inherently require creating a new Goal identity and migrating an entire dependency structure?" (`16-runtime-ontology/POSITION.md`). A reader found the graph restored by no reconstruction and read by nothing outside one incarnation; a judge found the cause: "The design needed migration only because it put the unsatisfied remainder *inside* the key" (agents' text).

**Reformulation.** The lead's ruling: "What the Run owes is derived, never stored". By Round 18 (2026-10-08 to 10-09), owed work was "named by its description in Program terms", "Any term derives the same descriptions from the same Program", "Work in flight serves all its consumers", and one procedure answered every piece with a step, a wait naming its live sources, or `no-admissible-choice` (agents' text, `18-commitment-trimming/design/`). Six decision points stayed as the structure of choices and two were opened to producers; the owner accepted hooks "only for `Realization` and `Split`, with others to be added based on actual needs" (2026-10-09). The word "recursion" left the design. The reduction also exposed a gap: the account of why values are kept had no place for when to release them, and Release at need became a rule. *Form:* re-rendering (an entity demoted to a description, the remainder moved out of the identity, a registry replaced by a lookup).

**Lesson.** R2: identity by description, with the computability test. R3: derived, not stored.

*Kind:* the form is enduring; the keys are objective-bound; the condition (an immutable, acyclic, region-exact Program and facts that can be read back) is contextual. *Study:* P16 · The decision is a function.

#### P17 · Construction as evidence about the problem

Same events as [E14](#e14--construction-and-the-check-layer) to [E18](#e18--tests-are-not-the-frontier).

**Need.** Build the designed system (Rounds 15, 17 and 19) and read what building showed.

**Formulation.** Each construction round took its design as the authority and sent only semantic questions to the owner.

**Pressure.** The owner switched modes ten times between 2026-10-01 and 10-09, each with a stated reason and none triggered by a failed build, test or review; the interval shortened from one day to forty-six cycles to fifteen. Of Round 15's twenty-five questions, coded later by one reader, fifteen rested on a premise of the representation that raised them, four were a missing capability, two a design fault, four the owner's choice; for thirteen of the seventeen the lead marked as disappearing, the adopted answer was already among the question's options. The remark "The three options listed in the question are all ways of re-attaching it" (agents' text) is the counter-case: it is about question 16, whose dissolving answer was not among its options. Of Round 17's eleven, seven rested on representations later withdrawn, two were capability, one design, one undetermined. The pressure was read at three levels. Round 16 allowed "the possibility that the specification is over-abstracted". Round 18 (2026-10-08) went further: "previous refactoring efforts focused primarily on **how to implement established semantics more concisely**; the necessity of the semantic commitments themselves has not undergone the same level of scrutiny", asking "**Should the constraint it attempts to satisfy be a design requirement for I³ at all?**" (`18-commitment-trimming/POSITION.md` §2). The accounting of the Interpreter's own memory had entered in Round 14, been kept and improved in Round 16 ("The requirement that queues and state remain bounded is real", 2026-10-07), and built in twelve of fifteen cycles of Round 17, six days and sixty-one cycles before the owner asked whether.

**Reformulation.** Thirty-three commitments were withdrawn; the bookkeeping became ordinary data whose overflow is a lost part. "The memory-charge accounting approach from Round 17, Cycle 16, is no longer a valid direction for implementation" (2026-10-09). Each removal carried a floor written as exceptions: eight gaps no removal may reopen in Round 16, nineteen items that must stay in Round 18, and "avoid trimming for the sake of trimming". *Form:* change of what is asked (a requirement relinquished), with the responsibility moved to the loss path and the operating system.

**Lesson.** M1: three levels of reading, each unavailable from the one below; the diagnostic is that if a stronger capability would not change the judgment, the difficulty is not one of capability. L3: the effort a mechanism induces is evidence about its requirement.

*Kind:* the alternation of rounds is objective-bound; the readings and the diagnostic are enduring; the codings are one reader's. *Study:* P17 · Construction as evidence about the problem.

### I⁵ Round 01: three to five (2026-10-09)

#### E19 · From three to five

**Situation.** Five research packages written against Round 18's design each found its limit at a boundary, not inside a component: a fixed decision procedure that producers' methods could advise at two points; seven closed Instruction kinds, so a new native facility had to pass itself off as an Apply; no designed observation space; Infrastructure organized by host family and Instruction kind.

**Revision.** The owner retired I³ and opened I⁵ (Round 01, 2026-10-09) with five concepts. The Interpreter became the host of decision programs; Instruction became an open set of typed contracts with latitude stated per action, D-3's resolution carried into an open set, not a return to a granted freedom; Information became a designed observation relationship. Two chapters added to Round 18 would have left the fixed procedure at the centre. The framing restated in its own words what carries forward and from which experience; its cross-reading restored boundaries a draft had dropped (the Run's three endings, the holder's fence) and turned what a draft carried from I³ by reference into the framing's own statements.

**Lesson.** C4 · Expand the platform, not the special case, and J14 The expansion test: progress is what the system can express, and the foundation is widened instead of adding cases. D5 and D4: what is kept is restated and owned, not inherited by citation.

*Kind:* the five-concept organization is objective-bound; widening the foundation rather than adding cases is enduring. *Study:* E19 · From three to five.

#### P18 · Three to five

Same event as [E19 · From three to five](#e19--from-three-to-five).

**Need.** Five research packages, written against the converged design of Round 18 with no implementation inspected and no benchmark run, and the owner's judgment that the direction "has expanded substantially" (2026-10-09, I⁵ `01-system-framing/POSITION.md`).

**Formulation.** "This is not merely a system rename, nor is it a matter of adding two software components to the existing I³ architecture. ... We now need to establish a new architectural starting point." The framing restated the objective: the decision procedure becomes "the thing that is produced, hosted, informed, and improved", and progress is expressibility, composition efficiency and decision usefulness, "not a score"; "The count of Instruction kinds, native families, relations or processes is progress on none of them either" (lead's text, `framing/01-system.md`).

**Pressure.** Of eleven limits the packages found, ten sat at joins between parts and one inside a component, in three shapes: a closed enumeration at the join, a fixed procedure on one side that content on the other had to fit, a missing meaning. The packages read one another, so the convergence is not independent.

**Reformulation.** A change of what is asked, and the recovery of an earlier intent at a higher level: "I⁵ is in part a return to I³'s first intent" (lead's text), after four weeks in which Intelligence's part had narrowed to advice at two points. The limiting joins were given semantics of their own and no runtime: "the five I's do not necessarily correspond to five independent software entities or runtimes" (owner). The floor survived by restatement; a review of the draft found thirty-three issues, and the fixing pass restored three boundaries of the Run the draft had dropped and turned a fixed process topology back into questions. And: "Do not make minimal implementation the objective of architectural design."

**Lesson.** L3: research against a converged design is a carrier, and a limiting join is repaired by giving it semantics owned once, enlarging neither side. The lost intent rests on this one episode, in the account of the lead who recovered the intent; whether the narrowing was the price of settling the floor was not tested.

*Kind:* strategy as a program is objective-bound; the joins and the floor's restatement are enduring; the order of settlement (narrow to settle the floor, then widen) is contextual and rests on the lead's account alone. *Study:* P18 · Three to five.

## Reading the cases together

**What held and what moved.** One thing was held fixed throughout: the role of a declaration that fixes the meaning of a computation and leaves realization free. The language that filled the role took its form in axle Round 06 and was revised rarely, on stated evidence, mostly by narrowing or by relocating a matter to the party that could act on it, and once by a widening bounded by what the solver must see to choose well (P1, P12, P14, P16). Everything above it moved: what the system answers for, the unit of decomposition, what a sub-problem is, who decides.

**What recursed.** A worker carrying capacity (P3), a cursor (P5a), a policy (P5b), a control request (P6), a goal in a graph (P15), a derivation (P16). Each step moved recursion out of the runtime's ontology and into the problem's derivation, and the word left the design when nothing runtime remained for it to name. The record names what the move cost: the explicit parent-to-child edge; deduplication by key between unequal demands, never offered; straight-line code for multi-stage decisions; and lifting at run time, never built. Beside the problem's recursion, the construction of computations, mechanical composition and native nesting were kept apart with no isomorphism (P10, P13, P14, P15).

**What triggered reformulation.** An imported frame recognized (P5a, P5b, P9, P12, P17); a tension rediscovered under several vocabularies (P9); a closed model answering every problem with an abstraction (P10); construction pressure read as evidence about the specification (P16, P17); research against a converged design finding limits at joins (P18). A sixth: the owner's recovery of an earlier intent at a higher level (P18). Several triggers were never recorded (D-1 to D-4; the replacement of the first framework), and no reformulation in the record was triggered by a failing build or test; the carriers were reading, research, review and the owner's reading of the tree and the history.

**The counts, and what each can carry.**

| Count | Case | What it shows | What it rests on |
|---|---|---|---|
| 77 of 332 sub-questions changed in the amendment that followed four rulings | P9 | Most of a problem space survives a reformulation at the premises; what changes is concentrated where the frames entered | The lead's dispositions, some resting on the lead's reading of the rulings |
| 416 problems: 228, 106, 29, 22, 19, 12 | P11 | Where difficulty lay: the formulation's ontology, an existing supplier or another owner, the object | Agents' classifications against one concrete object; the 29 measure the owner's premises |
| 15, 4, 2, 4 of 25; 7, 2, 1, 1 of 11 | P17 | Most construction questions rested on the premise of their own representation | One reader's coding of two rounds |
| Ten switches, none from a failed build, test or review | P17 | The loops alternated, and the triggers were patterns read in the tree and the history | One owner's record of nine days |
| 33 commitments withdrawn | P17, P18 | A trimmed design can still carry promises nobody relies on | The lead's count in I⁵ Round 01 |
| Ten of eleven limits at joins | P18 | A converged formulation shows its limits where it settled by an enumeration or a fixed procedure | One reading of five packages that read one another, with no execution |

**A caution.** These cases are told with their dead ends: the closure drive, the three charters of Round 06, the forms rejected one after another in axle's control line, the accounting episode, the constructs that replaced dissolved questions and were themselves withdrawn within days. A sequence read backwards from its end looks like a path from worse to better; it was not walked as one, and each earlier formulation was the representation the work needed then.

## Mechanism cases

Each ran across several moves of the history above; the *Study* pointer names the move or moves inside which the study tells it.

### Run endings

**Form and pressure.** On 2026-10-01 the owner ruled that a Run whose completion cannot be determined should end in an explicit indeterminate outcome rather than guess and repeat effects, and that an unresolved publication may end the Run in an explicit failure. Round 14 therefore had five endings and an ended record kept in two places. A Round 16 judge showed the two new endings bought only liveness under a lasting store outage: a store that refuses writes refuses the ending too, so the ending arrives only when the store answers again, when the position could have been settled, and it then forbids recovery after the operator fixes the cause.

**Revision.** The owner reversed his own ruling six days later: three endings, and "A lack of response from the Store implies we have not yet reached an ending, not that the system has entered a new type of ending"; past the bound the Interpreter exits "not ended" and restarts (2026-10-07, `16-runtime-ontology/POSITION.md`, ruling O1). Round 18 recorded the ending once, as the chain's last record. A check then found silence could still become a recorded ending (a switch reboots, the nodes go quiet, the Interpreter finds nothing admissible); now a wait names a live source, and silence never ends a Run.

**Lesson.** J19 Behaviour or policy: a state that answers a liveness choice is a policy on an existing mechanism. B5 · One path for loss: an observation gap is not a state. The owner's reversal, its reason stated in general terms, is the precedent for revising rulings by their reasons.

*Kind:* three endings are objective-bound; "an unanswered store is not an ending" is enduring. *Study:* E15 · The runtime ontology, with the later form under E17.

### The Commit and the frontier

**Form.** From Round 06 the Commit, the write that publishes durable progress, was an Instruction sent through a node, so the node could read the holder's authority first. Beside the chain of commit records stood a frontier pointer in etcd with its own digest and validation, a chain incarnation counter, a stored frontier in each record, and a validity rule that re-derived the Program's coverage.

**Pressure and revision.** A Round 13 review found the authority read was not part of the fence; create-once and the takeover were, so the Commit's reason to pass through a node was gone. A Round 16 judge traced the frontier's readers and found only the operator's diagnostic display; the chain incarnation decided nothing; the stored frontier was a pure function of the cut, stored and then re-checked; re-deriving the Program let one lost object invalidate the rest of the chain. The owner: the Commit is the holder's own conditional create, since putting it in the Instruction vocabulary "would obscure genuine software ownership for the sake of formal uniformity"; and a frontier pointer "would merely recreate a secondary state layer consisting of 'fact + description of fact + consistency between the two'" (2026-10-07, `16-runtime-ontology/POSITION.md`, O3 and O2). Round 18 later dropped version tokens from records, since create-once already guaranteed what they re-checked.

**Lesson.** J17 Decision placement: ownership of an act, not uniformity of vocabulary, decides who performs it (uniformity for its own sake). J16 What reads it?: a value with no reader but a display, or a pure function of what is held, is derived. B3 · One fact, one owner. A layer's reason can vanish when a premise elsewhere changes.

*Kind:* the create-once chain is contextual (stores with conditional create); the lessons are enduring. *Study:* E15 · The runtime ontology.

### Instruction kinds

**Form.** Round 05 modelled three levels of caller interface (facility, region, dependency group), each with its own interface. Round 06's concrete model had a flat set of nine kinds. Round 07 gave the three levels the fate "not arising": they existed because the region level needed a machine-side meaning of regions and the group level a machine-side graph, and the candidate gave the runtime neither; a graph was a sequence of instructions with `after` links. A Compose kind was declined, since a kernel made of two kernels is a new artifact delivered as knowledge.

**Revision.** Nine became eight when the Commit left (O3), and seven in Round 18 when Inspect left: it "existed for recovery; the listing carries the same facts" (Round 18 change record). I⁵ then opened the set as typed contracts around a common core.

**Lesson.** C2 · Boundaries from responsibility, not symmetry: no generic level over concrete acts. C3 · Distinctions as fine as their consumers. J18 The fates, and J3 The owner test for Inspect, a second carrier of facts the listing holds. C4: a closed set fits one objective and is widened at the foundation when the objective changes.

*Kind:* the seven kinds are objective-bound. *Study:* E6 for the three levels; E15 and E17 for the later counts.

### Outcomes

**Form.** Round 05 described what is known after a request leaves as a product of eight independent dimensions. Round 14 had five outcome classes, each defined by the evidence it required, about thirty closed reasons and five answers to a cancellation. Round 16 kept the five ("each class changes a decision differently") and removed the receiver-side evidence check, which validated a final against a restatement of itself.

**Revision.** A Round 18 judge re-asked the question of the act: exact knowledge is needed about external things that outlive the act (a store key, a scheduler step), not about the system's acts on its own memory. Uncertainty moved onto those things. Instructions end Complete, Not run (with a refusal class the Interpreter acts on: wait for capacity, choose differently, re-address) or Not established (with the facts that are established); reasons became text. The consumer test was checked against what the Interpreter's code actually branched on. Another judge would have kept an Unknown outcome for effectful acts; the converged design took the first form, with no separate owner ruling recorded.

**Lesson.** J5 The consumer test and C3 · Distinctions as fine as their consumers. B5's addition: uncertainty lives on the external thing it concerns, and a pure act whose result is unknown is simply not established.

*Kind:* the consumer test is enduring; recomputing pure work rather than proving it ran once is objective-bound (a deterministic tensor workload); three outcomes are objective-bound. *Study:* E17 · Commitment trimming.

### Knowledge delivery

**Form.** Round 01 stated the need with no mechanism: an improvement must reach a running computation without disturbing it, and the path "need not become a standalone workflow platform" (round text). Later rounds added a pin, sets adopted whole, an offer, validation, a guarded pin, uncertain-adoption states and a gate on the clean end; Round 16 simplified it to a cursor and, by owner ruling, live import of method content into advisors.

**Pressure and revision.** A Round 18 judge observed that knowledge selects how a Run computes, not what, since admitted implementations are equivalent; the correctness of committed progress does not depend on which knowledge was used. The adoption states existed only because the live channel existed. The premise went: a term reads its knowledge once, at its start, and the operator relaunches to change it; the owner's live-import ruling became moot rather than reversed. The cross-review then found the remaining path, relaunch, had no owner, and ruled that the holder follows the launch record.

**Lesson.** J12 The premise lever: one premise carried a pin, a gate, a reconciliation rule and per-adoption hosts. J9 The carrier rule: removing a live channel makes restart the mechanism, and restart needs an owner. A3: fix what, free how.

*Kind:* the separation of how from what is enduring; having no channel into a running job is objective-bound (long Runs, a trusted site, an operator who can relaunch). *Study:* E17 · Commitment trimming.

### Qualification

**Form.** On 2026-10-01 the owner ruled in one sentence: "This is not an owner design question. ... A profile is provided only after qualification on an identified real environment; profiles that fail or have not been qualified are simply not provided" (`13-baseline-synthesis/POSITION.md` Part VI). Round 14's closure built it as runtime state: records named by digest, five kinds of evidence, statistical windows, carry-forward rules, a withdrawal fact in etcd, and a node's offer computed from the record.

**Pressure and revision.** In construction the runner checked two criteria and recorded the rest as not run, which counted as failure, so no node offered anything and the system could execute nothing: in an agent's words, the design working correctly on missing evidence. The owner then found criterion identifiers in runtime code: "how an inspection is organized and which properties the software actually depends on are two different things" (2026-10-07, `16-runtime-ontology/POSITION.md`). Round 16 took the identifiers out of code; Round 18 relinquished the record as a runtime commitment: the operator is already the trust root, most criteria guard failures that are loud at first use, and no comparator ships such a record. Sites run delivered acceptance programs and enable what they trust; one hard gate stays (progress only to a location marked commit-capable), and silently corrupting routes stay off until enabled. The cross-review found that qualification had been the only source of what a "place" was; the site configuration took that over.

**Lesson.** The closure drive at its sharpest: an instruction about what to verify was read as something to run, which is why D5 marks each statement's kind. J9 The carrier rule: ask what silently relied on the removed thing. D3's line: the acceptance kit is product.

*Kind:* "offer only what is shown" is enduring and changed holder; the operator as trust root is objective-bound. *Study:* E13 for the build; E17 for the trim.

### Capability

**Form.** Round 09's worker definitions became, through Round 12, "capability definitions", and Round 14 made them a runtime concept with a pure side and a native side, a unified record and identity.

**Pressure and revision.** The owner on 2026-10-07: the program was "turning implementation relationships that the compiler already knows into data, and then recognizing them again at runtime": modules entered as strings and `match` statements rediscovered them (`16-runtime-ontology/POSITION.md`, supplementary direction). He asked: if Capability did not exist as a first-class concept, which behaviours would become impossible to express? The ruling kept the name, because it crosses four real boundaries (a producer's entry, a node's offer, an Instruction's descriptor, a profile's claim), and nothing else: each family owns typed forms reached by static dispatch on a closed list. What became impossible without it: nothing. The owner barred a replacement "generic trait, registry, Backend ontology, or unified object layer".

**Lesson.** B2 · A concept is not an object; J2 The boundary test, in the owner's thought-experiment form; the reification chain. What the compiler already knows is not turned into data to be recognized again.

*Kind:* the lesson is enduring; static dispatch on a release-fixed list is contextual (a statically linked language); no runtime-extensible families is objective-bound. *Study:* E15 · The runtime ontology.

### Drivers

**Form and fate.** E8 tells why the driver axis went; this case is what survived it. Round 09 kept the driver line's seven questions, their numbers and answer forms, as the "core-side part" of each worker definition; the default decision policy stayed modelled as a built-in method entry, a residue of the driver table; and in Round 16 the owner found "pure side and native side" inside Capability.

**Revision.** Round 16 ruled that built-in methods are not entries: the default is a fallback after the last method, not "a kind of method" with an identity, a version and a place in an ordering no behaviour used.

**Lesson.** Rename as revision in its subtle form: the axis goes, the structure along it stays and surfaces later under another name. Classifying by "is a kind of" promotes a default into an entry (B2, C3).

*Kind:* enduring. *Study:* E8 · The driver axis removed, and E15 for the later fate.

### Hosts, formations and their lifecycles

**Form and revision.** Round 14 had native domains, facilities and an incarnation allocated before any process existed; the code shadowed one native lifecycle (spawn, run, exit, cgroup empty) with at least three state machines. A Round 16 judge found two things merged under "incarnation": the place the Interpreter chooses, which exists before any process, and the host process node control runs for it. They were separated; a formation's identity became that of the Establish that formed it. The owner: "Host reattachment after the loss of node control is not supported", and the process lifetime "naturally determines the relationship lifetime" (2026-10-07, `16-runtime-ontology/POSITION.md`, O5, O6). The rewrite then republished the host as a public object, and a cross-reader removed it again.

**The lifecycle, three times.** Round 16 let native state survive the Interpreter for a successor to adopt, through a census, an Inspect Instruction and a coherence test. Round 18's agents proposed the opposite: native state ends with the Interpreter's term. The owner rejected both: the Interpreter's lifecycle, the recovery boundary of progress and native resources "should not be artificially coupled", and he asked for a re-examination "rather than simply choosing between existing options" (2026-10-08, `18-commitment-trimming/POSITION.md` §4). The converged design still promised survival in about forty passages; the owner corrected them: "Do not replace the old lifecycle coupling with a new mechanism for persistent state management" (2026-10-09, §5). What stayed strict: exclusion until the holder is gone.

**Lesson.** B6 · Lifecycles belong to their mechanisms: coupling by promise and coupling by destruction are both couplings, and reuse of what survives is an opportunity, not a commitment. D4: the opposite extreme is reached in two steps, and the second correction is of promises, not mechanisms. Regrowth and the better mechanism.

*Kind:* the native lifetime as the lifecycle is enduring; hosts dying with node control is contextual (no native way back into their state); the three lifecycles are objective-bound. *Study:* E15, and E17 for the lifecycle.

### Descriptions

**Form and pressure.** Round 14 gave each object a "complete description" of six parts, so that a successor Interpreter could learn what a surviving object was. Readers of the code found the node never built it; its constructors left it empty. The Interpreter built it beside the node's wire fact and compared the two field by field, one copy made from the other by the same code. The owner on 2026-10-07: "Every additional independent representation creates an additional consistency obligation by construction" (`16-runtime-ontology/POSITION.md`, supplementary direction).

**Revision.** The description went as a record; its parts returned to their owners. The owner revised his own answer of two days before: "There is no such thing as a 'complete description' that requires construction, naming, qualification, and maintenance"; completeness comes from aggregating what the owners hold at the time of reading (same file, O4). A judge forced back the logical tag stored with each object, which a behaviour needed; the node's comparison of tags went, since it "could only detect the Interpreter contradicting itself". In Round 18 the description is what the node holds, each field with one writer, compared with nothing.

**Lesson.** B3 · One fact, one owner; J3 The owner test; J16 What reads it?, whose rule deletes a check that can only catch the writer contradicting itself; the reification chain. A removal keeps what a behaviour needs.

*Kind:* enduring; the fields are contextual. *Study:* E15 · The runtime ontology.

### Accounting and bounds

**Form.** On 2026-09-26 the owner had ruled out allocation ledgers. Round 14 nonetheless gave each table a fixed capacity with a stated answer on overflow, reserved refusal rows, capacity notices and about sixty site-fixed values. The owner's 2026-10-07 critique of how bounds were measured was answered with typed charges (E16).

**Revision.** On 2026-10-08 the owner moved the question: not whether accounting is precise, but "whether independent resource control commitments for these internal coordination structures were ever necessary in the first place" (`18-commitment-trimming/POSITION.md` §2). A judge showed the ceilings had manufactured the overflow they answered. In Rust on Linux an exhausted heap ends in an abort or an OOM kill, not a refusal; a refusal was reachable only because the system set its own row count below real memory, and then it needed a reserved row, a notice, an acknowledgement rule, a stall class, typed sizes and about forty operator values, each correct given the ceiling and none needed without it. Coordination structures became ordinary data bounded by construction: a record retires when its reader acknowledges it, a value is released at its last consumer, one count limits work in flight. One byte budget stayed, for host memory holding tensor data, since an OOM kill of node control loses the node's hosts. The weakening was stated: pathological growth is an OOM kill and a restart. The cross-review set the native OOM scores, since the kernel picks victims by size.

**Lesson.** The manufactured limit; regrowth and the better mechanism, across rounds; J12 The premise lever and J4 The failure question. B5's convergence caveat: loss is an answer only if what overflowed does not overflow again on restart, so the remaining bounds sit where a real resource or that convergence requires them.

*Kind:* the lesson is enduring; "heap exhaustion is an OOM kill, never a refusal" is contextual (Rust on Linux with overcommit). *Study:* E17, with its antecedents under E7 and E16.

### Check layers

**The sequence.** Round 05's form check passed while carriage stood at zero (E4); Round 11's registers became acceptance gates (E10); Round 15's `tools/check` grew a parallel semantics (E14); Round 19 placed project tests below the frontier (E18). Alongside these, the runtime re-verified what its own processes had produced: body digests re-hashed by the receiver, covers re-tiled, contribution certificates re-validated, read signatures, a host's first message compared with a record. Round 18 withdrew them: each compared a fact against its sender's own construction, both ends ran one release, and a mismatch is a bug that should fail loudly. Checks remain where something comes from outside the release: producer content, store answers, operator input, native library behaviour. The cost was stated: an internal bug surfaces as a decode or native error. Cross-review found the re-verification regrowing at admission and removed it. In each episode the check moved to the owner of the fact or went, capability a harness held returned to its component, and nothing replaced the removed layer.

**Lesson.** D3 · No second specification; B4 · Facts by construction, checks at boundaries; the check layer; the recognizer of excess "a check against a fact the system itself produced". Verification is a tool where it removes a decisive uncertainty or guards a boundary, and becomes a proxy goal elsewhere.

*Kind:* the principle is enduring; the release as the trust boundary is contextual, resting on an objective-bound assumption (one team builds every process; a trusted single-tenant site). *Study:* E17 for same-release checks; E4, E10, E14 and E18 for the layers.

## Cases recorded after the history: the trial

On 2026-10-10 one reader applied this Skill's problem side, without the history, to three tasks outside it: a simulation campaign locating tipping points of an ice-sheet model; a build system with two years of accreted mechanisms; and an insurer's claims engine to which a fraud score was to be added (I⁵ Round 02; the trial's record belongs to the research record described in [origins.md](origins.md), which is not distributed). The build system was a running example on both sides of the Skill and measured recall, not transfer; the other two are the evidence, two cases from one reader. They broke three premises the history held: one owner of meaning (the claims engine answers to a contract, a statute, a regulator and courts; the campaign to a field's conventions); a deterministic meaning with exact answers and pure sub-problems (a regime label near a boundary, a test verdict that varies between runs, a fraud score); and a system being formed rather than a live one reformulated part by part. The sentences added for them sit under existing moves: estimates as facts with a source and an uncertainty (R1), several holders of meaning (F5, M2), versioned meaning (R2, R3), exploration and stopping as policies (R6), the cost of a transition (M1, M2, M4), probes (F5) and checks of the link to the world (F1). The rename of F1 to "The fixed meaning" came from the same reading: "fixed point" names an equilibrium in the campaign's own domain.

*Kind:* the three premises and the sentences written for them are enduring as conditions; the tasks are contextual.
