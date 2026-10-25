# COMP 361 – Lecture 1: Ad Hoc Software Engineering

**Course:** COMP 361D1, Software Engineering Project, Fall 2026
**Related reading:** Chapter 1 – Page 1 – Ad Hoc SE, Chapter 1 – Page 2 – A reading about Processes

---

## 1. Why start with ad hoc

**Ad hoc** (Latin: "for this purpose") means improvised, done on the spot, without a formal process. The scenario: someone calls you, says "we're in trouble, it has to be fixed by Friday," and you land there and solve it with whatever you have.

Starting the course here does two things at once:

- Gives a **big picture** of what software engineering is about.
- Practices **landing on your feet** when thrown into a project.

It also answers the question "what is the minimum set of things I need?" and lets you mix and match tools freely. The goal is to build a **bag of tricks** for particular situations.

**Software engineering** = best practices. It is evolving, and AI is changing the playing field. The course starts without AI and adds it later.

---

## 2. Vocabulary

### Developer
Not just "programmer." A developer is any of these roles:

| Role | What they do |
|---|---|
| Designer | Shapes what the product looks like and how it flows |
| System analyst | Turns the client's story into requirements |
| QA | Tests and verifies |
| Programmer | Writes the code |
| Team lead | Coordinates the team |

McGill trains you in all of them. A technical college might train you in one.

### Client vs. customer
- **Client** – the person you build the program for and who pays you. They are the **Oracle**: the final authority on what the product should be. If anyone else asks for something, confirm it with the Oracle.
- **Customer** – the client's customer, the end user who benefits from the tool.
- **Product owner** – the person at the client company responsible for the product. In a client-driven project, this is the Oracle.

### Project types

| Type | Oracle | Notes |
|---|---|---|
| School | None (prof is a weak one) | Group of peers, no hierarchy, different group dynamics |
| Client-driven | Product owner | **Course focus.** Small to medium projects |
| Personal | You | Can include friends |
| Solo | You | You are every role: front end, back end, IT |
| Ad hoc | Client | Emergency, improvised, compressed |
| Industry | Client | Very large projects, different dynamics |

About 90% of the work overlaps across all types. What you learn in one applies to the others.

---

## 3. The process (walked through with the kitchen timer example)

**Example story:** A client wants to sell a tablet for the kitchen. It runs a timer app for cooking, and maybe you can record recipes on it. That is the whole story.

### Step 1 – The story
The client describes the product in messy, non-technical language. They often think they are technical and misuse terminology. Your job is to figure out what the story means.

> **Anecdote:** A client said "print this report on the printer." The prof built a button that printed on paper. The client expected a full print-preview screen with page up/down, margin settings, and printer selection, "like Microsoft Word does." The prof had quoted hours for a button.

The client believes they have told you everything. They have not.

### Step 2 – Requirements
Extract facts from the story ("mystery, then fact"). Two techniques:

1. **Missing information** – what did they not say?
2. **Words that don't make sense** – vague terms to expand on.

For the timer app, the class surfaced:
- Who is the user? Home kitchen or restaurant?
- Internet connectivity?
- Android or Apple? (possibly two apps, two quotes)
- Touch screen? Keyboard? Scroll bars?
- What does "record" mean? RAM, local file, database, server?

Software is a **relationship**, not a Best Buy purchase. Expect multiple meetings over multiple days.

### Step 3 – Storyboard
A map of every screen as a labeled box with arrows between them. **No detail yet**: no buttons, no scroll bars. Like a film storyboard.

Example map: Welcome → Menu → { Recipes, New, Timer }

Rules:
- Draw it **live with the client** and get a "yes." Later you can point back to it.
- **No dangling pointers.** Every action (save, edit, select) must lead somewhere.
- Raise the technical questions the client cannot see: load from where? edit on the same screen or a new one? one screen or many?

The **server conversation** is a business question: backup and multi-device access are benefits, but a server means extra cost, internet dependency, and load delay. Ask "is this $100, or $100 plus subscription?" as a humble expert.

Which conversations to have with the client:
- **Must:** load, edit, save, whether there is a server.
- **Skip:** Mongo vs. MariaDB. They do not care.

### Step 4 – Wireframe
One sketch per storyboard box showing layout. Example menu: three big buttons (Timer, New Recipe, Recipes) because it is a touch screen and a parent might be using it. Maybe no Quit button, since the tablet boots straight into the app.

