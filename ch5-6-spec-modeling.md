# COMP 361 – Chapters 5+6: The Specification Document and System Modeling

**Readings:** Ch5+6 P1 Specification Document (Vybihal slides, 80 pp.), P2 System Modeling (Sommerville ch. 5, pp. 138–166).

Chapter 2 gathered requirements (elicitation artifacts). This chapter is **phase 2 of the engineering process** (Requirements -> **Specification** -> Design -> Development -> Deployment): turning those artifacts into a formal, signed document. Sommerville ch. 5 supplies the modeling vocabulary (UML) used to draw it.

---

## 1. What the specification document is (Vybihal)

- Converts the **elicitation artifacts** into a set of **formal, complete diagrams**.
- A **non-technical** document that fully describes the project **from the client's point of view, in their language**, but **structured using engineering principles**. It is the **bridge document** between elicitation artifacts and the contract.
- The **client signs off** on the project based on it; it **forms part of the contract**.
- The **design document** (next phase) is based on it.
- **Purpose:** formalize and finalize the user's expectations *before* planning data structures and algorithms.

**Important diagrams it must contain:** Storyboard, Screen layouts, Database and file schemas, Flowcharts of critical areas (**not pseudo-code**), Simple deployment diagram.

### 1.1 Strict formatting standards

- Numbered chapters, numbered subsections, **numbered diagrams** ("Figure x: description").
- Standard report-writing literary style, but concise; favour diagrams to augment paragraphs.
- **Never create a diagram without at least one paragraph explaining each part of it.** Diagrams make sense to the author, rarely to the reader. Add a **diagram key** (legend) where symbols are used.
- Diagram presentation layout: section title -> figure + caption -> one paragraph per component.

### 1.2 Required structure (the exact table of contents)

| Front / back matter | Contents |
|---|---|
| **Title page** | "Specifications", Project name, Date, Author(s) & IDs, Company name |
| **Table of contents** | Chapters with numbered subsections and page numbers |
| **Resources (appendices)** | A: References; B: Photocopies; C: Templates/Forms; D: Digital Source Locations; E: Index. Each is a titled page with a table (e.g. source locations), a list (references, index) or attached pages (photocopies, templates, forms). More appendices may be added |

Body chapters:

1. **Background**
2. **Overview**
3. **Definitions**
4. **Screen Layouts**
5. **Schemas & Queries**
6. **Critical Sections**
7. **Effort Estimation**
8. **Resources** (the appendices above)

---

## 2. Chapter 1 – Background (Why? Who?)

### 1.1 Motivation (context)
- Why is this being developed?
- What problem does it make better or solve?
- Who primarily asked for it, and why?
- Other purpose-related information to keep in mind.

Motivation examples: YouTube = keep users engaged with the platform to consume ads and be entertained; personal homepage = inform the public about the owner; web email client = simplify email management and creation.

### 1.2 Stakeholders (table)

| Type | Name | Coordinates | Success measure |
|---|---|---|---|
| Owner | M. Papadopoulos | phone, email and/or office number | "If it does x, I call the application a success!" |
| Manager | J. Chan | | |
| End user – employee | Gregory (cashier) | | |
| End user – customer | Lenora Wilmington | | |
| Indirect user (does not use it, but is impacted) | Fedora Felegund | | |

