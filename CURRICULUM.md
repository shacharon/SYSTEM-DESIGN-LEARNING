# CURRICULUM — SYSTEM-DESIGN-LEARNING

**Status: APPROVED (design finalized rev 3; Phase 2 implemented 2026-10-15).** The owner finalized the syllabus structure on 2026-10-15 (nine modules, 47 lessons, 9 reviews, Module 9 studied after Module 2). The mentor protocol, triggers and learning files now exist; no lesson has started. Lesson 02 is gated behind the Protocol review after Lesson 01 (`MENTOR.md` section 7). See "Unresolved decisions" at the bottom. Lesson ids 01–47 are stable.
**Rules for this file:** it is the contract. It changes only with the learner's explicit approval, and every change is logged in the Change log. It contains no lesson content, answers or hints; the mentor produces lesson material one lesson at a time (see `MENTOR.md`, once created). Design context: `docs/HLD.md`, `docs/LLD.md`.

## Format of every lesson
Theory and vocabulary → one practical scenario → the learner's written or spoken answer → hints only on request → rubric review → one interview question → record and stop. Numbers taught are orders of magnitude and labelled approximate. AWS facts are labelled "verify in current AWS documentation". Nothing is deployed. **Module 9 lessons are code lessons:** the learner implements a TypeScript stub against mentor-owned Vitest specs (`npm run check -- NN`), then the mentor reviews the design with the code-design rubric (`docs/LLD.md` 4.9). Tests passing is necessary, not sufficient. TypeScript and Vitest exist only for Module 9.

## Tiers
| Tier | The mentor supplies | The learner supplies |
|---|---|---|
| **A Guided** | Answer structure and a worked mini-example of the *method* on a different problem | Content for each heading |
| **B Constrained** | Requirements and constraints only | Structure, estimates, design |
| **C Open** | One-paragraph business problem | Clarifying questions, then everything |

Module 9 tiers (code): **A** stub with signatures and `TODO` comments + spec · **B** requirements, exported interfaces and a spec, no bodies · **C** scenario and acceptance criteria only; the learner designs the classes and writes some tests in `my-tests/`.

## Study order (this is the learning sequence; ids never change)
**M1 → M2 → M9 → M3 → M4 → M5 → M6 → M7 → M8 → Capstone.**
Lessons are taken in this order: 01–05, R1, 06–09, R2, **39–47, R9**, 10–14, R3, 15–19, R4, 20–24, R5, 25–28, R6, 29–32, R7, 33–36, R8, 37, 38. "Next lesson" always means the next entry in this order, never the next number. Lesson ids are stable file and table keys (39–47 stay 39–47).

## Pacing: mastery-based, not calendar-based
There are no deadlines, weekly targets or duration estimates. The learner moves on when the gate is met, however long that takes, and may repeat a lesson with a fresh scenario at any time. Progress is decided by evidence, never by elapsed time or lesson count:
- A lesson is `passed` only when the review shows no *Missing* on the critical dimensions and the interview question is rated at least *ok* (Module 9 adds: specs and `tsc` green). Any hint level used makes it `passed-with-help`.
- If it is not met, the mentor sets a **remediation scenario** on the same topic (new problem, same skill) and the attempt is logged; there is no attempt limit.
- Gaps and weak answers are re-asked after a number of **lessons**, not days (`docs/LLD.md` 5.7).
- Timers appear only inside simulated interviews (lessons 37, 38, 47), where the 45-minute limit is part of the skill being practised.

## Syllabus (9 modules, 47 lessons, 9 reviews)
Columns: prerequisites · practical scenario · interview question (asked at the end of the lesson).

