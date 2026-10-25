# COMP 361 – Chapters 5+6: Design, Architecture, and Report Writing

**Readings:** Ch5+6 P3 Design Document (Vybihal slides, "Design: The Software Engineering Process, Phase 3", 119 slides), P4 Architectural Design (Sommerville ch.6, pp. 167-194), P5 How to Write Reports 1 (Univ. of Newcastle Learning Development guide), P6 How to Write Reports 2 (Writing Support Services "Report Writing Guidelines" + 17-point revision checklist).

Pipeline position (slide 1): Requirements -> Specification -> **Design** -> Development -> Deployment. Chapter 2 focused on the client's needs; design is the switch to planning the **engineering**: the program itself *and* the development strategy for building it. Slogan: **"capture the big ideas, agile the details"**: you can't plan everything, but planning the big ideas controls the chaos, including how the team will work together "without killing each other" (a good team is like a family: intentionality, forgiveness, tolerance; professionalism and quality are assumed).

---

## 1. The Design Document (Vybihal)

### 1.1 What goes into a design
- **Software design**: domain model and design patterns; critical sections and UML; performance areas; development-cycle selection and setup.
- **Software construction**: dev tools, development environment, staging environment.
- **Quality assurance**: testing procedures, performance, user experience.
- **Deployment procedures.**

How-to steps (slide 5), four rows:
1. **From specifications:** storyboard, mockups, schemas, deployment, expectations, Gantt.
2. **Set up workflow:** incremental / iterative; waterfall / spiral / prototype.
3. **The software:** domain model, critical sections, schema -> databases/files, staging configuration, deployment configuration.
4. **Reflection:** quality assurance, performance, user experience, risk analysis.

### 1.2 Required structure (slide 6 outline + detailed slides)

| # | Section | Contents |
|---|---|---|
| – | **Title page** | "Design Document", project name, date, author(s), company name |
| – | **Contents** | Numbered sections with page numbers |
| 1 | **Definitions** | 1.1 Development cycle, 1.2 Engineering procedures, 1.3 Engineering constraints & assumptions, 1.4 Engineering success & failure statements |
| 2 | **Solution Architecture** (mostly deployment diagrams) | 2.1 Development env., 2.2 Staging env., 2.3 Deployment env., 2.4 Evolution env. |
| 3 | **Software Design** (domain modelling) | 3.1 Storyboard & critical sections (v2), 3.2 Code structure identification, 3.3 UML domain model, 3.4 Module breakdown |
| 4 | **Database, File, and API Definitions** | 4.1 DB diagrams, 4.2 DB schemas, 4.3 Files, 4.4 APIs. Complete schemas & SQL signatures **grouped by storyboard section** |
| 5 | **Critical Sections** | 5.1 Risk analysis, 5.2 Mitigation models (algorithms via UML diagrams and SQL) |
| 6 | **Appendix** | Optional: other documentation, references/links, standards |

Note: the overview slide words section 2 as Deployment / Development / Delivery environments (delivery = staging, migration (installation, backups, handoff), maintenance & support) and section 3 as storyboard, code structure (design patterns, algorithms, data structures, files/DBs, I/O), **type of program (OO vs modular)**, UML domain model. The detailed slides use the 2.1-2.4 and 3.1-3.4 numbering in the table. Same content, different grouping. Section 3 explicitly has **no class diagram**. Order is top (global view) down (detailed developer view): revisit, reflect, programmer's point of view.

### 1.3 Section 1: Definitions

**1.1 Development cycle** answers two questions:
- *How is the software built?* **Incremental** = modules built one after another, each fully (all features + QA) before the next. **Iterative** = all modules exist from the start; each loop adds one more feature to every module (M1F1, M2F1, M3F1 + QA; then F2s + QA; ...).
- *How does the team work?* Standard, Paired, Spiral, or Mixed/Custom.

Compatibility of project workflows with build style:
| Workflow | Build style | Flow |
|---|---|---|
| **Waterfall** | Either, but no going back after sign-off; can build in one go | Assign unit -> program -> integrate into codebase -> QA application -> customer assessment -> sign-off and next unit, or fix |
| **Spiral** | Iterative, build can repeat indefinitely | Assign unit -> program -> QA unit -> customer assessment -> risk & performance assessment -> integrate -> QA codebase -> repeat unit (poor results), next unit, or redo an older decision |
| **Prototype** | Incremental, client included in the QA step | Define first increment of the complete app -> program -> QA -> run on customer's machines with the customer -> evaluate success -> repeat increment or next increment |

