# SYSTEM-DESIGN-LEARNING — High-Level Design

Status: **DESIGN FINALIZED (rev 3); implementation not started.** `SYSTEM-DESIGN-LEARNING/` contains only `docs/HLD.md`, `docs/LLD.md` and `CURRICULUM.md`. Nothing here is implemented. Date: 2026-10-15. Rev 2 added Module 9 (OOP and Low-Level Design). **Rev 3:** Module 9 is studied after Module 2 (ids 39–47 unchanged), TypeScript/Vitest approved for Module 9 only, design review required beyond tests, capstone prerequisites include Module 9, pacing is mastery-based.

Legend: **[V]** verified by reading a file on disk (path given). **[P]** proposal, does not exist yet.

## 1. Purpose and scope

A learner (one person) prepares for senior engineering and Tech Lead interviews and for real architecture work. One AI mentor, operated directly in Cursor or Claude Code, teaches nine topic areas through short lessons, practical scenarios, interview questions and review exercises. Progress, questions, mistakes, decisions and behavioral stories are plain Markdown files.

In scope: the nine topics in `CURRICULUM.md`. Module 9 adds **practical TypeScript exercises with Vitest tests**; they are the only code in the project. Out of scope: building or deploying anything (no AWS account use, no infrastructure, no sample apps), a CLI, a backend, LLM API calls, multi-agent setups, automated grading of design quality.

## 2. Verified findings (inspection on 2026-10-15)

### 2.1 Existing mechanisms that can be reused

| # | Mechanism | Where | Verified |
|---|---|---|---|
| V1 | Mentor protocol: load order, 7-step lesson loop, tiers A/B/C, resume with "disk wins", hints only on request, advance only on explicit approval, hard limits, review checklist, interview-question protocol | `ai-agentic-lecture/MENTOR.md`, copied and adapted in `BIG-O-LEARNING/MENTOR.md` | [V] read both |
| V2 | Triggers: `CLAUDE.md` phrase list and an `alwaysApply` Cursor rule that both point at `MENTOR.md` | `ai-agentic-lecture/{CLAUDE.md,.cursor/rules/academy-mentor.mdc}`, `BIG-O-LEARNING/{CLAUDE.md,.cursor/rules/big-o-mentor.mdc}` | [V] |
| V3 | `CURRICULUM.md` contract: status line, tier table, per-module syllabus tables (prereq, scenario, challenge, interview focus), milestone gates, change log; changes need learner approval | `ai-agentic-lecture/CURRICULUM.md`, `BIG-O-LEARNING/CURRICULUM.md` | [V] |
| V4 | `PROGRESS.md`: overwritten CURRENT block; Lessons table; append-only Completed, Test results, Interview log, Knowledge gaps; untouched "Your notes"; single writer | both projects | [V] |
| V5 | `QUESTIONS.md` and `MISTAKES.md` templates (entry formats; model answer written only after the learner answered; first-person mistakes ending in **Lesson:**) | `BIG-O-LEARNING/` | [V] files exist. **Both are empty**, so they are untested in real use |
| V6 | Case-based, code-free Socratic mentoring: one business problem and one question at a time; never reveal the recommended architecture first; challenge the weakest assumption; six evaluation dimensions (correctness, reliability, security, latency, cost, observability); challenge toolbox ("10x traffic", "provider down two hours"…); resume restates position in 1–2 sentences | `CLAUDE-AI-AGENTIC-BASIC/architecture-lab/{MENTOR.md,CURRICULUM.md,cases/case-01-claims-triage.md}` | [V] read. Only case 1 exists and no answers recorded |
| V7 | Architecture decision log template (D-number, status, context, options, decision, why, consequences) | `CLAUDE-AI-AGENTIC-BASIC/banking-agent/learning/DECISIONS.md` | [V] |
| V8 | Per-lesson interview memory bank (`Q1…` with short answer and pointer; gotchas; mistakes) with real history and a `recap-all-modules.md` | `CLAUDE-AI-AGENTIC-BASIC/interview-questions/` (m1–m6, pe2, recap) | [V] m1 read; others listed only. Content is Agentic-AI, so the format is reusable, the content is not |
| V9 | Isolation convention: sibling projects state "do not modify other labs" | `banking-agent/CLAUDE.md`, `agentic-ai-academy/MENTOR.md` | [V] |
| V10 | TypeScript + Vitest exercise setup for a mentor-led project: strict `tsconfig` (`noUncheckedIndexedAccess`, `NodeNext`), Vitest scoped to `lessons/**/*.test.ts`, runner `scripts/lesson.mjs` (`check NN`, `experiment NN`, `typecheck`), lesson shape `LESSON.md` + `challenge/stub.ts` + `challenge/spec.test.ts` (+ `answer.md`), mentor-owned specs, learner-owned stubs, SOLUTION in chat only | `ai-agentic-lecture/{tsconfig.json,vitest.config.ts,scripts/lesson.mjs,lessons/01-tokens/}`, `BIG-O-LEARNING/{package.json,tsconfig.json,vitest.config.ts,scripts/lesson.mjs,lessons/01-growth-rates/}` | [V] read; in `BIG-O-LEARNING` I also ran `npm install`, `npm test`, `npm run typecheck` and `npm run check -- 01` in this environment (Node v20.17.0): tooling works, Lesson 01 baseline fails as designed (0/20) |