### M1 — System architecture and scalability
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 01 | Requirements, estimation, capacity numbers | none | URL shortener: how many requests, how much storage | "How do you size a system before designing it?" | A |
| 02 | Client-server, layers, monolith vs modular monolith vs microservices | 01 | A 12-person team's order system outgrows one codebase | "When would you not use microservices?" | A |
| 03 | Horizontal vs vertical scaling, stateless services, load balancing | 01 | Flash-sale traffic spikes 10x | "What makes a service easy to scale horizontally?" | A |
| 04 | Bottlenecks, latency budgets, back-of-envelope reasoning | 01, 03 | A page takes 3 s; where does the time go | "Walk me through finding the bottleneck." | B |
| 05 | Availability, SLAs/SLOs, single points of failure | 03 | Payments service must reach 99.9% | "What does 99.9% allow per month, and how do you get there?" | B |
| **R1** | **Review:** design a photo-sharing backend at scale (tier C) + five rapid-fire questions | 01–05 | | | C |

### M2 — API design and communication
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 06 | REST resources, verbs, status codes, pagination, versioning | 02 | Public API for orders | "How do you version an API without breaking clients?" | A |
| 07 | Idempotency, retries, rate limiting, error contracts | 06 | Duplicate payment on a client retry | "How do you make a POST safe to retry?" | B |
| 08 | REST vs GraphQL vs gRPC; sync vs async; webhooks | 06 | Mobile app, partner integration, internal services | "Why choose gRPC over REST internally?" | B |
| 09 | API security and auth: OAuth2/OIDC basics, tokens, authz models, abuse | 06 | Third-party access to customer data | "Where does authorization belong, gateway or service?" | B |
| **R2** | **Review:** design the API for a booking platform (tier C) | 06–09, M1 | | | C |

### M9 — OOP and Low-Level Design (code lessons, TypeScript + Vitest) · studied after Module 2
Rev 2 addition, placed in study order after Module 2 in rev 3. Every lesson has a TypeScript exercise with mentor-owned specs, a design review, and one senior interview question. Specs test behaviour through minimal entry points, so more than one valid design passes. Each lesson includes a case where the simplest code is the right answer.
| # | Topic | Prereq | Practical scenario (TypeScript exercise) | Senior interview question | Tier |
|---|---|---|---|---|---|
| 39 | OOP fundamentals: encapsulation, abstraction, polymorphism, inheritance basics; classes vs TypeScript's structural typing | none | Library lending: `Book`, `Member`, `Loan` with rules for borrowing limits | "What is polymorphism, and how does structural typing change what it means in TypeScript?" | A |
| 40 | Class and interface design: cohesion, coupling, invariants, immutability, `readonly`, discriminated unions, modelling errors | 39 | `Money` and `Order` value objects that can never be invalid | "How do you design a class so it cannot be put in an invalid state?" | A |
| 41 | SOLID I: Single Responsibility and Open/Closed | 40 | A do-everything `Invoice` class split up; a discount rule set that must grow without edits | "How do you know a class has too many responsibilities?" | B |
| 42 | SOLID II: Liskov, Interface Segregation, Dependency Inversion | 41 | Payment methods that break substitutability; a fat interface; injecting a notifier | "Give a real Liskov violation and how you fixed it." | B |
| 43 | Composition vs inheritance: delegation, mixins, when inheritance is right | 39, 42 | Notification channels sharing behaviour without a brittle base class | "Why prefer composition over inheritance, and when is inheritance still right?" | B |
| 44 | Design patterns I, creational and structural: Factory, Builder, Adapter, Decorator, Facade; when not to use them | 42, 43 | Integrating two payment providers behind one interface | "Adapter vs Facade vs Decorator: how do you choose?" | B |
| 45 | Design patterns II, behavioural: Strategy, Observer, State, Command, Template Method; pattern misuse | 43, 44 | Order lifecycle, pricing rules, undoable edits | "Strategy vs State: what is the difference in practice?" | B |
| 46 | Clean code and refactoring: smells, naming, small functions, characterization tests, safe refactoring steps | 41, 43 | A tangled `processOrder` function refactored under a provided safety-net spec | "How do you refactor code that has no tests?" | B |
| 47 | Mock low-level design round (45 minutes, unseen problem, implemented in TypeScript) | 39–46 | A problem chosen by the mentor at lesson time (for example parking lot or rate limiter) | "Walk me through your class design, then change one requirement: what breaks?" | C |
| **R9** | **Review:** refactor and extend a small system with a new requirement, plus five rapid-fire senior questions (tier C, `reviews/R9-oop-lld/`) | 39–47 | | | C |

