# COMP 361 Assignment 2 – Specifications

**Due:** Friday, October 30, 2026, 23:55, on myCourses (Assignment 2 box)
**TA office hours:** the week of Oct 26 to Nov 2, 2026
**Total:** 40 points (21 individual + 19 team)
**Tool:** UMLet for the individual artifacts
**Source:** `361 Ass 2 Fall 2026.pdf`

Same Story as A1 (ABC Industries Punch-in/out program, repeated verbatim in the handout; see `../A1/requirements.md`). Instruction: "develop the most well-thought-out, optimal, and clean solution"; the Story may hold more information than an artifact needs, so include only what fits ("never too much, never too little").

## What to submit

| # | File | Who | Contents |
|---|---|---|---|
| 1 | `A2Q1` (single PDF) | each student | Exercise 1: Activity Graph, days, total hours, Gantt Chart, end date, extra-days table |
| 2 | `A2Q2` (single PDF) | each student | Exercise 2: System Flowchart, Activity Diagram, comment on which is better |
| 3 | `A2Team.PDF` (single PDF) | team contact person **only** | Exercise 4 items 1–4 |

All go to the myCourses Assignment 2 box. Format everything so it is easy to read.

---

## Exercise 1 – Effort Estimation (individual, 12 pts)

Assume a team of **3 programmers**, and you are **not** one of them (so there are only three people). Names: **Dev1, Dev2, Dev3**. Draw optimal diagrams for the Story.

Required in `A2Q1`:
1. The optimal **Activity Graph** for the Story, assuming three developers.
2. How many **days** the program takes to complete according to the Activity Graph.
3. The **total hours of work** that must be paid to the developers.
4. A **Gantt Chart**, work starting **January 1, 2027**, including weekends, holidays and buffer days. Mark holidays and buffer days clearly (a different colour or a different label).
5. The project **end date** according to the Gantt Chart.
6. How many **extra days** the Gantt Chart allocates: weekend days total, holiday days total and buffer days total, **as a table with a grand total**.

### Rubric (12)
- Activity Graph: Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- Days to complete (Activity Graph): computed correctly 0–1
- Total work hours: computed correctly 0–1
- Gantt Chart: Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- End date (Gantt Chart): computed correctly 0–1
- Extra days: computed correctly 0–0.5, provided a table 0–0.5

---

## Exercise 2 – UML Flow Diagrams (individual, 9 pts)

Scope: the punch-in activity is complex because it includes a punch-out. It is a human-to-machine activity that can trigger an **automatic punch-out event**. This does **not** include the end-of-day automatic punch-out at 5:30 PM.

Required in `A2Q2`:
1. A **System Flowchart Diagram** for this punch-out operation.
2. The same punch-out operation redone as a **UML Activity Diagram**.
3. A **comment** on which drawing technique is more useful in this situation, and why.

### Rubric (9)
- System Flowchart Diagram: Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- UML Activity Diagram: Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- Which diagram technique is best: Completeness 0–1

---

## Exercise 4 – Requirements Phase (team, 19 pts)

