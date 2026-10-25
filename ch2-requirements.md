# COMP 361 – Chapter 2: Requirements, Use Cases, Wireframes

**Readings:** Ch2 P1 Requirements (Sommerville ch.4), P2 Simple Use Case (Benabderrezak), P3 Use Cases and Templates (Kulak & Guiney, *Use Cases: Requirements in Context* ch.2), P4 Wireframes (freeCodeCamp), two example wireframe images.

Ties back to Lecture 1: the client is the Oracle, and the story-to-install pipeline starts with **story -> requirements**. This chapter is how you turn the story into something a team can build from.

---

## 1. Requirements (Sommerville ch. 4)

**Requirement** = a description of a service the system should provide, or a constraint on its operation. Requirements engineering (RE) = finding, analyzing, documenting, and checking them.

### Two levels of detail
| Level | Written for | Style |
|---|---|---|
| **User requirements** | client managers, end users, architects | natural language + diagrams, high level |
| **System requirements** | developers, testers, engineers | detailed, precise, may be part of the contract |

Example (Mentcare, a mental-health clinic system): user req "generate monthly report of drug costs per clinic" expands into 5 system reqs (when generated, format, per-clinic breakdown, dose units, access control).

### Functional vs non-functional
- **Functional**: what the system does. Services, reactions to inputs, behaviour. Can also say what it must *not* do.
- **Non-functional**: constraints on the system as a whole. Timing, reliability, security, standards. Often *more* critical than any single functional req: a plane that misses its reliability target is not certified.
- Non-functional reqs come from three sources: **product** (performance, usability, dependability, security), **organizational** (development process, operational rules, environment), **external** (regulatory, legislative, ethical).
- Write non-functional reqs **quantitatively** so they are testable. "Easy to use" is a goal, not a requirement. "Staff can use all functions after 2 hours training and make under 2 errors/hour" is a requirement. Figure 4.5 gives metrics: speed (transactions/sec), reliability (MTTF), robustness (restart time), portability (% target-dependent code), etc.

### The RE process (spiral, Fig 4.6)
Three interleaved activities, repeated at increasing detail: **elicitation** -> **specification** -> **validation**. The output is the requirements document.

### Elicitation (4.3)
Why it is hard: stakeholders don't know what they want, use domain jargon, conflict with each other, have political motives, and the environment keeps changing.

Elicitation cycle: discover -> classify/organize -> prioritize/negotiate -> document -> repeat.

Two fundamental techniques:
1. **Interviewing** (closed = fixed questions, open = exploratory; in practice mix both). Don't say "tell me what you want." Use a springboard question or prototype. Interviews miss organizational/political issues and things experts think are too obvious to mention.
2. **Ethnography** (observe people actually working). Finds requirements from how people *really* work rather than how the process manual says they work, and from cooperation between people. Bad at innovation.

