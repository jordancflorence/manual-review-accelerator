# Manual Review Accelerator

**A design framework for keeping unworkable cases out of manual-review queues.**

![Type](https://img.shields.io/badge/type-design%20framework-1f2937) ![Status](https://img.shields.io/badge/status-proof%20of%20concept-0e7490) ![Data](https://img.shields.io/badge/data-synthetic-d97706) ![Focus](https://img.shields.io/badge/focus-operations%20%26%20process%20design-15803d)

Operations teams lose review capacity to cases that were never ready to be worked. This documents a rules-based readiness gate that catches them at intake instead.

![Illustrative operations dashboard showing modeled figures for first-time-right rate, avoidable manual touches, not-ready reasons, queue aging, and lane distribution.](./assets/dashboard-mock.svg)

> *Illustrative operations view. All figures are modeled against synthetic data and shown for layout purposes only.*

---

## The problem

**Most manual-review load is avoidable.**

A case fails automation and lands in a queue. An analyst picks up what looks like a five-minute ticket, finds a missing document or a skipped compliance check, and sends it back. The case round-trips, ages, and re-enters later. The slot was spent discovering a gap, not resolving the case.

**Why it matters:** the waste is not the review. It is the round trip, and the queue space it consumes twice.

## The idea

**Stop incomplete cases before they enter the queue.**

A deterministic readiness gate checks each case for completeness and baseline compliance at intake. Ready cases route to the right lane. Not-ready cases are returned immediately, with every reason listed, before an analyst is involved.

```mermaid
flowchart LR
    A[Case at intake] --> B{Readiness gate}
    B -->|Ready| C[Route to the right lane]
    B -->|Not ready| D[Return now, every reason listed]

    classDef gate fill:#1f2937,stroke:#111827,color:#ffffff;
    classDef done fill:#bbf7d0,stroke:#15803d,color:#14532d;
    classDef fix fill:#fde68a,stroke:#d97706,color:#1f2937;
    class B gate;
    class C done;
    class D fix;
```

The rules are transparent and auditable by design. No machine learning, no black box, every decision explainable to risk and compliance.

## Two ways cases arrive

**The same problem comes through two doors. The framework handles both.**

|  | Advisor-assisted | Self-guided |
|---|---|---|
| **Who assembles the case** | A trained advisor | The client, alone |
| **Why it fails** | Process slips | Misread requirements |
| **Where the gate sits** | After assembly, before the queue | At the point of entry |
| **What the fix points to** | Coaching and tooling | Form and content design |

## How you would know it works

**Two numbers carry it:**

- **First-time-right rate:** how many cases arrive workable.
- **Avoidable manual touches:** slots spent only to send a case back.

Both are modeled here against synthetic data. Real queue data drops straight in.

## What's inside

- **[Specification](./SPECIFICATION.md)** is the full framework: problem, scope, rule logic, data model, metrics, business case, and rollout.
- **[Advisor-assisted intake](./cases/advisor-assisted-intake.md)** is the human-in-the-loop case.
- **[Self-guided intake](./cases/self-guided-intake.md)** is the self-serve case.

## What this is, and is not

**Is:** a business-analysis and process-design package, with worked decision logic and a measurement framework.

**Is not:** running software. The figures are modeled against synthetic data and labeled as projections, not measured results.

---

## About

Built by Jordan Florence. I work on operational strategy and process optimization: finding where work breaks down, structuring the fix, and making it measurable.

LinkedIn: [jordanflorence](https://www.linkedin.com/in/jordanflorence/)    GitHub: [jordancflorence](https://github.com/jordancflorence) 
