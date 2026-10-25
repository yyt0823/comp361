# COMP 361 Assignment 1 – Artifacts

**Due:** Thursday, October 2, 2026, 23:55, on myCourses (Assignment 1 box)
**TA office hours:** Sept 30 to Oct 6, 2026
**Total:** 20 points (16 individual + 4 team)
**Tool:** UMLet for all artifacts
**Source:** `../361 Ass 1 Fall 2026.pdf`

---

## Exercise 1 – Requirements Gathering (individual, 16 pts)

Create Artifacts from the client's Story below, as an engineer would during requirements elicitation to "ground the conversation and make clear the client's needs."

### Submit 6 PDFs

| # | File | Scope |
|---|---|---|
| 1 | UML use-case diagram | the **entire** Story (a diagram, not the template) |
| 2 | UI mockup or wireframe | the punch-in/out program **only** |
| 3 | Jobs Completed report mockup | a **mockup, not a wireframe** |
| 4 | Impact statement | How will this program impact society or the industry? |
| 5 | Ethics statement | Any positive or negative ethical implications? |
| 6 | Performance statement | Performance requirements, and what could hinder the software's performance? |

Format everything so it is easy to read. Include only what is appropriate for each artifact: "never too much, never too little."

### The Story (verbatim)

> The manufacturing company, ABC Industries, produces parts to order for its customers. Each to-order part is called a Job. Customers of ABC Industries call the ABC Sales Rep to order the part they want to build. The Sales Rep enters the order into the company database as a Job. Each Job has an ID number (Job number), a title, a text description, a link to the assembly instructions, and a list of parts. The people who build the parts (handle the Job) are called the Floor Staff. When an individual Floor Staff employee has nothing to do, they go to the Punch-in/out computer to get a Job. They see a list of available jobs (i.e., jobs no one is working on), also known as the Jobs List. From that list, they select a job and enter their employee number to assign the work to themselves. At this point, the system checks whether the employee is already punched into another job. If so, the system punches them out from the previous job and punches them in for the new job. Another table in the database records how much time each Floor Staff employee has worked on a job. If the employee has worked on the job multiple times and/or multiple days, the system keeps a record for each work event. This event contains the date, start and end time, job number, and employee number. To punch out means the computer finds the current open record in the database and updates the end time. To punch in means appending a new record to the database with the date, job number, employee number, and start time (the end time is left blank). In addition to punching in/out of jobs from the user interface, the Floor Staff employee can also enter a date range to view all the Jobs they worked on (the Jobs Completed Report). The report is divided into days. For each day, it lists the jobs the employee worked on. At the end of the day, it displays the total hours and minutes worked. At the end of the report, it displays the total hours and minutes worked over the entire period.
>
> To summarize, the user of this program (the Punch-in/out program) can select four actions from the computer: punch-in, punch-out, report, and exit program. The punch-in operation will automatically punch out the employee if they are already punched in on another job. The punch-out operation only punches the employee out of a job. The employee should not exit the program, so it should prompt, "Are you sure?" If the user forgot to punch out at the end of the day, the program automatically punches everyone who has not already punched out at 5:30 PM.

### Rubric (each artifact group scored 0–1 on each line, 4 groups × 4 = 16)

Groups: use-case diagram · UI wireframe · Jobs Completed report mockup · the three statements

- **Syntax:** follows the drawing and writing standards presented **in class** (use-case diagrams must follow the class style, not the internet's)
- **Professionalism & Quality:** no hand-drawn drawings; no grammar or spelling errors; the solution is optimal, simple and uses good design principles; each drawing fits on one page or less; writing is neither wordy nor curt
- **Appropriateness, Gracefulness, Correctness & Completeness:** elements would be used in a real implementation; the solution is correct; edge cases are covered; errors and run-time issues are handled (the program never crashes or hangs, it prompts the user instead)
- **BS:** penalizes padding with jargon to hide uncertainty, and giving multiple alternative answers in the hope of partial credit

---

## Exercise 2 – Team Formation and Project Selection (team, 4 pts)

1. Form a team of 7.
2. Pick a team captain.
3. Choose the project by consensus (see the project description).
4. **Only the captain** fills out the Microsoft Form. It can be resubmitted.
5. Check the "Your TA" tab of the Prof & TA Coordinates sheet to confirm the information.

Nothing goes to myCourses for this exercise. Scoring: form not filled = 0, partially filled = 1–3, complete = 4.

---

## Progress

- [x] 1. Use-case diagram (`1.uxf`). Actors: Sales Representative, Floor Staff, Clock. Auto Punch Out «include» Punch Out; Punch Out «extend» Punch In. Jobs List and "Are you sure?" are steps inside other use cases, so no separate ovals. Box tightened; Exit renamed to Exit Program; Clock labelled Clock (5:30 PM). Before submitting: export to PDF.
- [x] 2. Punch-in/out wireframe (`2.uxf`). Menu bar on every screen; Punch In (Jobs List + employee # + messages, empty-list case), Punch Out, Report (employee #, From/To dates, messages, scrollable report area pointing to the mockup, empty-report case), Exit pop-up (Yes/No, No is default). Before submitting: check layout and export to PDF.
- [x] 3. Jobs Completed report mockup (`3.uxf`). Header (employee #, name, period), grouped by day, one row per work event (Job #, Start, End, Hours), day totals, period total 25h 00m. Auto punch-outs are not flagged because the story's record has no field for it (possible client question for the statements).
- [x] 4. Impact statement (`4-impact.md`)
- [x] 5. Ethics statement (`5-ethics.md`)
- [x] 6. Performance statement (`6-performance.md`)
- [x] All 6 PDFs exported to `pdf/` (2026-09-30)
- [ ] Upload the 6 PDFs to the myCourses Assignment 1 box (due Thu Oct 2, 23:55)
- [ ] Team form submitted by the captain
