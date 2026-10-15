# SYSTEM-DESIGN-LEARNING — Low-Level Design

Status: **DESIGN FINALIZED (rev 3); implementation not started.** Implements `docs/HLD.md`. Nothing here exists yet except the three design files. Date: 2026-10-15. Rev 2 added Module 9 (OOP and Low-Level Design) with TypeScript/Vitest exercises. **Rev 3:** Module 9 is studied after Module 2 (ids 39–47 unchanged); study order, mastery-based pacing and capstone prerequisites updated; spaced review counted in lessons, not days. Mentor and progress architecture preserved.
Legend: **[V]** verified existing mechanism (path in `HLD.md` section 2.1); **[P]** proposal.

## 1. Scope of this LLD

Defines files, formats, mentor behavior, triggers and validation for a file-only learning project operated by one IDE agent. It does not define code, infrastructure, exercises or agents; none will be created in the design phase.

## 2. Repository layout [P]

```text
SYSTEM-DESIGN-LEARNING/
  CLAUDE.md                        # trigger  (adapted from V2)
  .cursor/rules/sysdesign-mentor.mdc  # trigger (adapted from V2)
  MENTOR.md                        # the one shared protocol (V1 + V6 merged)
  CURRICULUM.md                    # contract (V3); draft now
  PROGRESS.md                      # V4 format
  QUESTIONS.md                     # V5 format, extended (section 5.3)
  MISTAKES.md                      # V5 format
  DECISIONS.md                     # learner-owned ADRs (V7 template), used from module 7
  STORIES.md                       # learner-owned STAR bank, used from module 8
  lessons/NN-slug/                 # created one at a time by the mentor
    LESSON.md                      # theory, vocabulary, trade-offs
    SCENARIO.md                    # the practical case shown to the learner
    answer.md                      # the learner's written answer (learner-owned)
    REVIEW.md                      # mentor's rubric result, after the answer
  reviews/Rn-slug/                 # module review exercise, same shape
  docs/HLD.md  docs/LLD.md
```

Modules 1–8 need no `package.json`, `tsconfig`, `node_modules`, scripts or tests. **Module 9 only** adds the exercise setup in section 2.1, created when the learner reaches Module 9, that is after gate M2 (HLD D2, approved). The design phase creates only `docs/HLD.md`, `docs/LLD.md` and `CURRICULUM.md`.

### 2.1 Module 9 exercise setup [P, copied from verified V10]
```text
  package.json  package-lock.json   # devDependencies only: typescript, vitest, tsx, @types/node; no runtime deps
  tsconfig.json                     # strict, noUncheckedIndexedAccess, NodeNext, include ["lessons","reviews"]
  vitest.config.ts                  # include lessons/**/*.test.ts and reviews/**/*.test.ts
  scripts/lesson.mjs                # copy of the verified runner: check NN | experiment NN | typecheck
  .gitignore                        # node_modules, dist, .env, *.log
  lessons/39-... .. 47-...          # LESSON.md, SCENARIO.md or REQUIREMENTS.md, challenge/stub.ts,
                                    #   challenge/spec.test.ts, challenge/answer.md, REVIEW.md
  reviews/R9-oop-lld/               # same shape; run with `npx vitest run reviews/R9-oop-lld` + `npm run typecheck`
  lessons/00-setup/smoke.test.ts    # setup check at M9 start, deleted after lesson 39 passes
```
Notes: the verified runner's `check NN` looks only under `lessons/`, so the R9 review is run with the Vitest command above (no runner change proposed); `npm run typecheck` covers both folders through `tsconfig.json`. Dependencies other than those four are not installed unless a lesson needs them, as in V1. TypeScript and Vitest are used **strictly for exercises and tests**: no application, CLI, server or API call.

## 3. Triggers [P]

Both files contain only the phrase list and the load order, nothing else (R10).

Phrases: "Continue my lesson", "start lesson N", "next lesson", "hint 1", "hint 2", "solution", "review my answer", "my progress", "where am I", "start review N", "log a mistake", "add a question", "add a decision", "add a story".
Action: read `MENTOR.md`, then the CURRENT block of `PROGRESS.md`, then only the current lesson's row in `CURRICULUM.md`; follow `MENTOR.md`. Never advance without explicit approval. Never write solutions to disk. Never generate future lessons.

