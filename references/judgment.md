# Judgment

The twenty judgment moves of this methodology, worked through, followed by the procedure for deciding whether a mechanism should be expanded, reorganized, absorbed or removed. [SKILL.md](../SKILL.md) lists the judgment moves as questions with consequences; the reasons behind them are in [principles.md](principles.md).

## Contents

- [How to use the moves](#how-to-use-the-moves)
- [The running examples](#the-running-examples)
- [Should this exist?](#should-this-exist)
  - [J1 The responsibility question](#j1-the-responsibility-question)
  - [J2 The boundary test](#j2-the-boundary-test)
  - [J3 The owner test](#j3-the-owner-test)
  - [J4 The failure question](#j4-the-failure-question)
  - [J5 The consumer test](#j5-the-consumer-test)
  - [J6 The world question](#j6-the-world-question)
  - [J11 The reification chain](#j11-the-reification-chain)
  - [J16 What reads it?](#j16-what-reads-it)
  - [J20 Comparators](#j20-comparators)
- [Where does it go?](#where-does-it-go)
  - [J8 The truncation and deletion tests](#j8-the-truncation-and-deletion-tests)
  - [J14 The expansion test](#j14-the-expansion-test)
  - [J17 Decision placement](#j17-decision-placement)
- [How do I proceed?](#how-do-i-proceed)
  - [J7 The two readings of pressure](#j7-the-two-readings-of-pressure)
  - [J10 The escalation criterion](#j10-the-escalation-criterion)
  - [J13 Flow pressure](#j13-flow-pressure)
  - [J15 Drawn and forced](#j15-drawn-and-forced)
  - [J18 The fates](#j18-the-fates)
  - [J19 Behaviour or policy](#j19-behaviour-or-policy)
- [How do I revise?](#how-do-i-revise)
  - [J9 The carrier rule](#j9-the-carrier-rule)
  - [J12 The premise lever](#j12-the-premise-lever)
  - [Watching for regrowth](#watching-for-regrowth)
  - [The counter-pass and the floor](#the-counter-pass-and-the-floor)
- [Expand, reorganize, absorb or remove](#expand-reorganize-absorb-or-remove)

## How to use the moves

A judgment move is a question that carries a consequence. It is not a step in a sequence and not a box to tick. Reach for the judgment move the situation raises: a new object in a draft raises J2; a second copy of a value raises J3; a requirement that sounds like it came from another kind of system raises J1; a question you are about to send to someone else raises J10. The consequence is what makes the move useful. A judgment move whose answer does not change the design was the wrong move for the moment.

Several judgment moves are one question seen from different sides. J1 and J2 are the same question at two levels: J2 (the object test) asks which objects must exist; J1 (the commitment test) asks which commitments must exist. A design can pass J2 everywhere and still carry commitments nobody needed, so ask both. J3, J11 and J16 all look at stored or carried state from different directions. J4 and J5 both ask who would notice.

Where two moves can point different ways, ask the world question (J6) before drawn-and-forced (J15): J15 applies to what the world does not carry. A proposed coordinator, for example, may be carried by an existing facility before it is either drawn as a new element or folded into an existing one.

Each section below gives the question, the consequence, why the move holds, when to reach for it, and a worked application to an ordinary system. The applications are deliberately outside the domain the methodology was learned in, so that what transfers is visible. They are examples, not answers for a system that resembles them. The source cases are in [cases.md](cases.md).

## The running examples

The worked applications use five ordinary systems.

- **An online store's order service.** It takes orders, reserves stock, charges through a payment provider and hands off to shipping. It has a database, a queue and an API gateway in front.
- **A build system.** It reads build files, forms a graph of actions, runs them locally or on remote workers, and caches their outputs locally and in a shared remote cache.
- **A text editor with plugins.** A desktop editor with autosave, crash recovery and third-party plugins for languages and previews.
- **A data pipeline.** Stages read events from a source, transform them and write to an analytical store that analysts query.
- **A mobile app's sync layer.** A notes app that works offline, keeps a local database and syncs with a server so a user's devices converge.

## Should this exist?

### J1 The responsibility question

**Question.** Is this property a responsibility of the system at all, or something the language, the operating system, the stack, the operator or the recovery path already carries?

**Consequence.** If it is not the system's, relinquish it. Change the premise, and the mechanisms that served it fall away together. State what a user loses, if anything.

**Why.** Requirements arrive by import (from a neighbouring kind of system: databases, real-time controllers, safety-critical software) and by drift (pursuing determinism, boundedness or completeness one reasonable step at a time). Once a property is a requirement, effort flows to guaranteeing it, and the debate becomes how to guarantee it more cheaply. That debate improves the mechanism and does not question the property. J1 asks of the property, not the mechanism. It is the commitment test: where J2 asks which objects must exist, J1 asks which promises must.

**When to reach for it.** When a mechanism is expensive and the discussion is about making it cheaper. When a requirement's wording sounds like another class of system. When several mechanisms seem to exist to serve one property nobody can trace to a user.

**Worked application: the sync layer.** The design says the local database is identical to the server's copy of the user's account at all times. Serving that property are a sync lock that blocks edits while a sync runs, a reconciler that compares version vectors, a "frozen" mode after long offline periods, and a full re-download when a mismatch is found. Ask who relies on identity. Users rely on three things: an edit they make is not lost; others' changes reach them soon; conflicting edits are shown to them rather than merged so that work disappears. None of these needs identity at each instant. Relinquish "identical at all times" and commit instead to: local edits are durable on the device and reach the server; remote changes arrive eventually; conflicting edits to one note are surfaced. The lock and the frozen mode go; reconciliation narrows to per-note conflict detection. The cost, stated plainly: a user may briefly see older data on a second device.

### J2 The boundary test

**Question.** Which real boundary does this object, identity, record, schema or descriptor correspond to?

**Consequence.** If none, it is scaffolding. Keep it in the design language, or as an ordinary structure: a type, a function call, a field in a local data structure, a relation computed when needed.

**Why.** A runtime object must be created, identified, stored, kept consistent and checked. That cost is worth paying only where something real makes an explicit representation unavoidable: a crossing between processes or machines; persistence across time or restart; concurrent owners; the gap between an asynchronous request and its completion; input from an untrusted party; the lifetime of an external resource; state that only a remote party knows; a public contract its consumers depend on. Justifications that do not count: it unifies the description; it lets implementations fit one schema; it makes the specification more complete; it makes classification or reasoning easier; it gives the thing an identity that can be validated. A useful reverse form: if this did not exist as a first-class thing, which behaviour would become impossible to express? If the honest answer is "none", it goes, and nothing generic replaces it.

**When to reach for it.** Whenever a noun in the design is about to become a class with an identifier, a table, a message type, a registry entry or a state machine.

**Worked application: the build system.** A draft introduces `Target` objects with globally unique identifiers, a target registry, a seven-state target lifecycle (declared, resolved, scheduled, building, built, failed, cached) and a serialized target descriptor sent to workers. Ask each in turn. The action cache key crosses time (an action is recognized across builds) and machines (the shared cache): it is real, and it is defined as a digest of the action's inputs. The request sent to a remote worker crosses a process boundary: it is a real message form, but what crosses is the action (a command and the digests of its inputs), not the target. The seven states are read by nobody outside the scheduler; after a crash the build is simply rerun against the cache, so nothing must be recognized across restart. They collapse into "done, with result" on a node of the scheduler's in-memory graph. The registry becomes a map local to the scheduler. The descriptor restates the parsed build file and goes.

### J3 The owner test

**Question.** Which single carrier owns this fact? Is this a second representation of one assertion?

**Consequence.** Name the carrier. Derive the other views on demand. Delete the check that copies agree.

**Why.** Each independent representation of one fact is a consistency obligation by construction: it must be updated, it can be stale, and the code that reconciles it must be built and maintained. The check between copies usually detects only the writer disagreeing with itself, because both copies were written by one party. The test distinguishes two situations that look alike: a second representation of the same assertion, which is removed, and two genuinely independent facts about the same thing, which may legitimately be compared. A check between carriers stays only where the carriers are independent sources.

**When to reach for it.** When you see a reconciler, a sync job, a "summary" or "status" table, a denormalized column, or a field written in one place and recomputed in another.

**Worked application: the order service.** An order's status is held in the orders table, in a summary table for the account page, in the search index, and in an event log; a nightly job compares them and pages someone on a mismatch. Name the carrier. If the service writes the orders table in the same transaction as the state change, that table is the carrier; the account page reads it or a view over it; the search index is a cache fed by change events, allowed to lag, and the design says so; the nightly job is deleted. If instead the event log is the carrier, the table is the derived view; the design cannot have both as authorities. One check stays: the payment provider's record of a charge against the store's record that it asked for one. Those are two parties' facts, and reconciling them catches real problems.

### J4 The failure question

**Question.** Whose failure, seen by whom, does this requirement prevent? Does the loss path, a native mechanism or the substrate already cover it?

**Consequence.** If it is covered, leave it out. If it prevents nothing anyone would see, leave it out.

**Why.** Requirements written as defences accumulate, each sensible alone. Naming the failure concretely (which party, what they would observe) turns a vague worry into something checkable, and the answer is often that the system's ordinary recovery (a restart, a re-read, a recomputation) already handles it, or that the platform does (a process killed on memory exhaustion, a socket closed on peer death), or that a loud failure is acceptable. This move is also the stopping criterion for designing gaps. A design driven to be "complete enough to implement without inventing anything" has no stopping point inside itself, because each closed gap adds an object whose own edges must be closed. Stop where going further prevents nobody's failure.

**When to reach for it.** For any new requirement, especially one phrased as a guarantee across all cases, and whenever a design is being completed.

**Worked application: the data pipeline.** A requirement says each stage delivers each record to the next exactly once. Whose failure, seen by whom? An analyst who sees revenue counted twice in the final table. Does something already cover it? The intermediate stages are pure transformations, and the sink writes with an upsert keyed by the source event's identifier, so a record delivered twice produces the same row twice and the second write replaces the first. Exactly-once delivery between stages prevents nothing anyone sees. Leave it out; keep at-least-once delivery and the keyed sink. What stays strict is the one thing the argument rests on: the sink's key is derived from the source event, not generated per attempt, or duplicates would appear.

### J5 The consumer test

**Question.** Who acts differently on this distinction?

**Consequence.** If nobody does, collapse it to text for a person. If someone does, keep it, however fine.

**Why.** Each distinct state, outcome, reason or kind must be produced correctly, carried, documented, tested and kept stable once anyone depends on it. If no party branches on it, all of that buys a label. Detail is still valuable to people (in logs, error messages, support tools), and text serves people better than an enumeration. The move works in both directions: a distinction some party does act on must not be collapsed for tidiness.

**When to reach for it.** When designing error codes, status enumerations, event types, outcome classes or modes.

**Worked application: the order service's API.** Payment failures are reported with fourteen error codes. The client applications branch on three things: try again later, ask the customer for another payment method, or stop. Collapse the codes to those three outcomes, each with a human-readable reason and the provider's detail for support staff. If a fraud-review tool later needs to act differently on suspected fraud, that becomes a fourth outcome, because now someone acts on it.

### J6 The world question

**Question.** Does something that already exists (the operating system, the language, a library, a service, the hardware) do this?

**Consequence.** If yes, let it carry the semantics. Design the contact with it, not a replacement for it. The system owns only the knowledge only it has.

**Why.** A rebuilt facility is a second copy of semantics someone else maintains better, and the two must then agree. The existing facility has been exercised by far more users than the new one will be. Designing the contact (when to call it, what to rely on, what one sentence the design must say about relying on it) is smaller and more robust than designing the facility.

**When to reach for it.** Before designing any scheduler, retry layer, isolation mechanism, lifecycle manager, journal, cache, quota system or discovery service.

**Worked application: the editor.** The design proposes a custom journal for crash recovery: a record format with checksums, segment rotation and a recovery tool. Ask the world. Writing a buffer's contents to a temporary file and renaming it over the recovery file gives "old or new, not torn" on common file systems. If the editor already embeds a transactional store for its settings, that store's transactions give crash-safe recovery of unsaved buffers with no new format. The design now owns only what the editor alone knows: which buffers count as unsaved, how often to write them, and how restore offers recovered work to the user.

### J11 The reification chain

**Question.** Is a known fact being re-expressed as a descriptive object, then given identity, schema and lifecycle, then copied or persisted, then validated, and finally reconfirmed?

**Consequence.** Break the chain at its first link. The fact already exists; let the structure that holds it express it.

**Why.** The chain is the most common path by which designs grow management. Each step is reasonable given the previous one: once there is a descriptor, it needs an identity to be referred to; once it has an identity, it needs a lifecycle; once it is copied, the copies need checking; once checked, a mismatch needs handling. At the end, the system spends effort reconstructing a fact it had at the start. A particularly clear form is turning relations the compiler already knows (which module implements what) into data and rediscovering them at run time.

**When to reach for it.** When you see descriptors, definitions, manifests, catalogues or registries that describe something already present in code or in another component.

**Worked application: the editor's plugins.** Plugins implement the editor's language interface in code. The draft adds a capability descriptor per plugin listing what it supports; descriptors get identifiers and are registered at startup; they are cached on disk for faster startup; at load each is validated against the plugin's actual exports; at each call the registry is consulted to confirm the plugin supports the method. The fact (what a plugin implements) is already the interface it exports. Break the chain at the first link: ask the loaded plugin. One real boundary remains: the editor wants to know, before loading a plugin, which file types should activate it, because loading is costly. That is a crossing in time. It is served by a field the plugin author writes once in the package manifest and the editor reads at activation, not validated against itself afterwards.

### J16 What reads it?

**Question.** For any stored, carried or published value: who consumes it?

**Consequence.** If the value is a pure function of what is already held, derive it rather than store it. If a check can only detect the writer contradicting itself, delete the check. If nothing reads the value, it goes.

**Why.** Values accumulate because they were convenient to compute at write time, or because someone might need them. Each stored value must be kept correct, and a stored derived value invites a reader to recompute it and compare, which is a check against the system's own output. Looking at the actual consumers (in code, not in intention) often shows the only reader is a diagnostic display or a validator.

**When to reach for it.** On any field in a record or message whose purpose you cannot state as "this party reads it to decide that".

**Worked application: the data pipeline.** Each partition's producer writes a row count and a checksum to a metadata table; the consumer recomputes both and refuses the partition on a mismatch. Who reads them? The checksum is read only by the comparison, and producer and consumer use the same library over the same bytes, so the comparison can detect only the pipeline contradicting itself; it goes. The row count is also read by a dashboard; it is a pure function of the partition, so the dashboard computes it on demand or reads it from a cache declared as derived. Contrast a file received from an external vendor with the vendor's own manifest of checksums: those are independent sources, and that check stays.

### J20 Comparators

**Question.** What do mature systems in the same situation do?

**Consequence.** The answer is evidence with a stated confidence, not a verdict on its own. A commitment none of them makes is not automatically excess; one all of them make is not automatically essential. The contrast obliges you to say why you differ.

**Why.** Mature systems have met the same forces over years and their choices carry information. But they also carry their own objectives and history, and claims about them are easy to get wrong. Say what you know, how you know it, and how sure you are; do not invent behaviour for a system you have not checked. Where comparators leave several selections comparable, the choice among them is made on operating burden, familiarity and licence, and is recorded as a selection that the design's arguments survive, not as a guarantee.

**When to reach for it.** When a commitment seems unusually strong or unusually weak, and you want a second view before applying J1 or J4.

**Worked application: a job runner in the order service.** A team designing the service's background job runner proposes byte-level memory accounting for its internal queues, with reservations and refusals. They compare with job systems they know. Suppose they are fairly sure that two widely used ones bound work by the number of jobs in flight and by backpressure, not by byte accounting of internal structures, and unsure about a third. The contrast sends them to J4: whose failure does byte accounting prevent? If the runner exhausts memory, the platform kills it, it restarts, and in-flight jobs are re-queued; the loss path covers it. What remains real is the risk that the same backlog overflows again on restart, which a count of jobs in flight prevents. They adopt the count and drop the accounting, and record the comparator claims with their confidence.

## Where does it go?

### J8 The truncation and deletion tests

**Question.** Stopping at this layer, do I hold a correct system at its scale? Given only the design, could a newcomer continue the work without its history?

**Consequence.** If not, a layer boundary or a reference direction is wrong, or the design depends on history. When a lower layer needs something the upper layer lacks to make sense (an outcome, a base case, a rule the argument rests on), the repair goes up: fix the layer that owns the argument.

**Why.** Layers that leak upward make each change ripple through all scales, and a design that leans on its history cannot be extended by anyone who was not there. Truncation finds the first; deletion finds the second. The repair direction matters: patching the lower layer to cover for the upper one hides the defect where it will be found again. The source history attests this move narrowly: the two tests were named in one round, and later the function survives as "layers add, they do not retell".

**When to reach for it.** When writing or reviewing any layered design; when a top-level description cannot be read without technology names; when a reader asks "why is this here?" and the answer is a story.

**Worked application: the order service's design.** The top-level document says orders are not charged twice because the service uses serializable transactions in its database and retries on serialization failure. Truncate at the top: is the system correct without the lower detail? The argument depends on a mechanism choice. Restate at the top the property the argument needs: each charge carries the order's idempotency key, and both the provider and the store's charge record refuse a second charge with the same key. The database becomes a selection in a lower layer, and the argument survives any store with a conditional insert. Now delete the history: a newcomer given only the design finds two charge tables and no reason for the second except a decision record from years ago. Either the second table has a responsibility the design states, or it goes.

### J14 The expansion test

**Question.** Does this extension widen what the system can express or choose, or does it add a case?

**Consequence.** Widen the foundation. Refuse the special case, or hold it until a foundation can carry it. Test a proposed shared abstraction against each instance it claims to cover: where the shared contract is absent for most instances, it is not shared, whatever its name.

**Why.** Special cases are each cheap and together make a system that cannot be extended without touching all of them. A widened foundation serves the next need too. The generality test protects the other side: a "shared" abstraction designed from one instance and wished onto the others becomes a layer that fits none of them.

**When to reach for it.** When a request arrives as "support X", and when the second or third similar request arrives.

**Worked application: the editor's previews.** Requests arrive for a Markdown preview, then a diagram preview, then a typeset-mathematics preview, each proposed as a mode with its own setting and command. Widen instead: give the document view a renderer contract. An extension declares the content types it renders and returns rendered output; the view hosts any renderer; the built-in Markdown preview becomes one renderer. Then test the contract against each instance's needs. The mathematics renderer compiles slowly and needs asynchronous results with progress; the diagram renderer runs an external process. So the contract allows asynchronous results. If one renderer alone needs scroll synchronization with the source, that stays outside the shared contract until a second needs it.

### J17 Decision placement

**Question.** Where must this decision be taken, relative to the irreversible step it precedes, and who holds the information needed at that moment?

**Consequence.** Place the decision there. Ownership of the act, not uniformity of vocabulary, decides who performs it.

**Why.** Decisions placed by symmetry (all retries in the gateway, all validation in one layer, all writes through one interface) end up made by a party that lacks the information or acts too late. A decision that must precede an irreversible step belongs with whoever can still change the outcome and knows enough to do so. The source history attests this move in one or two cases; the evidence is narrow.

**When to reach for it.** When a generic layer proposes to make a decision for all routes, and when an act is being forced into a shared vocabulary for consistency.

**Worked application: the order service's checkout.** The API gateway applies one retry policy to all upstream calls: three retries on timeout. For the payment call, a timeout says nothing about whether the charge happened, and repeating it may be a second real charge. The decision "retry, or query first" must precede the irreversible step (another charge), and the party holding the information at that moment is the payment client, which has the idempotency key and can ask the provider for the charge's status. So the payment client decides, and the gateway's uniform policy is switched off for that route.

## How do I proceed?

### J7 The two readings of pressure

**Question.** Is this construction difficulty the real system lacking a necessary semantic, or the design demanding an entity that need not exist?

**Consequence.** Answer before adding any field, message or object.

**The third reading.** The problem as formulated may manufacture the difficulty, so that neither a new semantic nor a removed entity is the repair: the statement is. Its signs include a construction question whose premise rides in its options and a requirement no party relies on; the rest are under [M3 The signs](reformulation.md#m3-the-signs).

**Why.** The default reading of difficulty is "the implementation is incomplete", which leads to adding fields and objects until the design's entity can be built. Construction is the most literal reading a design gets, and its pressure is evidence about the design. The signs are recognizable: fields added to satisfy an abstract object; mappings kept to preserve an identity; metadata carried to keep a classification; aggregates assembled to fit a contract; a second lifecycle beside a native one; a local relation promoted into an entity. A concept enters code as an identity, a carried field, a registry, a lifecycle or a computed relation, and only the last is free.

**When to reach for it.** Whenever construction asks "which field, message or object should carry X?".

**Worked application: the sync layer.** During construction, engineers add a sync session identifier to each record, then a table mapping old session identifiers to new ones after a reinstall, then a "session merge" step. Read it both ways. Does the system lack a semantic? Conflict attribution needs to know which device made an edit, and a device identifier crosses to the server and is persisted: that is real. Does the design demand an entity that need not exist? The "sync session" was a grouping the designers used to reason about batches of edits; nothing outside the client reads it. The session goes, and the mapping table and merge step go with it. The device identifier stays, and the design states that a reinstall is a new device.

### J10 The escalation criterion

**Question.** Would answering this change a long-term definition of the system? Before that: does the thing the question assumes need to exist?

**Consequence.** If the premise is the defect, the question disappears with it. If the answer changes no long-term definition, decide it as engineering and close it. If it does, put one question to whoever owns the system's meaning, with the options, what each would cost, what the question blocks, and a default assumption under which the work continues.

**Why.** Escalating by difficulty stalls the work and sends engineering questions to the person least placed to answer them. Escalating without the premise step hands them a choice among carriers for something whose necessity was not on the table. A question asked as posed gets answered as posed: in one history, most of the questions construction raised disappeared when the representation they assumed was removed, and the answered ones extended carriers a later revision withdrew ([cases.md](cases.md), E15, E17).

Long-term definitions are things like: a responsibility boundary between major parts; where authority or agreement lives; the failure semantics; principles about rollback or retry; whether live state becomes durable; the isolation or sharing model between users or tenants; what authority code or input from third parties has; the core supported platform; a long-lived public contract; a new core abstraction.

Questions fall into four kinds:

| Kind | What it is | Who settles it |
|---|---|---|
| Engineering choice | Several sound implementations exist | Whoever is doing the work picks one and closes it |
| Consequence of the existing design | The answer follows from what is already decided | Derive it, state the derivation, close it |
| Fact of the stack | The answer depends on how a library, service or platform behaves | Research only that, choose a realization or fallback |
| Choice of meaning | Coherent answers differ in what the system is | Whoever owns the system's meaning |

Two refinements. A question whose assumed answer changes nothing and whose alternative would change a long-term definition is closed on the assumed answer, as a consequence of the design, with the derivation stated; it is not held open for the alternative's sake. And disagreement among those doing the work is not a criterion; neither is difficulty.

**Examples.**

| Question | Kind and reason |
|---|---|
| Which JSON library should the order API use? | Engineering choice. |
| The queue redelivers a message after its visibility timeout; what should the consumer do with a duplicate? | Consequence: the consumer is idempotent by key, so nothing new is decided. |
| Does the storage provider's SDK support streaming uploads above a size limit? | Fact of the stack: look it up, pick a realization. |
| Should a cancelled order release its reserved stock immediately or at the end of the day? | Choice of meaning: it changes what customers and staff can rely on. Escalate, with a default. |
| Should two devices editing the same note offline be merged automatically or shown as a conflict? | Choice of meaning: it changes failure and conflict semantics. Escalate. |
| Which of three components should hold the plugin capability descriptor? | Premise step first: should the descriptor exist (J11)? It should not, and the question disappears. |
| Should we add a workflow engine to coordinate the order steps? | Would add a core abstraction; first apply J15: can it be drawn, is it forced, and does an existing element or the world already carry it? |

In a project with one designer, the criterion still applies. Mark the decisions that change meaning, take them deliberately, record them beside the design, and take everything else at the pace of engineering. The source history gives no case of a single designer; this follows from the criterion.

**When to reach for it.** Before sending any question to someone else for decision, and whenever a list of open questions is growing.

### J13 Flow pressure

**Question.** Which real path through the system has not yet forced these contracts to touch?

**Consequence.** Trace it in time order, through each part it touches. Where it cannot proceed, change the design until it proceeds forward through explicit actions. Do not route around the stop, and do not explain it away in prose.

**Why.** Parts designed separately each look complete. Their contracts meet only when something passes through them in time order: a decision, an admission, a handoff, a failure, a restart. A flow is not an illustration and not a proof that the design works. It is a tool that forces contracts that have not yet touched to make contact, and its value is where it stops. Close a flow by modelling what reality is after a failure, not by assuming the system returns to an earlier state.

**When to reach for it.** When parts were written by different people; when failure and restart have been designed separately from the main path; when a design feels complete but nobody has traced a hard case. Prefer a few paths that carry much information: ones that cross several parts and include a failure.

**Worked application: the sync layer.** Trace: the user edits a note offline; the operating system kills the app; the user restores the app from a backup onto a new phone; logs in; edits the same note on a second device. Follow it through the local store, the outbox, the sync client, the server and the second device. It stops at the second step: the outbox of unsent edits is held in memory, so the edit is lost when the app is killed. Change the design: the outbox is durable in the local store, written with the edit. Do not write "the app usually flushes before termination". The restore step stops next: the restored device carries the old device's identifier. The design states that a restored installation registers as a new device, and the flow continues.

### J15 Drawn and forced

**Question.** Can this element be drawn, with an owner (which process, which thread, which table) and a lifetime? Does a real fact force it: a responsibility only this system has, a crossing between real parts, or a relation no single part maintains?

**Consequence.** If it cannot be drawn, it is a word, not yet an element. If nothing forces it, it does not enter. "It was in the old model" and "our last system had one" are not facts.

**Why.** Elements enter designs because they were named in a discussion or existed somewhere else. Asking for an owner and a lifetime makes the element concrete enough to argue with; asking what forces it separates real structure from inheritance.

**When to reach for it.** When a new manager, coordinator, engine, service or registry is proposed.

**Worked application: the order service.** A proposal adds a workflow manager to coordinate reserving stock, charging and handing off to shipping. Can it be drawn? Which process runs it, which table holds its state, how long does each instance live? Is it forced? The relation "an order's steps happen in order, and a failed charge releases the stock" is real, and no single step maintains it. So something is forced. Does the world carry it (J6)? A durable workflow engine carries exactly this relation, with timers, retries and visibility of each instance. Prefer it when flows are long-lived, have timers or human steps, or are many; then the hand-built alternative is the second copy. These flows are a few short steps, so ask next whether an existing element carries it. The orders table has a state column, and each step's handler advances the state and enqueues the next step. That is the drawn form here: a column and handlers in existing processes, not a manager with its own lifecycle and store.

### J18 The fates

**Question.** For an inherited problem, requirement or concept: in what concrete form does it exist in the present design?

**Consequence.** It meets one fate: **dissolved** by the world (name the mechanism, and the one sentence the design must say about relying on it); **carried** by an existing element; **expands** the design (a real, unhandled need gets a constructed mechanism); **not arising** (the old frame made it, and it does not occur here); **the owner's** (a choice of meaning); or **outside** the system. Each fate is a finding, not a coverage claim. It is also a reading of the problem ([F5 The concrete form](formulation.md#f5-the-concrete-form)), and **not arising** states the condition under which the problem would arise.

**Why.** Inherited problem lists, requirements documents and earlier models carry the frame they were written in. Mapping their concepts onto the new design one to one imports that frame. Asking for the concrete form forces each problem to be re-asked in present terms. The "not arising" fate is the most informative, because it shows which problems were artefacts of the old frame.

**When to reach for it.** When migrating, rewriting, or designing against a requirements list or a previous model.

**Worked application: the order service, replacing a monolith.** The old system's requirements include a distributed lock around monthly report generation per tenant. In the new design, reports are jobs on a queue partitioned by tenant, with one consumer per partition: **not arising**, because the old frame (scheduled tasks on many hosts) made it. "Audit trail of changes" is **dissolved** by the database's change capture, and the design says once that it relies on it. "Retry failed emails" is **carried** by the email provider's delivery queue. "Customer-visible order tracking" **expands** the design. "How long invoices are retained" is **the owner's**, a legal and business choice. "Single sign-on with partners' identity providers" is **outside**, owned by the identity platform.

### J19 Behaviour or policy

**Question.** Does this proposed state or ending exist to answer a liveness or operational choice?

**Consequence.** State it as a policy on an existing mechanism (a timeout with a default, an alert rule, a supervisor's restart setting), not as a new state with its own transitions.

**Why.** A new state must be handled by each party that reads states, carried across boundaries and kept consistent on recovery. When what it really encodes is an operational choice (how long to wait, when to alert, when to give up), the choice belongs to whoever operates the system and can be changed without changing the state space. A related case: an observation gap is not a state. A party that has not answered means "not yet known", not a new kind of ending. The source history attests this move in one or two cases; the evidence is narrow.

**When to reach for it.** When someone proposes a stalled, unknown, indeterminate, degraded or suspended state.

**Worked application: the data pipeline.** A proposal adds a stalled state for jobs with no progress for two hours, with transitions back to running on progress and to failed after six hours, and alerts on entry. Ask what the state encodes: when to alert and when to give up. Both are operational choices. Express them as a policy: a no-progress timeout on the running job, with a default, that fails the job with the reason "no progress for N minutes"; and an alert rule on the job's progress metric. No new state. If the upstream source is silent, the job is still running and not yet done; the timeout policy decides when that is no longer worth waiting for.

## How do I revise?

Revision is where the methodology most differs from routine simplification. It works at the level of premises, names what carries each removed behaviour, watches for regrowth, and guards a floor.

### J9 The carrier rule

**Question.** Removing this, what behaviour must still hold, what carries it now, and what silently relied on it?

**Consequence.** State the behaviour and its carrier (an owner, a protocol, a native mechanism, a derivation), or that nobody needs it and what a user loses; and name what other parts used the removed thing as a source. Refuse a removal that reopens a safety gap. Watch for the same function regrowing under another name.

**Why.** A removal that does not name its carrier either drops something users relied on without saying so, or leaves the function to reappear somewhere unplanned. Naming the real resource the removed rule covered is how a removal stays above the floor: over-defence adds mechanisms, but over-trimming leaves a real resource outside any rule, and that error is silent until it corrupts something. What silently relied on the removed thing is the part most often missed; for example, in the source history a removed rule had been the only place a needed concept was defined (see the counter-pass below).

**When to reach for it.** On each removal, and when writing the ruling that records one. A ruling on a removal names what carries the behaviour now and what is lost; the full form the record prescribed also names what stays and what goes.

**Worked application: the order service.** Removing the nightly status reconciler (J3): the behaviour that must hold is that the account page shows the order's real status; the carrier is a read of the orders table. Nothing is lost. Removing the rate limiter on outbound calls to a partner's API: the behaviour that must hold is that the partner's quota is not exceeded. If the partner answers excess with a "try later" response and the client backs off, the partner's own limit carries it. If instead exceeding the quota suspends the store's account for a day, an irreversible effect on a real resource, the removal is refused: the limiter is at the floor.

### J12 The premise lever

**Question.** What single change of premise would make several mechanisms unnecessary?

**Consequence.** Prefer it to several trims.

**Why.** Mechanisms come in families that share a premise. Trimming them one by one leaves the premise in place, and the premise regrows them. Changing the premise removes the family at once and explains why each member existed. Related removals are made together because they change one another's meaning. When a premise changes, also re-examine what was added or removed under it: a mechanism dropped because of the old premise may be needed under the new one.

**When to reach for it.** When several mechanisms seem to defend the same thing; when each trim reveals another mechanism behind it.

**Worked application: the build system.** The shared cache has accreted a poisoning detector, per-machine toolchain fingerprints, a manual purge tool, a "suspect" flag on entries, and a rebuild-on-suspicion mode. All follow from one premise: actions may read inputs they do not declare, so a cache key does not fully determine an output. Change the premise: actions run in a sandbox that exposes only declared inputs, including the toolchain. The cache key then determines the output, and the five mechanisms go together. The cost, stated: toolchains must be declared, and some builds need fixing before they run sandboxed.

### Watching for regrowth

A removed structure tends to return, because the reasoning habits that produced it remain. It comes back in three recognizable ways: under another name (a "tracker" for a ledger, a "monitor" for a stall state, a "hint" for a removed state); as a smaller version of itself; or as a better mechanism for the same job. It can also move: an object removed from the inside of a component reappears as a public record, or a field removed from a message survives as internal state under three names.

Regrowth is prevented by changing the premise that generated the thing (J12), and caught by a short list of withdrawn things with their likely disguises, by a reading after removal by someone who did not remove, and by asking J4 of anything new: whose failure, seen by whom, does it prevent, and does the loss path, a native mechanism or the substrate already cover it? If nothing is left, the thing is not built. During construction, removal of withdrawn structures happens inside the work that builds their area's owner, not as a separate cleanup project, so that the owner is built without them rather than around them.

### The counter-pass and the floor

**The floor is B4's safety claims together with the joins with real resources** ([principles.md](principles.md), B4); revision does not trim below it. Safety claims are those where acting on a guess would silently corrupt data or a resource: that a resource may be reused, that an effect did not happen, that a value is ready, that participants acted in one order. They need positive evidence in every interleaving, and silence or a timeout never supplies it; this is the one place where "every" and "never" are meant literally. The joins with real resources are the places where a removed rule used to cover something finite or external: memory, devices, quotas, files, external effects.

A revision is not finished until someone who did not make the removals has read the result and tried to force things back. The person removing things is looking for removals; a different reader looks for losses. In practice the losses concentrate at the joins: a device could pass to the next user while a stuck process still held it, because nothing kept the exclusion once its controller exited; a removed rule had been the only place a needed concept was defined. The counter-pass names each such case, and the fix usually comes from the resource's own owner (the platform, the operator's tooling), not from a new protocol.

## Expand, reorganize, absorb or remove

When a system meets new complexity, a new capability requirement or a changed environment, the question is what to do with the mechanisms it has and the one being proposed. The judgment moves compose into a procedure. It is an order of questions that composes the moves, not a pipeline any round of the source history ran; each question can end it, and it is not a form to fill.

The four outcomes:

- **Expand.** Widen the foundation (a premise, a language, a contract, a family) so that a need is met by the system's own growth, a class of needs rather than one.
- **Reorganize.** Keep a responsibility and move it: to another layer, owner, moment or axis.
- **Absorb.** Let something else carry it, in one of two senses, named when used: the world carries it (a process boundary, a library, a service), adding at most a contact; or a broader existing element of the design carries it (a definition absorbs what was a separate axis).
- **Remove.** End it, with the carrier rule: what behaviour must still hold, what carries it, and what silently relied on it; or the relinquishment and its cost stated.

The procedure:

0. **Start from the occasion.** If the need arrived as a construction difficulty or a stuck flow, read it twice first (J7, J13); if it is inherited, re-ask it of the present design (J18). If the occasion is a difficulty that keeps returning, read it under [M1 The three readings](reformulation.md#m1-the-three-readings), since it may be the formulation's.

1. **Restate the need as a responsibility, in the words of whoever relies on it (J1).** If no one relies on it, or it belongs to the language, platform, operator or recovery path, the outcome is **remove**, and the premise that produced it is changed (J12), taking its family of mechanisms with it.

2. **Ask the world (J6) and the existing design (J18).** If the platform, a library or a service carries it, the outcome is **absorb into the world**: design the contact. If an existing element of the design carries it, **absorb into that element**: extend its owner rather than adding a party.

3. **Ask who would notice (J4, J5).** If the loss path or a native mechanism already covers the failure, or no party acts on the distinction, the outcome is **remove** or do not add.

4. **If something must exist, find where (J2, J3, J17).** Which boundary does it answer, which single carrier owns the fact, and where must the decision be taken relative to the irreversible step? If an existing owner holds the fact or the decision, **absorb** into it. If the right owner is missing, or the current boundaries put the fact in the wrong place, **reorganize**.

5. **Read the pressure (J7, J12).** If the need appeared as construction strain and step 0 found the design demanding an entity that need not exist, **remove** that entity and **reorganize** what it held to its real owners. If several mechanisms share a premise that the new need exposes, change the premise: what it makes unnecessary is **removed** together, and what remains is **reorganized** around it, not joined by a mechanism beside the others.

6. **Ask whether it widens or adds a case (J14).** If the need is one of a family (several backends, several formats, several kinds of extension), **expand** the foundation so the family is served, and test the shared contract against each instance. If it is a single special case, refuse it or hold it until a foundation can carry it.

7. **For each removal, apply the carrier rule (J9)** and stay above the floor. Make related removals together, then have someone else try to force things back.

Two cautions. A possible future need is not a reason to embed complexity now, and the absence of a capability from the current build is not a prohibition; expansion widens what the system can express, it does not pad it against hypothetical failures. And when the right answer is a premise change, the work is a rewrite of the affected part toward its new form, not deletion of clauses one by one.

**Worked application: adding a subscription product to the order service.** The store wants subscriptions: monthly orders charged automatically.

- J1: the responsibility is "a subscriber is charged once per period and receives the goods; a failed charge is retried a bounded number of times and the subscriber is told". The order service's responsibilities already include charging and fulfilling an order.
- J6 and J18: the payment provider offers recurring billing with retries and dunning emails. Charging on schedule is **absorbed into the world**; the store designs the contact (it receives the provider's "invoice paid" event).
- J4: "the store guarantees no subscriber is charged twice in a period" is covered by the provider's per-invoice idempotency; nothing is added.
- J2, J3 and J17: what crosses a boundary is the provider's invoice event (untrusted input, checked) and the subscription record (persisted, recognized across time). The subscription's status has one carrier, the provider; the store derives "active" from the latest event rather than keeping its own status machine.
- J14: on a paid invoice, the store creates an ordinary order. Subscriptions do not get their own fulfilment path; the order path is **expanded** to accept an order whose payment already happened, which also serves gift cards and invoiced business customers.
- Nothing is removed, and the one new element (a subscription record with a reference to the provider's subscription) can be drawn with an owner and a lifetime (J15).

**Where the procedure stops.** A procedure that chooses among the options on the table cannot produce an answer above them. For example, in the source history, when a controller could be lost, the options put forward were to destroy the native resources it held or to promise their survival into its successor's term; both coupled the resources' lifetime to the controller's. Whoever owned the meaning answered above the menu: the lifetimes were not to be coupled at all, and reuse of what survived became an observation, not a promise ([cases.md](cases.md), E17; [principles.md](principles.md), B6). J1 asked of the coupling itself, not of either mechanism, reaches that answer; the procedure is an aid to asking it, not a substitute.
