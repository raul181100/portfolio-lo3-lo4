---
type: portfolio
status: draft
created: 2026-11-18
hand-in: 2026-12-11
cssclasses:
  - portfolio
---
# Portfolio: Raul · HouseMate

> [!info] Focus of this draft
> LO3 (project plan and process) and LO4 (reflection and reporting). Feedback to answer: Chris (16 Nov) and the LO3 comment *"show me, don't just tell me"*.
> Language: English, to match the course material. The Dutch translation is in Canvas.
> Rule for this document: every claim links to a note, a date or a file. If there is no evidence yet, it says **[TODO]**.

## 0. How to read this portfolio

I document the project in one Obsidian vault. Every decision, bug, sprint, feedback session and daily log is a note that follows a fixed template. The links between the notes are the process itself:

`[[HouseMate]]` → `[[Sprint 3]]` → `[[Role type]]` → `[[Null enum in DB]]` → lesson in the Knowledge notes

Each note answers the same questions: what was the context, which options did I consider, what did I choose and why, how did I validate it, and would I decide the same today.

## 1. Competencies and where the evidence is

| Competency (course goal) | What I did in practice | Evidence |
| --- | --- | --- |
| Project organisation | Sprint plans with a "Done when" criterion per block. Group sprint split by person. | [[Sprint 3]] · [[Group_sprint 3]] |
| Communication and reporting | Feedback notes with "what I did" and "what changed". Daily logs. Sprint review with a MoSCoW proposal. | [[Frank - team rules and scope]] · [[Martin -Documentation on software development and useful technologies]] · [[Chris 2026-11-16]] |
| Exploratory research | Options tables for each decision. Bug investigation step by step. | [[Role type]] · [[Null enum in DB]] |
| Reporting | Sprint close (Done / Not done / Deviation / MoSCoW changes). | [[Sprint 1]] · [[Sprint 2]] **[TODO: empty, see §8]** |

> [!question] Mapping to LO3 and LO4
> I link the competencies to LO3 (planning, research, validation) and LO4 (reporting and reflection). **[TODO: confirm the exact LO3 and LO4 wording with Chris.]**

## 2. The project plan: from milestones to steps

### 2.1 Project level

| Sprint | Dates | Goal | Status on 18 Nov |
| --- | --- | --- | --- |
| 1 | 2–8 Nov | **[TODO: goal not written]** | Note empty |
| 2 | 9–15 Nov | **[TODO: goal not written]** | Note empty |
| 3 | 16–22 Nov | Tenant and landlord roles, landlord views, logout | In progress (see 2.2) |
| 4 | 23–29 Nov | **[TODO]** | Not started |
| 5 | 30 Nov–6 Dec | **[TODO]** | Not started |
| 6 | 7–11 Dec | **[TODO]** | Not started |

Source: [[HouseMate]].

### 2.2 Sprint 3 broken down into steps

The sprint has **7 blocks and 19 steps**. Each block has a "Done when" sentence, so I can check whether it is finished. This is how I answered the feedback "break tasks into smaller steps":

