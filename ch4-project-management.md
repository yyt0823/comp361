# COMP 361 – Chapter 4: Project Management

**Readings:** Ch4 P1 Lecture Notes (Vybihal: team roles, workflow, activity graph, effort estimation, Gantt), P2 Activity Diagrams (Sommerville 10th ed. web section "Planning activities"), P3 Creating Gantt Charts (gantt.com), P4 Introduction to Software Engineering Management (textbook ch. 2, pp. 35-44).

Chapter 3 picked a process. This chapter is about running it: who does what on the team, how the backlog becomes an ordered schedule (activity graph -> critical path -> Gantt chart), and what a project plan must contain and control.

---

## 1. Team roles and development cycles (P1, slides 1-3)

All three are drawn as **use case diagrams** (actors outside a system box, use cases as ovals, `<<includes>>` / `<<extends>>` dashed arrows).

### 1.1 Standard development cycle: Lead + Developer

**Lead's job is threefold:** plan the project, assign work to developers, ensure the work is completed as requested. Split into **writing** and **verifying**.

| Actor | Use cases in the diagram |
|---|---|
| **Lead** (writes) | Assignment, Standards |
| **Lead** (verifies) | Repo, Review |
| **Developer** | Assignment, Programming, Review |

- Programming `<<includes>>` Documentation, Standards, Testing, Repo.
- Review `<<includes>>` Standards; Review is `<<extended>>` by **Reassignment**.

Flow: Lead writes assignments that follow industry standards and the spec documents made with the client -> Developer codes to the due date, commits/merges to the repo, updates planner boards / progress forms -> Developer books a review with the Lead -> Lead inspects/curates the repo and holds a demo (source code + runtime) -> Lead documents issues and improvement requests, Developer incorporates them -> no issues left -> Lead gives the next assignment.

### 1.2 Paired development cycle

Same as standard, but **two developers get the same assignment**. Diagram actors: Senior Developer, Junior Developer, Lead. New use case: **Sub Task Assignment** (between Senior and Junior), which `<<includes>>` Programming. The Senior keeps the links to Assignment, Programming and Review.

