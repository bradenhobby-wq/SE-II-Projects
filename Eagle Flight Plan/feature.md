# Eagle Flight Plan — System Features

## Epic

**As a** student,  
**when** I want to do activities that prepare me to get a job when I graduate,  
**I want** a checklist of tasks and events I can complete each semester I am in school,  
**so that** I am prepared to successfully apply for a job.

This document breaks the epic into system features. Each feature includes one or more user stories that can be planned, implemented, and tested independently.

---

## Actors

Career Services owns the checklist. Students complete it. Faculty and advisors can view progress for advising; they do **not** submit tasks or sign off on items.

| Role | What they do |
| --- | --- |
| **Student** | Follows a per-semester checklist of tasks and events to get job-ready |
| **Career Services staff** | Add and edit the official tasks and events students see |
| **Faculty / advisors** | View a student’s progress to advise them; no catalog editing, suggestions, or sign-off |

**Out of scope:** professors suggesting custom tasks, faculty sign-off queues, and extra-major request workflows. Those added more process than they were worth.

---

## Feature summary

| ID | Feature | Who it serves | What it does |
| --- | --- | --- | --- |
| F1 | Student profile and current semester | Student | Matches the plan to the student’s year and major |
| F2 | Semester checklist and dashboard | Student | Dashboard: campus-wide + my major (completable). Browse other majors: view-only |
| F3 | Multi-semester flight plan | Student | Shows the full plan through graduation |
| F4 | Task tracking | Student | Complete, reopen, and review career-prep tasks |
| F5 | Event tracking | Student | Find, attend, and complete career events |
| F6 | Item details and guidance | Student | Explains how, why, and when to complete an item |
| F7 | Job-readiness progress | Student; faculty/advisors (view) | Shows how prepared the student is to apply |
| F8 | Reminders and next actions | Student | Points to the next task or event this semester |
| F9 | Official task and event catalog | Career Services | Add and edit the tasks and events students see |

---

## F1. Student profile and current semester

The system needs enough student context to show the right semester checklist (for example, freshman fall vs. senior spring) and the student’s **major** so major-specific catalog items appear for the right students.

### Stories

**F1-S1 — Set up my academic standing**  
As a student, when I start using Eagle Flight Plan, I want to record my major, expected graduation term, and current year/semester, so that my checklist matches where I am in school.

**F1-S2 — See my current semester plan first**  
As a student, when I open the system, I want to land on my dashboard for the current semester (campus-wide items plus my major’s items), so that only my relevant work pops up first.

**F1-S3 — Update my standing if it changes**  
As a student, when I take a leave, change majors, or shift my graduation date, I want to update my academic standing, so that future checklists stay accurate.

---

## F2. Semester checklist and dashboard

The core of the epic: a checklist of tasks and events for each semester, owned by Career Services. **Whoever creates a task or event decides** whether it is campus-wide or major-specific.

- **Dashboard (default):** campus-wide items plus **only** major-specific items for the student’s own major. Those are what “pop up.”
- **Browse (optional, view-only):** the student can look at major-specific tasks **across all majors**. Other-major items do not appear on the dashboard and **cannot be marked complete**. This keeps students from farming points or credit on easier work from another major.
- Major-specific items are **color-coded** so they are obviously different from campus-wide items.

### Stories

**F2-S1 — Dashboard shows only my work**  
As a student, when I open my dashboard, I want to see this semester’s campus-wide tasks and events plus major-specific items for **my major only**, so that other majors’ tasks do not clutter what I need to do.

**F2-S2 — Distinguish tasks from events**  
As a student, when I look at a semester checklist, I want tasks (things I complete on my own) and events (things I attend) clearly labeled, so that I know how to finish each item.

**F2-S3 — Mark only my dashboard items complete**  
As a student, when I finish a campus-wide or my-major task or event, I want to check it off, so that progress and points come from work that actually applies to me.

