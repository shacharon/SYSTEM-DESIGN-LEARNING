# PROGRESS — SYSTEM-DESIGN-LEARNING

> Written by the mentor only. The CURRENT block is the only part that is overwritten; every log below it is append-only.
> Add your own comments in "Your notes" at the bottom; the mentor never edits that section.
> No dates, deadlines or targets drive progress: it is mastery-based (see MENTOR.md section 7). Dates below are records only.

## CURRENT
- lesson: 01
- title: Requirements, estimation, capacity numbers
- tier: A
- step: 3 (learner answering)
- pending task: Answer Question 1 in lessons/01-requirements-estimation/SCENARIO.md, verbatim: "Using the Requirements heading from the lesson guide, what functional and non-functional requirements would you confirm or assume for LinkLite, and what would you explicitly leave out of scope for now?" (chat or lessons/01-requirements-estimation/answer.md)
- files: lessons/01-requirements-estimation/LESSON.md · lessons/01-requirements-estimation/SCENARIO.md · lessons/01-requirements-estimation/answer.md (you write, optional)
- last review: none
- hints used: 0
- awaiting: learner
- open interview question: none (asked at step 6, after the review)

Step legend: 0 not started · 1 theory presented · 2 scenario presented · 3 learner answering · 4 hint/solution requested · 5 in review · 6 interview question asked · 7 awaiting approval to advance.