## 4. Mentor protocol (`MENTOR.md`) [P, derived from V1 and V6]

### 4.1 Reused unchanged in substance [V]
Load order; resume protocol ("disk wins", restate in at most 3 lines, continue at exact step); steps legend 0–7; advancement only on explicit approval; passing is never approval; single writer; no future lessons; honest reporting; hard limits on overwriting learner files; HINT 1 / HINT 2 / SOLUTION only on request, SOLUTION in chat only.

### 4.2 Adapted [P]

| Reused piece | Adaptation |
|---|---|
| 7-step lesson loop (V1) | Step 2 "challenge" becomes a scenario with a **written answer** (`answer.md`) or a chat answer; step 5 "run tests" becomes the **rubric review** (4.4) |
| Tiers A/B/C (V1) | Redefined as Guided / Constrained / Open (4.3) |
| One question at a time, never reveal the architecture, challenge the weakest assumption (V6) | Applied inside step 3: after the learner's first answer, **one challenge per message**, drawn from the toolbox in 4.5 |
| Mentor-only probe list (V6) | Not stored. The mentor derives probes when the lesson starts, from `LESSON.md` and the rubric, and keeps them in the conversation (HLD principle 5) |
| Interview protocol (V1) | One realistic question per lesson, at most two follow-ups, rating weak/ok/strong, learner's answer excerpt recorded |
| Review checklist (V1) | Replaced by the rubric in 4.4 |

### 4.3 Tiers [P]

| Tier | Mentor supplies | Learner supplies |
|---|---|---|
| A Guided | Answer structure (headings: requirements, numbers, components, data, trade-offs, failure) and a worked mini-example of *method* on a different problem | Content for each heading |
| B Constrained | Requirements and constraints only | Structure, estimates, design |
| C Open | One-paragraph business problem | Clarifying questions first, then everything; mentor answers questions in character |

Module 8 (behavioral) uses the same tiers: A gives the STAR skeleton, B a prompt only, C an unprepared follow-up barrage.

**Module 9 (code) tiers**, same as the verified `BIG-O-LEARNING` scaffolding (V10): **A** `stub.ts` with signatures, exported types and `// TODO:` comments, plus a spec · **B** `REQUIREMENTS.md`, exported interfaces and a spec, no bodies · **C** `SCENARIO.md`, acceptance criteria and a spec through a minimal entry-point name; the learner designs the classes and writes some tests in `my-tests/`.

### 4.4 Review rubric [P]

Scored per dimension: **Strong / Partial / Missing**, one sentence of evidence quoted from the learner's own text.

| Dimension | Question |
|---|---|
| Requirements | Did they clarify functional and non-functional requirements and the scale? |
| Correctness | Does the design solve the stated problem? |
| Data | Is the data model and access pattern justified? |
| Scalability and cost | Are there numbers, bottlenecks, and the cost driver? |
| Reliability | What fails, how is it detected and recovered? |
| Security | Authn/z, data exposure, abuse |
| Operability | Metrics, logs, traces, alerts, deploy and rollback |
| Trade-offs | Alternatives named and rejected with reasons |
| Communication | Structure, clarity, brevity |

Rule: reward stated trade-offs and numbers, never agreement with a specific architecture (R3). For behavioral lessons the rubric is replaced by 4.6.

### 4.5 Challenge toolbox [P, extends V6]
"10x traffic tomorrow, what breaks first?" · "A zone is down for two hours." · "The cache is cold after a deploy." · "A consumer is slow and the queue grows." · "Budget cut by 40%." · "Two teams own this service, who decides?" · "This table has 5 billion rows." · "Show me how you would know it is broken at 3 a.m." · "Why not a monolith?" · "What do you do if the data migration fails halfway?" Use one at a time, tailored to the weakest assumption.