Notes: lesson ids 01–38 are unchanged. Module 9 is studied after Module 2 and before Module 3 (see Study order). Its lessons need only basic TypeScript, no knowledge from Modules 3–8. The exercise tooling (TypeScript + Vitest) is set up when the learner reaches Module 9 (after gate M2), and exists for Module 9 only.

### M3 — Databases and data modeling
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 10 | Relational modeling, keys, normalization, access patterns | 01 | Invoicing schema | "When do you denormalize?" | A |
| 11 | Indexes, query plans, transactions, isolation levels | 10 | Slow report query; double-spend race | "How do you decide what to index?" | B |
| 12 | NoSQL families (key-value, document, wide-column, graph) and when | 10 | Session store, product catalog, social graph | "SQL or NoSQL for this workload, and why?" | B |
| 13 | Replication, read replicas, consistency, backups, RPO/RTO | 11 | Region outage; stale reads after a write | "What does replication lag break?" | B |
| 14 | Partitioning and sharding, hot keys, migrations | 12, 13 | A table reaches billions of rows | "How do you choose a shard key?" | C |
| **R3** | **Review:** model and scale the data layer of a ride-hailing app (tier C) | 10–14, M1–M2 | | | C |

### M4 — Distributed systems, caching and queues
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 15 | Caching: patterns, TTL, invalidation, stampede | 03, 11 | Product pages overload the database | "Cache invalidation: how do you keep it correct?" | A |
| 16 | CDNs and edge caching | 15 | Global media delivery | "What should never be cached at the edge?" | B |
| 17 | Message queues and streams: delivery semantics, ordering, DLQ, backpressure | 07 | Order events to many consumers | "At-least-once vs exactly-once: what do you actually get?" | B |
| 18 | CAP/PACELC, consistency models, consensus at a conceptual level | 13 | Inventory across two regions | "Explain CAP with a real example." | B |
| 19 | Distributed patterns: sagas, outbox, retries, circuit breakers, idempotent consumers | 17, 18 | Checkout across payment, stock and shipping | "How do you keep a multi-service transaction consistent?" | C |
| **R4** | **Review:** design a notification platform with queues and caching (tier C) | 15–19, M1–M3 | | | C |

### M5 — AWS architecture
Conceptual and diagram-based; no account use. Service names are taught by role; every limit or price is "verify in current docs".
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 20 | Core building blocks: regions, AZs, VPC, subnets, security groups, IAM roles | 05 | Put a web tier and a database in a safe network | "Public vs private subnet: what goes where?" | A |
| 21 | Compute choices: EC2, containers (ECS/EKS), Lambda; autoscaling | 03, 20 | A bursty API vs a steady worker | "Lambda or containers for this service?" | B |
| 22 | Storage and databases on AWS: S3, RDS/Aurora, DynamoDB, ElastiCache | 12, 13, 15 | Choose the store for each data type of one product | "Aurora or DynamoDB, and why?" | B |
| 23 | Messaging and integration: SQS, SNS, EventBridge, API Gateway, load balancers | 17, 21 | Event-driven order pipeline | "SQS vs SNS vs EventBridge?" | B |
| 24 | Well-Architected thinking: multi-AZ, DR strategies, cost levers, least privilege | 20–23 | Make a design survive an AZ loss within budget | "Walk me through a DR strategy and its cost." | C |
| **R5** | **Review:** end-to-end AWS design for a SaaS product, with a cost and failure discussion (tier C) | 20–24, M1–M4 | | | C |