### 2.2 Verified gaps

- **No system-design, AWS, STAR or Tech Lead content exists** in any project (`grep -i aws` over the learning projects' Markdown found nothing). Everything topical is new.
- **No OOP, SOLID, class-design or refactoring content exists** (`grep` for SOLID, "design pattern", refactor over the learning projects' Markdown found only *agentic workflow* patterns in `ai-agentic-lecture` and `agentic-ai-academy`, and passing mentions in `banking-agent/learning`). Module 9 content is new; only the exercise tooling (V10) is reused.
- **No existing code-design review rubric.** Tests in V10 check behaviour only; nothing in the verified projects judges design quality.
- **No real learner history exists in the active template projects:** `BIG-O-LEARNING` question and mistake files are empty; `ai-agentic-lecture` Interview log and Knowledge gaps tables are empty. Only the Agentic-AI memory bank has history. [V]
- **All mentor rules are advisory** (instruction files only, no hooks or scripts enforce them). [V by absence]
- `ai-agentic-lecture` is a git repo with **zero commits**; `BIG-O-LEARNING` has one commit and is pushed to `github.com/shacharon/BIG-O-LEARNING`. [V]
- `architecture-lab` stores a "mentor-only" probe checklist inside the case file, which the learner can open. [V]

### 2.3 Active vs legacy (partly inferred; owner to confirm)

| Path | Classification | Basis |
|---|---|---|
| `BIG-O-LEARNING/` | **Active, primary template** | Newest, pushed, trimmed protocol (V1–V5), Lesson 01 in progress |
| `ai-agentic-lecture/` | **Active, upstream source** of the protocol | Approved curriculum, Lesson 01 in progress; do not modify |
| `CLAUDE-AI-AGENTIC-BASIC/architecture-lab/` | **Active, pattern source** for case-based mentoring | Own mentor, case 1 presented |
| `CLAUDE-AI-AGENTIC-BASIC/banking-agent/learning/` | **Active**, source for the decision log | Verified skeleton, milestone pending |
| `CLAUDE-AI-AGENTIC-BASIC/interview-questions/` | **Active reference**, format only | Real history, wrong topic |
| `agentic-ai-academy/` | **Legacy candidate** | Overlaps `ai-agentic-lecture`, never approved, no code |
| `agentic-ai-sandbox`, `agentic-ai-sandbox-cursor`, `CURSOR-AI-AGENTIC-BASIC` | **Legacy / parallel labs** | Code-only, no mentor files |

Classification is inferred from content; many files share a 2026-10-14 18:12 timestamp (bulk touch), so mtimes are not evidence.

## 3. Design principles [P]

1. **The IDE agent is the single mentor.** No runtime of our own.
2. **Files are the state.** Markdown only; the agent edits them with its normal tools; a human can read and fix them.
3. **Conversation over code, except Module 9.** Modules 1–8 are discussion and written reasoning with no code or build tooling. Module 9 (OOP and Low-Level Design) uses TypeScript and Vitest strictly for its exercises and tests, reusing V10. The tooling is created only when Module 9 is approved to start, not before.
4. **Socratic, one question at a time**, borrowed from `architecture-lab` (V6), combined with the lesson loop and approval rules of `ai-agentic-lecture` (V1).
5. **No answer keys on disk.** The learner never sees a model answer before attempting; probing notes are produced at lesson time, not stored (fixes the V6 weakness).
6. **Progressive difficulty** via tiers: guided, constrained, open.
7. **Trade-offs and numbers.** Every design answer is judged on the six dimensions from V6, plus data model and operability.
8. **Honesty about facts.** Cloud-service limits, prices and features change; the mentor labels them "verify in current docs" and never invents numbers as facts.
9. **Copy, don't import.** Existing repositories are read-only sources.

## 4. Conceptual architecture [P]

```text
learner ──► Cursor / Claude Code chat  (single mentor = the IDE agent)
               │ reads on trigger                 │ writes (mentor session only)
               ▼                                  ▼
 MENTOR.md  CURRICULUM.md  PROGRESS.md      PROGRESS.md · QUESTIONS.md · MISTAKES.md
                                            · DECISIONS.md · STORIES.md
               │ creates one lesson at a time
               ▼
 lessons/NN-slug/  LESSON.md · SCENARIO.md · answer.md · REVIEW.md
 lessons/39..47    (Module 9 only, studied after Module 2) + challenge/stub.ts · challenge/spec.test.ts
```

No server, database, CLI or API call. The "system" is a dozen Markdown files plus two trigger files. **From Module 9 only**, a small TypeScript/Vitest exercise setup (V10) is added; it contains learner exercises and mentor-owned specs, nothing else.

## 5. Learning model [P]

- **Nine modules**, 47 lessons, 9 review exercises, each module ending with a **review** and a **gate** (see `CURRICULUM.md`). Module 9 adds lessons 39–47 and is **studied after Module 2**; ids 01–38 are unchanged.
- **Study order:** M1 → M2 → M9 → M3 → M4 → M5 → M6 → M7 → M8 → Capstone. "Next lesson" is the next entry in that order, not the next id.
- **Mastery-based pacing:** no deadlines, weekly targets or duration estimates. A gate is met by evidence (rubric, interview rating, and for Module 9 green specs plus design review). If not met, the mentor sets a remediation scenario on the same topic; attempts are logged and unlimited. Re-asking is counted in lessons, not days. Timers exist only inside mock interviews (37, 38, 47).
- **Capstone prerequisites:** gates M1–M9 including R9; lesson 37 ends with a class-level drill-down of one component.
- **Two kinds of lesson:** discussion lessons (M1–M8: written/chat answer reviewed with the rubric) and **code lessons** (M9: a TypeScript stub the learner implements against mentor-owned Vitest specs, then a design-rubric review of the learner's code). Passing tests is necessary, never sufficient: tests check behaviour, the rubric judges design.
- **Lesson loop** (adapted from V1): theory and vocabulary → one practical scenario → learner answers in writing or chat → hints only on request → mentor reviews with the six-dimension rubric → one interview question → record and stop.
- **Tiers:** A Guided (mentor supplies the answer structure: requirements, estimates, components, trade-offs), B Constrained (requirements and constraints only), C Open (scenario only; the learner drives, the mentor attacks assumptions).
- **Review exercises:** at module end, a mixed scenario that reuses earlier lessons; plus gap warm-ups (V4 Knowledge gaps) at the start of later lessons.
- **Artifacts the learner keeps:** question bank, mistakes log, decision log (ADR practice for module 7), STAR story bank (module 8).

## 6. Constraints

- Single learner, single IDE session at a time.
- English only in project files (as in V6, V9).
- No secrets, no employer-confidential detail in files: if the repo is pushed to GitHub, everything in it is exposed (see risk R5).
- Learner writes the answers; the mentor does not write the learner's STAR stories or designs.

## 7. Alternatives considered

| Option | Verdict |
|---|---|
| Build a CLI or web app around an LLM API | Rejected by the owner's pattern (BIG-O rev 2) and by cost; the IDE agent already does this |
| Reuse `architecture-lab` directly (extend it) | Rejected: it is an active lab of another project and must not be modified |
| Fork `BIG-O-LEARNING` including TypeScript/Vitest from day one | Rejected for Modules 1–8 (nothing to compile). Accepted narrowly for Module 9 only, set up when it starts (D2 revised) |
| Teach OOP/LLD as discussion only, no code | Rejected: SOLID, composition and patterns are learned by writing and refactoring classes under tests; interviews also ask for live class design |
| Separate project for OOP/LLD | Rejected: it is one of the nine senior-interview topics and shares the mentor, rubric and question bank |
| Hands-on AWS labs | Rejected for now: needs an account, costs, and the owner said no infrastructure |
| Lecture-style content in files | Rejected: static answers on disk leak solutions and go stale |

## 8. Risks

| # | Risk | Mitigation |
|---|---|---|
| R1 | Mentor rules are advisory; the agent may advance early, reveal answers or overwrite files | Resume protocol "disk wins", git history, short rules, explicit approval gate |
| R2 | No tests means no objective pass/fail; ratings are the mentor's judgment and may drift | Fixed rubric in `MENTOR.md`; store the learner's answer excerpt with each rating |
| R3 | System design has no single correct answer, so "strong" can become "agrees with the mentor" | Rubric rewards stated trade-offs and numbers, not a specific architecture |
| R4 | AWS and numeric facts go stale or are hallucinated | Label as unverified, require "verify in current docs", prefer reasoning over memorised limits |
| R5 | Behavioral stories and decision logs may contain employer-confidential or personal data and be pushed to GitHub | Private repo, sanitise rule in `MENTOR.md`, never record customer, secret or personal data |
| R6 | Scope: 47 lessons is long and open-ended because pacing is mastery-based (no calendar end date) | Milestone gates give coherent stopping points; owner may cut modules; the mentor reports gates passed, never time spent |
| R7 | Template drift between three similar projects | Record the copy date and source in `MENTOR.md` |
| R8 | Reused patterns are mostly unproven with real answers (empty logs) | Pilot with lesson 01 and adjust the protocol before module 2 |
| R9 | Active/legacy classification is inferred | Owner confirmation; nothing is deleted or edited |
| R10 | Cursor and Claude Code triggers can diverge | Keep both to one paragraph pointing at `MENTOR.md` |
| R11 | Specs pass with ugly code: tests cannot judge design quality, so "green" may hide a bad design | Mandatory design-rubric review (`LLD.md` 4.9) after green; specs test behaviour through minimal entry points so more than one valid design passes |
| R12 | Over-engineering: learners (and the mentor) may force patterns where none is needed | Rubric dimension "fit, no over-engineering"; every lesson includes a case where the simplest code wins |
| R13 | Exercise tooling arrives late (at Module 9) and is untested in this project | Validate it with a smoke test at M9 setup, exactly as done in `BIG-O-LEARNING` (V10) |
| R14 | Mentor-authored specs can encode one "right" design | Specs fixed once published (V1); the mentor states any spec bug before changing it; learner may add own tests in `my-tests/` |

## 9. Approval decisions

| # | Decision | Recommendation |
|---|---|---|
| D1 | Single source of truth for the protocol: `BIG-O-LEARNING/MENTOR.md` (derived from `ai-agentic-lecture`) with the architecture-lab Socratic rules merged in | **Resolved (rev 3)**: owner said to preserve the existing mentor and progress architecture |
| D2 *(revised)* | TypeScript + Vitest only for Module 9 exercises and tests; none in Modules 1–8; tooling created when the learner reaches Module 9 (after gate M2) | **Resolved (rev 3): approved** |
| D3 *(revised)* | Nine modules, 47 lessons and 9 reviews as in `CURRICULUM.md` | **Resolved (rev 3)**: all 9 OOP lessons and R9 kept, Module 9 after Module 2 |
| D4 | Private GitHub repo and the confidentiality rule (R5) | **Unresolved**; blocks first push |
| D5 | AWS taught by reasoning and diagrams only, no live account | **Unresolved**; shapes Module 5 only |
| D6 | Extra learner-owned files `DECISIONS.md` and `STORIES.md` | **Unresolved**; blocks Phase 2 file set |
| D7 | Active/legacy classification in section 2.3 | **Unresolved**; informational |
| D9 | Module 9 placement | **Resolved (rev 3)**: immediately after Module 2; ids 39–47 preserved |
| D10 | Design review is rubric-based and required beyond passing tests; a green solution may be sent back for rework | **Resolved (rev 3): approved** |
| D11 | Pacing is mastery-based, not calendar-based | **Resolved (rev 3): approved** |
| D12 | Capstone prerequisites include Module 9 (gates M1–M9) | **Resolved (rev 3): approved** |
| D8 | Proceed to Phase 2 (create protocol, triggers, learning files) | **Not given**; owner said not yet |