Reasons to pair:
1. Seniority (the diagram's assumption)
2. The assignment is hard and needs two experts
3. It needs two different skills, so pair people with those skills
4. Just to finish faster

First task of the pair: **divide the work in two**. Junior/Senior pair: the **Senior divides**, the **Junior reports to the Senior**, and **only the Senior talks to the Lead**.

### 1.3 Lieutenant team (larger projects)

The Lead has too much work, so delegates to a **Lieutenant** and a **Quality Assurance** person. In large projects QA can be a whole team, and the actor becomes **QA Lead**.

| Actor | Responsibilities (diagram + text) |
|---|---|
| **Lead** | Still writes Documentation and talks to the client. Main job after documentation: **project tracking and scheduling** via the **Gantt** chart and **Checklists**. Joins client Demos. Holds **Meetings** with the Lieutenant. Writes a Checklist per assignment specifying the testing mechanisms QA must use |
| **Lieutenant** | Writes **Assignments** (Assignments `<<includes>>` Documentation); regular communication with the Lead |
| **Developers** | Assignments, Programming (`<<includes>>` Debugging), Repo |
| **Quality Assurance** | Curates the repo, validates the software (Testing, Standards, Checklists), demos with the client |
| **Client** | Demo (`<<includes>>` Feedback) |

Checklists come back to the Lead **as progress reports** after QA reviews a developer's submission.

---

## 2. Standard team workflow (P1, slide 4)

Drawn as a **sequence diagram** "Standard Workflow", precondition `{specification document & design document}`, lifelines **:Lead**, **:DeveloperGroup**, **:QualityAssurance** (stereotyped «incomplete QA workflow»).

1. Lead: *planning*. **Loop {foreach task in gantt}**: create assignment -> A_i; create checklist -> C_i.
2. Output **Batch = {A + C}**; then *assigning(Batch)*.
3. **Loop {foreach group in developers}**: Lead gives an assignment per group; async message *give checklist* to QA.
4. Developer **Loop until done**: code, debug (local programming and testing).
5. Developer -> QA async: *Please QA assignment*. QA **Loop until good**: test -> result; *fix bug {if found}* -> Developer -> *fixed* -> QA.
6. QA -> Lead async: *assignment completed*. Lead *double check*; `{if good}` done, else *asyncMsg(feedback) {if still problem}* back into the loop.

Text version: QA writes notes on the Checklist (what worked, what didn't, improvements) and returns it to **both** Developer and Lead (or Lieutenant). Developer fixes (may meet Lead/Lieutenant), sends **version 2** to QA, repeat until done. Finally the code is shown to the **client for final approval**: OK -> next assignment; not OK -> reopen with the client's issues.

---

## 3. Activity graph and the longest path (P1, slides 5-6)

An **activity graph** orders every backlog task into activities, including parallel ones. It can cover the app alone or the whole development process.

- **Node** = a module of the app or a phase of the development process (drawn as a circle).
- **Arc** = hours/days to complete a node (slide callout: the arc K -> L labelled 2 means "Node K takes 2 days"). Parallel activities are parallel arcs; tasks that cannot be parallelized sit in sequence along an arc. **Merge points** are where parallel arcs meet.
- **All nodes must complete.** The graph is **not cyclic**; the **longest path = the earliest the project can complete**.
- **Optimize** by maximizing parallelism and shortening arc lengths.
- Parallelism depends on (a) tasks that can naturally run in parallel and (b) **number of team members**. The graph is limited by the **weakest link**: if there are more parallel arcs than people, cut the arcs down to the team size. Paired workflow means fewer people available for parallel arcs.

### 3.1 Worked example (slide 5)

START = A, FINISH = L.

| Arc | Days | Arc | Days | Arc | Days |
|---|---|---|---|---|---|
| A-B | 2 | C-E | 5 | G-I | 6 |
| B-C | 3 | E-H | 2 | I-J | 2 |
| B-F | 4 | E-F | 3 | I-K | 4 |
| B-D | 2 | H-L | 3 | J-L | 1 |
| D-G | 3 | F-I | 5 | K-L | 2 |

Earliest finish times (computed from the graph; the slide asks the question but does not print the answer): A 0, B 2, C 5, D 4, E 10, G 7, H 12, F max(6, 13) = 13, I max(18, 13) = 18, J 20, K 22, **L max(15, 21, 24) = 24**.

**Longest (critical) path: A-B-C-E-F-I-K-L = 2+3+5+3+5+4+2 = 24 days.** Sum of all arcs = **47** (matches slide 6's "Total").

### 3.2 Effort estimation table (slide 6)

Document every arc with its duration and **pre-conditions**:

| Node | Duration | Pre-conditions |
|---|---|---|
| A-B | 2 | Met all stakeholders |
| B-C | 3 | Docker image available |
| B-F | 4 | Internet available |

Three numbers:
- **Total** (here 47) = days/hours someone must work to finish every node = what you pay for.
- **Optimal** = calendar time with **infinite people** (needs the optimal graph; for this graph the longest path, 24).
- **Practical** = calendar time **under the real constraints** (needs the practical graph, i.e. arcs cut to team size).

---

## 4. Critical paths in an activity chart (P2, Sommerville)

**Activity chart** = schedule representation showing dependencies: what can run in parallel and what must be sequential. **Tasks = rectangles** labelled with duration in working days; **milestones = rounded shapes** labelled with the date they should be reached (British format d/m/y, start dates). Working days are Mon-Fri; a task starts Monday morning and ends Friday evening, so **you cannot just add days to the start date** for tasks over 5 days.

Figure 1 (start 7/7/14):
- start -> T1 (10 d), T2 (15 d), T4 (10 d)
- T1 -> M1 (18/7/14) -> T3 (15 d) -> M4 (8/8/14) -> T9 (15 d) -> M6 (29/8/14) -> T11 (10 d) -> M8 (12/9/14) -> T12 (10 d) -> **finish 26/9/14**
- T1/T2 -> M3 (25/7/14, red 18/7/14) -> T6 (5 d) -> M4 (red 25/7/14)
- M1 -> T7 (20 d) -> M7 (15/8/14); T2/T4 -> M2 (25/7/14, red 18/7/14) -> T5 (10 d) -> M7 (red 8/8/14); M7 -> T10 (15 d) -> finish (red 29/8/14)
- T4 -> M1 (18/7/14) -> T8 (25 d) -> finish (red 22/8/14)

Reading the dates: **black = date reached after the longest incoming path**; **red = planned completion of a shorter incoming task**. M4 is reached 8/8/14 (after T1 + T3), but T6 finishes 25/7/14, so **T6 can slip without affecting the schedule as long as it's done by 8/8/14**. All paths into a milestone must complete before moving on (T9 starts only when T3 and T6 are done).

**Critical path** = longest path = sequence of dependent activities that sets the minimum project time. Here: **T1-M1-T3-M4-T9-M6-T11-M8-T12 = 12 weeks / 60 working days** (bold boxes around the outside, clockwise).
- Slippage on a critical activity delays the project.
- Delays off the critical path don't, as long as they don't push that path past the critical one. **T8 delayed 2 weeks: no effect.** PM tools compute the allowed delays (shown in the bar chart).
- Managers use activity charts to allocate work and spot non-obvious dependencies; redesigning the system to **shorten the critical path** cuts waiting time.

---

## 5. Gantt charts (P1 slides 7-8, P3)

### 5.1 Lecture view

The activity graph counts days only. A **Gantt chart maps it onto a real calendar** (weekends, holidays, vacations, sick days).

- **Rows** = project phases and software modules. **Columns** = actual start and end dates. **Flags** = important milestones (and $ penalties may apply).
- Allows parallelism and teams; shows **where you are vs where you should be**. Great for the lead and client.
- Trick: find today's date in the top row, draw a vertical line down; **everything left of it should be done**.
- Colour-code (e.g. frontend blue, backend yellow); add flags for milestones and demos.
- Slide 7 example: 3-month chart, rows Market Research, Specifications, Planning, Design, Development, Training, Assessment, Documentation; bars coloured by Team A/B/C; purple milestone flags.
- Slide 8 example (also P3): Jan-Apr by week, groups Planning (Bob Johnson), Packaging (Henry Leblanc), Marketing (Anne Hopkins), Sales (Benjamin Otterson), Collect Statistics (Kathy Gaines), each with sub-task bars; owner shown by **colour and name**. Other formats use a wide left margin for key data. **Simple is better, but too simple is useless.**
- Slide question: 47 days, Mon-Fri only, no holidays -> 47 workdays = 9 weeks + 2 days ≈ **65 calendar days** (my arithmetic; not printed on the slide).

### 5.2 How to build one: 6 steps (gantt.com)

Built in **PMIS** tools (Primavera Project Planner, Microsoft Project, MindView). Meeting with the team to list activities gives *a* schedule, not necessarily a *complete* one. **100% Rule**: the scope baseline must cover 100% of project scope, so the activities derived from it do too.

1. **Review scope baseline**: its 3 parts are the **Scope Statement**, **Work Breakdown Structure (WBS)**, **WBS Dictionary**. Confirm it covers 100% of scope.
2. **Create activities**: **decomposition** of each WBS work package into activities. Set rules; too many activities is as bad as too few. Identify deadlines and milestones (figure: milestone diamond, deadline marker, warning icon when a task passes its deadline).
3. **Sequence activities**: every activity except first and last has a predecessor and successor. Four relationships:

| Relationship | Rule |
|---|---|
| **Finish to Start** | Successor can't start until predecessor finishes (sequential, most common) |
| **Start to Start** | Successor can't start until predecessor starts (parallel / overlapping) |
| **Start to Finish** | Successor can't finish until predecessor has started |
| **Finish to Finish** | Successor can't finish until predecessor finishes |

   Figure: book project (Planning, Writing, Editing, Creating Artwork, Final Changes, Printing, Paper to Printers) linked with these arrow types.
4. **Estimate resources**: labour, material, equipment. Techniques: **Analogous, Parametric, Three-Point, Bottom Up**. Consider skills, competencies, technology. Load resources against activities; build a **resource calendar** (figure: January grid for Adam, Matthew, Amanda, John, Sara with individual holidays and weekends shaded).
5. **Estimate durations**: duration = time from start to end of an activity. Use the same techniques; identify **constraints** (limitations on an activity, e.g. "Must finish on 07/09/2024").
6. **Develop schedule**: load everything into the PM tool and review. Add **buffers** at activity and/or project level (**buffer = activity with no resources or scope**, adds time to reduce schedule risk). Use **resource smoothing / leveling**. The approved chart becomes the **schedule baseline**. (Figure: Project Scope hub linked to Mission Statement, Procurement Strategy, Commission & Validation Plan, Construction Plan, Scope, Risk Identification, Project Controls, Resource Planning, Project Execution Approach, Design Plan.)

### 5.3 Using the Gantt chart

- The schedule baseline is the formal document to execute, monitor and control the schedule. Members status their WBS work packages by **Percent complete** (simple, subjective) or **Earned Value Management System (EVMS)** (measures value of work done).
- Compare actual vs planned to find **variances**. **Critical path = longest path, zero float**; any delay on it delays the end date by the same amount. Usually drawn **red** (figure: Planning -> Writing -> Editing -> Creating Artwork in red).
- If variance exceeds a threshold: preventive or corrective action. Tools:
  - **Lead** = start earlier than planned (accelerates, raises risk). **Lag** = deliberately delay a start. Relationships stay the same.
  - Accelerate without cutting scope: **Fast tracking** = overlap activities (**more risk**); **Crashing** = add resources (**more cost**). Figure: Normal (Task 1 then Task 2, one worker each) vs fast-tracked (Task 2 overlaps Task 1) vs crashed (two workers per task, shorter bars); both give a compressed schedule.
- **Forecasting**: Estimate-to-Complete (ETC), Estimate-at-Completion (EAC), Earned Value techniques.

---

## 6. Software engineering management (P4, textbook ch. 2)

Learning objectives: know the contents of a **project plan**; understand the **dimensions along which a project is controlled**.

### 6.1 Boundaries of a project

- **Information planning** = the meta-project planning across an organization (other projects, priorities).
- Organization-wide rules (standards, data formats, security policy, web layout; product-line architecture) form **boundary conditions**, like zoning rules for a building.
- Software isn't built in isolation: it interfaces with, extends, or builds on existing software, libraries, frameworks.
- "Software development project" is a **misnomer**: we develop **systems** (input -> output) including software, documentation, hardware, procedures, and people. Library automation example: besides DB and UI components, barcode scheme, scanning/printing hardware, relabelling all books, training staff, customer documentation, web access (browse catalogue, reserve online).
- **Figure 2.1 (systems view)**: information planning -> boundary conditions -> a system ellipse containing people, documentation, procedures, and inside it software made of interacting programs; input arrow in, output arrow out.

### 6.2 The project plan (2.1)

Planning is the first step, but not one-shot: it is dynamic and guides the project. How much upfront planning depends on the problem: for highly **explorative** projects, rigid early planning stifles and raises failure risk, so plan nominally and manage for change (agile vs planning-driven).

**14 constituents of a project plan:**

| # | Item | Content |
|---|---|---|
| 1 | Introduction | Background, history, aims, deliverables, responsible people, summary |
| 2 | Process model | Which activities, milestones, how to check they're reached, critical paths |
| 3 | Organization of the project | Relation to user/parent/other organizations; what users must provide and when; roles (PM, tester, programmer, analyst), responsibilities, training gaps |
| 4 | Standards, guidelines, procedures | Working discipline, tool-enforced where possible; documentation agreements (when, quality, kept current); often in a Configuration Control Plan / QA Plan |
| 5 | Management activities | Status/progress reports; priorities among requirements, schedule, cost |
| 6 | Risks | Identify early (late hardware, missing staff, missing info); more uncertainty = larger risk |
| 7 | Staffing | Start, duration, amount, expertise of personnel per category |
| 8 | Methods and techniques | For RE, design, implementation, testing; version/configuration control; test environment and equipment; integration order; acceptance testing procedures |
| 9 | Quality assurance | Organization and procedures to meet quality requirements |
| 10 | Work packages | Break into activities per team member; hierarchical **work breakdown structure** |
| 11 | Resources | Hardware, CPU cycles, tools, personnel per phase |
| 12 | Budget and schedule | Budget allocated per WBS activity; scheduled in time (e.g. **PERT chart**); how expenditure is tracked |
| 13 | Changes | Orderly change procedures. Agile: lightweight, part of every iteration. Heavyweight: register, review, estimate cost, then incorporate. Back-door changes -> bad code, poor docs, overruns. Usually in a Configuration Control Plan |
| 14 | Delivery | Procedures for handing the system over |

Careful planning doesn't remove surprises but means fewer and makes you less vulnerable; it gives orderly procedures so decisions are justifiable.

### 6.3 Controlling the project (2.2): five dimensions

| Dimension | Key points |
|---|---|
| **Time** | Progress is hard to measure ("90% of code written" = rosy). Phased approach gives a measuring instrument. Time vs people trade-off: more people = more coordination; past a point it lengthens the project. **Brooks' Law: "Adding people to a late project only makes it later."** |
| **Information** | Above all, documentation: technical, user, and project docs (current state, agreed changes, decisions); handled via configuration management. Agile keeps knowledge tacit, but docs are still needed at hand-over |
| **Organization** | Everyone must know their role and what's expected; unclear expectations -> people set their own goals. Team organization depends on the project and environment |
| **Quality** | Customers want systems that fit real needs. Quality requirements conflict; balanced with stakeholders at architecture time; assess regularly. **Quality is built in, not an add-on** |
| **Money** | Mostly **labour cost** (hardware/tools are predictable and smaller). Cost = manpower, driven by size (amount of code) and productivity (experienced balanced teams >> new inexperienced ones; strict reliability/response-time constraints reduce productivity). Alternative: fix a cost threshold and build the most pressing requirements first (fits agile) |

- Ways to cut cost: better tools, and **using software instead of building it**; development then becomes **capital-intensive rather than labour-intensive** (Wegner 1984).
- Continuous assessment leads to adjustments in time, cost, organization, information, quality. **"To measure is to know"**: collect quantitative data (e.g. unit-test error data to estimate remaining test effort; time/effort spent to re-estimate). Use it in a **post-mortem** (what went wrong, what we learned, what to change). In practice little hard data is kept; organizations run chaotically in crises (link to the Capability Maturity Model).
- Summary questions: Time (how to assess progress?), Information (document integrity and change requests), Organization (team structure and coordination), Quality (define and assess for process and product), Money (cost, largely set by software size).
- Exercise 9 fact: per **Brooks (1995)**, a product for others can take **three times** the effort of a program for personal use.

---

## 7. Applying it to the project

- Team of 7: pick a structure. A Lead + Lieutenant + QA split (section 1.3) frees the Lead to own the Gantt chart and checklists; pairs (Senior/Junior or skill-based) reduce how many parallel arcs you can staff.
- For every backlog item, produce an **assignment + checklist** batch; QA tests against the checklist and returns it to dev and lead; loop until good, then demo to the client (section 2).
- Build the activity graph, record each arc's duration and pre-conditions, and report **Total, Optimal (longest path) and Practical** (graph trimmed to the number of available people).
- Find the critical path and put the risky work on it first; non-critical tasks have slack.
- Map the graph onto the real term calendar (weekends, midterms, holidays) as a Gantt chart with owners, colours, and milestone flags for demos and deadlines. Use the vertical-line check each week to see if you're behind; respond with fast tracking (risk) or crashing (cost) rather than adding people late (Brooks' Law).
