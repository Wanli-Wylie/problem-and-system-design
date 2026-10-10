# Writing and working

How to write a design so that it can be built from without growing mechanisms it did not intend, and how to organize design and construction work among several people or agents without the organization becoming the work. The principles behind both are D3, D5 and D6 in [principles.md](principles.md); escalation is worked through in [judgment.md](judgment.md), J10.

## Contents

- [Part I. Writing a design](#part-i-writing-a-design)
  - [What the design is for](#what-the-design-is-for)
  - [Statement kinds](#statement-kinds)
  - [Layers, views and closure](#layers-views-and-closure)
  - [One definition, one word](#one-definition-one-word)
  - [Freedom as the default, and limits by kind](#freedom-as-the-default-and-limits-by-kind)
  - [What to leave out](#what-to-leave-out)
  - [The record beside the design](#the-record-beside-the-design)
- [Part II. Organizing the work](#part-ii-organizing-the-work)
  - [Units of work and where authority lives](#units-of-work-and-where-authority-lives)
  - [Direction from whoever owns the meaning](#direction-from-whoever-owns-the-meaning)
  - [Briefs](#briefs)
  - [Readers by boundary, judges by question, writers by part](#readers-by-boundary-judges-by-question-writers-by-part)
  - [The spine](#the-spine)
  - [One cross-reading and one fix pass](#one-cross-reading-and-one-fix-pass)
  - [Rulings](#rulings)
  - [Construction](#construction)
  - [Verification during construction](#verification-during-construction)
  - [What has worked and what has not](#what-has-worked-and-what-has-not)

## Part I. Writing a design

### What the design is for

A design document is the authority from which a system is built. That role changes how each sentence is read. A builder, and especially an agent, reads the text literally: a sentence written to explain becomes a condition, and the condition becomes a check in code. A universal sentence that ordinary engineering cannot meet ("no wakeup is lost", "each refusal is reported") grows a mechanism to meet it. A sentence about what the system does not provide becomes a prohibition someone enforces. Write as if each sentence will be implemented, because it will be.

The design says what the system is, what each part is responsible for, and how the parts relate and compose. It is written constructively. It is not a record of how it was reached, a list of what was rejected, or a defence against past mistakes.

### Statement kinds

Each sentence in a design is of one kind, and the kind should be plain from its form or its place.

| Kind | What it is | Binds construction? | Example in an ordinary system |
|---|---|---|---|
| Guarantee | Something a user or operator relies on. There are few. Each is stated once, where its consumer would look. | Yes, exactly | "An order that has been confirmed to the customer is charged at most once." |
| Safety rule | A claim where acting on a guess would corrupt data or a resource. Marked as such. A universal ("every", "never", "in all interleavings") belongs here, or in a guarantee a structure makes true by construction. | Yes, in its strict form | "A storage block is never reused while a reader may still hold a reference to it." |
| Boundary form | What crosses a real boundary: a message, a durable record, a file format, a document another party writes. | Yes, exactly | The schema of the order event published to the warehouse. |
| Mechanism | A chosen means. It may change while the guarantees and boundary forms hold. | As described, but replaceable | "Status changes are written in the same transaction as the order row." |
| Explanation | Why something is as it is, an example, an illustration. | No | "This keeps the account page consistent without a reconciler." |

Only guarantees, safety rules and boundary forms bind the implementation exactly. Mechanisms are built as described, but a better mechanism that keeps the guarantees is a legitimate change, not a deviation. Explanations bind nothing; if an explanation is needed to make a guarantee true, it is a guarantee and should be stated as one.

Two consequences follow. First, keep guarantees few and in their users' words; a guarantee that describes an internal structure ("the scheduler's queue never exceeds its bound") is usually a mechanism that has been promoted, and it will be defended as if users relied on it. Second, when you weaken a guarantee on purpose, say so where the guarantee is stated, with what a user will see. A silently weakened guarantee gets built as if it still held.

### Layers, views and closure

A design of any size is read at more than one depth. Organize it as a few layers on one line of elaboration, each a closed description of the whole system at one scale, plus views beside the line that are not rungs on it.

**Name each layer by the question it answers and by what closes it.** A top layer might answer "what is the system answerable for, and who decides what?" and close when each kind of decision has one owner. A contracts layer might answer "what do the parts rely on from each other?" and close when each exchange has its parties, content, endings and the meaning of each ending. A mechanisms layer answers "how does each owner do its job?". A runtime layer answers "what processes run where, on what technology?". A software layer answers "what code structure realizes this?". Your system may need fewer; impose no layer that cannot pass truncation on its own.

**Two placement tests decide where a statement goes.**
- *Contract or mechanism.* What two parties rely on is a contract; what only one owner relies on is mechanism. If a lower layer finds it needs something of the first kind (an outcome, a base case, a rule an argument rests on), the layer that owns the argument is incomplete and is fixed there.
- *Rule or selection.* A rule belongs above the technology layer if an argument made there depends on it whatever the technology. The technology layer holds selections: choices where any alternative would leave the argument above valid.

**Name technology where it is the selection.** Above the technology layer, describe the environment by role and required property ("a store with a conditional create"), and name the product where it is selected. Do not forbid technology names so strictly that you must invent stand-in concepts to avoid them; for example, in one distributed runtime, a strict ban produced invented concepts that later failed the boundary test ([cases.md](cases.md), E13). The test is whether the argument above survives any alternative selection.

**Define endings by evidence, not procedure.** In a contract, define each way an exchange can end by the evidence it requires ("refused before any effect" requires proof that no effect occurred), not by how that evidence is produced. This keeps contracts free of the mechanisms below them.

**Keep views beside the line.** Some descriptions are not the system at a scale. A language the system processes refers to nothing in the system, and the system's layers use it. The production of the system over time (build, release, deployment, upgrade) reads all the layers and nothing reads it. Making either a layer gives that layer two forms of closure and makes truncation meaningless. And the source tree is a maintenance structure, organized by what changes together and when; it is not a projection of the concept model.

**Test with truncation, deletion and example deletion.** Stopping at a layer, the reader should hold a correct system at that scale. Given only the design, a newcomer should be able to continue the work. An upper layer may illustrate with a lower-layer instance, but deleting the example must leave the meaning intact; a sentence that fails this is leakage.

**Lower layers add; they do not retell.** Each layer says what is new at its scale and links up for the rest. A design that retells the same behaviour in four layers in four vocabularies gives itself four chances to disagree.

### One definition, one word

State each thing once, where it is owned, and link to it from elsewhere. A concept is defined in the highest layer where it can be stated whole, or in the language view if it belongs to the language. Two statements of one rule drift into two rules; a builder who finds both will implement one and check against the other.

Fix the vocabulary before parallel writing begins. One word per thing, one thing per word. Where two different things share a word in current use (an act's outcome and a process's ending; a resource type and a build profile), separate them before anyone writes, and record the separation where writers will see it. Vocabulary drift between parts written in parallel is the commonest inconsistency a cross-reading finds.

Give the design a short entry document: what the system is in a paragraph, how the design is read (its layers and views, its statement kinds), and its layout. This is an index, not a summary; it does not restate the chapters.

### Freedom as the default, and limits by kind

What the design does not state as a guarantee, safety rule or boundary form is the implementation's choice. Say this once, in the entry document, so that builders do not treat silence as prohibition or as an invitation to ask.

Tuning values have defaults in code. An operator states only what is genuinely the deployment's: its identity, endpoints, locations, credentials. A value without a default makes the operator invent a number for something the developers understand better, and it makes the number look like semantics when it is tuning.

Latitude is written into the definition of the thing it applies to ("the reduction may be performed in any order"), not granted separately. A separately granted freedom has an edge someone must police.

Limits come in kinds; keep them apart and do not close any of them with an invented default:

| Kind of limit | What it means | How the design says it |
|---|---|---|
| Not yet designed | A real need with no design yet | In the owning chapter, with what blocks it |
| Absent from this build | Designed or designable, not built | Not a prohibition; nothing forbids adding it |
| Accepted limitation | A decided absence users rely on knowing | Once, where the affected guarantee is stated |
| Not reached | No probe or flow has exercised it | Recorded as open, not as settled |
| Release gate | Must be shown before it is offered | With the condition for offering it |

And a design element can have a standing: committed; a decision to be made (with its alternatives and what each would block); or to be established against the real environment.

### What to leave out

Each item below has cost real systems mechanisms. Leave them out, for the reason given.

- **History as reason.** "As decided in", "unlike the previous version", "for compatibility with the old model". A decision holds because of its reasons; the record of who and when lives beside the design. One file, the change note, may name the previous design.
- **Defensive wording.** Prohibitions written against past mistakes, warnings, "must not under any circumstances". They turn into checks for things nobody would do.
- **Lists of what the system does not provide.** Each becomes an enforced prohibition. State a decided absence once, as an accepted limitation, where a reader of the affected guarantee would look.
- **Restatement of the platform's semantics.** If the database, the operating system or a library defines a behaviour, rely on it in one sentence; do not copy its contract into yours.
- **Universal sentences that would need a mechanism.** "Every request is logged", "no event is ever dropped". A universal belongs in a safety rule, or in a guarantee that a structure makes true by construction (typing does not wait on extension code, because the code runs in another process); where meeting it would need a mechanism, it grows one. If it is a guarantee, state it as one, scoped; if it is a mechanism, describe it as one.
- **Coverage for its own sake.** Sections that exist because the template has them; corner cases enumerated because they can be.
- **Polish while the design moves.** Terminology sweeps, editorial convergence and restructuring wait until the design has stopped changing substantively. Before that they freeze wording that is about to change.

### The record beside the design

The design states what the system is. The reasons for decisions, the alternatives considered and the history live beside it, in records that do not substitute for it.

**The decision record.** One row per decision: what was asked, its kind (engineering choice, consequence of the design, fact of the stack, choice of meaning), the outcome in one line, and where the design now says it. Keep it concise. When the record grows into a parallel account of the system, it has become a second design.

**Rulings on removals.** A ruling on a removal names what carries the behaviour now and what is lost; the full form the record prescribed also names what stays and what goes. It names the real resource the removed rule covered. The reasoning behind a ruling (the behaviour it serves, the verdict, the native form, what is lost, what is gained) may be longer and lives in the working record of the judges who reached it.

**The words of whoever owns the meaning.** Direction and answers from whoever owns the system's meaning are recorded verbatim, with the date. Code or design text that depends on an answer cites it rather than restating it.

**Read-only records.** A completed record is not amended to reflect a later decision. The later decision is recorded later, and it says what it inherits, supersedes or reinterprets. This keeps the reasoning at each point recoverable, which is what lets a later revision reread a premise instead of only its conclusion.

**The change note.** When a design is rewritten, one file maps old to new: what was withdrawn, what replaced it or that nothing did, and why. It is the only place the design names its predecessor.

## Part II. Organizing the work

This is the organization that worked for large designs read and built by many agents under one owner of meaning; that form is objective-bound, so take from it what your scale needs. The parts that hold at any scale are one spine of names, one independent reading, escalation by semantic consequence, and state recovered from the design and the product. The aim throughout is that the organization serves the design and does not become a second object that defines it.

### Units of work and where authority lives

Organize design work in bounded units, each with its own direction, inputs, deliverable and standing (open, completed, superseded). For example, one design effort ran as numbered research rounds, each a directory with its direction recorded verbatim, its working material and its deliverable ([cases.md](cases.md), E12). The form is contextual; what matters is that each unit says where its deliverable is and what standing it has.

Design authority lives in the deliverables of these units, not in a global file that spans them. A global document that accumulates design principles, constraints and history becomes an unreviewed design in its own right; keep any global file to how the work is organized and how to find the current state. A later unit records what it inherits from earlier ones, what it supersedes and what it reinterprets.

Working material (briefs, reading reports, judgments, notes) holds no authority. It is input to the deliverable.

**Which loop a unit is in.** A unit names which of the two loops it is in and what it hands the other, by the rule of [L1 Which loop](reformulation.md#l1-which-loop). Semantic consequence, the criterion escalation already uses (D6; J10 in [judgment.md](judgment.md)), separates a change of what is asked (one that alters what the system is answerable for, what it fixes or what a party relies on), which goes to whoever owns the meaning, from re-rendering and replacement, which are decided as engineering and recorded under [M4 The record](reformulation.md#m4-the-record).

### Direction from whoever owns the meaning

Whoever owns the system's meaning gives direction: what the unit is for, what it must not become, and any premise it is to take as fixed. Their role is to fix the principled world of the system and let the platform, the language and the engineering judgment of those doing the work complete the rest.

Some practices that kept work moving:

- **Approval with defaults.** When a plan lists default assumptions for open questions, approving the plan adopts the defaults as decisions, and work proceeds without a second round of approval.
- **Bounded sessions.** A unit of work is bounded to one question, with the layers or decisions it must not reopen named.
- **Gates before execution.** Where the next phase is expensive to undo (writing the full design after its structure; construction after design), stop for approval at the gate rather than running proposal and execution as one continuous flow.
- **Intervention by kind.** The owner of meaning intervenes most usefully by naming a kind of structure that is growing (a check layer, reified objects, accounting for internal structures, tests treated as product), not by fixing individual defects. Naming the kind lets those doing the work find all its instances.

### Briefs

A brief tells one worker what to do. It says what the task is and why; what to read and in what order; what not to do (the over-corrections to avoid, not a list of forbidden words); the form and budget of the output; and where to record objections. It gives the worker the canonical names to use. A good brief is short enough to be read in full and specific enough that two workers given it would produce compatible outputs.

### Readers by boundary, judges by question, writers by part

When a large design or codebase must be read and judged, divide the work by the shape of the system, not by an inventory of its objects.

**Readers by boundary.** Each reader takes one real boundary of the system (a process boundary, a durable store, an external interface) and reports how the design's named things cross it: as identities, carried fields, registries, lifecycles or computed relations, and where construction strained. Readers report evidence and may give a first judgment, but their judgment is an input. Readers who see code without the whole tend to propose removals more aggressively than the whole supports.

**Judges by question.** Each judge takes one question that cuts across the boundaries ("what does recovery need?", "what does the interior of this component need to retain?", "if this were built today from its behaviours and its platform, what shape would it have?"). Each judge starts from a list of behaviours that must hold between parties, over time and after loss, written without naming any object the design introduced. Everything is judged against that list. This is what protects against over-correction: a removal that breaks a behaviour on the list is forced back. Judges read the design and the code themselves where a verdict turns on it. One judge should hold the whole.

**Whoever leads rules.** Disagreements between readers and judges, or between judges, are resolved in writing with the reason, and the reasons are kept. Lead rulings sometimes go against all the judges; the record should show why.

**Writers by part, against a spine.** Writers each take one part of the deliverable and write it against the spine. Each keeps notes: what they introduced, what they left for another part, what they could not resolve, what they believe the spine gets wrong. An integrator then makes the parts one design.

### The spine

Before writers work in parallel, whoever leads fixes one working document: the names everything will be called, the positions taken, where each shared concept is defined, what has been withdrawn and what now carries it, and the budget for each part. Parallel writers without a spine produce several designs that must then be reconciled by argument. A spine with a short table of withdrawn things, each with the function standing in its place and the names it is likely to return under, is an effective defence against regrowth during writing.

The spine is a working document and holds no authority; the deliverable does. Writers who disagree with the spine write to it and record the objection, so that the disagreement reaches whoever leads instead of becoming a second formulation in the deliverable.

### One cross-reading and one fix pass

After a version is formed, it gets one independent reading, by readers who did not write it, followed by one fix pass. Judging, cross-reading and fixing are different tasks and may each have their phase; what is avoided is the loop: review, fix and re-review cycles of one version become the work, and each cycle polishes what the last one introduced.

Cut the cross-reading along lines that cross the parts: the main path end to end; resource safety; whether the design keeps only what it must own; whether a builder could build it from the text. Classify findings as broken, inconsistent, a gap, regrown, or over-trimmed. Style, wording, length, and anything the spine settled are not findings. Whoever leads rules on each finding, accepting the finding's own smallest fix where it is sound.

What cross-readings tend to find: contradictions between layers written by different hands; a removed mechanism whose replacement rules were not written; things regrown under new names; and safety at the joins with real resources, where a removal left a resource outside any rule. Plan for these.

### Rulings

A ruling records a decision on something that changes. A ruling on a removal names what carries the behaviour now and what is lost; the full form the record prescribed also names what stays and what goes. It names the real resource the removed rule covered. Where a ruling disposes of an open question, it says which. Where a ruling touches an earlier decision by whoever owns the meaning, it says so, so that the owner can see which of their own sentences is being reread.

Rulings are terse. The reasoning lives in the judgments that reached them, and the design does not depend on either.

### Construction

Construction builds the product from the design and is also the design's most literal reading. Organize it so that the product's state is recoverable at any point from the design and the product itself.

The history this section draws on had no live users; the rules for a live system follow from the reasons, not from a case. In a system with live users, the final form is reached through steps each of which leaves the system serving; moving units (orders, tenants, teams) from old to new while the old drains is migration, not a compatibility layer, provided no unit is governed by both; onboarding first users to learn what the defaults should be is a probe, not a pilot.

**Two sources of truth.** The design says what the system should be; the product (the code tree and its history) says what has been built. Nothing else may come to define either. No plan files, backlogs, status files, ledgers or coverage maps carry authority; a planner reconstructs the state of the work from the design and the tree each time. Tests confirm that the implementation meets the design and do not set the frontier; where they set it, they become a second specification and progress becomes making them pass. Harnesses that feed the product facts its own components should establish become an alternative source of truth, with entry points in the product that exist only for them.

**The frontier.** The frontier is the set of parts of the design not yet built whose prerequisites already work in the product. Among them, choose the transition that makes most of the system real: what most other parts need, and the owners whose absence leaves built parts without their designed caller. The frontier is not the shortest path to a demonstration. Code that contradicts the design is part of the frontier; nothing in the product is kept because it exists.

**Cuts.** Each cycle makes the largest coherent transition toward the final form that it can. Several small transitions are worse than one coherent one, because each small one leaves seams that the next must accommodate. Each layer built is the final one for its part: no pilots, toy versions, placeholders or mock services. What runs first becomes the architecture, and a stub lets a missing owner look present; a capability not yet built stays unbuilt and visibly so, and one the environment cannot yet supply is unavailable rather than simulated. Frameworks, plugin layers and generic helpers for parts not being built wait for their consumer, whose shape they would otherwise fix.

**What counts as progress.** After a cycle, the product holds a capability of the designed system that it did not hold before, in final form and connected to what was there. Files nothing uses, structure without behaviour, stubs, harnesses, documents, renames and a fix to a problem the same cycle created are not progress. A cycle that makes none means the next cycle changes approach, not that it retries the plan.

**Cycles.** Plan, execute, synthesize. The plan is a short message for this cycle (the state, the transition, the units of work, how they integrate, what may go wrong) and ends with the cycle. Workers have disjoint write scopes. Whoever synthesizes makes the result one coherent whole and records it.

**The record of a cycle.** Record what was built (by component, and what it connects to), what was removed and which owner, protocol, native mechanism or derivation now carries its behaviour (or that nothing does), the local decisions made and where they live in the code, and what remains open at the seams. Do not record evidence of verification (hashes, counts, transcripts of passing runs): the history is the record of the system's evolution, not an evidence system, and evidence crowds out description.

**Questions during construction.** Classify each issue: an engineering choice (settled by whoever is doing the work, recorded in the code); a local design gap (settled by the reading most consistent with the surrounding design, recorded at the code and in the cycle record); an environment issue (changes nothing in the design); or a semantic question (would change what the design states: a contract, a guarantee, an identity, a format's meaning, who owns what). Only the last goes to whoever owns the meaning, and it blocks only the work that depends on it. A difference between the product and the design is implementation work, not a question. Before raising a semantic question, ask whether the thing it assumes should exist (J10).

**Construction as reverse pressure.** When construction keeps adding fields to complete an abstract object, mirror functions to keep records in step, or accounting for internal structures, stop treating it as incompleteness of the code. Read it as evidence about the design (D2, J7). If the pressure is consistent, the right next step may be a design revision, with construction paused until the revised design converges.

**Revision during construction.** When the design changes, construction moves behaviour to its newly designated owner and removes the old structure inside the cycle that builds that owner, not as a separate cleanup project, sweep or inventory. A part of the product changes because of what it does and who should do it, not because of the words it uses: a rename that leaves behaviour and ownership where they were is not a transition. Inside a set of parts changed together, no compatibility layer keeps an old structure and its replacement alive together; at a boundary with parties who cannot change with you (a public API, a file format, an extension contract), compatibility is a guarantee and is paid for there ([literature.md](literature.md), T5). A withdrawn structure is not rebuilt under another name, as a smaller version or as a better mechanism for the same job; the premise that removed it still holds, so ask J4 of anything new.

### Verification during construction

Two clarifications prevent over-correction. Verification is part of ordinary engineering: compiling, running, tracing paths and integration checks are encouraged, as working acts that leave nothing later work relies on as evidence. And tooling that users run (a conformance suite for other implementers, an acceptance kit for operators) is a capability of the product and is built as product when it is the frontier. What a verification is for decides its standing.

When cycles turn into checking or auditing sweeps rather than building, whoever coordinates stops and reports to whoever owns the meaning.

### What has worked and what has not

The evidence for which of these practices worked and which did not, in the history this methodology was drawn from, is in [cases.md](cases.md). The study that weighed it is part of the research record behind the methodology, which is not distributed with this Skill; [origins.md](origins.md) says what that record holds.
