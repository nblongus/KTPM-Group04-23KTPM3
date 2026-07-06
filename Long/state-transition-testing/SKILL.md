---
name: state-transition-testing
description: Analyze behavioral specifications and design State Transition Testing artifacts, detailed test cases, and a consolidated final report through mandatory human-review checkpoints. Use when requirements describe states, status changes, counters, retries, locks, timeouts, lifecycle rules, or valid and invalid actions from specific states, and when Codex must produce candidate-feature analysis, state diagrams, transition tables, valid/invalid transition tests, path coverage, and a complete traceable report without inventing requirements.
---

# State Transition Testing

Apply State Transition Testing (STT) to requirements whose behavior depends on current state or event history. Work in exactly three phases and stop after every phase for human review. Immediately after completing Phase 3, generate the mandatory consolidated report as the final Phase 3 completion artifact; this is not a fourth phase or an additional checkpoint.

## Non-negotiable rules

- Treat the supplied specification as the only requirement source. Cite requirement IDs and short paraphrases; never invent behavior.
- Separate explicit requirements, logical derivations, assumptions, and unresolved questions. A plausible implementation is not a requirement.
- Never infer missing reset behavior, timeout aftermath, error text, response code, UI destination, persistence scope, or counter semantics. Record each gap as `Unspecified`.
- Never inspect implementation code to fill a requirement gap unless the user explicitly changes the source of truth.
- Require explicit user confirmation before moving from Phase 1 to Phase 2 and from Phase 2 to Phase 3. A previous feature request is not checkpoint approval.
- Finish the current phase, report created files and unresolved items, ask for review, then end the turn. Do not start the next phase in the same turn.
- Do not consider Phase 3 complete until `report.md` has been updated from the approved analysis and detailed test cases.
- Distinguish design coverage, executable coverage, and actual execution results in the report. Never imply that a test was executed unless execution evidence is in scope and available.
- Keep all artifacts for this technique under `state-transition-testing/`. Do not mix them with another technique.
- Preserve existing user files. Update only current technique/feature artifacts.

## Output layout

Keep exactly three Markdown files in the method directory. Preserve requirement IDs and stable test-case IDs inside their consolidated files.

```text
state-transition-testing/
├── SKILL.md
├── report.md
└── test-cases.md
```

Use `report.md` for candidate selection, approved analysis, and the final consolidated report. Use `test-cases.md` for detailed test cases, with one H2 section per test case. Do not create nested artifact directories or additional Markdown files.

## Phase 1 — Discover candidate features

1. Locate and read the user-designated specification sufficiently to understand cross-references. If no source is designated, locate likely requirement files and state which file is used.
2. Identify features whose output depends on current state, prior actions, counters, retry history, time, or lifecycle status.
3. Rate suitability as `High`, `Medium`, or `Low`:
   - `High`: explicit states/transitions or history-dependent rules.
   - `Medium`: meaningful state behavior exists but important transitions are underspecified.
   - `Low`: behavior is mainly stateless input/output validation.
4. Create or update the candidate-selection section in `state-transition-testing/report.md`.
5. If the user already named a feature, include and assess it; do not treat that selection as approval to enter Phase 2.
6. Present candidates and requirement gaps. Ask the user to confirm the feature set.
7. Stop. Do not create a state model, transition table, paths, or test cases.

## Phase 2 — Produce design analysis

Begin only after explicit Phase 1 confirmation. For each confirmed feature:

1. Add the approved state-transition analysis to `state-transition-testing/report.md`.
2. Explain why STT fits, tied to specification evidence.
3. Define states as distinguishable behavioral conditions. Include counter values as separate states only when they change allowed behavior or expected results. Do not create implementation-only states.
4. Define events/actions, triggers, guards, and time events stated by the specification.
5. Give every state and transition a stable ID (`S0`, `S1`; `T01`, `T02`).
6. Draw a Mermaid `stateDiagram-v2`. Ensure every valid table transition appears in the diagram.
7. Build one State Transition Table with exactly these columns: `Start`, `Action`, `End`, `Valid/Invalid`. Put the transition ID first in `Action`, for example `T01 — Submit valid credentials`.
8. For an invalid transition, use the unchanged start state as `End` only when the specification explicitly or logically requires no state change. Otherwise write `Unspecified` and raise a question.
9. Derive valid- and invalid-transition test inventories. Each row maps to transition IDs but is not yet a detailed test case.
10. Choose exactly one path extension:
    - Use **1-switch paths** when adjacent transition pairs are finite and state history is central. Cover every feasible pair of consecutive valid transitions at least once and identify infeasible pairs.
    - Use **end-to-end flow** when the feature is primarily one lifecycle spanning components and exhaustive adjacent-pair coverage is not useful. Explain the choice and cover the main requirement-backed lifecycle.