### 4.6 Behavioral rubric (module 8) [P]
Situation specific · Task and personal ownership ("I" not "we") · Actions concrete and decision-focused · Result measurable · Reflection (what changed) · Length 90–120 seconds · Honest (no invented facts; mentor never writes the story). Follow-ups: "What would you do differently?", "What did the other person think?", "How do you know it was your impact?"

### 4.7 Fact discipline [P]
- Numbers (latency, throughput, price, limits) are taught as **orders of magnitude** and always labelled "approximate". Cloud-service facts carry "verify in current AWS documentation".
- The mentor states uncertainty rather than inventing an exact limit, and never claims to have checked a source it did not read.
- No instruction to create or change real cloud resources.

### 4.8 Hard limits [P, mostly V1]
No answer keys or solutions on disk; no future lessons; no overwriting `answer.md` or `STORIES.md` text the learner wrote (show a diff, wait for approval); never write the learner's STAR story; no commit/push without explicit approval; never modify other repositories; no secrets, customer data, employer-confidential or personal data in any file (R5); only one IDE session open on the project.

### 4.9 Code-lesson loop and design rubric (Module 9) [P, loop from V1/V10]
Loop for a code lesson: theory and vocabulary → scenario or requirements → learner implements in `challenge/stub.ts` (and answers any prose question in `answer.md`) → hints only on request → mentor runs `npm run check -- NN` **read-only** → if green, **design review** → one senior interview question → record and stop.
Tests are mentor-owned and fixed once published (V1); they check behaviour through minimal entry points so several valid designs pass. **Green is necessary, not sufficient.** The mentor never edits files the learner has changed under `challenge/` or `my-tests/` (show a diff, wait for approval) and never writes a solution to disk (SOLUTION is chat only). A lesson is `passed` only when specs and `tsc` are green **and** the design review has no *Missing* on Cohesion, Coupling and Testability; `passed-with-help` if any hint level was used.

Design rubric (Strong / Partial / Missing, one quoted-evidence sentence each):
| Dimension | Question |
|---|---|
| Cohesion and responsibility | Does each class/module have one reason to change? |
| Coupling and dependencies | Do dependencies point at abstractions and flow one way? Can parts be swapped or faked? |
| Abstraction and interfaces | Are interfaces small, named for the client's need, and free of leaked details? |
| Inheritance vs composition | Was the relationship chosen deliberately, with substitutability respected? |
| Pattern fit | Is a pattern used for a real force, and is the simplest code kept where no pattern is needed (no over-engineering)? |
| Invariants and encapsulation | Can an object be put in an invalid state from outside? |
| Readability | Names, function size, no duplication, no needless comments |
| TypeScript quality | No `any`; unions and `readonly` used where they remove bugs; errors modelled explicitly |
| Testability | Could the learner's own tests exercise it without the whole system? |
Rule: reward reasoning and trade-offs, not a specific pattern or class structure (R3, R11).

### 4.10 Mastery-based pacing and study order [P]
- **No calendar logic anywhere:** no due dates, deadlines, streaks, weekly targets or duration estimates in any file or message. The mentor never says a learner is "behind".
- **Study order** is read from `CURRICULUM.md` (M1 → M2 → M9 → M3 → … → Capstone). Prerequisites are checked by lesson id against `passed`/`passed-with-help` in `PROGRESS.md`; the *order* comes from the sequence.
- **Mastery evidence** for `passed`: discussion lessons need the rubric (4.4/4.6) with no *Missing* on the module's critical dimensions and the interview question at least *ok*; code lessons (Module 9) additionally need green specs and `tsc` and a design review (4.9) with no *Missing* on Cohesion, Coupling, Testability. A green build alone never passes a lesson.
- **Remediation:** if the evidence is not met, the mentor creates a **new scenario on the same skill** (not a rewritten answer key), appends the attempt to the `PROGRESS.md` Completed tasks log and continues; no attempt limit. A lesson passed after a hint or solution is `passed-with-help` and its gap is re-asked later (5.7).
- **Learner control:** the learner may repeat any passed lesson with a fresh scenario or ask to jump ahead; a jump needs the learner's approval and a change-log entry (V1 §7).
- **Timers** appear only inside simulated interviews (37, 38, 47) as part of the skill; elapsed time is recorded but never used to pass or fail.