**F2-S4 — See remaining work on my dashboard**  
As a student, when I have not finished everything that applies to me, I want incomplete campus-wide and my-major items to stay visible, so that I know what is left before the semester ends.

**F2-S5 — Filter or sort my dashboard**  
As a student, when a semester has many items, I want to filter by type (task vs. event), source (campus-wide vs. my major), or status (done vs. not done), so that I can focus on the next activity I can actually complete.

**F2-S6 — See major-specific items by color**  
As a student, when I see a major-specific item, I want it color-coded in a way that is clearly major-specific, so that I can tell it apart from general Career Services tasks and events.

**F2-S7 — Browse other majors’ tasks (view-only)**  
As a student, when I want to see what other programs recommend, I want to view major-specific tasks across **all majors** without being able to complete them, so that I can explore ideas but cannot farm points from another major’s easier items.

---

## F3. Multi-semester flight plan

Job prep is spread across every semester in school, not only the current one.

### Stories

**F3-S1 — Browse the full plan**  
As a student, when I want to plan ahead, I want to view checklists for every semester from now until graduation, so that I understand the whole path to being job-ready.

**F3-S2 — See past semester history**  
As a student, when I look back at earlier terms, I want to see which items I completed, so that I can prove I have been preparing over time.

**F3-S3 — Preview upcoming semesters**  
As a student, when I am planning next term, I want to preview the next semester’s tasks and events, so that I can register for events or start longer tasks early.

---

## F4. Task tracking

Tasks are activities the student can complete independently (resume, LinkedIn, cover letter, career assessment, and similar work). Official tasks live in the Career Services catalog (F9).

### Stories

**F4-S1 — Complete a task**  
As a student, when I finish a campus-wide or my-major career-prep task, I want to mark it complete and record the completion date, so that my checklist reflects real progress (not work copied from another major’s list).

**F4-S2 — Reopen a task if I need to redo it**  
As a student, when a task needs an update (for example, an outdated resume), I want to mark it incomplete and work on it again, so that my materials stay ready for applications.

**F4-S3 — Attach or note evidence of completion**  
As a student, when I complete a task, I want to add a short note or file (such as a resume version), so that I can reuse that work when I apply for jobs.

**F4-S4 — See recommended order**  
As a student, when some tasks should happen before others, I want the checklist to show a suggested order, so that I do not skip foundational work (for example, writing a resume before a career fair).

---

## F5. Event tracking

Events are scheduled activities such as career fairs, workshops, info sessions, and mock interviews. Students mark attendance themselves; faculty do not sign off.

### Stories

**F5-S1 — See events on my semester checklist**  
As a student, when my semester includes career events, I want those events listed with date, time, and location (or link), so that I can show up prepared.

**F5-S2 — Mark that I attended an event**  
As a student, when I attend an event, I want to check it off my list, so that event-based prep counts toward job readiness.

**F5-S3 — Find events I can still attend**  
As a student, when the semester is underway, I want to see upcoming events that are still open, so that I do not miss activities that help me apply for a job.

**F5-S4 — Handle events I missed**  
As a student, when I miss a required or recommended event, I want to see whether there is a makeup option or a later offering, so that one missed date does not block my plan.

---

## F6. Item details and guidance

A checklist is only useful if the student knows what “done” looks like and why the item matters for job applications.

### Stories

**F6-S1 — Read how to complete an item**  
As a student, when I open a task or event, I want clear instructions, resources, and a definition of done, so that I can complete it correctly.

**F6-S2 — Understand why it matters**  
As a student, when I am deciding what to do this week, I want a short explanation of how the item helps a job application, so that I stay motivated to finish it.

**F6-S3 — See timing expectations**  
As a student, when an item is best done early or late in the semester, I want to see a recommended window or due date, so that I finish it while it is still useful.