11. Add traceability: requirements → states/events → transitions → planned TC IDs → selected paths.
12. List ambiguities that block reliable expected results. Do not resolve them silently.
13. Present the analysis and ask the user to approve or request changes, then stop. Do not create detailed TC files.

## Phase 3 — Generate detailed test cases

Begin only after explicit Phase 2 confirmation.

1. Create or update one H2 section per approved test case in `state-transition-testing/test-cases.md`.
2. Use IDs `STT-<FEATURE>-V-NNN` and `STT-<FEATURE>-I-NNN`. Keep IDs stable across revisions.
3. Include every field exactly once: `TC ID`, `Feature`, `Technique`, `Precondition`, `Steps`, `Test Data`, `Expected Result`, `Covered Transition`.
4. Set `Technique` to `State Transition Testing — Valid Transition` or `State Transition Testing — Invalid Transition`.
5. Make the precondition establish the start state observably and reproducibly. Do not assume hidden database values without setup instructions.
6. Keep steps atomic and numbered. Put concrete values in `Test Data`.
7. State only requirement-backed expected results. For unspecified behavior, keep the TC blocked pending clarification or assert only the specified observable portion.
8. In `Covered Transition`, use `Txx: Sx --action--> Sy`. A test may cover multiple ordered transitions.
9. Ensure every approved valid and invalid transition is covered unless marked infeasible or blocked with a reason.
10. Map the selected 1-switch paths or end-to-end flow to detailed TC IDs.
11. Audit consistency across diagram, table, inventories, paths, and TC sections. Check that no requirement was added.
12. Finalize `state-transition-testing/report.md` after the consistency audit.
13. Audit the report against its approved analysis and `test-cases.md`. Report mapped/design coverage separately from fully executable coverage and actual execution results.
14. Present the report, consolidated test-case file, coverage gaps, and blocked cases for user review, then stop.

## Mandatory consolidated report after Phase 3

Treat the report as the authoritative handoff index, not a replacement for the detailed artifacts. Include:

1. Report metadata, source of truth, feature scope, exclusions, and overall design status.
2. Executive summary with counts for states, transitions, valid/invalid TCs, executable/partial/blocked TCs, and whether tests were actually run.
3. Candidate-selection context and STT suitability.
4. Explicit requirements, logical derivations, assumptions, and unresolved items as separate classifications.
5. States, events/actions, Mermaid diagram, and the approved State Transition Table.
6. Selected 1-switch paths or end-to-end flow and their detailed TC mappings.
7. A detailed test-case register linking every TC ID to its section in `test-cases.md` and summarizing precondition, data, expected result, transitions, and readiness.
8. Coverage and traceability matrices from requirements through states/events, transitions, paths, and detailed TC IDs.
9. Coverage gaps, blocked cases, risks, clarification questions, and recommended next actions.
10. An artifact index listing `SKILL.md`, `report.md`, and `test-cases.md`, plus a conclusion that does not overstate coverage or test execution.

Use only approved content and the designated specification. If sections disagree, correct the inconsistency or expose it; do not silently choose one. Link to test-case sections instead of duplicating every test step verbatim.

## Modeling guidance

- Model externally meaningful behavior, not screens alone.
- A self-transition is valid when an accepted action leaves the modeled state unchanged.
- An invalid transition is an action rejected or prohibited in a given state. Invalid input formatting is not automatically an invalid state transition.
- For thresholds, model only values needed to expose changed behavior, such as `0 failures`, `1 failure`, `2 failures`, and `locked`, when supported by the specification.
- For temporary states, model the explicit time event but flag its destination if post-timeout behavior is unspecified.
- Do not claim full transition coverage while a table transition lacks a planned or detailed TC.

## Completion checks

Before ending each phase, verify:

- Artifact lives in one of the three files in the dedicated STT directory.
- Every statement is traceable to the designated specification or labeled as a gap.
- Current phase contains no artifact reserved for a later phase.
- The response requests review and does not continue past the checkpoint.
- After Phase 3, `report.md` links every detailed TC section in `test-cases.md`, distinguishes mapped from executable and executed coverage, and lists all blocked or unspecified behavior.
