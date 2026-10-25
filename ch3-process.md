# COMP 361 – Chapter 3: The Software Process

**Readings:** Ch3 P1 The Software Process (Sommerville ch.2), P2 Spiral Method Summary, P3 Spiral Model (GeeksforGeeks), P4 Methods in Game Development (GDLC).

Lecture 1 was *ad hoc*: no process, land on your feet. This chapter is the opposite: named processes you choose deliberately. Chapter 2 (requirements) is the first activity inside every one of them.

---

## 1. What a process is (Sommerville ch. 2)

A **software process** = a set of related activities that produces a software system. No universal one; it depends on the software type, the customer, and the team. Every process includes four fundamental activities:

1. **Specification** (define functionality and constraints)
2. **Development** (design and implement)
3. **Validation** (check it does what the customer wants)
4. **Evolution** (change it as needs change)

A process description also says: **products** (deliverables), **roles** (who), and **pre/postconditions** (what must hold before and after an activity).

**Plan-driven** = plan everything in advance, measure against the plan. **Agile** = plan incrementally as you go. Most real projects balance both.

### 2.1 Three general process models

| Model | Idea | Use when |
|---|---|---|
| **Waterfall** | Sequential phases, each signed off before the next: requirements -> design -> implementation + unit test -> integration + system test -> operation + maintenance | Embedded systems (hardware is inflexible), safety-critical systems (need full spec for analysis), large multi-company systems (need complete specs for independent work) |
| **Incremental** | Interleave spec, dev, validation. Build a version, get feedback, build the next. Early increments carry the most important functionality | Business systems, software products, anything where requirements will change |
| **Integration & configuration** (reuse) | Search for existing components/systems, refine requirements to fit them, configure or adapt, integrate | When reusable components exist. Cheaper and faster, but you compromise on requirements and lose control of component evolution |

Waterfall's real problem: phases actually overlap and feed back. Freezing requirements early means problems get ignored or programmed around.

Incremental's advantages: cheaper to change, easier customer feedback, early delivery of useful software. Its management problems: process is invisible (no regular documents), structure degrades as increments pile on (fix by refactoring). Large long-lived systems still need an architecture planned up front.

Reusable component types: standalone application systems, component collections (e.g. Spring framework packages), web services.

**RUP** (Rational Unified Process) is a "universal" hybrid: inception, elaboration, construction, transition. Used at IBM, not widely adopted.

**Boehm's spiral** (sidebar): risk-driven, incremental. Each loop is a phase (feasibility, then requirements, then design...). Combines change avoidance with change tolerance. See section 3 below.

### 2.2 Process activities in detail

**Specification / RE** (2.2.1): feasibility study first. Then elicitation & analysis -> specification -> validation, producing the requirements document. Two levels: user requirements and system requirements. (This is Chapter 2 of the course.)

**Design & implementation** (2.2.2): design inputs are platform info, requirements, data descriptions. Four interdependent design activities: **architectural** (structure, components, distribution), **database**, **interface** (unambiguous contracts between components so they can be built separately), **component selection and design**. Outputs: architecture, DB design, interface specs, component descriptions. Design rework is inevitable. Programming is individual; there is no fixed process. **Testing finds defects; debugging locates and fixes them.** They are different activities.

**Validation / V&V** (2.2.3): show the system conforms to spec *and* meets customer expectations. Three stages of testing:
1. **Component testing** by the developers (JUnit etc.)
2. **System testing** after integration: finds interaction errors, checks functional and non-functional reqs
3. **Customer testing** with real data (acceptance testing; "beta testing" for products)

Plan-driven projects use test plans derived from each spec level. Fig 2.7 is the **V-model**: each development stage on the left has a matching test on the right.

**Evolution** (2.2.4): the split between development and maintenance is artificial. Software engineering is an evolutionary process: define requirements -> assess existing systems -> propose changes -> modify -> new system -> repeat.

### 2.3 Coping with change