(The handout numbers it #4; there is no Exercise #3.)

1. Select your **project theme**.
2. Decide on the program:
   a. give it a **name**;
   b. write a **story** describing the application in layperson terms.
3. Describe the project from the user's perspective:
   a. a **single high-level Use-Case Diagram**;
   b. a **Storyboard**;
   c. **Wireframes** of the most important user interfaces (wireframes, not mockups).
4. Tentatively define the team's software development strategy (can change later):
   a. **team type**, and why;
   b. **roles** of each team member, and why;
   c. **software evolution strategy**, and why;
   d. **software building strategy**, and why.

### Submission rules for `A2Team.PDF`
- Only the **team contact person** submits it. Name the contact person on the **first page** (in case someone else submits by mistake).
- List **everybody's name on the first page** so the TA can record the grade. Everyone gets the same grade for this part.
- Suggested: divide the work among members (to avoid "Hero").
- **Required:** the team meets together to discuss the answers.

### Notes in the handout
- **Ubisoft teams:** learn Unity and start deciding which basic assets and algorithms to build. Write vanilla code you can port into the competition theme once it is announced (you need to catch up with other schools). Contact the professor for guidance; formal meetings start once teams are formed with the Games Club.
- **Scrum Journal:** start your private scrum journal now; rules are in the project description (see below).

### Rubric (19)
- Project Theme: 0–1, correctly selected from the project options and used correctly in the Story
- Program Name: 0/1, present or missing
- Program Story: 0–1, at least one paragraph and consistent with the selected Theme
- Use-Case Diagram: Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- Storyboard: Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- Wireframes (not mockups): Syntax 0–1, Optimality 0–1, Correctness 0–1, Completeness 0–1
- Team type and why: 0–1, correctly described
- Team member roles and why: 0–1, correctly described and every person has a role
- Software Evolution Strategy and why: 0–1, correctly described
- Software Building Strategy and why: 0–1, correctly described

---

## Grading definitions (from the handout)

- **Syntax:** drawings and writing follow the standards presented **in class** (e.g., use-case diagrams strictly follow the class style, not the internet's).
- **Professional:** presented professionally; no hand-drawn drawings; no grammar or spelling errors.
- **Quality:** execution optimality, a simple algorithm, good design principles (e.g., design patterns), fast running time; each drawing fits on a page or less; writing neither wordy nor curt.
- **Appropriate:** elements would be used in a real implementation; the right algorithms and design patterns identified for every case.
- **Correct:** the solution is correct.
- **Complete:** the question is fully answered; edge cases and additional features are described where needed.
- **Graceful:** errors and run-time issues are handled so the program never crashes or hangs (it prompts the user instead).
- **BS:** penalizes hiding uncertainty under lots of technical language, and giving multiple solutions in the hope of partial credit.

---

## Progress

- [ ] Ex 1 Activity Graph
- [ ] Ex 1 days, total hours
- [ ] Ex 1 Gantt Chart (from Jan 1, 2027), end date, extra-days table
- [ ] Ex 1 exported as `A2Q1.pdf`
- [ ] Ex 2 System Flowchart
- [ ] Ex 2 Activity Diagram
- [ ] Ex 2 comment, exported as `A2Q2.pdf`
- [ ] Team: theme, name, story, use-case diagram, storyboard, wireframes, strategy (`A2Team.PDF`, contact person submits)
- [ ] Start personal scrum journal

---
---

# COMP 361 Project 2026–2027 (DRAFT description)

**Source:** `COMP 361 Project 2026 2027 - DRAFT.pdf` (5 pages, marked DRAFT). Two-term project ("Multiple Due Dates"). Fall: design the software and self-study the tools (libraries, languages, engines). Winter: official programming.

## Who does what (groups)

| Group | Students | Must do |
|---|---|---|
| 1 | CS majors (only) and CS majors with Software Engineering specialty (other majors count as CS only) | Base Project only, **or** Base Project + Theme #1 |
| 2 | CS majors with Games specialty | Base Project + Theme #2, **or** Base Project + Theme #3; must use a game engine (Unity or Unreal) |
| 3 | Group 1 students on a team with Group 2 students | may switch to Group 2 rules; the reverse is not allowed (Games students MUST build a game in an engine) |

## Team rules

- Teams of **7**. If the class does not divide evenly, one group may have **6 or 8**; get the professor's approval first for any size other than 7.
- A1 pointed to the form for reporting team members, captain and theme.
- Finding a team: people you know; ask people near you ("What theme is your project?"); post on uAsk with `#project`; come to class for the professor's matchmaking ("Who needs a team?"); contact the McGill Games Club (https://gamedevmcgill.ca/).

## Base Project

- **Application:** a desktop application in any language.
- **Base Theme:** propose a project on the theme **"App to help students, a club, or McGill."** Get the professor's approval **before registering** the group (deductions otherwise).
- **Minimum features:**
  - graphical user interface (not only text-based);
  - database or some input/output file system (persistent storage);
  - security feature(s);
  - cannot be a website (that is COMP 307).
- **Each team member** is responsible for at least one module, where a module means:
  1. one or more GUI interfaces (window/screen; if one interface is a GUI, a second can be something else, like text-based or an API);
  2. reading/writing the database or file system;
  3. more than one object handling the business logic for the interface;
  4. following design-pattern rules;
  5. automated test cases for their code;
  6. well-documented code (comments and a readme file).
- **As a team:**
  - identify the Patterns and Anti-patterns the application is based on;
  - choose a common development stack: IDE, repository, code documentation standards, automated testing method, software management tools;
  - choose an "official" deployment/runtime platform (e.g., the captain's laptop or the Mimi server). A module counts as working **only** if it runs on the official platform;
  - demos run from a single laptop: the official runtime platform.
- Extra elements can be added after the professor approves.

## Themes

- **Theme #1 – Hex Game Project:** Base Project with Theme #1 replacing the Base Theme. A video game with a hex-based map, loosely based on Dungeons & Dragons. **No game engine**; a graphics library is allowed (e.g., Java Swing).
- **Theme #2 – Game Engine Project:** Base Project with Theme #2 replacing the Base Theme. A video game loosely based on D&D, built in **Unreal or Unity**. (The draft's text for Theme #2 still says "The Hex Game Project is the Base Project…", apparently copied from Theme #1.)
- **Theme #3 – Ubisoft Competition** (Ubisoft Game Lab Competition; runs only in the Winter semester; the theme is revealed late January, maybe early February):
  - **Fall:** do Theme #2: design a D&D game and complete the assignments like everyone else. In parallel, learn Unity or Unreal and start building assets and scripts for the surprise theme reveal; make an appointment with the professor for guidance.
  - **Winter:** meet the professor to plan the term; Ubisoft mentors are assigned at some point; attend Ubisoft-required meetings and events; submit the **Scrum Journal but no other reports**.

## Deliverables and timeline

### Fall semester
| Deliverable | Content (per the draft) |
|---|---|
| A1 – Team Formation and Project Selection | find team, choose theme, confirm with professor, register team |
| A2 – Artifacts for the Specification Document | application mechanics and user interaction; first glimpse of tech stack. Lists: UML use-case diagram **and template**, storyboard, wireframes, **initial technology stack**, **product owner win and loss conditions** (the professor is not the product owner), among other things (business rules, effort estimation) |
| A3 – Artifacts for the Design Document | after the product owner's OKAY and the product Freeze: design patterns, final tech stack, libraries, language(s), UML domain models, activity diagrams, sequence diagrams, deployment diagrams, database schemas, some screen mock-ups, critical sections, etc. |
| A4 – Artifacts for the Development Document | IDE, test cases, QA, repository pipelines, Agile, Scrum, customer-in-the-loop, management tools, templates, scheduling, deployment environment, teamwork assignment (responsibilities), etc. |

### Winter semester
| Deliverable | When | Grading |
|---|---|---|
| Three Progress Meetings | 2nd week of each month, with TA or professor (your "handler") | individual, on contribution to planning/research |
| Three Progress Demos | 4th week of each month, demo of the current program | individual, on contribution to the code base |
| Final Demonstration | by appointment, when close to done | individual. Handler may not touch the program; one member demos; handler questions each member on contribution and knowledge of the program and SE methods |
| Acceptance Test | after the final demo | group grade on application quality. Team only launches the program, then hands over the laptop; members may not speak; handler asks no questions (unless emergency). Not everyone must attend. Ends the programming portion of the course |
| Showcase | week before the Winter final exam season | attendance graded. Deployment laptops on tables, one host per team (can swap), others try projects; secret ballot for best program, small prize (TBD) |

### Scrum Meeting Journal (both terms)
Personal and private (only the professor reads it), starting from A2, submitted on myCourses in the Assignment module. Format:
- **Each team meeting** (min 2–4 per month): summary of what was discussed (your POV), summary of decisions (your POV), your current reflection about the project and team.
- **End-of-Month Feelings** (1 per month): what I liked this month; what I am not liking; next steps to fix personal and technical issues; next steps on the project.
- **End-of-Term** (1 per term, 2 total): what worked; what did not work; what I would do again (each personally, team-wise, technically); personal reflections and feelings (conclusions and future).

## Grading

The draft gives **no point weights or percentages** for any project component. It only says which items are graded and whether individually or as a group (see the Winter table). Fall assignment grading is defined in each assignment handout.

## What is new or different vs earlier info

- **Base Theme is now specified:** "App to help students, a club, or McGill", and needs professor approval before registering (deductions otherwise). Earlier info only said desktop app + GUI + persistent storage + security.
- **New Base requirements:** not a website (COMP 307); the detailed per-member module definition (GUI, DB/file I/O, multiple business-logic objects, design patterns, automated tests, docs + readme); team-level patterns/anti-patterns, common dev stack, and one official runtime platform that alone counts for grading and demos.
- **Group rules:** Group 1 picks Base only or Base + Theme #1; Games students must pick Theme #2 or #3 in an engine; Group 1 students on a team with Games students may switch to Group 2 rules.
- **Team size:** still 7, but one team may be 6 or 8 with prior approval.
- **Theme #3 details:** Fall = Theme #2 plus Unity/Unreal prep; Winter = Ubisoft mentors and events, Scrum Journal only, no other reports.
- **A2 scope mismatch:** the draft's A2 list includes a use-case **template**, initial technology stack, product owner win/loss conditions and business rules, which the actual A2 handout does **not** ask for. The handout asks for theme, name, story, use-case diagram, storyboard, wireframes and team strategy (plus individual effort estimation and flow diagrams). Follow the handout; the extra items may come later.
- Themes #1 and #2 (hex D&D with no engine; D&D in Unity/Unreal) are unchanged.