### Step 5 – Info
Things the client needs from you and you need from them:
- **Cost** – they have to pay you.
- **Time** – how long it will take.
- **Success and fail criteria** – e.g. "if it's not easy to use, that's a fail." Once you hear this, you become hypersensitive to it.

Steps 2 to 5 form a **loop**: client's view → storyboard/wireframes → info → repeat. The client gives you 30 minutes, you need 4 hours, so you come back.

### Step 6 – OK and freeze
Two parts:

1. **The OK.** The client stamps the design. When they later say "that's not what I wanted," you can say "you stamped it." You still fix it, but it is a change of mind, not your error.
2. **The freeze.** No more changes. Tell the client explicitly: new ideas are welcome, but any idea stops the project and restarts the whole cycle, including cost and time.

> **Why:** the client's "small idea" (e.g. two people editing the same recipe at once, when you built a local CSV file) is a completely different architecture to you. Software is connected in surprising ways; small additions break things. "It will only take half an hour" is never true.

### Step 7 – Technology
Now that requirements are frozen, choose:

| Decision | Example choice | Note |
|---|---|---|
| Language | Java with Swing | A tablet runs regular programs, so stay in familiar territory |
| IDE | Any, but **one per team** | Switching IDEs with repo push/pull causes problems |
| Repo | git | |
| Libraries/tools | SQL database, internet API | |
| Server stack | AWS + Linux + Apache | A separate deliverable from the app |

This is a **second freeze, for you.** Once you start coding in a stack, switching means deleting everything. The client does not care about this freeze.

Advice:
- **Prototype first.** Build toy versions before quoting a price, to check the stack can meet the fail criteria.
- **Breadth matters.** If Python is the only language you know, that is the only answer you can give. Know many tools so you can match the tool to the problem.
- **You will never know everything.** The client thinks you are a god. Say "I'll tell you the cost later," go home, experiment, come back.

### Step 8 – Build
Simplest plan: a numbered table.

| # | Task | Due date |
|---|---|---|
| 1 | Timer core (buzz, pause, snooze) | ... |
| 2 | Server + API + schema | ... |
| 3 | Menu screens | ... |

- **Due dates are for you only.** Nobody else sees them, but they tell you early whether you are ahead, behind, or not sleeping tonight. Especially important in a team.
- **Get the hard parts out of the way first.** That is where time gets wasted. In a team: one person does the timer, one does the server, the rest build menus.
- **Get something demoable early.** Menus can be run and clicked. A server needs a separate testing program and means nothing to the client.

Three things to balance: **time**, **hard places**, **client in the loop**.

### Step 9 – Keep the client in the loop
Never disappear for a month. Even if they OK'd it and you built exactly what they said, 100% of the time they will not like it.

- Demo often, and demo things they can **touch**. "What's an API? Why are you showing me a tester?"
- A clickable menu lets them react to colors, layout, and **response time** early. (Prof's story: waits 30 seconds for an app, thinks "stupid program." Clients will judge you the same way.)

### Step 10 – Install
Installation never works the first time. **Your laptop is not their laptop.**

- Do an **incremental install at each demo**, on the client's machine, not yours.
- Failures are almost always **configuration**: IDE default absolute paths that don't exist on their machine, libraries installed years ago that you forgot about, driver version mismatches.
- Arrive early, run it on their computer, do any last-minute `pip install`, then say it is ready.
- Cloud deployment helps eliminate many issues, but the cloud environment must match the target (the tablet) exactly, and something is always slightly off.

---

## 4. Recurring themes

- **Backward arrows are normal.** Every step can send you back. Iterating is cheapest on paper and most expensive once you are in the IDE.
- **The client has a picture in their mind and wants you to read it.** Flexibility of interpretation is your enemy. Ask, draw, confirm.
- **Be the humble expert.** You raise the questions they cannot see (server, subscription, storage) without lecturing.
- **Two freezes.** Requirements freeze constrains the client. Technology freeze constrains you.
- **Breadth and play.** Take varied courses, build toy projects at home, and go experiment when you hit something you do not know. A startup where you are the only tech person is the fastest way to grow.

---

## 5. Quick reference: the pipeline

```
Story → Requirements → Storyboard → Wireframe → Info (cost, time, pass/fail)
      ↺ loop with client until...
OK + FREEZE (client)
      → Technology + FREEZE (you)
      → Build (numbered table, due dates, hard parts first)
      → Client in the loop (weekly demos)
      → Incremental install on their machine
```
