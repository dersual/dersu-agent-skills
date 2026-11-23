# Learning, Curriculum Mastery & Engineering Coaching

Domain vocabulary for mapping subjects into hierarchical concept trees, acquiring durable mastery through probing and practice, and driving learning-first software engineering with checkpoints, implementation gears, and verification audits.

## Concept Topology

**Semantic Tree**:
A directed dependency graph of a subject that organizes concepts by prerequisite inheritance rather than chronological lecture order.
_Avoid_: Syllabus, chapter list, linear roadmap

**Root**:
A foundational mental model or prerequisite from an earlier subject that must be understood before entering the current subject.
_Avoid_: Background reading, warmup

**Trunk**:
The core 20% invariant laws, mechanics, and first principles of a subject from which 80% of applied topics inherit their behavior.
_Avoid_: Overview, summary, intro chapter

**Branch**:
A major module or sub-discipline that extends a specific Trunk principle into an applied domain.
_Avoid_: Lecture week, unit

**Leaf**:
A specialized detail, syntax rule, historical note, or exam-only edge case that hangs off a Branch and can be learned on demand.
_Avoid_: Core concept, fundamental

**Cross-Link**:
An explicit conceptual connection showing how two separate Branches (or two different courses) share the same underlying mechanism.
_Avoid_: Side note, tangent

**Course Overlay**:
The mapping of a specific class's syllabus, deadlines, lecture files, and problem sets onto the nodes of a subject's Semantic Tree.
_Avoid_: Study schedule, calendar plan

## Pedagogical Loop

**Probe**:
A short, adaptive pre-test that locates the exact boundary between what the learner already knows and where understanding breaks across prerequisite strands.
_Avoid_: Placement exam, pop quiz

**Lock-In Check**:
A single targeted question or micro-exercise at the end of a concept step that verifies comprehension before moving to the next node.
_Avoid_: Final test, review sheet

**Practice Artifact**:
Learner-authored work submitted during problem solving—such as code, LaTeX derivations, prose explanations, or photos of handwritten math—used to diagnose exact reasoning steps.
_Avoid_: Multiple-choice click, passive reading

## Code Coaching & Learning-First Development

**Build Checkpoint**:
An open-ended reasoning prompt before design or code changes that requires the developer to articulate a technical approach, data representation, or trade-off in their own words.
_Avoid_: Multiple-choice menu, automatic recommendation, AI-proposed plan

**Design Checkpoint**:
A formal pause summarizing the developer's chosen architecture, trade-offs, verification strategy, and any separated AI-proposed additions, recorded without authorizing code changes.
_Avoid_: Rubber-stamp approval, silent architecture choice

**Implementation Checkpoint**:
A gated authorization pause that defines the exact coding and testing scope and selects the active Implementation Gear before any project files are created or modified.
_Avoid_: Immediate code generation, unscoped edit

**Implementation Gear**:
One of three selectable divisions of labor after design approval: `Architect` (developer designs, agent writes code and tests), `Guided Pair` (agent writes plumbing and red tests, developer writes core logic), or `Hands-On` (agent outputs structural TODO scaffolds, developer writes all production logic and tests).
_Avoid_: Rigid mode, single-style coaching

**Verification Audit**:
A two-layer post-implementation check combining pipeline verification (distinguishing tests written from E2E/unit checks actually executed) with human diff verification (prompting the developer to inspect a specific generated seam for failure modes or coverage gaps).
_Avoid_: Passive summary, unverified diff

**Toy Example**:
A minimal, runnable code snippet demonstrating a language mechanic, library, or design pattern in an unrelated domain so the developer learns the underlying principle without being handed their project's solution.
_Avoid_: Project code dump, abstract prose explanation