Team workflows:
| Type | How it works |
|---|---|
| **Standard** | Lead writes and assigns work -> developer codes against spec + design doc -> lead verifies code against spec/design, decides "done, take a new task" or "not complete" |
| **Paired** | Same flow as standard, plus training of juniors; senior assigns subtasks to junior; group development. Team = lead + N pairs |
| **Spiral** | (1) Risk analysis and step selection with everyone, (2) detailed increment assignment written, (3) work assigned, (4) client included at review, usually repeat 1-4 until satisfied, (5) if satisfied, evolve (pick next thing), back to 1 |
| **Mixed** | Combine any of the above, add your own elements. Get business done -> standard; risky -> spiral; culture + large teams -> paired |

Practice examples in the slides: Canadarm feature for the Canadian Space Agency, 7 devs (1 lead Montreal, 3 Toronto, 3 Hong Kong); bridge, rocket, cooking-timer app, MMO upgrade.

**1.2 Engineering procedures** = the standards you follow while developing: daily scrum, regular or scheduled client demos, a backup at each successful phase, tools (repo, IDE, AWS, Zoom, Slack), common directory structure, "you push/merge, you fix the repo (even other people's code)", morning announcements, assignments with due dates, Gantt progress meetings.
- Example 1 (per increment): *Start* (meet, assign work, due dates on Gantt) -> *Daily* (9 AM scrum, 10 AM everyone pulls, programming + unit testing, 4 PM everyone pushes and resolves conflicts) -> *QA* (testing, performance, UX after the feature is done; pass = next increment, fail = fix) -> *End* (meet on state of increment). Discussion question: what do programmers do during QA?
- Example 2 (weekly): Monday plan with a Friday deliverable per person; 9 AM scrum; pull in the morning; push to your **branch** at end of day; when deliverable done, merge to main and debug main; Friday PM review of the week and workflow; at a milestone, demo to client and record issues.

**1.3 Constraints and assumptions.** List *only things that are concerns*.
- **Constraints** limit development choices: languages, tools, hardware, technology, funding, schedule, people.
- **Assumptions** are things obvious to you that would impact the project if they happened (expectations of the client, suppliers, programmers).
- Format: one table each, columns **Item | Constraint (or Assumption) | Expected Impact | Workaround Plan**.
- Examples: company vacation in July mid-project; key people busy until February; funding $10K of $15K needed; team must learn backend DB programming. Assumptions: client available for the spiral; resources available by January 21.

**1.4 Success and failure statements.** Success = goals the dev team wants to meet (Gantt goals, improvement over the last project). Failure = "if X happens, you would not be happy with yourself, your team, or the project". Format: one table each, **Item | Success (or Failure) | Expected Impact | Discussion & Alternatives**. Examples: success = all delivery dates met, not over budget, happy client; failure = delays from poor scheduling/monitoring, failed team dynamics, poor documentation or repo state. Used during regular project reviews as **harbingers**: when one starts appearing, plan how to deal with it.

### 1.4 Section 2: Solution Architecture (deployment diagrams)

**Configuration** = all adjustable elements of a run-time environment (installed hardware, OS services, tools, libraries, config files).

Development (n iterations, feedback loop) -> Staging -> Deployment (once):
| Environment | Contents |
|---|---|
| **Development** | Dev server, workstations, repo, IDE, libraries, scrum/cycle, effort/Gantt, domain model, QA |
| **Staging** | 3rd-party infrastructure matching client's run-time env, test database, current pre-release version, client's sandbox |
| **Deployment** | Client's infrastructure; archive & retire previous software and DB; migrate old DB; release to public |

**2.1 Development environment.** Standardize it: different OSes/IDEs complicate merging. Employers either (A) buy everyone the same computer, (B) have everyone SSH into one server, or (C) use **Docker**. Deliver: deployment diagram (configuration), a list (completeness), procedures (expected way to work). List format: **Item | Name | Version | Description/Environment | Quantity**, followed by **Installation Procedure** and **Expected Workflow** (which encodes iterative/incremental, waterfall/spiral/prototype, paired/classical/spiral programming).

**2.2 Staging environment.** A fake deployment environment, because deploying disturbs the client, you deploy often for integration/compatibility testing, and you need a safe place to demo. Loop: integration testing -> QA testing -> demo with client -> feedback -> improve. Types (view -> play -> use):
1. Developer's location: client visits, might touch it.
2. Developer's laptop: you visit the client.
3. Client's laptop: install, show, leave it for a few days.
4. Staging server the client can access: they "play" for days, data deleted after.
5. The deployment environment itself: client starts real use, data concerns.

Caveat: staging is never identical to deployment, so deployment-specific bugs remain; plan testing after deployment. Sommerville quote: many security problems come from misconfiguration at deployment, so design in facilities that simplify deployment and check for configuration errors. **Mismatch areas**: system (OS, DLLs/OS components, security settings, hardware, load) and communication (client uses the program in unexpected ways).

