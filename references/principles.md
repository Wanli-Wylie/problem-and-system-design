# Principles

The nineteen design principles of this methodology, each in its operative form. [SKILL.md](../SKILL.md) gives them in one line each; this file gives the depth you need when a principle is in question.

## Contents

- [How to read this file](#how-to-read-this-file)
- [A. What the system is answerable for](#a-what-the-system-is-answerable-for)
  - [A1 Responsibilities before mechanisms](#a1-responsibilities-before-mechanisms)
  - [A2 Effectiveness over completeness](#a2-effectiveness-over-completeness)
  - [A3 Fix meaning, free execution](#a3-fix-meaning-free-execution)
- [B. What exists already, and what the system must add](#b-what-exists-already-and-what-the-system-must-add)
  - [B1 Design inside the existing world](#b1-design-inside-the-existing-world)
  - [B2 A concept is not an object](#b2-a-concept-is-not-an-object)
  - [B3 One fact, one owner](#b3-one-fact-one-owner)
  - [B4 Facts by construction, checks at boundaries](#b4-facts-by-construction-checks-at-boundaries)
  - [B5 One path for loss](#b5-one-path-for-loss)
  - [B6 Lifecycles belong to their mechanisms](#b6-lifecycles-belong-to-their-mechanisms)
- [C. How the whole is organized](#c-how-the-whole-is-organized)
  - [C1 Closure at each scale](#c1-closure-at-each-scale)
  - [C2 Boundaries from responsibility, not symmetry](#c2-boundaries-from-responsibility-not-symmetry)
  - [C3 Distinctions as fine as their consumers](#c3-distinctions-as-fine-as-their-consumers)
  - [C4 Expand the platform, not the special case](#c4-expand-the-platform-not-the-special-case)
- [D. How the work is done, and how it revises](#d-how-the-work-is-done-and-how-it-revises)
  - [D1 A concrete object early](#d1-a-concrete-object-early)
  - [D2 Construction is evidence](#d2-construction-is-evidence)
  - [D3 No second specification](#d3-no-second-specification)
  - [D4 Revise at the level of premises](#d4-revise-at-the-level-of-premises)
  - [D5 The design explains itself](#d5-the-design-explains-itself)
  - [D6 Escalate by semantic consequence](#d6-escalate-by-semantic-consequence)
- [Where the principles pull against each other](#where-the-principles-pull-against-each-other)
- [How the principles make one method](#how-the-principles-make-one-method)

## How to read this file

Each principle has the same elements: a **statement** in its mature form; **why** it holds and what failure it prevents; **where it came from**, as the moves of the source history (told in [cases.md](cases.md)); **what it is not**, the over-correction, which is part of the principle, because nearly all of these were first stated together with their opposite danger and a principle without it becomes a slogan pushed too far; **when it applies**; **signs you are violating it**; and the **kinds** of its examples. The principles are stated at the enduring level. Examples are **contextual** (they hold because of a technology) or **objective-bound** (they follow from one system's goals). Import the principle, not the example. The examples from the source history come mostly from one distributed runtime for scientific computation.

## A. What the system is answerable for

### A1 Responsibilities before mechanisms

**Statement.** A design begins by naming the few things the system is answerable for, in the words of those who rely on it, and derives from them the guarantees it makes. Everything else is a chosen means that may change while the guarantees hold. The count is small. The system's purpose (for one system, efficient use of hardware) is the measure by which the whole is judged, not a guarantee; it binds no construction below it. An aim binds nothing while it is an aim; the same aim stated as something a named party observes and relies on, with its scope (typing does not wait on extensions; one team's volume does not degrade another's; cost grows in a way a team can see and steer), is a guarantee and is written as one, with its bound. Cost, responsiveness and data protection enter the design this way, as responsibilities with a party, not as purposes. Each relinquished commitment is stated with its user-visible cost, and a weakened guarantee is named as weakened.

**Why.** Mechanisms justify one another. A bound needs a refusal, the refusal a report, the report an acknowledgement, each correct given the one before. Without a short list of responsibilities there is nothing outside the chain to ask whether the first link was needed. The list also tells the implementation where it is free. Stating the cost of a relinquished commitment keeps the trade honest; a silently weakened guarantee gets built as if it still held.

**Where it came from.** E13 The closed, self-explaining design; above all E17 Commitment trimming, which reduced a long list of responsibilities to three and reread the earlier principles as their applications.

**What it is not.** It is not a call to promise little. A responsibility that users rely on is kept in its strict form however expensive it is. It is not a mission statement: a purpose turned into a guarantee binds each lower layer to defend it. And it is not a fixed list: when the objective changes, the responsibilities change and their mechanisms are reexamined.

**When it applies.** At the start of any design and at each revision; most of all in systems that have accumulated mechanisms nobody can trace to a user. The responsibilities are the answerability of [F2 Answerability](formulation.md#f2-answerability), stated there and received here; promises to a party are kept apart from the means of keeping them.

**Signs you are violating it.**
- The design opens with components rather than with what anyone relies on.
- A requirement cannot be traced to a user or operator who would notice its absence.
- The guarantees describe internal structures.
- An aim appears as a guarantee that lower layers must prove, with no named party who relies on it.
- A change weakens what a user can rely on and the design does not say so.

**Kinds of example.** For example, in one distributed runtime, the three responsibilities were control of real computational resources, correctness of results and persistence of progress ([cases.md](cases.md), E17). That list is objective-bound: a system with different users would have a different list. Reducing to a few responsibilities and rereading the principles as their applications is enduring.

### A2 Effectiveness over completeness

**Statement.** The objective is the whole system's effect in the world, not the formal completeness of its description, the uniformity of its mechanisms, coverage of each corner case, or the improvement of a local metric. A semantic space is kept small but is bounded by what the system must be able to do well, not by minimalism for its own sake.

**Why.** Completeness, uniformity and coverage are easy to measure and to show, so they attract effort, and the effort goes to the representation rather than the system. None of them is what users get. The second half guards the other side: a semantic space kept small for smallness lacks what the system needs to perform, and performance is then recovered by special cases outside the design.

**Where it came from.** E3 Indexing without designing (record a gap; do not fill it from general knowledge); E4 The generic model closed; E10 The skeleton's checks removed (completeness and checks as proxy goals); E12 Authority into the rounds; computation versus execution (a small semantic space bounded by performance); E17 Commitment trimming (requirements of another class of system).

**What it is not.** It is not indifference to correctness or to edge cases that users meet. It is not a license to leave the design vague; vagueness is not effectiveness. And it is not minimalism: if a capability matters to what the system must do well, it belongs in the core even if it enlarges it.

**When it applies.** Whenever a design is judged, by its authors or by others. It is most needed when the judgment is being made by counting: sections filled, questions answered, cases enumerated, tests passing.

**Signs you are violating it.**
- Success is reported as a count (questions closed, coverage, rows dispositioned) rather than as a capability.
- A section exists because the template has one.
- Corner cases nobody will meet have their own states, modes or ordering rules.
- A distinction was dropped to keep the core small, and performance now depends on an undocumented special path.

**Kinds of example.** For example, in one distributed runtime, the computational language admitted a feature only if it was "materially useful for high-performance realization", which kept the language small without starving it ([cases.md](cases.md), E12). The criterion is objective-bound (performance was that system's purpose); bounding a semantic space by what the system must do well is enduring.

### A3 Fix meaning, free execution

**Statement.** A specification fixes what is computed or promised, with only the constraints needed to establish identity and correctness, and leaves how it is realized to whoever can choose with the most information at the time of choice. Freedom is the default: what the design does not state as a guarantee or a boundary form is the implementation's choice; tuning values have defaults; the design does not list what it does not provide. In its sharpest form, latitude is a property of the definition of the thing it applies to, not a separately granted resource. Proposal, decision and execution are kept apart: a proposal confers no authority, and a decision has one decider.

**Why.** A specification that fixes how forecloses realizations the specifier could not see; the party closest to the execution, at that moment, usually knows more. The sharpest form matters because a freedom granted as a separate thing has an edge that must be policed: someone decides whether an act falls inside the grant, and becomes a hidden second decider. When the latitude is part of what the operation means ("this reduction may be performed in any order"), there is no edge to police.

**Where it came from.** E2 Removing the database frame (freedom defined by the instruction's own semantics, which dissolved a tension found three times); E12 Authority into the rounds; computation versus execution; E17 Commitment trimming (defaults, not mandates).

**What it is not.** It is not underspecification. Where identity, correctness or a boundary form needs a constraint, the constraint is fixed exactly. It is not freedom for the sake of freedom either; a choice nobody can make well (because nobody holds the information) is better fixed. And "the design does not list what it does not provide" does not forbid stating a decided absence that users rely on; it forbids prohibitions written for features nobody offers.

**When it applies.** In any interface between a party that says what and a party that decides how: a language and its compiler, an API and its implementations, a job specification and a scheduler, a protocol and its peers. The formulation chooses the representation and says what it fixes ([F1 The fixed meaning](formulation.md#f1-the-fixed-meaning)); this principle holds that line in the design and frees execution beneath it.

**Signs you are violating it.**
- The specification says how ("use a hash map", "process in arrival order") where only what matters.
- A "latitude", "policy" or "permission" object stands beside the operations it governs.
- Operators must supply values the developers understand better, with no defaults.
- A current limitation of the implementation is written as a rule of the language.

**Kinds of example.** For example, in one distributed runtime, a tensor language fixed the computation and left tiling, placement and fusion to the interpreter ([cases.md](cases.md), E12). Where that line fell is objective-bound. The principle, and especially the rule that latitude belongs inside the definition, is enduring.

## B. What exists already, and what the system must add

### B1 Design inside the existing world

**Statement.** The operating system, the language, the libraries, the hardware and the services around the system already have semantics, lifecycles and boundaries. A problem is first asked of them; many dissolve; what remains is designed as a real software structure before any new general concept is considered. A system owns exactly the knowledge only it has and lets each other fact be carried by its owner.

**Why.** Rebuilding a facility that exists creates a second, weaker copy of semantics someone else maintains, and the two must agree. Designing from an empty world also leaves concepts defined only by other concepts. Asking the world first turns abstract problems into concrete questions ("does the process boundary already isolate this?") whose answers are facts.

**Where it came from.** E5 The concrete object; E6 Constructive contact and flow pressure (question, then constructive mechanism, then specification); E7 Runs as processes, no mini-OS; E15 The runtime ontology; E17 Commitment trimming (own what only you know).

**What it is not.** It is not "the old design minus what the platform supplies": the coordination between existing components is often exactly what the system must own. It is not a special case per backend: semantics that must hold across realizations stay explicit above them. And it is not bending a sound design to the API shape of whatever library is at hand.

**When it applies.** Whenever the system runs on, calls or sits beside anything mature; most of all in infrastructure and services, where rebuilding scheduling, isolation, retry or storage is tempting.

**Signs you are violating it.**
- The design has its own scheduler, quota system, retry layer, lifecycle manager or isolation mechanism beside a platform that provides one.
- A problem is answered by a new concept before anyone asked whether the operating system, database or queue already answers it.
- The design restates the semantics of a library or service as its own contract.
- Each backend has its own meaning for the same outcome.

**Kinds of example.** For example, in one distributed runtime, run isolation was delegated to operating-system processes, and per-run quotas and ledgers were refused ([cases.md](cases.md), E7). The particular substrate (Linux, a specific language, a specific coordination service) is contextual; the principle is enduring.

### B2 A concept is not an object

**Statement.** Naming something in the design language does not give it runtime identity, schema, lifecycle, registry or protocol. A thing exists in the running system only where it must cross a real boundary: between processes or machines, across time or restart, between concurrent owners, between an asynchronous operation and its completion, from untrusted input, from an external resource's lifetime, from state only a remote party knows, or as a public contract its consumers depend on. What fails this test is scaffolding for the designer's reasoning and stays in the design language.

**Why.** Designers need concepts to think. The failure is to carry them into the runtime, where each must be created, identified, stored, kept consistent and validated, and none of that serves a user. Each item on the boundary list is a place where something real (a process, time, another owner, an untrusted party) makes an explicit representation unavoidable. Where none applies, the thing can be a type, a function, a module or a local relation, which cost nothing at runtime.

**Where it came from.** E4 The generic model closed; E15 The runtime ontology (the threshold and the boundary test); E13 The closed, self-explaining design as the counter-case, whose drive to completeness added objects later removed.

**What it is not.** It is not anti-abstraction: formal structures at real boundaries (a wire protocol, a durable record format) are what the design should fix. The design text may keep a rich conceptual language as explanation while the runtime keeps only what must exist. And after removing an overweight model, its objects usually disappear into ordinary structures; they are not replaced by a better model. A registry is asked the same question: where the set of extensions is fixed when the system is built, a build-time list or the module system is the place; where third parties add extensions at run time, the registry crosses a real boundary and holds only what must be known before their code loads.

**When it applies.** Whenever a noun in the design is about to become a class with an identifier, a table, a message type, a registry entry or a state machine. The list of boundaries is phrased for software that spans processes and time; for other systems, ask the same question with the boundaries your system has (a public API to third parties, a file format on disk, a user's device and a server).

**Signs you are violating it.**
- An identifier exists that nothing outside one process ever reads.
- A descriptor or "definition" object restates what the type system or module structure already says.
- A local relation has been promoted into an entity with identity, description and persistence.
- Justifications offered for a new object are "it unifies the description", "it lets implementations fit one schema" or "it makes the system easier to reason about".
- A tree of sub-problems, a process per level of a decomposition or a registry of sub-problems, where the problem's own derivation would serve ([R3 Derived, not stored](recursion.md#r3-derived-not-stored)).

**Kinds of example.** For example, in one distributed runtime, a "complete description" object for each data object, assembled by one party and compared field by field against another party's copy, was removed; the description's parts returned to the owners that actually held them ([cases.md](cases.md), E15). The boundary list is close to enduring but phrased for distributed software; the test itself is enduring.

### B3 One fact, one owner

**Statement.** Each independent representation of one fact is a consistency obligation by construction. Each fact has one authoritative carrier; other views are derived on demand; no party is asked to check that copies agree; a way of describing a fact does not become a fact the system must manage.

**Why.** A second copy is not free. It must be written when the first changes, it can be stale, and the reconciliation code is then tested and debugged as if it were a feature. The check between copies usually detects only the writer disagreeing with itself, because both came from one source. Naming one carrier removes the obligation instead of discharging it.

**Where it came from.** E15 The runtime ontology (a stored pointer that duplicated a chain's head removed); E16 Behaviour decides, not names (no dual representations kept in step); E17 Commitment trimming (same-release re-verification withdrawn).

**What it is not.** It is not a ban on caches or on replication. A cache is a derived view that may be discarded; replication for availability is a mechanism with one authoritative history. It is not a ban on checks between genuinely independent sources either: bytes received against the content identity they were requested by, or a remote party's report against what was asked of it, are two facts, not one fact twice.

**When it applies.** Anywhere state is stored, carried in messages or published: databases with denormalized columns, services with their own copy of another service's data, configuration repeated in several files, documents that restate other documents.

**Signs you are violating it.**
- A reconciler, sync job or consistency checker whose only purpose is to keep two of your own records in agreement.
- A field that is computed by the writer, stored, recomputed by the reader and compared.
- A fact recorded in two places with a repair procedure for when they disagree.
- A "frontier", "summary" or "status" record beside the data it summarizes.

**Kinds of example.** For example, in one distributed runtime, a separate pointer to the latest committed record was removed because the chain's valid head already was the durable position ([cases.md](cases.md), E15). The specific stores are contextual; the principle is enduring.

### B4 Facts by construction, checks at boundaries

**Statement.** A property is made to hold by the program's structure (types, ownership, data flow, create-once keys, single writers) rather than established and then verified. Checks sit where something crosses a trust boundary or where a wrong claim would corrupt data or a resource. A trust boundary raises two questions: where checks go, and what the party behind it may do. Claims of that second kind (that a resource may be reused, that an effect did not happen, that a value is ready, that participants acted in one order) need positive evidence in every interleaving, and silence and timeouts never supply it. This is the safety floor, and "every" and "never" in it are meant literally. Everything else is ordinary engineering: events as the norm, timers as insurance, bounded retries, a clear failure when nothing can change.

**Why.** A check is paid on each act and catches only what its author thought of; a structure that makes the wrong state unrepresentable is paid once and covers cases nobody listed. Where something enters from outside the system's control, or acting on a guess would silently corrupt state, the check is the design. The safety and liveness split puts rigour where a mistake is silent and harmful, and leaves waiting and retrying, where a mistake is visible, to ordinary engineering.

**Where it came from.** E17 Commitment trimming (facts by construction; safety strict, liveness ordinary; the trust boundary); E14 Construction and the check layer; E12 Authority into the rounds; computation versus execution (validation removed, preconditions kept).

**What it is not.** It is not "no validation". Untrusted input, external services' answers, operator configuration and remote state are checked. It is not a relaxation of safety: the claims listed above keep their strict form however much else is relaxed. And removing a validation mechanism does not delete the precondition it checked; the precondition remains part of the definition and is met by construction or by the caller. A check of the link between a representation and the world (a key's completeness, a model's convergence) is not a check of a fact the system produced; it belongs at the boundary where facts come from outside ([F1 The fixed meaning](formulation.md#f1-the-fixed-meaning)).

**When it applies.** In any system that checks its own outputs, re-validates data between its own components, or uses timeouts as evidence. The placement of the trust boundary depends on who builds and deploys what. Parties who cannot change with you (authors of extensions, consumers of a public API or a file format) are across it, and compatibility with them is a guarantee, paid for at that boundary ([literature.md](literature.md), T5).

**Signs you are violating it.**
- A component re-hashes, re-parses or re-validates what another component of the same release just produced.
- A timeout is taken to mean an operation did not happen, or that a resource is free.
- Liveness properties ("no wakeup is lost", "each event reaches each reader") are stated in the absolute form and need machinery to meet.
- The code establishes a fact and then a separate task verifies that it still holds.

**Kinds of example.** For example, in one distributed runtime, the trust boundary was placed at the release: processes built together from one repository trust one another's outputs, and a mismatch is a bug caught by tests ([cases.md](cases.md), E17). That placement is contextual, resting on an objective-bound assumption (one team builds every process; a trusted single-tenant site), and would change for multi-tenant or mixed-release deployments; which claims count as safety there is objective-bound; the principle is enduring.

### B5 One path for loss

**Statement.** A system has one story for what happens when a part is lost, and each failure reaches it.
- What the lost part held is gone, the rest continues, and progress resumes from what is durable and from what can be freshly observed.
- No second defence is built for a failure this path covers.
- An unknown outcome stays unknown and is re-observed, not guessed or retried transparently. Whether a lost effect is compensated depends on the objective; where it is, the compensation belongs to whoever owns the effect, as one path, not a second defence.
- Uncertainty lives on the external thing it concerns, not on each act.
- The few bounds that remain exist where a real resource requires them, or where the loss path would not otherwise converge.

**Why.** Each extra recovery path is exercised rarely, interacts with the others, and is where the hard bugs live; one path that all failures reach is exercised often, so it works. The convergence caveat keeps this from being naive: if what overflowed would overflow again on restart, a bound that prevents the crash loop is part of the path. Keeping uncertainty on external things (a key that may have been written, a job that may have launched) lets pure work be redone while effects that would duplicate harmfully keep their care.

**Where it came from.** E2 Removing the database frame (reality moves forward; "unknown" kept as knowledge); E12 Authority into the rounds; computation versus execution; E17 Commitment trimming (loss as the answer to failure; the convergence caveat).

**What it is not.** It is not "ignore failures": the loss path is designed and states what a user loses. It is not a ban on retry: a repeat absorbed by name (an idempotent write keyed by content) is fine; a repeat that would be a second real effect is not done blindly. The pattern keeps the observation (identities, re-query, "unknown") and drops the guarantee (exactly-once, transparent retry). And a detector for the failure that silences the loss path itself (an alerting path that cannot report its own death) is not a second defence; J4 decides whether it is needed.

**When it applies.** In any system with parts that can fail independently: services, pipelines, sync layers, distributed jobs. It carries most weight where loss is cheaper than a coordination layer that would prevent it.

**Signs you are violating it.**
- Two recovery mechanisms for the same failure (a restart path and a takeover protocol, a retry layer and a repair job).
- Survival of in-memory state across a crash is promised and needs its own protocol.
- Each operation, pure ones included, carries an "unknown" state and a query duty.
- A discipline (no retry, no resend) is relaxed by counting exceptions rather than by its stated reason.

**Kinds of example.** For example, in one distributed runtime, internal bookkeeping structures lost their ceilings because exhausting memory already meant a process loss that the recovery path handled, while one byte budget stayed because without it a restart would overflow again ([cases.md](cases.md), E17). Forward-only recovery without compensation is objective-bound: it suits computations whose loss is cheaper than a coordination layer, and a payment system would choose differently. The single-path principle is enduring.

### B6 Lifecycles belong to their mechanisms

**Statement.** Things that the world keeps alive separately are not coupled by the design: the end of one is not an event for another, nothing is promised to outlive what its mechanism promises, nothing is ended because an unrelated thing ended, and reuse of what happens to survive is an opportunity, not a commitment with its own machinery. Coupling by promise (persist across) and coupling by destruction (end with) are both couplings. The floor is real safety: nothing is reused while something may still reach it.

**Why.** Each lifetime already has an owner: the operating system for a process, the driver for a device context, the database for a connection. Coupling two of them needs machinery to stretch one lifetime (handover, persistence states, an inventory on restart) or to cut it short (teardown cascades, drains), duplicating a decision the mechanism already makes. Survival observed rather than promised can be used without being owed.

**Where it came from.** E17 Commitment trimming, where a choice between two couplings (adopt survivors, or destroy them) was rejected as a choice, and opportunistic reuse written as a guarantee was struck; E15 The runtime ontology.

**What it is not.** It is not a ban on all coupling. Where a native mechanism ties two lifetimes (a child process dies with its parent's session; a connection dies with its socket), the coupling is a fact and the design states it. It is not a license to destroy usable resources out of tidiness, nor to keep them out of optimism. And it does not relax safety: a resource another party may still touch is not reused, whatever a timer says.

**When it applies.** Wherever a controller, a session, a request, a cache or a process holds or refers to something with its own lifetime: connections, file handles, device memory, background jobs, user sessions, subscriptions.

**Signs you are violating it.**
- A handover or "adoption" protocol so that a successor can take over another's resources.
- Teardown that destroys resources still usable, because their creator ended.
- A guarantee that something "survives" a failure, or an inventory of survivors as a special recovery step.

**Kinds of example.** For example, in one distributed runtime, a controller's term, the durable progress of a computation and the lifetime of device resources were stated as three lifecycles, none ending another ([cases.md](cases.md), E17). The three lifecycles are objective-bound; the specific mechanisms (process groups, device contexts) are contextual; the principle is enduring.

## C. How the whole is organized

### C1 Closure at each scale

**Statement.** A system is described as closed systems at several scales and from several views, not as one tree. Each layer is complete in its own concepts over the problems it owns: a reader who stops there holds a correct system at that scale (the truncation test), and a reader given only the design can continue the work without its history (the deletion test). Lower layers add and realize; they do not retell or redefine. Views (conceptual, runtime, software, source, build, deployment) are related by elaboration and are not forced into one-to-one correspondence; the source layout is not the design. Forbidding a lower layer's vocabulary above it should not force the invention of technology-free proxies: a technology may be named where it is the selection, provided the argument above would survive any alternative selection. Among comparable selections, the choice is made on operating burden, familiarity and licence, and is recorded as a selection that the arguments above survive, not as a guarantee. A problem is closed where it is answered, not where it is handed to a new abstraction, interface or external prerequisite.

**Why.** A design written as one tree makes a problem, a component, a directory and a deployment unit interchangeable, so a change at one scale ripples through all. Closure at each scale lets a reader stop at the depth they need and lets a change land in the layer that owns it. Truncation catches upward leaks; deletion catches dependence on the story of how the design came to be. The proxy caution is from experience: a strict ban on naming technology above a line produced stand-in concepts that later failed the boundary test.

**Where it came from.** E9 Unfolding and closing layers; E12 Authority into the rounds; computation versus execution (layout kept apart from runtime); E13 The closed, self-explaining design (truncation and deletion); E17 Commitment trimming (layers add, not retell).

**What it is not.** Closure of a layer means its problems are answered at its scale, not that each noun has a form. It is not a requirement to enumerate each corner case or to write defensively. It does not demand a fixed number of layers, nor that views be projections of one another.

**When it applies.** Any design large enough to be read at more than one depth: most systems beyond a single module. In a small system, one layer may be enough, and imposing several is ceremony.

**Signs you are violating it.**
- The top-level document needs runtime vocabulary to say what the system is.
- A lower layer redefines or retells what an upper one said.
- An upper layer must deny lower-layer vocabulary ("this is not a thread"), which means it is already thinking in it.
- The directory tree mirrors the concept model one-to-one.
- A newcomer must read the decision history to understand the design.
- A layer's open problems reappear as requirements on a new component or on the environment.

**Kinds of example.** For example, in one distributed runtime, the design had five layers and two views, with the computational language as a view that refers to nothing ([cases.md](cases.md), E13). That particular cut is objective-bound; closure at each scale is enduring.

### C2 Boundaries from responsibility, not symmetry

**Statement.** A software boundary (a process, a service, a runtime, a protocol, a lifecycle, a top-level area) exists where ownership, execution or trust actually changes, not because a concept can be named independently, because a taxonomy wants a row, or because two mechanisms differ. When two concrete mechanisms differ, no generic layer is invented above them. A type space may be flat while the ownership graph is recursive; a second classification axis is a dimension the system must then maintain. The unit of extension and the axis of a layout are chosen by what changes together and when. Ownership includes a team's: the test is what changes together and when, and who changes it. A proposed shared abstraction is tested against each instance it claims to cover.

**Why.** Each boundary costs a protocol, a failure mode and a hand-off of state. At a real change of ownership or trust the cost buys something; for symmetry it buys a diagram. A generic layer over two differing mechanisms must be maintained and hides the difference that mattered. A second axis doubles the places each new thing must be placed. Testing a shared abstraction against each instance's own documentation catches the common case of a contract that exists for one instance and is wished onto the others.

**Where it came from.** E7 Runs as processes, no mini-OS; E8 The driver axis removed; E11 The canonical division and the lifecycle repository; E15 The runtime ontology (an act kept out of a vocabulary for the sake of ownership); E19 From three to five (five concepts, not five runtimes); Conway's law, in [literature.md](literature.md).

**What it is not.** It is not a refusal of shared abstractions where independent instances genuinely share a contract, nor of layout structure, which a repository needs but which is not the concept model. The same criterion (what changes together and when) can give different structures at different scales, and that is not inconsistency. And a boundary with parties who cannot change with you (a public API, a file format, an extension contract) is real however few processes it crosses; compatibility across it is a guarantee.

**When it applies.** Whenever a new service, process, module boundary, plugin interface, protocol or top-level directory is proposed, and whenever two mechanisms "should" be unified.

**Signs you are violating it.**
- One service per noun of the domain model.
- A "provider interface" or "adapter layer" whose only instance is the thing it abstracts, or whose other instances do not have the contract it assumes.
- A classification axis (by kind, by role, by provider) added beside an existing one.
- An act placed under a shared vocabulary although a different party owns it.
- A top-level directory per concept.

**Kinds of example.** For example, in one distributed runtime, a durable write performed by the process that held authority was kept out of the vocabulary of instructions sent to other nodes, because putting it there would have obscured who owned it for the sake of formal uniformity ([cases.md](cases.md), E15). That specific placement is objective-bound; the principle is enduring.

### C3 Distinctions as fine as their consumers

**Statement.** A state, outcome, reason, kind or check exists as a separate case only where some party acts differently on it. State machines are kept for genuine alternatives. Everything finer is text for a person.

**Why.** Each distinct case must be produced correctly, carried, documented, tested and kept stable once anyone depends on it. If no party branches on it, that cost buys a label. Finer detail serves people, and text serves people better than an enumeration. The test works in reverse too: where parties act differently, collapsing the distinction loses something real.

**Where it came from.** E17 Commitment trimming (some thirty reasons collapsed to the cases any consumer branched on); E11 The canonical division and the lifecycle repository (the converse: distinct situations kept distinct).

**What it is not.** It is not a rule to minimize states. Where a consumer acts differently, the distinction stays even if it is subtle. It is not a ban on diagnostic detail; the detail moves to text.

**When it applies.** Error codes, status enums, event types, outcome classifications, refusal reasons, permission kinds, configuration modes.

**Signs you are violating it.**
- An error enumeration with more cases than any client's handling code has branches.
- A state in a state machine that has the same outgoing transitions as another.
- A classification carried across a boundary only so the receiver can re-derive or check it.
- Catalogue identifiers used to organize an argument have become part of an API.

**Kinds of example.** For example, in one distributed runtime, instruction results collapsed to complete, not run (with what to do next), and not established, with all other detail as text ([cases.md](cases.md), E17). The three cases are objective-bound; the test is enduring.

### C4 Expand the platform, not the special case

**Statement.** When a need appears, the foundation is extended (a premise, a language, a contract, a family of hosts) so that capabilities grow with it; a special mechanism around one requirement is a liability. A premise change that removes ten mechanisms is worth more than ten trims. Construction takes large coherent transitions toward the final form, not pilots, placeholders or minimal versions. The absence of a capability from the current build is not an architectural prohibition, and a possible future need is not a reason to embed complexity now.

**Why.** Special mechanisms are each cheap and together make a system nobody can extend without touching all of them; a widened foundation serves the next need too. Pilots look like caution, but whatever runs first tends to become the architecture. The two rules about absence protect the platform from both sides: a missing capability is not frozen out by a rule, and an imagined one is not paid for now.

**Finding the foundation.** The foundation to widen is found, not given. Choose the unit of extension by what changes together and when (C2). Measure a widening by what the system can then express, choose or observe, not by the mechanisms added. Test a proposed shared contract against each instance it claims to cover (J14). Write latitude into definitions, so that the choice space stays wide without a grant to police (A3). Moving the atomic case of a problem (a new primitive, an implementation over a larger region) is one way the foundation widens, done outside the live solving where the meaning must hold for a run ([R5 The atomic case](recursion.md#r5-the-atomic-case)).

**Where it came from.** E8 The driver axis removed (classify a change by how it lands; choose units of extension by what changes together); E12 Authority into the rounds; computation versus execution; E14 Construction and the check layer (the frontier; no pilots); E17 Commitment trimming (the premise lever); E19 From three to five.

**What it is not.** It is not a minimal platform, and it is not deferral of building: the foundation is built, in large steps, to its final form. It is not speculative generality either; the foundation is widened in what the system can express, choose or observe, not padded with mechanisms for hypothetical failures. And a probe that answers a question about the world (how a library behaves) is research, not a pilot; what is refused is a toy whose shape becomes the architecture. In a system with live users, the final form is reached through steps each of which leaves the system serving; moving units from old to new while the old drains is migration, not a compatibility layer, provided no unit is governed by both; onboarding first users to learn what the defaults should be is a probe, not a pilot. These follow from the reasons above rather than from a case: the source history had no live users.

**When it applies.** Whenever a request arrives as "support X", and whenever construction is being planned. Most of all for foundational software whose responsibilities are known. Where what is unknown is the need itself, a small working version that answers that question is a probe (D1), and its shape is not kept as the architecture.

**Signs you are violating it.**
- A mode or option added for one customer or one backend; special cases sharing a shape nobody has named.
- "Let's get one path working end to end first" setting the architecture; stubs standing in for real owners.
- A capability missing from this version described as forbidden, or complexity justified by a need that might come.

**Kinds of example.** For example, in one distributed runtime, a fixed decision procedure and a closed set of work kinds each met its limit at a boundary, and the successor design widened them into hosted decision programs and an open set of typed contracts ([cases.md](cases.md), E19). Those particular widenings are objective-bound; widening the foundation is enduring.

## D. How the work is done, and how it revises

### D1 A concrete object early

**Statement.** Procedures that search for a structure before a concrete object exists generate concepts that explain one another. The work forms a concrete candidate early, makes it the coordinate system, and asks each subsequent question of it. The candidate is held fixed as a reference, not as a verdict: nothing in it is sacred because it exists, and no earlier model has a right of inheritance. A model whose guarantees all hold only under named conditions that no party has committed to has not yet touched its world.

**Why.** Without an object, a question can only be answered by other concepts, and each answer opens questions of the same kind; the work feels productive while the design floats. A concrete candidate (processes, tables, messages, states, steps with an actor) gives each question somewhere to land, and a reader can point at an element and ask why it is there.

**Where it came from.** E4 The generic model closed; E5 The concrete object (procedure-first charters retired for a rough model that could be attacked); E6 Constructive contact and flow pressure.

**What it is not.** It is not a pilot or a prototype that runs; the object is a model that can be argued with. It is not commitment to the first draft: the candidate is revised freely, at premise level when needed. And it does not forbid research before the object exists; focused study of mature systems is how the object gets its footing, and a probe that answers a question about the world (how a library behaves) is research, not a pilot.

**When it applies.** At the start of any design, and whenever work has been organized as a procedure (a list of questions to close, a register to fill, a cycle of review) before anyone has drawn the system.

**Signs you are violating it.**
- Many pages of concepts and no drawing of what runs and what holds state.
- Progress measured by questions closed or rows dispositioned.
- Each guarantee hedged with "given a suitable provider", and an "assumptions" section reading "none".
- An earlier model's concepts being mapped one by one onto the new design.

**Kinds of example.** The source history's case is told in [cases.md](cases.md) (E4, E5). The kind of object chosen there (a master-and-workers runtime) is objective-bound; the principle is enduring.

### D2 Construction is evidence

**Statement.** Flows and construction force contracts into contact. When building shows pressure (fields added to satisfy an abstract object, mappings to preserve an identity, metadata propagated to keep a classification, aggregates to fit a contract, a second lifecycle beside a native one), the pressure is read with two possible conclusions, not one: the system lacks a necessary semantic, or the specification demands an entity that need not exist. Distinguishing them precedes any repair. A design concept enters code as an identity, a carried field, a registry, a lifecycle or a computed relation; only the last is free.

**Why.** Construction is the most literal reading a design gets, so it shows what the design actually demands. The default reading of difficulty, "the code is incomplete", adds fields and objects until the design's entity can be built. The second reading, "the design asks for something that need not exist", removes work, and is available only if asked for. Flows (a real path traced in time order through independently written parts) do the same before code exists.

**Where it came from.** E6 Constructive contact and flow pressure; E14 Construction and the check layer; E15 The runtime ontology (software read as reverse pressure).

**What it is not.** It is not "whatever is hard to build is wrong". Some pressure is a real missing semantic, and then the design gains it. It is not a reason to let the code redefine the design; the conclusion of the reading is a change to the design, made there.

**When it applies.** During any construction, and in any design review where someone can trace a real path.

**Signs you are violating it.**
- Construction questions are all phrased as "which field or object should carry X", not as "should X exist".
- Code keeps several records of one thing in step with mirror functions.
- A native operation has become awkward because it does not line up with a design object's boundary.
- A flow stops and the design text explains the gap away instead of changing.

**Kinds of example.** See [cases.md](cases.md), E15, for the reading of a built system by boundary. The specific symptoms (serialized descriptors, string-keyed dispatch) are contextual; the principle is enduring.

### D3 No second specification

**Statement.** Tests, checks, registers, ledgers, plans, coverage maps, directory layouts and hash manifests serve the work and do not define it. The design text and the product are the only sources of what the system is; whatever starts to define validity beside them is removed, with any product capability it held returned to its owner. Progress is measured by state transitions of the product, not by counts. What a verification is for decides its standing: verification that confirms an implementation is subordinate and sets no goal; verification delivered to users (a conformance suite, an acceptance kit) is product and is built as product; checks at real boundaries are design. A representation of the problem the system is to solve (a list, register or model of its problems) is held the same way: a lens to query, never a parts list to realize item by item ([F6 The map](formulation.md#f6-the-map)). The work's own apparatus is held to the same rule: no management layer for the work; one independent reading of each version by someone who did not write it, cut along lines, with judging, cross-reading and fixing as different tasks rather than review-fix-review loops; state recovered from the design and the product, not a ledger.

**Why.** Anything that can say what is correct becomes a target: making checks pass replaces asking whether the system is advancing. The apparatus also drifts; it holds premises the product does not, and it can pass while the product lacks the capability it claims to verify. With the design and the product as the only sources, state can be recovered from them at any time, without a bookkeeping universe to maintain.

**Where it came from.** E4 The generic model closed (a check that passed while coverage stood at zero); E10 The skeleton's checks removed; E14 Construction and the check layer; E18 Tests are not the frontier.

**What it is not.** It is not hostility to testing. Tests confirm that an implementation meets the design and are part of ordinary engineering. It is not a ban on verification as a working act. And it is not a ban on artifacts users run: a conformance runner is a capability of the product.

**When it applies.** Whenever verification, planning or tracking apparatus is growing, and especially in construction by agents, who optimize toward any explicit target.

**Signs you are violating it.**
- Progress reported as tests added, coverage reached, checks passing or tasks closed.
- A harness feeds the product facts its own components should establish, through entry points that exist only for the harness.
- A plan, backlog or status file is consulted to know what the system is.
- Commit messages are mostly evidence of verification rather than descriptions of what was built.
- Review cycles of one version that do not end.

**Kinds of example.** For example, in one distributed runtime built by agents, test-driven development was ruled out for construction because the tests would have become a second specification ([cases.md](cases.md), E14, E18). That prohibition is objective-bound: it follows from building by agents from a prose design, which is how that system chose to work. In a project where a test suite is the delivered contract for other implementers, that suite is product. The principle is enduring.

### D4 Revise at the level of premises

**Statement.** A revision asks first whether the constraint a mechanism satisfies should be a requirement at all, and changes premises rather than trimming mechanisms. A premise that should not be a requirement is a reformulation of the problem ([M2 The operation](reformulation.md#m2-the-operation)), recorded under [M4 The record](reformulation.md#m4-the-record). Each removal names the behaviour that must still hold and what carries it now (an owner, a protocol, a native mechanism, a derivation); nothing is reintroduced under another name or as "a better model"; and the opposite extreme is guarded: safety claims and the joins with real resources are the floor below which trimming does not go. The two errors differ in kind: over-defence adds mechanisms; over-trimming leaves a real resource outside a rule. A removal therefore names the real resource the removed rule covered, and a counter-pass that tries to force things back, done by someone who did not do the removing, is part of the method. Related removals are made together because they change one another's meaning. Each mechanism rests on a premise, and when a premise changes, what was added or removed under it is reexamined. A critique of how a mechanism works invites a better mechanism where the question wanted was whether it should exist.

**Why.** Trimming a mechanism while its premise stays leaves the premise free to regrow it under another name; changing the premise removes the whole family and explains why each member existed. Naming the carrier keeps a removal from silently dropping what users relied on; naming the real resource keeps it above the floor. The counter-pass exists because whoever removes things is looking for removals, and a different reader is needed to look for losses.

**Where it came from.** E3 Indexing without designing (the list a revision tests against is itself a representation); E15 The runtime ontology (removals that name their carrier; regrowth in cross-reading); E16 Behaviour decides, not names; E17 Commitment trimming (the premise question; safety restored at the joins).

**What it is not.** It is not trimming for its own sake. The criterion is the behaviour of the system, not the principle that fewer mechanisms are better. It is not a replacement of old mechanisms with new ones that offer the same function in a more elegant form. Inside a set of parts changed together, a compatibility layer keeps two models alive; at a boundary with parties who cannot change with you (a public API, a file format, an extension contract), compatibility is a guarantee and is paid for there, so keeping an old form alive there is not regrowth. And it is not reopening settled decisions indiscriminately; it asks of each premise whether it should be a requirement, with reasons.

**When it applies.** Whenever a design feels heavy, whenever construction keeps meeting the same kind of difficulty, and whenever an objective changes.

**Signs you are violating it.**
- A revision that deletes clauses one by one while the requirements stay as they were.
- A removed structure returning as a "monitor", "survey", "hint" or "tracker".
- A removal that does not say what carries the behaviour, or says "nothing" for something users relied on.
- Removals made separately that interact.
- A question answered as posed, when its premise was the defect.

**Kinds of example.** See [cases.md](cases.md), E17, for one premise change (internal structures need no enforced ceilings, because exhausting memory is already a loss the recovery path handles) that removed about ten mechanisms at once. The specific premises are objective-bound; the method is enduring.

### D5 The design explains itself

**Statement.** The design is written constructively: what the system is, what each part is responsible for, how parts relate and compose. Each thing is stated once where it is owned and linked from elsewhere. Each sentence has a kind (a guarantee, a safety rule, a boundary form, a mechanism, or an explanation) and the kind is plain. Limits come in kinds that are kept apart (not yet designed, absent from this build, an accepted limitation, not reached by any probe, a release gate); a design element has a standing (committed, a decision to be made, or to be established against the real environment); and nothing is closed by an invented default. History, provenance and "who decided" are not reasons the design holds; the record of why lives beside the design, not inside it; completed records are read-only and later decisions are recorded later.

**Why.** When the design is the authority for construction, a sentence written to explain becomes a condition, and the condition becomes a check in code. A universal sentence ordinary engineering cannot meet ("no wakeup is lost", "every refusal is reported") grows a mechanism; a sentence about what the system does not provide becomes an enforced prohibition. Statement kinds say which sentences bind. Stating each thing once keeps two statements from drifting into two rules. Keeping history out lets a decision hold by its reasons, not its author.

**Where it came from.** E10 The skeleton's checks removed (standings instead of completeness); E12 Authority into the rounds; computation versus execution; E13 The closed, self-explaining design; E17 Commitment trimming (statement kinds, after a way of writing was found to have produced the mechanisms removed).

**What it is not.** It is not a ban on explanation; explanation is one of the statement kinds and binds nothing. It is not a ban on recording history; the record exists, beside the design. And it is not literary polish: the design can be terse.

**When it applies.** To any design document that others will build from, and most strongly when the builders are agents who read the text literally.

**Signs you are violating it.**
- "Unlike the previous version" or "as decided in" inside the design.
- The same rule stated in three chapters in three slightly different ways.
- The words "every", "never" and "always" scattered through descriptions of ordinary mechanisms.
- Long lists of what the system does not do.
- Defensive wording about past mistakes.

**Kinds of example.** The writing form is treated in full in [writing-and-working.md](writing-and-working.md). Its reasons are enduring; the particular five statement kinds are a convenient cut, and another design may need a slightly different set.

### D6 Escalate by semantic consequence

**Statement.** A question goes to whoever owns the system's meaning only when its answer would change a long-term definition (a responsibility boundary, where authority lives, failure semantics, a public contract, a new core abstraction). Each other question is an engineering choice, a consequence of the existing design or a fact of the stack, and is settled by whoever is doing the work. Before escalating or answering, ask whether the thing the question assumes should exist; if not, the question disappears with it.

**Why.** Escalating by difficulty sends engineering questions to the person least placed to answer them and stalls the work. It also hands the owner of meaning a choice among carriers for something whose necessity was not on the table: the question as posed may be the defect.

**Where it came from.** E6 Constructive contact and flow pressure (twenty-eight open questions reduced to one); E13 The closed, self-explaining design (escalate only a genuine fork); E14 Construction and the check layer; E17 Commitment trimming.

**What it is not.** The owner of meaning does not stay out: they give direction, approve plans with default assumptions adopted as decisions so work keeps moving, bound each session to one question, and intervene by naming a kind of structure that is growing. It is not a license to change long-term definitions by calling them engineering. With one designer it still applies: mark which of your own decisions change meaning, take them deliberately and record them. The source history gives no case of a single designer; this follows from the criterion.

**When it applies.** Whenever more than one party works on a design, and whenever a question is about to be put to someone else for decision.

**Signs you are violating it.**
- An owner-question list that grows each session and is mostly about APIs, schemas or mechanism choices.
- Escalation because agents disagree; work paused for routine engineering choices.
- A resolution record that has become a second design.

**Kinds of example.** The criterion's list of long-term definitions in the source history (the boundary between two named subsystems, failure semantics, the sharing model between runs) is objective-bound ([cases.md](cases.md), E6). The criterion is enduring. How to apply it is in [judgment.md](judgment.md), J10.

## Where the principles pull against each other

Several principles pull against each other. The methodology holds each tension this way.

**Closure against ontology (C1 against B2).** Closure is of problems at a scale, judged by truncation; it does not require that each named thing have a runtime form. B2 decides what exists; C1 how it is described.

**Trimming against safety (D4 against B4).** B4's safety claims are the floor; D4 operates above it; J9 refuses a removal that reopens a safety gap.

**Platform against minimalism (C4 against A2 and B2).** The platform is extended in expressibility: what can be computed, chosen or observed. Capability foundations grow; defensive and management structures do not.

**Native-first against special cases (B1 against C2 and A3).** Semantics that must hold across realizations stay explicit above them, stated once; realizations below are native.

**Freedom against shared contract (A3 against B2).** Boundary forms exist exactly where real boundaries exist and are fixed there; everything else is free.

**Concrete object against premature commitment (D1 against D4).** The candidate is a coordinate system, not a verdict; D4 revises it at premise level. D1 only forbids searching without one.

**Verification as a tool against verification as a virtue (B4 and D3).** Verify what removes a decisive uncertainty or guards a boundary; state what is trusted and move on. What a check is for decides its standing.

**Authority against autonomy (D6).** Whoever owns the system's meaning fixes the principled world; those doing the work complete the engineering; the line between them is semantic consequence.

**Layer purity against invented proxies (C1 against B2).** Name a technology where it is the selection, and check that the argument above would survive any alternative, rather than inventing stand-in concepts.

**A simple working system first, against the concrete object (D1 and C4).** The familiar advice that a working complex system evolves from a working simple one is held this way: what must exist early is the concrete object and its real-world footing, then a product built in coherent steps toward its final form, not a toy that runs.

## How the principles make one method

The four groups are one method seen from four sides. Group A says what the system is for. Group B says, for any proposed structure, whether it answers to the world or only to the representation. Group C says how what remains is arranged so that each scale closes over its own problems without displacing them. Group D says how the work stays anchored to a concrete object, reads construction as evidence, and revises at premises.

Together they give a procedure for a question that design writing usually leaves to taste: which complexity is essential? Essential complexity is what the system is answerable for (A1, tested by J1), what crosses a real boundary (B2, tested by J2), and what some party acts on (C3, tested by J5). The rest is accidental, however elegant. The judgment moves that apply this procedure are in [judgment.md](judgment.md). Where these principles restate or depart from established design literature is in [literature.md](literature.md).