**F6-S4 — See which major an item is for**  
As a student, when I open a color-coded major-specific item, I want to see which major it is for, so that the color coding is explained — including when I am browsing another major’s list.

---

## F7. Job-readiness progress

The epic’s outcome is being prepared to successfully apply for a job. Progress should make that outcome visible using **dashboard items** (campus-wide plus the student’s major). Faculty and advisors may view a student’s progress to support advising, without owning the checklist.

### Stories

**F7-S1 — See semester completion**  
As a student, when I am working through a term, I want a simple progress indicator for this semester’s checklist, so that I know whether I am on track.

**F7-S2 — See overall job-readiness**  
As a student, when I think about applying for internships or full-time jobs, I want an overall view of completed vs. remaining prep across all semesters, so that I know if I am ready to apply.

**F7-S3 — See application-critical gaps**  
As a student, when I am about to apply, I want the system to highlight unfinished items that most affect applications (resume, interview practice, career fair, and similar), so that I can close the gaps that matter first.

**F7-S4 — Advisor views student progress**  
As a faculty member or advisor, when I meet with a student about career prep, I want to see their flight-plan progress, so that I can advise them without managing their checklist.

---

## F8. Reminders and next actions

Students should not have to remember the whole plan unaided. Next-up items and reminders come from the **dashboard set** (campus-wide + the student’s major), not from other majors’ lists.

### Stories

**F8-S1 — Get a next-up item**  
As a student, when I log in, I want the system to suggest the next campus-wide or my-major task or event for this semester, so that other majors’ items never appear as my next step.

**F8-S2 — Get notified about upcoming events**  
As a student, when an event on my checklist is coming up, I want a reminder, so that I do not miss it.

**F8-S3 — Get a mid-semester check-in**  
As a student, when the semester is half over and I still have incomplete items, I want a reminder of what is left, so that I can finish before the term ends.

---

## F9. Official task and event catalog

Career Services owns what students see. Staff add and edit tasks and events so the plan stays current. **The person who creates the item decides** whether it is campus-wide or major-specific (one or more majors).

### Stories

**F9-S1 — Add a task or event**  
As Career Services staff, when I create a career-prep activity, I want to choose whether it is campus-wide or major-specific (and which majors), and assign it to one or more semesters, so that it shows on the right students’ dashboards.

**F9-S2 — Edit a task or event**  
As Career Services staff, when details change (date, instructions, which semester or majors it belongs to), I want to edit the item, so that students are not working from outdated information.

**F9-S3 — Retire an item**  
As Career Services staff, when an activity is no longer offered, I want to retire it from future checklists without erasing student history, so that past completions still count.

---

## Story map (epic → features)

```
Student wants a per-semester checklist of tasks and events
to be ready to apply for a job
│
├── Student
│   ├── F1 Profile & current semester
│   ├── F2 Dashboard (completable: campus-wide + my major); browse other majors view-only
│   ├── F3 Full multi-semester plan
│   ├── F4 Task tracking
│   ├── F5 Event tracking
│   ├── F6 Details & guidance
│   ├── F7 Job-readiness progress
│   └── F8 Reminders & next actions
├── Career Services
│   └── F9 Official task and event catalog
└── Faculty / advisors
    └── F7-S4 View student progress (advising only)
```

## Acceptance notes for the epic

The epic is satisfied when:

1. A student can identify their current semester and major and land on a dashboard of campus-wide items plus **their** major-specific items only.
2. A student can optionally **view** major-specific tasks across all majors; those items are not completable and do not appear on the dashboard (no point/credit farming).
3. A student can mark tasks and events complete themselves (no faculty sign-off).
4. A student can look ahead and back across semesters and tell whether they are ready to apply for a job.
5. Career Services can add, edit, and retire items; the creator chooses campus-wide vs. major-specific.
6. Faculty and advisors can view progress for advising, but they do not suggest tasks or approve completions.
7. Major-specific items are color-coded so students can tell them apart from campus-wide items.
