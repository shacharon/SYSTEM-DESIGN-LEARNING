# Lesson 01 — Requirements, estimation, capacity numbers (Tier A: guided)

**Type:** discussion lesson. No code. All scenarios are fictional.

## Vocabulary you must be able to define
functional requirement · non-functional requirement (latency, availability, durability, consistency) · scale (users, requests per second, data size) · read/write ratio · peak vs average load · QPS · back-of-envelope estimation · order of magnitude · capacity (storage, bandwidth, memory) · assumption.

## What / why / when
- **Requirements first:** a design is only "good" relative to what it must do and how well. The same product needs very different systems at 100 users and at 100 million.
- **Estimation:** quick, rough arithmetic that tells you which problems are real (storage? read traffic? write traffic?) before you pick technology. Aim for the right order of magnitude, not precision.
- **When it matters:** at the start of every design discussion and every interview. Skipping it is the most common reason answers sound generic.

## Numbers to remember (approximate, orders of magnitude)
| Item | Rough value |
|---|---|
| Seconds in a day | about 86,400 (use about 100,000 for mental math) |
| Seconds in a month | about 2.5 million |
| 1 million requests per day | about 12 requests per second on average |
| Peak vs average load | often 2x to 10x the average; choose and state your assumption |
| 1 KB x 1 million | about 1 GB; 1 KB x 1 billion is about 1 TB |
| One typical database server | thousands of simple queries per second is plausible; always state it as an assumption |

## Answer structure (this is the Tier A guide)
Use these headings, in order, for the scenario:
1. **Requirements:** functional, then non-functional, then what is explicitly out of scope.
2. **Numbers:** users or volume, read/write ratio, requests per second (average and peak), data size per item, storage over time.
3. **Components:** the main pieces and how a request flows.
4. **Data:** what is stored and how it is accessed.
5. **Trade-offs:** at least one alternative you rejected and why.
6. **Failure:** what breaks first and how you would notice.

Lesson 01 focuses on headings 1 and 2. Headings 3–6 are introduced progressively in later lessons.

## Worked mini-example of the *method* (a different problem)
*Problem:* a receipt-upload tool for a company of 2,000 employees.
- **Requirements:** functional: upload a receipt photo, list my receipts. Non-functional: receipts must not be lost (durability), uploads feel instant (under 2 s), only the owner and finance can view. Out of scope: OCR.
- **Numbers (assumptions stated):** 2,000 users, each uploads 10 receipts a month, so 20,000 uploads per month, about 0.01 uploads per second on average; month-end peak maybe 50x average, still under 1 per second. Photo about 2 MB, so 20,000 x 2 MB = 40 GB per month, about 0.5 TB per year.
- **Conclusion from the numbers:** traffic is tiny; storage and access control are the real concerns. A heavy distributed design would be over-engineering.
Notice: the numbers *changed what matters*. That is the point of estimating.

## Common mistakes
- Designing before asking anything.
- Giving numbers without stating assumptions.
- Estimating only average load and ignoring peak.
- Treating all requirements as equally important instead of naming the one or two that drive the design.
