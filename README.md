# Problem and system design

An Agent Skill: a methodology for formulating the problems computational systems solve and for designing the systems that solve them. It treats the two as loops that change each other: a problem is a representation that can be wrong, so it is fixed as a meaning that leaves realization free and asked of a concrete object, and building the system returns evidence about whether the problem was stated right. The Skill holds nineteen design principles, twenty judgment moves, twenty-two moves for formulating, expanding and reformulating a problem, the reformulation operations with their tests, twenty-eight failure patterns to read a draft against, the disciplines of writing a design and working among agents, and a worked history of one system's design and reformulation from which all of it was drawn. It is a set of questions with consequences, not a checklist: an agent reaches for the question a situation raises and lets its answer change the problem or the design.

## Who it is for

Anyone, human or agent, who defines, scopes or decomposes a problem for a computational system, or designs, structures, reviews, simplifies, extends or revises a system, platform, runtime, service, framework, data model or protocol. It is written for agents first: it names the things an agent formulating a problem or designing a system is most prone to (closing each gap with a new abstraction, building checks that become the goal, treating a list of problems as a list of parts, stating a problem in the shape of the mechanism it expects) and gives the moves that catch them. It is also useful to people who brief agents on such work, or who want to know why a design keeps growing mechanisms.

## Installing

The Skill is published at [github.com/Wanli-Wylie/problem-and-system-design](https://github.com/Wanli-Wylie/problem-and-system-design). The repository is the Skill directory itself, so cloning it into a skills directory installs it:

```
git clone https://github.com/Wanli-Wylie/problem-and-system-design.git ~/.claude/skills/problem-and-system-design
```

To update, pull in that directory. A downloaded archive of the repository, unpacked and renamed `problem-and-system-design`, works the same way.

**Claude Code.** Place the directory, named `problem-and-system-design`, in `~/.claude/skills/` to make it available in every project, or in `.claude/skills/` at the root of a project to share it with everyone who works in that repository. Claude Code reads the name and description from the frontmatter of `SKILL.md`. The Skill then triggers by itself when a task matches its description, and it can also be invoked by name, as `/problem-and-system-design`.

**Other environments.** Any environment that follows the Agent Skills specification can load the directory as it is: `SKILL.md` with YAML frontmatter (`name` and `description`) and Markdown instructions, and a `references/` directory of Markdown files that the instructions name and that are read only when needed. There are no scripts, assets or dependencies.

## How it is used

The Skill triggers when a task asks what problem a system should solve or how a system should be built: defining, framing, formulating, decomposing or reformulating a problem, requirement, objective or specification; deciding what a system fixes and what it leaves free; designing solvers, planners and pipelines that expand work recursively; asking whether a difficulty is a missing capability, a design fault or the wrong problem; writing a problem statement, research direction or brief; designing, architecting, reviewing or simplifying a system; deciding whether to add a layer, registry, coordinator, lifecycle, state or check; reading a codebase or a construction under way as evidence about its design; organizing design work among agents. Short requests such as "is this the right problem", "how should we break this down", "how should I structure this" or "is this over-engineered" trigger it too.

Read `SKILL.md` first. It holds the stance, the working loop, every principle and move with its question and consequence, the failure patterns and how the two sides join, and most work can proceed from it alone. When a move needs working through, or a case or source is wanted, open the reference its closing table names for that occasion. The references are loaded only then, so the Skill costs little context until its depth is needed.

## Layout

```
problem-and-system-design/
  SKILL.md                      the entry: stance, working loop, principles, moves, operations, failure patterns, writing and working, how the two sides join, which reference to open, revising
  README.md                     this file
  CHANGES.md                    the change record, newest first
  references/
    formulation.md              F1 to F7: what a computational problem is, in depth
    recursion.md                R1 to R7: recursive expansion and the reuse of mechanisms
    reformulation.md            M1 to M4 and L1 to L4: diagnosing a difficulty, reformulating with a record, the two loops
    principles.md               the nineteen principles A1 to D6, each with what it is not and the signs of breaking it
    judgment.md                 the twenty judgment moves J1 to J20, and the procedure expand, reorganize, absorb or remove
    writing-and-working.md      writing a design document; organizing reading, writing and judging among agents
    cases.md                    the history the methodology was drawn from, event by event, with the lessons of each
    literature.md               the sources, and where the methodology restates, sharpens or departs from them
    origins.md                  for maintainers: the predecessor Skills, the research behind them, the integration
  LICENSE                       MIT
```

## Origins

The Skill integrates two earlier Skills, one on system design (first edition 2026-10-09) and one on problem formulation (first edition 2026-10-10), into one methodology. Both were drawn from a study of the design and revision history of one distributed computing system and the work that preceded and followed it, carried out in the second research round of the I⁵ project. That research record is not distributed and nothing here depends on it; the cases the methodology needs are in `references/cases.md`. Maintainers will find an account of the predecessors and of the research, and a map from the old files and numbers to this Skill's, in `references/origins.md`.

## Revising

The methodology is meant to change when applying it produces a worse problem or system, or when it is silent on a decision that mattered, and the reason can be stated in general terms. The closing section of `SKILL.md` says how: the methodology is applied to itself, the case that forced the change is added to `references/cases.md` as a later case, and a row is added to `CHANGES.md` saying what changed, what forced it and what it replaces.

## License

MIT; see [LICENSE](LICENSE). The methodology may be copied, adapted and redistributed with the copyright notice kept.