## 5. File formats [P]

### 5.1 `PROGRESS.md` [V shape from V4]
Sections: CURRENT (overwritten) · Lessons table · Completed tasks log · Interview log · Knowledge gaps · Review log · Your notes (never touched). Differences from the verified files: **Test results log is replaced by Review log** (date, lesson, rubric summary line, rating); Interview log keeps the `Answer summary` column from `ai-agentic-lecture` (V4), which `BIG-O-LEARNING` dropped.

CURRENT block keys: `lesson, title, tier, step, pending task (verbatim), files, last review, hints used, awaiting, open interview question`.

### 5.2 Lesson folder [P]
| File | Written by | When |
|---|---|---|
| `LESSON.md` | Mentor | Lesson start. Sections: scenario type, vocabulary, what/why/when, trade-off table, numbers to remember (labelled approximate), common mistakes |
| `SCENARIO.md` | Mentor | Lesson start. Business story, constraints, the single first question |
| `answer.md` | Learner | Step 3. Mentor never edits it. In Module 9 it holds the learner's reasoning (why this design, what trade-offs) next to the code |
| `challenge/stub.ts`, `challenge/spec.test.ts` | Learner edits stub; mentor owns spec | Module 9 only (section 2.1) |
| `REVIEW.md` | Mentor | After the learner answers (Module 9: after the specs are green): rubric table (4.4, 4.6 or 4.9), what a strong answer would have covered (written only now), one improvement |

### 5.3 `QUESTIONS.md` [V format, extended]
Entry: `### Q<n> — Lesson NN`: Question · Short answer (after the learner answered) · Where it appears · Rating · My question? · **Tags** (module) · **Last asked** (date, record only) · **Re-ask after** (lesson id, in study order). Tags and the lesson marker support spaced review (5.7). Add every learner question marked `(my question)`.

### 5.4 `MISTAKES.md` [V format]
`### M<n> — Lesson NN`: I thought · What was true · **Lesson:** · linked gap id.

### 5.5 `DECISIONS.md` [V7 template]
`### D<n>: title` — Date · Module · Status (proposed / approved / superseded by D<n>) · Context · Options (at least two) · Decision · Why · Consequences. Used in module 7: the learner writes realistic ADRs for scenarios; the mentor reviews. Contains fictional or sanitised scenarios only (R5).

### 5.6 `STORIES.md` [P]
`### S<n>: short title` — Competency tags (conflict, failure, leadership, ownership, ambiguity, mentoring, influence-without-authority) · Situation · Task · Action · Result · Reflection · Sanitised? (yes) · Rating history. Learner-written only.

### 5.7 Spaced review [P]
Re-asking is counted in **lessons completed in study order**, never in days: *weak* → re-ask within the next 2 lessons, *ok* → after 5 lessons, *strong* → at the module review. At the start of each lesson the mentor asks at most **two** due questions or open gaps as a warm-up. A gap closes only on a good answer (V1 §7).

## 6. Review exercises [P]

Each module has one review `Rn` before its gate:
1. Mixed scenario spanning at least three lessons of the module and one earlier module (interleaving).
2. Tier C, no time limit (pacing is mastery-based), written in `reviews/Rn-slug/answer.md`.
3. Mentor review with the rubric (4.4); the gate needs no dimension marked Missing on Requirements, Trade-offs, Reliability. **R9 (code)** uses the design rubric (4.9): specs and `tsc` green, and no Missing on Cohesion, Coupling, Testability.
4. A short "rapid-fire" set of five questions drawn from `QUESTIONS.md` for that module.
Gate passes only with the learner's explicit approval (V1 §7).

## 7. Curriculum mechanics [P]

`CURRICULUM.md` is the contract (V3): status line, tier table, module tables with columns *# · Topic · Prereq · Practical scenario · Interview question · Tier*, a review row per module, gates, coverage matrix, change log. Nine modules: M1–M8 (lessons 01–36, reviews R1–R8), capstone (37–38, unchanged ids), and M9 (lessons 39–47, review R9). Lesson ids are stable keys; the **study order** is M1 → M2 → M9 → M3 → M4 → M5 → M6 → M7 → M8 → Capstone, and `CURRICULUM.md` carries it as an explicit sequence. "Next lesson" means the next entry in that sequence, never the next number, and the `PROGRESS.md` Lessons table is kept in study order. The capstone prerequisite is gates M1–M9. It contains no lesson content or answers. A lesson is `passed` when the learner completed the answer, the review has no Missing on the module's critical dimensions, and the interview question is rated at least ok; `passed-with-help` if any hint level was used.