| Block | Done when (from the sprint note) | Steps |
| --- | --- | --- |
| Documentation & planning | Group tasks split by person; role decision and endpoints documented | 3 |
| Roles | Every user has a role saved in the database and the app receives it at login | 3 |
| Views per role | Tenant and landlord see different screens after login | 3 |
| Landlord: create houses | A landlord can create a house; a tenant cannot | 2 |
| Expenses | In a house: list, add, open detail | 3 |
| IoT | The app shows IoT data from the backend in a chart | 4 (depends on Nikolay's data) |
| Logout | Logout returns to login; back button does not re-enter | 1 |

### 2.3 Group level (Group Sprint 3, 16–22 Nov)

| Member | Tasks this sprint | Note |
| --- | --- | --- |
| Raul | IoT ↔ Android · Roles | Roles is my individual block |
| Nikolay | IoT ↔ Android · Website ↔ Spring Boot | Depends on Nikolay for the IoT data |
| Anushree | Website ↔ Spring Boot | |
| Daniel | Group tasks only | Database. The eduCloud database was not ready on 16 Nov. |
| Everyone | Research · planning and Trello document | |

Source: [[Group_sprint 3]].

## 3. How I arrived at this plan

The plan did not come from one moment. It was changed after each input. This is the timeline.

| Date   | Input                                                                              | What I did with it                                                                                                                                                                           |
| ------ | ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 10 Nov | Frank: avoid an ambitious project with little time; set group rules                | Group rules and regular meetings with a focus per meeting. Result: better communication, commitment still "in progress". [[Frank - team rules and scope]]                                    |
| 13 Nov | Martin: do not leave integration until the end; document with diagrams (C4)        | Back end unified into [[Spring Boot]]. Diagrams per layer. [[Martin -Documentation on software development and useful technologies]]                                                         |
| 13 Nov | My own review of Sprint 3: 7 blocks in one week, IoT depends on data I do not have | MoSCoW proposal for the sprint (see 3.1).                                                                                                                                                    |
| 13 Nov | Group review: four integrations in one week                                        | Candidate to move to Sprint 4: Website ↔ Spring Boot. **[TODO: confirm whether the group decided this on Monday.]** [[Group_sprint 3]]                                                       |
| 16 Nov | Chris: LO3 needs research and validation, not opinions                             | I restructured my documentation: how I got the knowledge, how I used it, why. [[Chris 2026-11-16]]                                                                                           |
| 16 Nov | Could not connect to eduCloud: the database was not set up                         | Dependency on Daniel found. Backend started locally on 18 Nov with the container password as an environment variable. [[Diario 2026-11-16]] · [[Diario 2026-11-18]] |
| 17 Nov | Null value error on the role column: 90 minutes lost                               | Root cause found, fix applied, lesson recorded. [[Null enum in DB]]                                                                                                                          |

### 3.1 MoSCoW for Sprint 3 (the proposal from 13 Nov)

| Priority | Blocks | Why |
| --- | --- | --- |
| Must | Roles · Views per role · Logout · Documentation | Without roles, the other blocks have no meaning |
| Should | Landlord: create houses · IoT: analyse data and endpoint | Needed, but IoT depends on someone else |
| Could | Expenses | Already partly works according to [[HouseMate]] |
| Next sprint | IoT logic and chart | Depends on data that does not exist yet |

> [!note] Why this is a proposal and not a finished decision
> The rule I set myself: whatever moves to Sprint 4 is written as a **decision** in "MoSCoW changes", not as "no time".

### 3.2 Was the scope right? (honest check on 18 Nov)

**No, not completely.** Evidence:

- Sprint 3 had 7 blocks, but the Views block depends on the role being saved first. On 13 Nov I wrote the IoT block depends on data I did not have, but I did not write the same warning for the Views block.
- The Trello workload showed I had 4 cards alone in week 3 (Roles). The null-value bug cost 90 minutes of that week.
- The sprint is still open: "Done: 0" in the sprint note is out of date, but several steps are not finished (no endpoint checks the role yet; views are in progress).

**What I would change:** decide the Must/Should/Could split on the first day of the sprint, and make the database dependency a step of its own with an owner and a date.

## 4. Research and validation

### 4.1 What I looked at, and where the information came from

| Source | What it gave me | Used in |
| --- | --- | --- |
| Frank (10 Nov), Martin (13 Nov), Chris (16 Nov) | Scope, documentation approach, LO3/LO4 expectations | §3, §5 |
| c4model.com (recommended by Martin) | Levels of diagrams: general view, then zoom in per layer | Diagrams in [[Diagrams]] |
| Android docs: Navigation component, start destination | How the start screen is chosen in `nav_graph.xml` | [[Role-based screens]] |
| howtodoinjava: NotBlank vs NotNull | Why a new field fails on old rows | [[Null enum in DB]] |
| My own code: `RoleType`, `CreateUserRequest`, `UserResponse` (code check 16 Nov) | What the backend already does | [[Role type]] |
| Team: Trello board and Nikolay's IoT data | Who depends on what | [[Group_sprint 3]] · [[IoT devices]] |

**[TODO: add the sources for the options in BCrypt, PostgreSQL, Retrofit and Java instead of Kotlin. Those notes have no sources yet.]**

### 4.2 Decisions and how I validated them

| Decision | Options I compared | Chosen | How I validated it | Status |
| --- | --- | --- | --- | --- |
| [[Role type]] | Boolean · int code · Java enum · two tables | Java enum `RoleType`, stored as string | Code check 16 Nov. Fix confirmed in the database on 17 Nov (screenshot). | taken |
| [[Rol saved from Login]] | Save in registration · pass by Intent · save at login | Save at login (SharedPreferences) | Pendientes Android says "test with User and Landlord accounts" is done, but the 18 Nov daily says **not yet checked**. **[TODO: resolve this conflict.]** | status says "Close" |
| [[Role-based screens]] | Visibility (`GONE`) · two activities · one host with fragments | One host with fragments, `GONE` for small differences | Not yet. Plan: log in as User and Landlord and call a landlord-only endpoint with a User account. | proposed |

**Empty decision notes** (status "taken", but no options, no sources, no validation): [[BCrypt for passwords]] · [[PostgreSQL as shared database]] · [[Retrofit for API calls]] · [[Java instead of Kotlin]] · [[SharedPreferences session]]. **[TODO: fill them or change their status. As they are, they show a decision without the reasoning, which is the opposite of what LO3 asks for.]**

## 5. Challenging my assumptions and iterating

This is the part I want to show most. Each row is an assumption I had, what challenged it, and what I changed.

| My assumption | What challenged it | What I changed |
| --- | --- | --- |
| A boolean `is_landlord` is enough for two roles | Houses need an owner with specific rules. New roles will come. | Java enum: two values now, easy to extend. |
| Two activities (one per role) is the clean option | Login, registration and profile would be duplicated. The nav graph still pointed to placeholder `FirstFragment` / `SecondFragment`. | One host activity with fragments; role decides the start screen and menu items. |
| The role is only needed at login | After restarting the phone the role was lost. | Stored in SharedPreferences, cleared on logout. |
| `@NotBlank` is fine for a new field | Old users had no role, so the `NOT NULL` column could not be added. The insert failed with a 500. | `@NotNull`, passed from `UserService`, and an SQL update for old users. Lost 90 min. Lesson recorded. |
| Creating houses is new work for landlords | Creating houses and expenses already work. | **[TODO: confirm what I did: adapt the existing endpoint or rebuild it.]** |
| Integration can be done at the end | Martin's warning; the eduCloud database was not ready on 16 Nov. | Integration moved into the planning as its own step, with a dependency on Daniel. |

## 6. Reflection (LO4) **[TODO: write this in your own words]**

Prompts from the feedback. Answer each one with an example from §3–§5:

- What did I know before this project, and what did I learn from Obsidian, the feedback sessions and the bugs?
- Which decision would I make differently today? (Each decision note has a "Review" section for this. Fill it at the end.)
- Which feedback changed my process, and which did I *not* follow? Why?
- What did the group do well, and what would I do differently in the next group sprint?

## 7. Evidence index

| Evidence | Where | Status |
| --- | --- | --- |
| Trello board, Sprint 3 | `Images/Trello_Sprint3_1.png` | Available |
| Role column in the database | `Images/Role_Column_DB.png` | Available |
| Role selector in the app | `Images/RolType_Selector.png` | Available |
| Enum class in Spring | `Images/Enum_Class_Spring.png` | Available |
| Group FeedPulse | `Images/Feedpulse_1.png` | Check: [[HouseMate]] still says missing |
| Feature map photo (11 Nov) | — | **Missing** |
| Five activities screenshots | — | **Missing** |
| User and Landlord home screens | pending list in `Claude/Evidence` | **Missing** (needs the role check) |
| Backend starts without connection errors | pending list in `Claude/Evidence` | **Missing** |

## 8. Before submitting: checklist

- [ ] Write the goal and close of Sprint 1 and Sprint 2. Mark them as *written from memory* if they are.
- [ ] Update the frontmatter of [[Sprint 3]] (`done: 0` is out of date).
- [ ] Resolve the status conflicts in §4.2.
- [ ] Fill or clean the five empty decision notes (§4.2).
- [ ] Fix the links to notes that do not exist: [[Software teacher - code review]] · [[Docker]] · [[Retrofit]] · [[LoginActivity]] (in the vault these are missing or named differently).
- [ ] Keep one place for decisions. Notes exist in both `Claude/Decisions` and `Projects/HouseMate/Decisions` for the same topics (role from login, SharedPreferences, fragments).
- [ ] Add the group decision on Website ↔ Spring Boot (§3, 13 Nov).
- [ ] Take the missing screenshots (§7).
- [ ] Write §6 in your own words.