Best practice: identify client's run-time configuration + the app's configuration needs -> identify the differences -> **staging server = merge of client's run-time and app requirements** -> **script** installs code on client's server and applies the differences. In the Gantt chart, QA (including configuration testing and a client demo) happens at staging at each milestone.

**2.3 Deployment environment.**
- Option 1: program must run on client's infrastructure unchanged -> one deployment diagram.
- Option 2: infrastructure must be upgraded -> two diagrams (current, upgraded) + ordered step-by-step upgrade plan.
- Plus the installation procedure, including decommissioning old software and migrating databases.

Configuration steps (scripts standardize and record exactly what happened): *Part 1*: (1) identify software config requirements, (2) match staging to client run-time, (3) tools to manage configuration. *Part 2*: (4) tool to install the app, (5) tool for data migration.

First-time install & migration procedure: schedule with client (everyone stops using computers) -> archive data and software to retire (plus a script to quickly reactivate the old app in the worst case) -> install new DB and verify via command line -> migrate archived data (scripted, verified) -> configure client machines (script + checklist) -> install app on all machines, verify with client -> everyone resumes, you hang around -> set up a support line, be ready to return in month 1.

Basic install procedure: Step 1 manual (configure OS, install non-downloadable apps, archive old system, copy app to temp dir). Step 2 script (download/install 3rd-party apps, configure OS: mkdir, cp, VER/ENVIRONMENT vars, cron jobs; install or build DB; merge archived data; run DB validation scripts; install launch script/shortcut; clean up). Step 3 run it yourself (built-in unit tests). Step 4 run with client. Step 5 open to everyone, stay around.

Data migration example: old Customer(custID, name, email, address) + Orders(orderID, itemDescription, quantity, unitPrice) -> new Customer(custID, name, email, street, city, postal, country) + Orders(orderID, itemID, quantity, subtotal) + Items(itemID, unitPrice, quantityInStock, description). Question: by hand or by script?

**Support and maintenance.** Month 1: on-site presence + hotline. After: hotline + online ticketing (can be integrated into the app). Maintenance = (A) complaints after completion (short window, e.g. a month; price it in and put it in the Gantt), (B) regular updates under a service contract, (C) end of support; much later without a contract = new contract, slower response, priced issue filing. Example plan: ticket system (call/email/web; client can track; dates registered/assigned/review/completed; names of client, developer, reviewer; devs and manager can assign/edit/log), a process for reporting back (email, demo), and an update method (physical or automatic).

**2.4 Evolution environment.** Lifecycle: initial development -> **evolution** (client keeps paying for new capabilities) -> **servicing** (fixes only) -> **phaseout**. Evolution flow: change identified -> change proposal (spec, effort, Gantt, cost) -> development -> install update. Update process: change request -> **impact analysis** (fault repair, side-effect mitigation, platform adaptation, other enhancements) -> **release planning** (when to install, what to shut down, plan B) -> development -> install. Evolution is costlier than the first build (people forget code, new structures clash with old, new programmers may not know the language). Legacy assessment grid: business value vs system quality (A high value/low quality, B high/high, C low/low, D low/high); question posed: which to retire.

### 1.5 Section 3: Software Design

**3.1 Storyboard v2 & critical sections.** Revisit the client storyboard after analysing deployment/development/maintenance. Consider adding modules: import/export (migration, demos), backup, security ("bad guy" concerns from the deployment diagram), ticketing, install/update scripts. Three purposes: tell devs the macro structure; revisit and modify given the deploy/develop/stage diagrams; add **developer** critical sections to the client's. Table: **Item | Title | Description | Location (module/screen/phase) | Owner (client/developer)**. Goal: reformat the spec for developers without losing the client's perspective.