Stakeholder types to consider: direct, indirect, manager, owner, technicians. Example: grocery cash register (simplify teller's life, process customers quickly, record sale for manager and accountant) vs. self-checkout (easy for customer, simplify payment/rewards, record sale, easy issue management for staff): same domain, different stakeholders and goals.

---

## 3. Chapter 2 – Overview

### 2.1 Usage
- **Table of how/when each stakeholder uses the app.**
- **Description of how each stakeholder launches/accesses features** (e.g. self-serve register: scan products or keyboard product codes; keyboard also enters discount vouchers).

### 2.2 Project
- **Scheduling:** expected development start and completion dates.
- **Architecture:** **Storyboard diagram** and **Deployment diagram**.

### 3.1 The Storyboard
- A **high-level architectural flowchart of the whole application**, from the **user's point of view**: what the user interacts with on launch and use, highlighting files/databases/network resources accessed or changed.
- A **graph of all possible paths**. **Node** = a UI screen or top-level background process (**not** an object/function). **Arc** = a **labelled trigger** moving the user to the next node.
- Goal: a single, comprehensive view of the entire app **on one page**, from the client's perspective, followed by a paragraph per node.

| Symbol | Meaning |
|---|---|
| Rectangle | UI/GUI screen (assumes processes) |
| Double-headed arrow | Menu (2-way navigation) |
| Single arrow / bold arrow | Link / Secure link |
| Double-bordered rectangle | Begin/End |
| Dashed arrow | Redirect |
| Ellipse | Process without UI |
| Cylinder | DB/File |
| Wavy-bottom box | Document |
| Plain line | Interaction (e.g. with a DB) |

Examples: **website** (Landing -> About / Research / Login / Register; Login & Register touch a Members DB; Login -> Dashboard <-> Project 1, Project 2; Dashboard -> Logout process, which redirects to Landing). **Telescope app** (Welcome -> Menu -> Select Source / About / Take Picture -> Stack Images -> Print, with Images files; Exit).

### 3.2 The Deployment diagram
Goal: show what the program looks like **installed in the client's infrastructure**. Describe things completely, labelled with **much technical detail**.

| Element | Notation / meaning |
|---|---|
| **Device** | 3D box, e.g. `«device» Web Server – PC – Quad Core – 32 GB RAM` |
| **Execution / runtime environment** | Nested box: device, OS, interpreter (e.g. `«execution environment» Windows 11`, Apache) |
| **Component / program** | e.g. "Load Balancing Queue & Core Manager", Python CRUD API |
| **Document / file** | e.g. Cookie, CSV config, ZIP backups |
| **Communication channel** | **Labelled** paths; **ball & socket with direction arrow** for network communication and local API calls (e.g. SQL, TableI) |

Diagrams should be **nested and exhaustive**. Slide exercise: servers drawn without an OS is a problem unless *any* OS truly works (Windows, Mac, Linux, Unix, Minix, Android... are you sure?). Practice question: list the parts of a self-checkout grocery machine and app.

Tools: UMLet, Figma.

---

## 4. Chapter 3 – Definitions

Mostly point lists or tables (except 3.1 and 3.5). **Cannot be left blank or skipped.**

| Section | Contents | Slide example |
|---|---|---|
| **3.1 Branding** | Look and feel, colour palette, logo, a sample image/page combining them, **justification** of choices | Branding for Héma-Québec; look-and-feel questions: how screens transition (slide from side?), experienced user -> dashboard app, novice -> friendly step-by-step dialog |
| **3.2 Required Technologies** | Devices, languages, libraries, runtime environment; compute, computers, servers, network | ABC Inc.: offices = 4 Windows PCs, 1 MacBook Pro (owner, with printer), 1 Windows server on Ethernet; plant = 3 Windows PCs (punch clock, network supervisor, CAD) on the office server; no Internet, LAN intranet in PHP + SQL running one common app "Gem". One app must be compatible with all |
| **3.3 Project & System Constraints** | Budget, equipment, technology limitations | Budget < $50,000; cannot add another server; must run in the browser only |
| **3.4 Client Expectations** | Must-have features, expectations/wants, assumptions, what counts as success/failure, what the project importantly **will and won't** do | |
| **3.5 Impact / Ethics / Performance Statements** | Formal write-up of what was discussed during requirements gathering | |

Note the distinction: **client** = the person you build the program for; **customer** = the people the client serves or sells to.

Tools: design.com logo maker, colors.muz.li, visme colour schemes.

---

## 5. Chapter 4 – Screen Layouts

- **4.1 Screen mockups:** indexed by **Storyboard naming**; **every** Storyboard UI/GUI screen must be defined.
- **4.2 Specialty screens** (not in the Storyboard): welcome/splash, terminate/outro, error/warning screens.
- Drawn following the branding. Purpose: client understands what they will receive and can say what they like/dislike.

**Elements of a mockup:** a realistic drawing in the agreed branding + **numbered bubbles** on parts of the screen + a **description table** (e.g. 1. pressing the circle selects a picture; 2. social icons launch the existing social app; 3. press login after username/password; 4. "forgot password" and "create account" text buttons).

**Section format:** start with a small image of the storyboard as a "table of contents", identifying which boxes are expanded below and listing them as "Mockup x" and why. Then *Mockup 1 – Login* + table, *Mockup 2 – Main Page* + table... Do **not** combine everything into one image.

Tip: build the GUI in the project's language with no "meat"; it is a starting point for developers and the client can play with it. Tools: Balsamiq, Figma.

---

## 6. Chapter 5 – Schemas & Queries

Capture **relationships, rules, structure**. For each data item answer: Purpose (why needed?), Structure (how stored?), Usage (how used?), Rules (restrictions?), Look.

- **5.1 Defining file structures**
  - 5.1.1 **Database diagram**: all files/DBs in one image, ideally one page. Shows table/file name, fields & type info, associations & counts. Legend: M = member, PI = primary key, K = key, F = foreign member. All-in-one version suits small DBs; a simple diagram without field names suits very large DBs, augmented with tables.
  - 5.1.2 **Database table structures**: one table per DB table, columns *Field name, Type, Length, Key/Primary/Sort, Constraints, Legal values* (e.g. First_Name String 30, alpha/space/hyphen; Last_name String 50, primary key, alphabetical; Age Int 3 digits, range 0–120).
  - 5.1.3 **Formatted text files** (CSV, JSON, XML, INI, custom), each in its standard representation, e.g. CSV header `firstName, lastName, age`; XML `<Membership>` with `type` and `constraints` attributes.
  - 5.1.4 **Defined operations**: queries written as **SQL** (formal yet readable for clients and developers, even if not implemented in SQL) plus returned value format. Table columns: *SQL | Motivation* (e.g. `Select * from Membership where age<18` -> search for underage members).
- **5.2 Remote API definitions**: from the user's view "just another type of query". Per area (Membership, Transactions...): **Signature** (`GET membership/list`, `GET membership/search vybihal`), **Description** (syntax, input requirements, error behaviour, expected response time if needed), **Return format** (complete syntax, normally JSON/CGI/DB table, with at least one example).

Tools: UMLet, spreadsheets.

---

## 7. Chapter 6 – Important (Critical) Sections

A **critical section** = a moment in the client interview when they expressed **concern about the correctness of a particular operation**. Typically 0–10 per project. (Examples asked: a live bus-position app; a device synchronously sending two packets Data1={p1,p2}, Data2={p3,p4}.)

- **6.1 Table of contents of critical sections:** *Title | Module | Location | Comments*.
- **6.2 Each critical section:** title; description of importance & purpose; proposed solution in words; **flowchart of the solution (not pseudo-code)**; explanation of the flowchart.

| Way to describe | When |
|---|---|
| **Flowchart** (best) | Traditional, non-UML symbols: start/end, action, if (true/false), loop, document, file, parallel split & merge. Human-readable text, not code expressions. **System flowchart** variant uses swimlane-like boxes per actor/device vs. software |
| **State diagram** (best) | When it is easier to talk about events than flow; may have a main system and a subsystem, each with its own initial state |
| **Query** | When a single structured sentence (SQL) says it; give example output |
| **Interaction diagram** | Many interacting components, multiple timing/validation constraints, function calls and objects; `ref` = reference to a use case, `sd` = embedded sequence diagram. Better suited to the design document |

Practice: flowchart a calculator menu (+, −, ×, ÷, Terminate); state diagram of a handheld calculator. Tools: UMLet, Lucidchart.

---

## 8. Chapter 7 – Effort Estimation

| Subsection | Question it answers |
|---|---|
| **7.1 Optimal workflow graph** | Which development workflow? Ideal (theoretical, unconstrained) shortest path vs. practical shortest path under constraints |
| **7.2 Effort estimation table** | How many hours/days of work? |
| **7.3 Gantt chart** | Calendar-based commitment to the workflow |
| **7.4 Estimated project cost** | Final cost breakdown covering all requirements |

### 8.1 Choosing a workflow
A workflow defines how the engineer interacts with client and developers (an ideology, method, work ethic; often a flowchart). Two kinds: project evolution (now) and how people do their jobs (next semester).

| Method | Behaviour | Trade-off |
|---|---|---|
| **Waterfall** (business) | Requirements -> Spec -> Design -> Build & Test -> Deploy; leave a phase, never return. Signed MOU after requirements, signed contract after spec | Fastest, cheapest; sensitive to mistakes |
| **Prototyping** (SpaceX) | Requirements, then loop: toy spec/design/build/test/deploy -> feedback | Partially working app every phase; "everyone sees your dirty laundry" but lots of feedback |
| **Spiral** (NASA) | Loop all phases; phases never done; stay in a stage until everyone (engineers, managers, stakeholders, client) signs off | Highest quality, fewest failures; slowest, most expensive; precise scheduling hard |

Modifications: **Agile** (schedule slips, specs keep changing -> new working method + buffers/catch-up periods; sprints, each spiralling all waterfall steps, "launch" means internal); **Iterative by module** (build and test one module fully, keep earlier modules unbroken; quality at schedule cost); **Iterative by stakeholder sign-off** (client never likes the result -> regular demos and sign-off per goal, final sign-off before maintenance). **RAD** is not spiral: rapid partial construction -> client-site deployment -> feedback -> repeat.

### 8.2 Activity graph -> table -> cost -> Gantt
- **Activity graph:** node = app module or development phase; arc = hours/days to complete it; acyclic; **longest path = earliest possible completion**. Optimize by maximizing parallelism and shortening arcs. Constraints (number of developers, vacation, sickness, budget, client compute) give the **practical** path, which feeds the Gantt chart. Present both to the client.
  - Slide example (A..L): arc sum = **47 days** of total effort; longest path (my computation) A-B-C-E-F-I-K-L = 2+3+5+3+5+4+2 = **24 days**.
- **Effort table:** *Node | Duration | Pre-conditions* (A–B 2, met all stakeholders; B–C 3, Docker image available; B–F 4, Internet available...). **Total** = person-days to pay for (sum of all arcs); **Optimal** = calendar time with infinite people; **Practical** = calendar time under constraints.
- **Cost table:** *Element | Unit cost | Units | Additional | Subtotal*, e.g. workdays $100/day × 47 = $4,700 + GitHub Pro $500/yr = **$5,200**. Cost uses the arc sum; delivery date uses the path.
- **Delivery date:** practical shortest path + ~**10% padding** + calendar realities (weekends, hours/day, holidays, sick days).
- **Gantt chart:** rows = phases and modules; columns = real dates; flags for milestones (demo, deliverable; penalties may apply); colours per person; shows parallelism and where you are vs. should be.

---

## 9. System Modeling (Sommerville ch. 5)

**System modeling** = building abstract models of a system, each a different view/perspective, usually in **UML**. Models are used in requirements engineering (derive requirements), design (describe system to implementers), and after implementation (document it). Models of the **existing** system clarify what it does and focus discussion on strengths/weaknesses; models of the **new** system explain proposed requirements and design, and with **MDE** can generate code.

A model is an **abstraction** (deliberately leaves out detail, keeps salient characteristics), not an alternative **representation** (e.g. a translation keeps all information).

**Four perspectives:** external (context/environment), interaction (system–environment or between components), structural (organization of the system or its data), behavioral (dynamic behaviour, response to events).

**Three uses of graphical models:**
1. Stimulate/focus discussion: may be incomplete and informal (agile modeling).
2. Document an existing system: need not be complete but must be **correct**.
3. Detailed description to generate an implementation: must be **complete and correct**.

**UML:** 13 diagram types, from 1990s OO modeling; UML 2 finalized 2004; variants like SysML. A survey (Erickson & Siau 2007) found five types capture the essentials: **activity, use case, sequence, class, state** diagrams.

### 9.1 Context models (5.1)

- Decide early on **system boundaries**: what is in the system vs. its environment, what is automated vs. manual or done by other systems, overlaps with existing systems. Limits cost and time.
- Boundaries may be clear (replacing an existing system) or flexible. **Mentcare** example: collect only consultation info and rely on other systems for personal data (avoids duplication, but slower and unusable if those systems are down) vs. collect it too. **iLearn**: users too diverse, so a configurable system whose boundaries are set at deployment.
- Boundary placement is **not value-free**: social/organizational/political factors (keep analysis on one site, avoid a difficult manager, inflate cost so the development division grows).
- **Figure 5.1 Mentcare context:** boxes stereotyped `«system»`: Mentcare connected to Patient record system, Management reporting, Admissions, HC statistics, Prescription, Appointments systems. Context models show *that* other systems exist, **not** the type of relationship (data producer/consumer, shared data, network, co-located).
- So they are used with **business process models**, drawn as UML **activity diagrams**.

**Activity diagram notation (Figure 5.2, involuntary detention):**

| Element | Notation |
|---|---|
| Start / end | Filled circle / filled circle inside a circle |
| Activity | Rounded rectangle |
| Object / system | Rectangle, with stereotype `«system»` |
| Flow | Arrow |
| Coordination | Solid bar: join (all incoming must finish) / fork (outgoing may run in parallel) |
| Decision | Diamond, with **guards** in square brackets |

Flow: Confirm detention decision -> fork: Inform patient of rights, Record detention decision (uses «system» Mentcare) -> join -> decision: [dangerous] Find secure place -> [available] Transfer to secure hospital / [not available] Transfer to police station; [not dangerous] Admit to hospital («system» Admissions) -> fork: Inform social care, Inform next of kin, Update register («system» Mentcare) -> join -> end.

### 9.2 Interaction models (5.2)

Model user interaction (find user requirements), system-to-system interaction (communication problems), component interaction (will the structure deliver performance and dependability?). Two approaches: **use case** modeling (system ↔ external agents) and **sequence diagrams** (between components, may include agents). UML also has communication diagrams (an alternative form of sequence diagrams, not covered).

**Use cases (5.2.1)** (Jacobson, 1990s):
- Each = a **discrete task involving external interaction**; ellipse + **stick-figure actors** (people *or* other systems/hardware).
- Formally lines have **no arrows** (messages go both ways); Figure 5.3 uses arrows informally to show who initiates (Medical receptionist -> *Transfer data* -> Patient record system).
- Add detail via text, a **structured table**, or a sequence diagram. **Figure 5.4 tabular description** fields: **Actors, Description, Data, Stimulus, Response, Comments** (Transfer data: actors Medical receptionist, PRS; data = personal info, treatment summary; stimulus = user command; response = confirmation PRS updated; comment = needs security permissions).
- **Composite** diagrams group related use cases, e.g. Figure 5.5, all "Medical receptionist" use cases: Register patient, Unregister patient, View patient info, Transfer data, Contact patient.
- Sommerville skips include/extend-style sharing constructs: end-users find them hard to understand.

**Sequence diagrams (5.2.2):** interactions in one use case/instance, read top to bottom.

| Element | Notation |
|---|---|
| Actors/objects | Along the top, e.g. `P: PatientInfo`, `D: Mentcare-DB`, `AS: Authorization` |
| Lifeline | Dotted vertical line |
| Activation | Rectangle on lifeline (object is involved in computation) |
| Message | Annotated arrow: call, parameters; dashed arrow for return value |
| Alternatives | `alt` box, conditions in [brackets], options separated by dotted line |
| Object creation | Arrow to a new object box (e.g. `:summary`) |

- **Figure 5.6 View patient info:** receptionist -> `ViewInfo(PID)` on P -> `report(Info, PID, UID)` on D -> `authorize(Info, UID)` on AS -> authorization -> alt [authorization OK] patient info / [authorization fail] Error (no access).
- **Figure 5.7 Transfer data:** login() to PRS actor (direct actor–actor communication); alt [sendInfo] updateInfo() -> updatePRS(UID) -> authorize(TF, UID) -> update(PID) -> update OK -> Message(OK) / [sendSummary] UpdateSummary() -> summarize(UID) -> authorize -> creates `:summary` -> update(PID) -> Message(OK); logout().
- Unless generating code, you **need not include every interaction**; defer implementation-dependent ones (e.g. how the UID is obtained).

### 9.3 Structural models (5.3)

Organization of a system as components and relationships. **Static** (design structure) vs. **dynamic** (organization at runtime, e.g. interacting threads) – not the same. Used for architecture (component, package, deployment diagrams: covered in ch. 6, 17) and here **class diagrams**.

**Class diagrams (5.3.1):** class = general definition of one kind of object; **association** = a link meaning a relationship exists. Early on, objects are real-world things (patient, prescription, doctor). Simplest form: class name in a box, lines for associations.

| Feature | Notation | Book example |
|---|---|---|
| Association | Line, optionally **named** | Fig 5.9: Patient *diagnosed-with* Condition, *referred-to* Consultant, *referred-by* General practitioner, *attends* Consultation; Consultation *prescribes* Medication/Treatment, *involves* Hospital Doctor |
| **Multiplicity** | Number at each end: `1`, `1..4`, `1..*` | Fig 5.8: Patient 1 — 1 Patient record; Patient–Condition 1..* to 1..*; Consultation involves 1..4 Hospital Doctors |
| Full class | Three compartments: **name / attributes** (types optional) **/ operations** | Fig 5.10 Consultation: Doctors, Date, Time, Clinic, Reason, Medication prescribed, Treatment prescribed, Voice notes, Transcript; New(), Prescribe(), RecordNotes(), Transcribe() |

At this level class diagrams resemble **semantic data models** (entities, attributes, relations; Hull & King 1987); UML has no DB-modeling diagram, but entities ≈ classes without operations.

**Generalization (5.3.2):** classify to manage complexity (rodents share characteristics). Put common info in one place so changes are made at the most general level; implemented via inheritance. Notation: **hollow arrowhead pointing to the more general class**. Fig 5.11: Doctor <- Hospital doctor, General practitioner; Hospital doctor <- Consultant, Team doctor; Team doctor <- Trainee doctor, Qualified doctor. Subclasses inherit attributes/operations and add their own: Fig 5.12 Doctor (Name, Phone #, Email; register(), de-register()), Hospital doctor (Staff #, Pager #), General practitioner (Practice, Address).

**Aggregation (5.3.3):** whole composed of parts (a course study pack = book, slides, quizzes, reading). Notation: **diamond at the "whole" end**. Fig 5.13: Patient record ◇— 1 Patient and ◇— 1..* Consultation.

**Data-flow diagrams** (sidebar): functional perspective; each transformation = one function/process; show data flowing through processing steps. UML activity diagrams may represent DFDs.

### 9.4 Behavioral models (5.4)

Dynamic behaviour while executing: response to stimuli, which are **data** (data becomes available) or **events** (may carry data). Business systems are mostly **data-driven**; real-time systems mostly **event-driven**.

**Data-driven modeling (5.4.1):** sequence of actions from input to output (end-to-end); 1970s DFDs. Simple and intuitive, so stakeholders can validate them.
- **Figure 5.14 insulin pump** as activity diagram: Blood sugar sensor -> Get sensor value -> Sensor data -> Compute sugar level -> Blood sugar level -> Calculate insulin delivery -> Insulin requirement -> Calculate pump commands -> Pump control commands -> Control pump -> Insulin pump (activities = rounded rectangles, data = rectangles).
- Alternative: **sequence diagram** with messages only left-to-right. **Figure 5.15 order processing:** Purchase officer -> FillIn() on :Order -> Validate() -> [validation ok] Update(amount) on Budget -> Save() to «datastore» Orders -> Send() to Supplier.
- Sequence models highlight **objects**; DFDs highlight **operations**. Nonexperts find DFDs more intuitive; engineers prefer sequence diagrams.

**Event-driven modeling (5.4.2):** finite states; events cause transitions (valve open -> closed on operator command). Suited to **real-time systems**. UML **state diagrams** (based on Harel's Statecharts, 1987) show states and events, not data flow.

| Element | Notation |
|---|---|
| State | Rounded rectangle, optional `do:` action |
| Transition | Arrow labelled with the stimulus |
| Start / end | Filled circle / bull's-eye |
| **Superstate** | One state on the high-level model, expanded in a separate diagram, to hide detail (state explosion) |

- **Figure 5.16 microwave oven** (half/full power switch, numeric keypad, start/stop button, display): Waiting (display time) -> Half power (set power = 300) / Full power (set power = 600), can switch between -> Timer -> Set time (get number; exit: set time) -> Door closed -> Enabled (display "Ready") / Door open -> Disabled (display "Waiting") -> Start -> Operation (operate oven) -> Door open -> Disabled; Cancel -> Waiting. Usage: select power, input time, press Start; must not operate with door open; buzzer at end.
- **Figure 5.17 Operation superstate:** Checking (check status) -> OK -> Cook (run generator, Time self-loop) -> Timeout -> Done (buzzer on for 5 s) -> Waiting; Turntable fault / Emitter fault -> Alarm (display event) -> Disabled; Door open -> Disabled; Cancel -> Waiting.
- **Figure 5.18** pairs the diagram with a **table of states and stimuli with descriptions** (e.g. Half power = 300 W, display "Half power"; Disabled = light on, "Not ready"; Enabled = light off, "Ready to cook"; stimuli Half power, Full power, Timer, Number, Door open, Door closed, Start, Cancel).

### 9.5 Model-driven engineering and MDA (5.4.3, 5.5)

- **MDE:** models, not programs, are the main outputs; programs are generated automatically, raising abstraction above languages and platforms. Grew from **MDA** (Object Management Group). MDA covers design and implementation; MDE covers the whole process (model-based requirements, processes, testing). Adoption has been slow.
- **MDA's three model levels:**

| Model | Content |
|---|---|
| **CIM** (computation independent) | Domain abstractions ("domain models"); several CIMs for different views (security CIM: asset, role; patient-record CIM: patients, consultations) |
| **PIM** (platform independent) | System operation without implementation reference; UML static structure + event responses |
| **PSM** (platform specific) | PIM transformed per platform; can be layered (middleware-specific, then database-specific) |

- **Figure 5.19:** CIM -> PIM -> PSM -> executable code, each via a **translator** fed by domain guidelines, platform patterns/rules, language patterns. CIM->PIM still needs a **human** (e.g. mapping a security "role" to a hospital "staff member"). PIM->PSM is simpler; tools exist (Koegel 2012). **Figure 5.20:** one PIM -> J2EE translator -> J2EE model -> Java code generator -> Java program, and .NET translator -> .NET model -> C# generator -> C# program.
- Benefits: fewer errors, faster design/implementation, reusable platform-independent models, re-hosting by writing a new translator.
- **Executable UML (xUML):** a UML 2 subset with defined meanings plus operation semantics, enabling full compilation (Mellor & Balcer 2002).
- **Why MDA is not mainstream:** tool support is partial and environment-specific (companies avoid building/depending on niche tools); discussion abstractions ≠ implementation abstractions (reuse of off-the-shelf systems may be better); implementation isn't the main problem (requirements, security, dependability, legacy integration, testing are); platform independence pays off only for large long-lifetime systems; agile methods diverted attention and contradict up-front modeling.
- Successes: **systems products** (hardware + software, long lifetime, well-understood domains like automotive and air traffic control). Hutchinson et al. 2012: mixed results, but most report higher productivity, lower maintenance cost, more reuse. Ambler: parts of MDA usable in agile but code generation impractical; Motorola succeeded with agile + code generation (Zhang & Patel 2011).

### 9.6 Key points and exercises (end of chapter)

Key points: models abstract; complementary models for context, interaction, structure, behaviour; context models define boundaries; use cases + sequence diagrams describe interactions; class diagrams = static structure; behaviour from data or events; activity diagrams model data processing; state diagrams model reaction to events; MDE transforms models to code.

Exercises 5.1–5.10 include: how a context model prevents **scope creep**; activity diagram for planning a party; Mentcare use cases for a doctor; sequence diagram for course registration with limited places; class model of email messages/mailboxes; ATM cash withdrawal as activity + sequence diagram; state diagrams for washing machine, DVD player, phone camera; obstacles to fully automated model translation.

---

## 10. How the two readings connect

| Spec section (Vybihal) | Sommerville model that fits |
|---|---|
| 2.2 Storyboard | User-view navigation graph; closest to an activity/state view of screens |
| 2.2 Deployment diagram | UML deployment diagram (Sommerville defers to ch. 6/17) |
| 1.2 Stakeholders / 2.1 Usage | Context model (boundaries, external systems) + use cases per actor |
| 5 Schemas & Queries | Class diagrams as semantic data models (entities, multiplicities, aggregation) |
| 6 Critical Sections | Flowcharts/activity diagrams (data-driven), state diagrams (event-driven), sequence/interaction diagrams |
| 7 Effort Estimation | Not modeling; project management (Ch4) |

---

## 11. Applying it to the project / A2

- **Follow the exact skeleton:** title page (project, date, authors + IDs, company), TOC, chapters 1–7, Resources appendices A–E. Number every chapter, subsection and figure. No section of Chapter 3 (Definitions) may be blank.
- **Every diagram gets a caption and a paragraph per part**, plus a key if it uses symbols. This is the most explicit grading-style rule in the slides.
- **Storyboard first, on one page**, using the legend above; then name mockups after storyboard nodes, covering every UI node plus splash, outro and error screens, each with numbered bubbles and a description table.
- **Deployment diagram:** nest device -> OS/runtime -> program; label hardware specs, OS, and communication paths (ball & socket); don't leave the OS unspecified.
- **Data:** a DB diagram with multiplicities (Sommerville's `1`, `1..*` notation works), a table per DB table with constraints and legal values, file formats in their standard form, SQL for every operation, and API signature/description/return example per area.
- **Critical sections:** pick the operations the client worried about; use a flowchart (not pseudo-code) or a state diagram (event-heavy features, like the microwave), explained in words.
- **Use cases and sequence diagrams** from Sommerville are the natural way to back the Usage section and any multi-component critical section; use `alt` boxes for success/failure paths and tabular use-case descriptions (Actors, Description, Data, Stimulus, Response, Comments).
- **Effort:** choose a workflow and justify it, draw the activity graph, give total vs. optimal vs. practical durations, a cost table, ~10% padding, and a Gantt chart with milestone flags.