## Lessons (study order: M1, M2, M9, M3, M4, M5, M6, M7, M8, Capstone; ids are stable keys)
| # | Lesson | Tier | Status | Hints used | Rating | Interview | Date |
|---|---|---|---|---|---|---|---|
| 01 | Requirements, estimation, capacity numbers | A | in progress | 0 | - | - | - |
| 02 | Client-server, layers, monolith vs modular monolith vs microservices | A | locked | - | - | - | - |
| 03 | Horizontal vs vertical scaling, stateless services, load balancing | A | locked | - | - | - | - |
| 04 | Bottlenecks, latency budgets, back-of-envelope reasoning | B | locked | - | - | - | - |
| 05 | Availability, SLAs/SLOs, single points of failure | B | locked | - | - | - | - |
| R1 | Review R1: design a photo-sharing backend at scale | C | locked | - | - | - | - |
| 06 | REST resources, verbs, status codes, pagination, versioning | A | locked | - | - | - | - |
| 07 | Idempotency, retries, rate limiting, error contracts | B | locked | - | - | - | - |
| 08 | REST vs GraphQL vs gRPC; sync vs async; webhooks | B | locked | - | - | - | - |
| 09 | API security and auth: OAuth2/OIDC basics, tokens, authz models, abuse | B | locked | - | - | - | - |
| R2 | Review R2: design the API for a booking platform | C | locked | - | - | - | - |
| 39 | OOP fundamentals: encapsulation, abstraction, polymorphism, inheritance basics; classes... | A | locked | - | - | - | - |
| 40 | Class and interface design: cohesion, coupling, invariants, immutability, `readonly`, d... | A | locked | - | - | - | - |
| 41 | SOLID I: Single Responsibility and Open/Closed | B | locked | - | - | - | - |
| 42 | SOLID II: Liskov, Interface Segregation, Dependency Inversion | B | locked | - | - | - | - |
| 43 | Composition vs inheritance: delegation, mixins, when inheritance is right | B | locked | - | - | - | - |
| 44 | Design patterns I, creational and structural: Factory, Builder, Adapter, Decorator, Fac... | B | locked | - | - | - | - |
| 45 | Design patterns II, behavioural: Strategy, Observer, State, Command, Template Method; p... | B | locked | - | - | - | - |
| 46 | Clean code and refactoring: smells, naming, small functions, characterization tests, sa... | B | locked | - | - | - | - |
| 47 | Mock low-level design round (45 minutes, unseen problem, implemented in TypeScript) | C | locked | - | - | - | - |
| R9 | Review R9: refactor and extend a small system with a new requirement, plus five rapid-f... | C | locked | - | - | - | - |
| 10 | Relational modeling, keys, normalization, access patterns | A | locked | - | - | - | - |
| 11 | Indexes, query plans, transactions, isolation levels | B | locked | - | - | - | - |
| 12 | NoSQL families (key-value, document, wide-column, graph) and when | B | locked | - | - | - | - |
| 13 | Replication, read replicas, consistency, backups, RPO/RTO | B | locked | - | - | - | - |
| 14 | Partitioning and sharding, hot keys, migrations | C | locked | - | - | - | - |
| R3 | Review R3: model and scale the data layer of a ride-hailing app | C | locked | - | - | - | - |
| 15 | Caching: patterns, TTL, invalidation, stampede | A | locked | - | - | - | - |
| 16 | CDNs and edge caching | B | locked | - | - | - | - |
| 17 | Message queues and streams: delivery semantics, ordering, DLQ, backpressure | B | locked | - | - | - | - |
| 18 | CAP/PACELC, consistency models, consensus at a conceptual level | B | locked | - | - | - | - |
| 19 | Distributed patterns: sagas, outbox, retries, circuit breakers, idempotent consumers | C | locked | - | - | - | - |
| R4 | Review R4: design a notification platform with queues and caching | C | locked | - | - | - | - |
| 20 | Core building blocks: regions, AZs, VPC, subnets, security groups, IAM roles | A | locked | - | - | - | - |
| 21 | Compute choices: EC2, containers (ECS/EKS), Lambda; autoscaling | B | locked | - | - | - | - |
| 22 | Storage and databases on AWS: S3, RDS/Aurora, DynamoDB, ElastiCache | B | locked | - | - | - | - |
| 23 | Messaging and integration: SQS, SNS, EventBridge, API Gateway, load balancers | B | locked | - | - | - | - |
| 24 | Well-Architected thinking: multi-AZ, DR strategies, cost levers, least privilege | C | locked | - | - | - | - |
| R5 | Review R5: end-to-end AWS design for a SaaS product, with a cost and failure discussion | C | locked | - | - | - | - |
| 25 | Metrics, logs, traces; RED/USE; SLIs/SLOs and error budgets | A | locked | - | - | - | - |
| 26 | Alerting, on-call, incident response, postmortems | B | locked | - | - | - | - |
| 27 | CI/CD, deployment strategies, feature flags, rollbacks, migrations | B | locked | - | - | - | - |
| 28 | Reliability engineering: load testing, capacity planning, chaos, graceful degradation, ... | C | locked | - | - | - | - |
| R6 | Review R6: run a simulated incident and write the postmortem | C | locked | - | - | - | - |
| 29 | Architecture decision records, trade-off analysis, reversible vs irreversible decisions | A | locked | - | - | - | - |
| 30 | Technical debt, build vs buy, migration and strangler strategies | B | locked | - | - | - | - |
| 31 | Technical leadership: estimates, roadmaps, stakeholders, disagreement and influence | B | locked | - | - | - | - |
| 32 | Quality and team practices: reviews, standards, mentoring, onboarding, risk communication | C | locked | - | - | - | - |
| R7 | Review R7: a full ADR set and a written one-page proposal for a re-architecture | C | locked | - | - | - | - |
| 33 | STAR structure, story inventory, competencies | A | locked | - | - | - | - |
| 34 | Conflict, failure and feedback stories | B | locked | - | - | - | - |
| 35 | Leadership, influence and ambiguity stories | B | locked | - | - | - | - |
| 36 | Delivery under pressure; handling tough follow-ups | C | locked | - | - | - | - |
| R8 | Review R8: deliver four stories back to back with follow-ups | C | locked | - | - | - | - |
| 37 | Mock system design round (45 minutes, unseen problem), ending with a class-level drill-... | C | locked | - | - | - | - |
| 38 | Mock Tech Lead + behavioral round | C | locked | - | - | - | - |

Status values: `not started | locked | in progress | passed | passed-with-help`. Reviews (R1–R9) use the same values.

## Completed tasks log (append-only)
| Date | Lesson | Task | Result |
|---|---|---|---|
| 2026-10-15 | setup | Phase 2: MENTOR.md, triggers, PROGRESS/QUESTIONS/MISTAKES/DECISIONS/STORIES | done; no lesson started |

## Interview log (append-only)
| Date | Lesson | Question | Answer summary | Rating (weak/ok/strong) | Gaps |
|---|---|---|---|---|---|

## Review log (append-only)
| Date | Lesson | Rubric summary (one line) | Result (passed / passed-with-help / remediation) |
|---|---|---|---|

## Knowledge gaps
| id | Topic | Origin lesson | Re-ask after lesson | Status (open/closed) | Related mistake |
|---|---|---|---|---|---|

## Protocol review log (append-only)
The Protocol review after Lesson 01 is **required before lesson 02** (MENTOR.md section 7). Record: one-question-at-a-time held? hints withheld until asked? rubric evidence quoted? saves done? too long or too easy? changes proposed (applied only with the learner's approval).
| Date | After lesson | Findings | Changes approved | Status |
|---|---|---|---|---|
| - | 01 | pending | - | **not done** |

## Your notes
(Free space for the learner. The mentor never edits this section.)