## 8. Validation plan for the later implementation phase [P]

No test runner exists, so validation is by inspection:
1. Every file listed in section 2 exists and each trigger names `MENTOR.md`.
2. `CURRICULUM.md` lesson ids equal the rows in `PROGRESS.md` Lessons table, and the table follows the study order sequence (checked with a one-line `grep`/`diff` in the shell, not committed code).
3. `grep` finds no file under `lessons/` containing "Model answer" or solution text before the learner's `answer.md` exists.
4. Dry run: say "Continue my lesson" in a fresh Cursor session and in a fresh Claude Code session; both must restate the pending task and start nothing.
5. Dry run "start lesson 1" before syllabus approval: both must refuse.
6. Review of the first real `REVIEW.md` for rubric consistency before starting module 2.
7. **Module 9 setup validation (when approved):** `npm install`, `npm run typecheck`, `npm test` on the smoke test, then `npm run check -- 39` must show the lesson's baseline as FAIL with `tsc` PASS before the learner starts; the spec is validated against a throwaway reference solution kept **outside** the repo and deleted, as done for `BIG-O-LEARNING` Lesson 01 (V10).

## 9. Build phases (each needs approval) [P]

1. Design (this step): HLD, LLD, draft CURRICULUM. **Stop.**
2. Setup: `MENTOR.md`, two triggers, `PROGRESS.md`, `QUESTIONS.md`, `MISTAKES.md`, `DECISIONS.md`, `STORIES.md`, `.gitignore`; validation 8.1–8.5.
3. Lesson 01 only, after the syllabus is approved.
4. Pilot review (8.6); adjust protocol; then modules proceed one lesson at a time.
5. **Module 9 setup (separate approval, when the learner reaches Module 9, i.e. after gate M2):** exercise setup 2.1, smoke test, validation 8.7, then lesson 39 only.

## 10. Risks specific to this LLD

| # | Risk | Mitigation |
|---|---|---|
| L1 | Written-answer review is unverifiable by machine | Rubric with quoted evidence; learner may ask for a second opinion by rephrasing; no test-based claims |
| L2 | Mentor "probes derived at lesson time" may be inconsistent across sessions | Probes belong to the conversation only; `REVIEW.md` records what was asked |
| L3 | `answer.md` and `STORIES.md` could be overwritten by the agent | Hard limit 4.8; git commits by the learner |
| L4 | Re-ask markers are counted in lessons, so a long idle gap leaves items unasked until the learner returns | Intended under mastery pacing; the mentor asks due items first on resume, max two per lesson |
| L5 | Merging V1 and V6 may produce a longer `MENTOR.md` than the agent follows reliably | Keep to the headings above; target under 150 lines; re-test with dry runs 8.4–8.5 |
| L6 | Interleaved reviews may reference lessons not yet taken in a partial run | Review scenarios use only lessons `passed` at that time |
| L7 | Verified patterns come from projects with empty logs, so the exact formats are untested under real answers | Pilot (phase 4) before module 2 |
| L8 | Mentor-written specs for open design problems may reject valid designs | Specs go through minimal entry points and observable behaviour only; spec bugs disclosed before any change; learner may add `my-tests/` |
| L9 | `scripts/lesson.mjs` `check NN` only searches `lessons/`; R9 sits in `reviews/` | Use the documented `npx vitest run reviews/R9-oop-lld`; no runner change proposed |
| L10 | Interview-style live class design (lesson 47) cannot be time-boxed by the tooling | Learner self-times 45 minutes; the mentor records the actual time taken |
| L11 | Design-rubric ratings are judgments and can drift | Quote the learner's own code in each rating; compare against previous REVIEW.md files |