**Stories and scenarios**: people relate to concrete examples. A *story* is narrative and high level (Fig 4.9: Jack's fishing class project). A *scenario* is structured: initial assumption, normal flow, what can go wrong, other concurrent activities, end state (Fig 4.10: uploading photos).

### Specification (4.4)
Notations: natural language sentences, structured natural language (templates/forms), graphical (UML use case, sequence), mathematical (formal, rarely accepted by customers).

Guidelines for natural language:
1. Fixed format, one or two sentences per requirement.
2. **"shall"** = mandatory, **"should"** = desirable.
3. Highlight key parts.
4. Avoid jargon.
5. Attach a **rationale** and source to each requirement.

Structured spec template (Fig 4.13, insulin pump): function, description, inputs, source, outputs, destination, action, requires, precondition, postcondition, side effects. Use tables for conditional logic (Fig 4.14).

**Use cases** (4.4.3): actors as stick figures, interactions as named ellipses. Sommerville's own view: too fine-grained for early RE, better for design. (The next two readings disagree. Know both positions.)

**The requirements document / SRS** (4.4.4): IEEE-based structure in Fig 4.17: preface, introduction, glossary, user reqs definition, system architecture, system reqs spec, system models, system evolution, appendices, index. Agile teams replace this with user stories on cards plus a short document on business and dependability reqs.

### Validation (4.5)
Checks: **validity**, **consistency**, **completeness**, **realism**, **verifiability**. Techniques: reviews, prototyping, test-case generation (if you can't write a test for it, it is a bad requirement). Fixing a requirements error late is far more expensive than fixing a code error.

### Change (4.6)
Requirements always change: wicked problems, environment changes, payers vs users differ, stakeholder priorities shift. Need **requirements management**: unique IDs, a change process (analyse problem -> cost the change -> implement), traceability, tool support (spreadsheets are fine for small projects). Enduring reqs (core business) vs volatile reqs (supporting activities).

---

## 2. Use case diagrams: the short version (Benabderrezak)

Behavioral UML diagram, external user's view.

Elements:
1. **System boundary**: a box. Inside = the system.
2. **Actors**: stick figures. People, other systems, devices.
3. **Use cases**: ovals. Actions the system performs for actors.
4. **Relationships**:
   - **Association**: solid line actor to use case.
   - **Include**: dotted arrow to a use case that is *always* performed as part of another (Borrow Book includes Check Availability).
   - **Extend**: dotted arrow to a use case that *optionally* adds behaviour.

Steps: define boundary -> identify actors -> identify use cases -> draw associations -> add include/extend if needed.

---

## 3. Use cases in depth (Kulak & Guiney ch. 2)

### The argument
Traditional requirements tools fail users:
- **Requirements lists** ("the system shall...") are itemized, easy to duplicate or contradict, no cohesive view. Drop them.
- **DFDs** (data-flow diagrams) confuse users; the system/user line is fuzzy. Drop them from requirements (still OK in design).
- **ERDs** (entity-relationship diagrams) are for database design, not users. Drop them from requirements.
- **Prototypes** are loved by users but they get lost in button colours, think the prototype *is* the system, and the team is tempted to ship prototype code. Use them to *support* use cases, not replace them.

Core idea: users see the system as a **black box**. They care about what goes in and what comes out. That is the **what**. Everything else is the **how** (design). Use cases show the what exclusively. Pirsig's motorcycle: the *classic* view is subsystems (developers), the *romantic* view is what you can do with it (users). Use cases take the romantic view.

### History
Ivar Jacobson, Ericsson, 1992 (Objectory). Merged with Booch and Rumbaugh ("Three Amigos") into UML, standardized by OMG in 1997. UML is a *notation*, not a methodology. Nine diagrams: use case, sequence, collaboration, statechart, activity, class, object, component, deployment. Use case diagram comes first; the others follow from it.

### Goals of a good use case
1. Each interaction provides **value to an actor**.
2. **No implementation-specific language**: no specific people (roles instead), no departments, no UI widgets, no IF-THEN-ELSE, no pseudocode. Table 2.1: "The clerk pushes the OK button" -> "The clerk signifies completion of the transaction."
3. **User-appropriate detail**: start general, get detailed later.
4. **User-appropriate volume**: Jacobson said even a huge system has 70-80 use cases; most have 20-50. Few use cases forces real abstraction. (Number of *scenarios* can be large.)

### Diagram rules
- **Actors** initiate; use cases never do. Actors can be people, systems, or a time/event ("7 PM last workday of month"). Show a secondary actor if its behaviour affects the system's response.
- **Role names** on the arrow ends when the relationship needs more than "interacts" (e.g. `+observer`).
- **Generalization**: superactor/subactor (Service Rep <- Customer Service Rep, Field Service Rep). Use when subactors share interactions or descriptions.
- **Include**: reuse. Think of it as a function call.
- **Extend**: optional special case. Extending use case cannot exist without the extended one.
- Be sparing with include/extend; they are for simplifying use cases, not for designing the solution.
- **Stereotypes** like `<<mission-critical>>` tag use cases that must meet extra criteria.

### The use case template (Fig 2.14)
Standardizing on *a* template matters more than which one. Fewer boxes is better. Author and Date go at the *bottom*; the most important info goes at the top.

| Field | Meaning |
|---|---|
| Use Case Name | unique English identifier, not a number |
| Iteration | Facade / Filled / Focused / Finished (the four stages of refinement) |
| Summary | 1-2 sentences, don't repeat the steps |
| Basic Course of Events | the "simple correct path". Actor acts, system responds, back and forth. The most *common* path, not the simplest |
| Alternative Paths | less common but still correct paths (pay by credit card instead of PO). Each says which step it branches from |
| Exception Paths | what happens when something goes *wrong* (invalid date, record not found) |
| Extension Points | where extending use cases hook in |
| Triggers | why/when an actor enters this use case |
| Assumptions | things you assume true but haven't verified. Critical for project managers |
| Preconditions | what must be in place before (a ledger exists) |
| Postconditions | what is true after, regardless of which path (transaction posted) |
| Related Business Rules | reference, don't copy |
| Author, Date | date of each iteration |

### Scenarios
Three conflicting definitions in the industry:
1. Alternative path (redundant with the template).
2. **Instance of a use case with specific data** (the authors' choice: "Jenny Carmela calls July 5 for a fitting on Aug 22"). Proves the use case handles a real case; feeds directly into testing.
3. Synonym for use case.

Exception vs alternative: alternative = correct but rare; exception = an error occurred.

### Where else use cases apply
Inquiry-only systems (data warehouses), RFPs, package evaluation (gap analysis), non-OO systems.

---

## 4. Wireframes (freeCodeCamp, Adrian Twarog)

A wireframe is a low-fidelity sketch of layout and navigation. Pencil and paper is enough. It is living documentation for you and the client, done *before* any code.

Conventions: box with an X = image, horizontal lines = text, circle with L = logo, hatched box = heading.

Six steps:
1. **Sitemap**: boxes for pages, lines for hierarchy. Skip for tiny sites.
2. **Homepage wireframe**: menu, hero/slider, about, sponsors, footer (contact form, contact info, logo).
3. **Markup**: red labels saying what each block *represents* ("Intro Title"), not the real content. Helps devs, clients, managers read it.
4. **Reusable components**: copy header/footer to other pages. Figma components update everywhere.
5. **Features and Contact pages**: reuse components, add map, form, phone, email.
6. **Mobile responsive version**: columns collapse, images shrink, some sections get taller. Annotate which desktop section maps to which mobile section.

Both example images show exactly this: annotated boxes with red markup, a desktop and a mobile column side by side.

---

## 5. How this fits the project

- Your team's story from the client becomes **user requirements**, then **use cases** (20-50 max, user language only, one template for the team), then **wireframes** for the screens.
- Write non-functional requirements as numbers you can test.
- Keep a **rationale** and an **assumptions** list. Assumptions are where projects die.
- Scenarios with concrete data double as your acceptance tests later.