**3.2 Code structure identification.** Technologies, design patterns, data structures, presented as three tables, each with its own explanatory text:
1. **System-wide structures** (can't be assigned to one module).
2. **Module-based structures** (grouped by module/class).
3. **Procedure-based structures** (grouped by *project* phase: deployment, evolution, development...).

Columns (variable): item, grouping (system/module/procedure), title, purpose, technology description (language or pseudocode/data structure), location (method or step name), owner (client or developer). Things to consider: languages, libraries, data structures, files/DBs, algorithms, system/network/hardware components, interrupts, error handling, deployment.

**3.3 UML domain model.** The developer's single high-level picture, as the storyboard is the user's. Think OOP (or modular), design patterns, data structures/ADTs. Combines class-diagram and sequence-diagram techniques. Shows only important elements; the rest is decided later.

| Domain model | Class diagram |
|---|---|
| Class syntax + structural info | Class syntax + structural info |
| Some flow arrows | No flow |
| Brief classes | Detailed classes |
| Some code and conditions | None |
| Notes allowed | Notes should not be used |
| Responsibilities optional | Responsibilities required |
| Arc labelling expected | No arc labelling |

Notation covered: class box, attributes, connectors (implementation / function call; generalization "like Java extends"; realization "variation of implements"), shared vs separate inheritance targets, cardinality (any label), **aggregation** (reference set via setter: object passed in), **composition** (reference created with `new` in the constructor: owned), **dependency** (no field, only a local variable), labelled directional arcs mixing processing ("Generate") and structural ("Has") verbs, `<<comments>>`, side definitions, UML context box, structs/JSON/arrays attached to associations, code comments in pseudocode attached to methods with dashed lines, constraint labels. Rules: **always include the main method and its class**; avoid the plain association arrow unless necessary; build the structural picture first, then add flow. Domain models are wordier but show fewer members than class diagrams. If one diagram is too big, split by storyboard component (DM 1, DM 2...), each with **title, purpose description, how to read it, the diagram**.

### 1.6 Section 4: Database, File, and API Definitions
- Database diagram; full structure with validity rules (range, size, type, naming); optimized for the SQL you'll run; **indexing** for speed; important SQL statements (SELECT/INSERT/DELETE/UPDATE; CREATE/DROP DATABASE, CREATE TABLE).
- APIs (assumes 3-tier app): signature `URL/Path/Program?var=val&var2=val2`. Document each as **API name, signature, each variable's name/type/range, description**.
- Files: configuration (INI, XML, custom) and data (CSV, XML, JSON, custom). Use files when there is no DB, when users should edit configuration outside the program, or for tiers in a 3-tier app that have no DB.

### 1.7 Section 5: Critical Sections
A **critical section** is where: several solutions exist but the client wants a particular one; order of operations matters; it's hard to understand what to do; optimization is essential; special requirements affect the algorithm; or you want it done a particular way. Stories, storyboards, mockups, domain models, SQL and APIs aren't detailed enough, so use UML behaviour diagrams (or SQL for simple cases).

- **5.1 Risk analysis**: brainstorm all critical sections as a team; group by location/module; pick the best modelling tool per section. Report: a table grouping all critical sections (**item, title, description**), then a page or two per section with its mitigation model.
- **5.2 Mitigation models**: 5.2.1 <name> + mitigation algorithm, 5.2.2 ..., one per critical section. Choosing the right diagram matters:

| Diagram | Best for | Practice question |
|---|---|---|
| **Activity** | Steps inside one or a few functions (flowchart) | Username/password verification |
| **Sequence** | Order of operations among many parts (object-method algorithm). Arrows: blocking/synchronous, parallel/asynchronous, regular call, return, callback; labelled with signature and return value. Lifelines, destruction X, focus box, gates, external processes, loops/conditions, self-calls | Cash register: scan items, then pay |
| **State machine** | Event processing / message passing | Cooking timer: set, wait for ring, turn off |
| **Timing** | Order of operations when timing is critical | Double- vs single-click; NIC buffer -> OS RAM buffer -> process leaving ready queue |

---

## 2. Architectural Design (Sommerville ch. 6)

Architectural design = how a system should be organized and its overall structure. It is the first stage of design, the critical link between design and requirements engineering. Output: an **architectural model** of communicating components (e.g. Fig 6.1 packing robot: vision system, object identification, arm/gripper controllers, packaging selection, packing system, conveyor controller). In agile, design the overall architecture **early**: refactoring components is cheap, refactoring the architecture is expensive. In practice RE and architecture overlap: you propose an abstract architecture during RE to structure discussion.

- **Architecture in the small**: how one program decomposes into components (this chapter).
- **Architecture in the large**: enterprise systems of systems, distributed, possibly owned by different companies (ch. 17-18).

Architecture drives **non-functional** properties: performance, robustness, distributability, maintainability (Bosch; Chen et al. 2013 found NFRs had the most significant effect). Bass et al.: explicit architecture gives (1) **stakeholder communication**, (2) **system analysis** (early check of critical NFRs), (3) **large-scale reuse** (e.g. product lines).

Block diagrams: boxes = components, nested boxes = subcomponents, arrows = data/control flow. Criticized by Bass et al. (no relationship types, no external properties) but widely used because models serve two purposes: (1) **facilitating discussion** (uncluttered, good for stakeholders and for managers assigning work) and (2) **documenting a designed architecture** (complete model of components, interfaces, connections). ADLs give rigour but are expensive and their cost-effectiveness is unknowable, so rarely used.

### 2.1 Architectural design decisions (6.1)
A creative process best seen as a **series of decisions**, not a sequence of activities. Fig 6.2 questions:
1. Is there a generic application architecture to use as a template?
2. How will the system be distributed across cores/processors?
3. What architectural patterns or styles might be used?
4. What will be the fundamental approach to structure the system?
5. How will structural components be decomposed into subcomponents?
6. What strategy will control the operation of components?
7. What architectural organization best delivers the NFRs?
8. How should the architecture be documented?

Embedded and PC/mobile apps needn't be distributed; most large systems are. "Pattern" and "style" now mean the same (Garlan & Shaw 1993); style covers questions 4-6 (structure, decomposition, control model).

| NFR critical | Architecture should... |
|---|---|
| **Performance** | Localize critical operations in a few **large** components on the same computer (fewer communications); consider replication across processors |
| **Security** | **Layered**, most critical assets in the innermost layers with the highest validation |
| **Safety** | Co-locate safety operations in one or few components (cheaper validation, enables protection/shutdown systems) |
| **Availability** | **Redundant** components, replace/update without stopping (fault tolerance, ch. 11) |
| **Maintainability** | **Fine-grain, self-contained** components; separate producers from consumers; avoid shared data structures |

Conflicts: large components (performance) vs small ones (maintainability); compromise or use different patterns for different parts. Security is now almost always critical. Evaluation is hard (real test is in use); compare against reference architectures or generic patterns.

### 2.2 Architectural views (6.2)
No single diagram can show everything. **Kruchten's 4+1 view model**: four views linked by common **use cases/scenarios** (the "+1"):
| View | Shows | Useful for |
|---|---|---|
| **Logical** | Key abstractions as objects/classes; relate requirements to entities | Relating requirements to design |
| **Process** | Runtime composition as interacting processes | NFR judgements (performance, availability) |
| **Development** | Decomposition into components implemented by one dev or team | Managers, programmers |
| **Physical** | Hardware and how components are distributed across processors | Systems engineers planning deployment |

Hofmeister et al. add a **conceptual view**: abstract view used to decompose requirements, decide reuse, represent product lines (Fig 6.1 is one). Conceptual views are almost always developed; others only as needed. Sommerville's opinions: UML is too implementation-close for architecture, mostly used informally; useful when documenting in detail or for model-driven development. ADLs (components + connectors + rules) unlikely to become mainstream. Agree with agile that detailed design docs go mostly unused; except for **critical systems**, don't build all 4 views, just the ones useful for communication.

### 2.3 Architectural patterns (6.3)
A pattern = stylized, abstract description of good practice tried in different systems; described by **name, description, graphical model, example, when used, advantages, disadvantages**. Pattern idea from the GoF design-patterns book (Gamma et al. 1995); architectural styles (Shaw & Garlan 1996); POSA handbooks (1996-2007).

| Pattern | Description | When used | Advantages | Disadvantages |
|---|---|---|---|---|
| **MVC** | Separates presentation and interaction from data. **Model** = data + operations; **View** = how data is presented; **Controller** = user interaction (keys, clicks), passes it to View and Model | Multiple ways to view/interact with data; future presentation/interaction requirements unknown | Data changes independently of representation and vice versa; same data shown several ways, a change in one shown in all | Extra code and complexity when data model and interactions are simple |
| **Layered** | Related functionality in layers; each serves the layer above, lowest = core services | Building on existing systems; teams each own a layer; multilevel security | Replace whole layers if interface is kept; redundant facilities (e.g. authentication) per layer increase dependability | Clean separation is hard, high layers may bypass to lower ones; performance cost of multiple interpretation levels |
| **Repository** | All data in a central repository; components interact only through it | Large volumes of long-lived data; data-driven systems where adding data triggers an action/tool | Components independent and unaware of each other; changes propagate to all; consistent management (backups in one place) | Single point of failure; inefficient to route all communication through it; hard to distribute |
| **Client-server** | Functionality as services, each from a separate server; clients use them | Shared DB accessed from many locations; servers can be replicated; variable load | Servers distributed over a network; general services (e.g. printing) available to all clients, not implemented by every service | Each service a single point of failure (DoS, server failure); unpredictable performance (network); management problems if servers owned by different organizations |
| **Pipe and filter** | Each component (filter) does one discrete data transformation; data flows (pipe) between them | Data processing (batch and transaction) with separate stages | Easy to understand; transformation reuse; workflow matches business processes; evolve by adding transformations; sequential or concurrent | Data format must be agreed; each transform parses/unparses (overhead); can't reuse components with incompatible data structures |

Details from the text and figures:
- **MVC** (Fig 6.5): Controller maps user actions to model updates and selects the view; View renders the model, requests model updates, sends user events to controller; Model encapsulates state and notifies the view of changes (state change / state query / change notification arrows). Basis of interaction management in most web frameworks. Fig 6.6 web version: Controller = HTTP request processing, app-specific logic, data validation; View = dynamic page generation, forms management; Model = business logic, database; browser talks to both.
- **Layered**: supports incremental development (a layer's services can be released as built); changing a layer interface only affects the adjacent layer; localizes machine dependencies, so porting reimplements only the machine-dependent layers. Fig 6.8 generic four layers: user interface / UI management, authentication & authorization / core business logic, system utilities / system support (OS, DB). Number of layers is arbitrary. Fig 6.9 iLearn: browser UI + iLearn app / configuration services (group, application, identity management) / application services (email, messaging, video conferencing, word processing, simulation, VLE, etc.) / utility services (authentication, logging & monitoring, interfacing, user storage, app storage, search).
- **Repository**: example Fig 6.11 IDE (UML editors, code generators, Java/Python editors, design translator, design analyzer, report generator around a project repository, possibly version-controlled). Suits command-and-control, MIS, CAD, IDEs. Tradeoff: all tools must fit an agreed data model; distributing it means keeping copies consistent. Repository is passive (components control); alternative **blackboard** model (from AI) triggers components when particular data appears, suits unstructured data (Nii 1986).
- **Client-server**: three parts: servers (print, file, compile; several can run on one machine), clients (many concurrent instances), network (usually Internet protocols). Can even run on one computer; key benefit is separation and independence. Clients must know server names; servers needn't know clients. Request-reply (e.g. HTTP), client waits for reply. Fig 6.13 film library: catalog server (library catalogue), video server (film store, needs fast synchronized low-res frames and compression), picture server (high-res photos), web server (film and photo info); clients are browsers. Easy to add or upgrade servers transparently.
- **Pipe and filter**: name from Unix pipes. Batch sequential variant = billing systems; embedded systems may be a process pipeline. Fig 6.15 invoices: read issued invoices -> identify payments -> issue receipts (paid) / find payments due -> issue payment reminders (unpaid). Best for batch and embedded systems with little user interaction; **poor for interactive/GUI systems** whose control is event-based.
- Sidebar: control patterns = **centralized control** (one component calls others) and **event-based control** (system reacts to external events).

### 2.4 Application architectures (6.4)
Businesses in the same sector share needs, so application architectures encapsulate the principal characteristics of a class of systems (reuse is often implicit via ERP and configurable off-the-shelf systems). Five uses: (1) **starting point** for design, (2) **design checklist**, (3) **organizing team work** (stable structures built in parallel), (4) **assessing components for reuse**, (5) **vocabulary** for discussing applications. Sidebar: **reference architectures** capture everything that might be in a domain's architecture, for evaluating/comparing designs and education.

**Transaction processing (TP) systems.** Database-centred, process requests for information or updates; most common interactive business systems (banking, e-commerce, information, booking). A DB **transaction** is an atomic unit: all operations complete before changes are permanent, so failure can't leave inconsistency. User-level transaction = coherent sequence satisfying a goal; a pure query needn't be a DB transaction. Example: ATM withdrawal (check balance, modify, dispense; incomplete until all done). Usually asynchronous requests. Fig 6.16: **I/O processing <-> application logic <-> transaction manager <-> database**. Can be pipe-and-filter: Fig 6.17 ATM: Input (ATM: get customer account id, validate card, select service) -> Process (database: query account, update account) -> Output (ATM: print details, return card, dispense cash).

**Information systems.** All systems interacting with a shared DB are transaction-based information systems (library catalog, flight timetable, patient records), almost always web-based. Fig 6.18 layered: user interface / user communications + authentication & authorization / information retrieval and modification / transaction management + database. Fig 6.19 **Mentcare**: web browser / login, role checking, form & menu manager, data validation / security management, patient info manager, data import & export, report generation / transaction management + patient database (commercial DBMS). E-commerce adds e.g. a shopping cart (several items, one payment transaction). Usually a multi-tier client-server: **web server** (user communication, browser UI), **application server** (app logic, storage/retrieval requests), **database server** (data movement, transaction management). Multiple servers -> high throughput (thousands of transactions/min); add servers at any tier as demand grows.

**Language processing systems.** Translate a formal language into another representation, possibly execute it: compilers, DB command interpreters, XML, natural language translation (e.g. French to Norwegian). Fig 6.20: source instructions -> **translator** (check syntax, check semantics, generate) -> abstract machine instructions -> **interpreter** (fetch, execute; uses input data) -> results. Interpreter can be hardware (compiled code) or software (Ruby, Python). Generic compiler components: **lexical analyzer** (tokens -> internal form), **symbol table** (names of variables, classes, objects), **syntax analyzer** (grammar -> syntax tree), **syntax tree**, **semantic analyzer** (tree + symbol table -> semantic correctness), **code generator** (walks tree -> abstract machine code); optionally optimizers. Two organizations:
- **Repository** (Fig 6.21): AST, grammar definition, symbol table, output definition in a shared repository used by lexical/syntax/semantic analyzers, formatter, editor, optimizer, code generator. Best for an integrated, interactive programming environment (syntax-directed editors, debuggers, pretty-printers) where changes must be reflected immediately.
- **Pipe and filter** (Fig 6.22): lexical -> syntactic -> semantic analysis -> code generation, sharing the symbol table/syntax tree. Best for **batch** compilation without user interaction (e.g. XML-to-XML translation).
Compilers are typically a composite of repository + pipe and filter.

### 2.5 Key points
Architecture describes organization and drives performance/security/availability. Decisions: application type, distribution, styles, documentation and evaluation. Views: conceptual, logical, process, development, physical. Patterns reuse knowledge and state when to use + pros/cons; common ones: MVC, layered, repository, client-server, pipe and filter. Generic application models help understand, compare, validate, and assess reuse. TP systems let many users access/modify a DB remotely (information and resource-management systems are examples). Language processing systems translate texts and execute instructions via a translator and abstract machine.

Exercises worth trying: why start architecture before requirements are complete (6.1); justify a system architect to a non-technical manager (6.2); argue that performance and security conflict (6.3); conceptual + process views for a railway ticket machine, video conferencing, robot floor cleaner (6.4); patterns for cattle-herding drones (6.5); iTunes-like music store architecture (6.6); layered asset-management system from Fig 6.18 (6.7); NL-to-SQL language processor (6.8); box-office information system (6.9); should "software architect" be a separate profession (6.10).

---

## 3. Report writing

### 3.1 Report vs essay (Reading 1, McKeown 2016)
| | Essay | Report |
|---|---|---|
| Purpose | Argues a position, draws conclusions | Presents facts and analysis about a problem, often suggests a solution |
| Structure | Intro, body, conclusion; flow via paragraphs | Preliminary pages (exec summary, TOC); clearly divided **numbered headings**, flow comes from the logic of headings |
| Format | No dot points (reflective reading) | Brief paragraphs and dot points OK so readers extract info fast; tables and figures; often **recommendations** |

### 3.2 Sections (Reading 1, with Reading 2's additions)
Possible order: (letter of transmittal) -> title page -> executive summary -> table of contents -> (list of figures/tables, glossary) -> introduction -> literature review -> methodologies -> findings -> discussion -> conclusion -> recommendations -> references -> (appendices). Reading 1 lists TOC before exec summary; Reading 2 lists exec summary before TOC.

| Section | Rules |
|---|---|
| **Letter of transmittal** | Accompanies report or goes after title page (paginated as preliminary). Single-spaced, blank line between paragraphs; return address, date, inside address, salutation, optional subject line, complimentary close, signature; introduces report by name; acknowledges recipient's help; highlights key findings/conclusions/recommendations; professional tone |
| **Title page** | Informative title showing focus and **nature** of report (evaluation, recommendation, feasibility study, survey, lab report); date; author's name, title, affiliation; for whom it was written (course: name, student no., course name and code) |
| **Table of contents** | All 1st- and 2nd-level headings (3rd optional), reproduced **exactly** with numbering; full titles of appendices. Generate it from Word heading styles |
| **Lists of figures / tables** | Separate lists with page numbers; exact numbering and full titles |
| **Glossary** (optional) | Alphabetical; grammatically parallel definitions. Integrating definitions in the body is usually better |
| **Executive summary** | Written **last** though placed first. Stands alone for a managerial/non-technical reader; 1-2 pages (preferably 1), **≤500 words**; focus, context, method; key info: problem, conclusions, recommendations, financial implications; **nothing not in the report**. Components in example: objectives, points of focus, approach, report outline, findings. (Abstract = 50-250 words, technical audience, research reports; some reports have both) |
| **Introduction** | Contextualizes and shows relevance: background, purpose, scope, key terms, structure of the report. Explains the problem/opportunity; must stand alone **without** the exec summary; gives general readers enough background; **no conclusions or recommendations**. May be followed by objectives ("To..." list), scope (includes/excludes), background, literature review |
| **Methods** | When, where, how research was done, in enough detail (e.g. who was surveyed and how); informative subheadings (evaluation criteria, ethics, usability testing procedure) |
| **Body / findings / discussion** | Discussion is usually longest: critically analyse findings, establish significance, build the argument for recommendations, judge whether the research answered the question (example components: overview of findings, specific findings, analysis linked to existing research, interpretation). Use informative headings ("Economic Considerations", not "Findings"), a brief intro per section, lists/tables/figures, citations; no conclusions/recommendations. Results vs discussion separate in research reports, sometimes combined: ask |
| **Conclusion** | Reinforces and ties together the body; summarizes most important findings and their significance ("so what"); only conclusions that flow from the data; shows objectives met; **no new information**; points to gaps addressed by recommendations |
| **Recommendations** | Actions in light of conclusions: what, who, time frame, cost. **SMART** (specific, measurable, achievable, realistic, timely). Numbered list if several. May be omitted or merged with conclusions |
| **References** | In-text citations + reference list in a standard format (APA, IEEE); all cited sources and only those |
| **Appendices** | Detailed info for specialists, not essential to the body; Appendix A, B, C... in order of mention, informatively titled; not section-numbered |

### 3.3 Formatting conventions (Reading 2)
- Preliminary pages in lowercase Roman numerals (i, ii...), **no number on title page**; body starts at p. 1 with the Introduction (Arabic) through the appendices. In Word: section break (next page) before p. 1, then change number format.
- Section numbering optional; if decimal: Introduction 1.0, next 2.0, subsections 2.1, 2.2. References and appendices unnumbered.
- Start on a new page: transmittal, title page, exec summary, TOC, lists of figures/tables, glossary, introduction, references, appendices. Other sections follow on the same page if space permits.
- Figures and tables: separate numbering series; informative titles (e.g. "Table 1: Annual precipitation in Calgary, 1980-1990"); **table titles above, figure titles below**; legends/footnotes for abbreviations; referred to and discussed in the text; cite the source if borrowed.
- Typography, lists, informative headings make structure clear.

### 3.4 Style rules (Reading 2 checklist item 13 and 16)
- Start by asking: purpose/objectives, and who the readers are (background, familiarity, receptive or hostile, expectations of content/detail/format). Check for workplace guidelines and past reports.
- Audience-sensitive: define terms, avoid jargon for general readers, gender-neutral language.
- Paragraphs begin with a **topic sentence**; few paragraphs over half a page; few sentences **over 30 words** (two typed lines).
- Plain words: "use" not "utilize", "now" not "at this point in time", "We" not "The writers". Precise ("a large increase" is vague).
- **Active voice**, strong verbs ("The Ministry investigated the problem"), except Methods sections which are often passive.
- Grammatical parallelism in lists and headings. Past tense for completed work, present for conclusions and general statements. Link new info to known info. Plural generalizations ("users") avoid pronoun problems.
- Sources: quote only when wording matters; quotation marks or block quote (>40 words); swapping a few words while keeping the original sentence structure is **plagiarism even when cited**; every quote or paraphrase gets an in-text citation.

---

## 4. Applying it to the project

- **Design document = the deliverable.** Use the 6-section structure exactly (title page, contents, Definitions, Solution Architecture, Software Design, DB/File/API Definitions, Critical Sections, Appendix) and the slide table formats: constraints/assumptions (item, constraint, impact, workaround), success/failure (item, statement, impact, discussion), critical sections (item, title, description, location, owner), dev environment list (item, name, version, description, quantity + install procedure + expected workflow), API (name, signature, variables with type/range, description).
- **Section 1** for a 7-person team: pick incremental vs iterative, a project flow (spiral or prototype fit a term project), and a team workflow (standard/paired/mixed); write concrete procedures (daily standup time, pull/push rules, branch-then-merge, Friday review, demo at each milestone).
- **Section 2**: standardize the dev environment (same IDE/versions or Docker), define a staging environment where the TA/client can try the build, and script installation; include a support/ticket plan even if lightweight.
- **Section 3**: redo the storyboard from Chapter 2 with developer modules (backup, import/export, security, install), then a domain model (not a class diagram) including the main class, split per storyboard component if large. Pick an architectural pattern explicitly and justify it by the NFRs: e.g. MVC for the UI/game state, client-server for multiplayer, layered for security, repository for shared game/data state; note the pattern's disadvantages as risks.
- **Section 5**: brainstorm critical sections as a team, then give each a mitigation model in the right UML diagram (activity for one algorithm, sequence for multi-object flows like client-server messages, state machine for game/event states, timing for real-time constraints).
- **Write it as a report**: informative headings, numbered sections, figures titled below and tables above and all referenced in the text, active voice, short paragraphs, consistent TOC, appendices for long material.