Change is inevitable and costs **rework**. Two strategies:
- **Change anticipation**: predict changes before they cost you. Main tool: **prototyping**.
- **Change tolerance**: design the process so changes are cheap. Main tool: **incremental delivery** (and refactoring).

**Prototyping** (2.3.1): quick early version to check requirements and design feasibility. Process: set objectives -> define what to include/leave out -> build -> evaluate. Leave out error handling and non-functional requirements unless they are the point. Only sensible way to design a UI. Pitfalls: users may not use the prototype the way they'd use the real system; not enough training time; a slow prototype changes user behaviour.

**Incremental delivery** (2.3.2): deliver increments to the customer's *real* environment, highest-priority services first. Requirements for the current increment are frozen; later ones can still change. Advantages: early value, realistic feedback, most-used parts get the most testing. Problems: replacing an existing system (users want everything at once), shared basic facilities are hard to identify early, conflicts with fixed-spec contracts (governments).

### 2.4 Process improvement

Two philosophies: **process maturity** (plan-driven, add good practice, measure) vs **agile** (cut overhead, deliver fast). Improvement cycle: **measure -> analyze -> change**.

**Capability Maturity Model** (SEI, Humphrey 1988), five levels:
1. Initial
2. Managed (documented plans, resource management)
3. Defined (organization-wide standard processes, tailored per project)
4. Quantitatively managed (statistical control)
5. Optimizing (continuous data-driven improvement)

Only large companies bother; the overhead is too high for small teams and hard to apply to agile.

---

## 2. The Spiral Model (Boehm 1986/1988)

Risk-driven. Combines waterfall's systematic steps with iterative loops. Called a **meta-model** because each loop can borrow from waterfall, incremental, or prototyping depending on the risk profile.

Each loop has four quadrants:
1. **Objective setting / planning**: goals, functional and non-functional requirements, alternatives, constraints.
2. **Risk analysis**: identify cost/schedule/performance/tech risks, pick the best alternative, build prototypes to retire high risks early.
3. **Engineering (development & test)**: build and test what this loop planned.
4. **Evaluation / review**: stakeholders review, feedback collected, next loop planned.

Geometry: **radius = cost so far**, **angle = progress within the current phase**.

| Pros | Cons |
|---|---|
| Strong risk management | Complex; needs people who can actually analyse risk |
| Handles changing requirements | Expensive; overkill for small projects |
| Early user feedback | Number of loops unknown, so schedule is hard to estimate |
| Suits large, uncertain projects | Frequent reviews take time |

E-commerce example across loops: basic listing/cart/payment prototype -> secure payments, registration, cart refined -> order tracking, reviews, search plus performance/security testing -> deploy and monitor.

Quiz answer: the spiral is for **risk handling in large, complex projects**.

---

## 3. Game Development Life Cycle (GDLC)

Adapts the software process for creative, multidisciplinary teams (programmers, artists, audio, writers).

1. **Initiation / idea**: concept, genre, audience, vision.
2. **Pre-production**: scope, first prototypes, scripts, engine choice.
3. **Production**: mechanics, art, audio, levels.
4. **Testing**: **Alpha** (internal, bugs) then **Beta** (external, UX and server stability).
5. **Release**: publish to PC / console / mobile.
6. **Post-release**: patches, updates, DLC.

Maps onto Sommerville: pre-production ≈ specification + prototyping, production ≈ development, alpha/beta ≈ component/system/customer testing, post-release ≈ evolution.

---

## 4. Choosing for the project

- Requirements *will* change, so pick something incremental. A lightweight spiral (plan -> risk -> build -> review each sprint) fits a term project: the risk quadrant forces the team to prototype the scary parts (unfamiliar tech, the hardest feature) first.
- Deliver highest-priority use cases first so the client sees value early and the most-used code gets tested most.
- Prototype the UI (wireframes from Chapter 2 are the paper version of this).
- Keep testing staged: unit tests as you go, integration when combining, client demo at the end of each increment.