### M6 — Production engineering and observability
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 25 | Metrics, logs, traces; RED/USE; SLIs/SLOs and error budgets | 05 | Define SLOs for a checkout service | "How do you know the system is healthy?" | A |
| 26 | Alerting, on-call, incident response, postmortems | 25 | Latency alert at 3 a.m. | "Walk me through your last incident process." | B |
| 27 | CI/CD, deployment strategies, feature flags, rollbacks, migrations | 21 | Ship a risky change safely | "Blue/green vs canary: when each?" | B |
| 28 | Reliability engineering: load testing, capacity planning, chaos, graceful degradation, cost | 25, 19 | Prepare for a 5x launch | "How do you prepare a system for a big launch?" | C |
| **R6** | **Review:** run a simulated incident and write the postmortem (tier C) | 25–28, M1–M5 | | | C |

### M7 — Tech Lead and architecture decisions
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 29 | Architecture decision records, trade-off analysis, reversible vs irreversible decisions | M1–M4 | Write an ADR for a queue vs direct call | "How do you document and defend a decision?" | A |
| 30 | Technical debt, build vs buy, migration and strangler strategies | 29 | Replace a legacy module without a rewrite | "How do you decide to pay down tech debt?" | B |
| 31 | Technical leadership: estimates, roadmaps, stakeholders, disagreement and influence | 29 | Two senior engineers disagree on a design | "How do you handle a design disagreement?" | B |
| 32 | Quality and team practices: reviews, standards, mentoring, onboarding, risk communication | 30, 31 | Raise quality on a team under deadline | "How do you raise the bar without slowing delivery?" | C |
| **R7** | **Review:** a full ADR set and a written one-page proposal for a re-architecture (tier C) | 29–32 | | | C |

### M8 — Behavioral interviews and STAR
Learner-written stories only; the mentor reviews and never writes them. No confidential or personal data.
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 33 | STAR structure, story inventory, competencies | none | Pick five real stories and map them to competencies | "Tell me about a time you owned a hard problem." | A |
| 34 | Conflict, failure and feedback stories | 33 | Disagreement with a peer; a project that failed | "Tell me about a time you failed." | B |
| 35 | Leadership, influence and ambiguity stories | 33, M7 | Led without authority; unclear requirements | "Tell me about a time you led without authority." | B |
| 36 | Delivery under pressure; handling tough follow-ups | 34, 35 | Stakeholder pushback; "what would you do differently" | Unprepared follow-up barrage on one story | C |
| **R8** | **Review:** deliver four stories back to back with follow-ups | 33–36 | | | C |

### Capstone — Mock interview day
| # | Topic | Prereq | Practical scenario | Interview question | Tier |
|---|---|---|---|---|---|
| 37 | Mock system design round (45 minutes, unseen problem), ending with a class-level drill-down of one component | gates M1–M9 (including R9) | A new problem chosen by the mentor | Scored with the rubrics in `LLD.md` 4.4 and, for the drill-down, 4.9 | C |
| 38 | Mock Tech Lead + behavioral round | 37, M7, M8, M9 | Architecture decision case plus three stories | Scored with the rubrics in `LLD.md` 4.4 and 4.6 | C |

## Milestone gates
Gates are passed in study order. A module's gate needs every lesson `passed` or `passed-with-help` and its review without a *Missing* on Requirements, Trade-offs or Reliability (Module 9: specs and `tsc` green and no *Missing* on Cohesion, Coupling or Testability), plus the learner's explicit approval. Skipping or reordering needs approval and a change-log entry.

| Gate | After | You can… |
|---|---|---|
| M1 | R1 | Size a system, choose an architecture style, and name its bottleneck and failure modes |
| M2 | R2 | Design a safe, evolvable API with retries, limits and auth |
| M3 | R3 | Model data for its access patterns and say how it scales and survives failure |
| M4 | R4 | Choose cache, queue and consistency approach and defend the semantics |
| M5 | R5 | Map a design to AWS services, justify them, and cover multi-AZ, DR and cost |
| M6 | R6 | Define SLOs, run an incident, and ship safely |
| M7 | R7 | Record and defend architecture decisions and lead technical disagreement |
| M8 | R8 | Tell sharp, honest STAR stories under follow-up |
| M9 | R9 | Design, implement and refactor classes in TypeScript with SOLID, composition and patterns used for a real reason, and defend the choices |

## Coverage check (requested topics → lessons)
| Requested topic | Lessons |
|---|---|
| System architecture and scalability | 01–05, R1 |
| API design and communication | 06–09, R2 |
| Databases and data modeling | 10–14, R3 |
| Distributed systems, caching and queues | 15–19, R4 |
| AWS architecture | 20–24, R5 |
| Production engineering and observability | 25–28, R6 |
| Tech Lead and architecture decisions | 29–32, R7 |
| Behavioral interviews and STAR | 33–36, R8 |
| OOP and Low-Level Design (OOP, SOLID, composition vs inheritance, patterns, clean code and refactoring, class and interface design, TypeScript exercises, senior questions) | 39–47, R9 |
| Capstone mocks | 37–38 |

Out of scope (a conscious choice): hands-on AWS labs, building applications (Module 9 exercises are small isolated classes, not an app), ML system design, front-end architecture, security certification content, concurrency and threading models, functional-programming deep dives.

## Decisions resolved in rev 3 (owner instruction, 2026-10-15)
| Decision | Resolution |
|---|---|
| Module 9 placement | Studied immediately after Module 2; ids 39–47 and R9 preserved |
| TypeScript + Vitest | Approved for Module 9 only; created when Module 9 starts |
| Module 9 size | Keep all 9 lessons (39–47) and R9; no merge of 44/45 |
| Design review | Required beyond passing tests (rubric in `LLD.md` 4.9) |
| Capstone prerequisites | Include Module 9 (gates M1–M9; lesson 37 adds a class-level drill-down) |
| Pacing | Mastery-based, not calendar-based |
| Mentor and progress architecture | Preserve the verified patterns (`HLD.md` section 2.1) |

## Unresolved decisions (block or shape implementation)
1. **Learner-owned files `DECISIONS.md` and `STORIES.md`** (HLD D6): needed to decide the Phase 2 file set. Blocks Phase 2 file creation.
2. **Repository visibility and confidentiality rule** (HLD D4): private repo and a no-confidential-data rule. Blocks the first push, not local creation.
3. **AWS taught by reasoning and diagrams only, no live account** (HLD D5): shapes Module 5, does not block Phase 2.
4. **Active vs legacy classification** (HLD D7): informational; nothing depends on it.
5. **Explicit go for Phase 2** (HLD D8): not given yet.
6. **ML/AI system design** is not included; confirm that is intended.
7. **Whether to run the Phase 2 pilot protocol review** after lesson 01 before Module 2 (recommended, `LLD.md` 8.6).

## Change log
| Date | Change | Approved by |
|---|---|---|
| 2026-10-15 | Draft created | not yet approved |
| 2026-10-15 | Rev 2: added Module 9 (lessons 39–47, review R9); totals 9 modules, 47 lessons, 9 reviews. Lessons 01–38 and M1–M8 unchanged. Capstone prerequisite "all modules" now includes Module 9 | not yet approved |
| 2026-10-15 | Rev 3: Module 9 moved to study order after Module 2 (ids 39–47 unchanged); TypeScript/Vitest approved for Module 9 only; mastery-based pacing added (calendar estimates removed); design review required beyond tests; capstone prerequisites now gates M1–M9, lesson 37 gains a class-level drill-down; status set to design finalized | owner (rev 3 instruction); Phase 2 not started |
| 2026-10-15 | Status set to approved after Phase 2 implementation (mentor protocol, triggers, learning files created); no content change | owner (Phase 2 instruction) |
