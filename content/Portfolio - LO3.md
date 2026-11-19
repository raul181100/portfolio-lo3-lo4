---
type: portfolio
learning-outcome: LO3
status: draft
updated: 2026-11-18
hand-in: 2026-12-11
cssclasses:
  - portfolio
---
# Portfolio LO3: planning and process in HouseMate

> [!info] About this document
> This document covers LO3 only: how I planned the project, what I looked at to make the plan, and why I made each choice. Following Chris's feedback (16 and 18 Nov), it focuses on concrete steps and the reasons behind them.
>
> Status on 18 November 2026. Items marked **[TODO]** still need evidence or confirmation.

## 1. The project in brief

- **Product:** HouseMate, an app to share a house: houses, members, shared expenses, and, from Sprint 3, two roles: tenant and landlord ([[HouseMate]]).
- **My part:** the Android app (Java) and the Spring Boot REST API ([[Endpoints]]).
- **Team:** Anushree (website), Daniel (database), Nikolay (website–API connection and IoT). We meet on Monday, Wednesday and Friday.
- **Hand-in:** 11 December 2026.

## 2. The plan

### 2.1 Sprints

| Sprint | Dates | Goal | Status on 18 Nov |
| --- | --- | --- | --- |
| 1 | 2–8 Nov | **[TODO: goal not written]** | Registration and login work ([[HouseMate]]) |
| 2 | 9–15 Nov | **[TODO: goal not written]** | House creation, joining by code and expense split work ([[HouseMate]]) |
| 3 | 16–22 Nov | Tenant and landlord roles, landlord views, logout | In progress (see 2.2) |
| 4 | 23–29 Nov | **[TODO]** | Not started |
| 5 | 30 Nov–6 Dec | **[TODO]** | Not started |
| 6 | 7–11 Dec | **[TODO]** | Not started |

Sprints 1 and 2 were not filled in during the sprint. **[TODO: write their goals and closes, and say clearly that they were written afterwards.]** See [[Sprint 1]] and [[Sprint 2]].

### 2.2 Sprint 3 in steps

The sprint has seven blocks and 19 steps. Each block has a "Done when" sentence, so I can tell if it is finished ([[Sprint 3]]).

| Block | Done when | Steps | Status on 18 Nov |
| --- | --- | --- | --- |
| Documentation and planning | Group tasks split by person; role decision and endpoints documented | 3 | Group split done ([[Group_sprint 3]]). Role decisions documented. The endpoints note still needs the new role endpoints. |
| Roles | Every user has a role in the database and the app receives it at login | 3 | Enum and column done (16–17 Nov). Registration saves the role (17 Nov). The app reads the role at login. End-to-end test not confirmed (see §8). |
| Views per role | Tenant and landlord see different screens after login | 3 | Navigation graph and the two home fragments created (18 Nov). Not tested yet. |
| Landlord: create houses | A landlord can create a house; a tenant cannot | 2 | Not started. No endpoint checks the role yet ([[Pendientes Android]]). |
| Expenses | A list of expenses, adding one, and opening its detail | 3 | List works. Adding and the detail screen are not in the app yet ([[Endpoints]]). |
| IoT | The app shows IoT data in a chart | 4 | Waiting for Nikolay's data ([[IoT devices]]). |
| Logout | Logout returns to login; back does not return into the app | 1 | **[TODO: status]** |

### 2.3 Group level

| Member | Tasks in Group Sprint 3 | Note |
| --- | --- | --- |
| Raul | IoT ↔ Android, roles | Roles is my block. Four cards on the board alone ([[Group_sprint 3]]). |
| Nikolay | IoT ↔ Android, website ↔ Spring Boot | IoT depends on his data. |
| Anushree | Website ↔ Spring Boot | |
| Daniel | Group tasks | Owns the shared database. |

## 3. How I arrived at the plan

The plan changed after each input. This is the timeline.

| Date | Input | What I did with it |
| --- | --- | --- |
| 10 Nov | Frank: avoid an ambitious project with little time; set group rules. | Group rules and regular meetings, each with a focus. Commitment improved but is still in progress. [[Frank - team rules and scope]] |
| 13 Nov | Martin: do not leave integration to the end; document with diagrams (C4). | Back end unified into [[Spring Boot]]; diagrams per layer ([[Diagrams]]). [[Martin -Documentation on software development and useful technologies]] |
| 13 Nov | My review of Sprint 3: seven blocks in one week, and IoT depends on data I do not have. | A MoSCoW proposal for the sprint (§3.1). |
| 13 Nov | Group review: four integrations in one week. | Website ↔ Spring Boot is the candidate to move to Sprint 4. **[TODO: confirm what the group decided on Monday 16.]** [[Group_sprint 3]] |
| 16 Nov | Talk with Chris about LO3: concrete steps and evidence. | I prepared questions and restructured the documentation around decisions. [[Chris 2026-11-16]] |
| 16 Nov | I could not connect to the shared database from eduCloud. | I ran the backend against the database on my own machine. Dependency on Daniel noted. [[PostgreSQL as shared database]] |
| 17 Nov | The role column failed on existing users (90 minutes lost). | Root cause found; fix applied; lesson noted. [[Null enum in DB]] |
| 17 Nov | Frank did not attend the planned talk. | I moved the topics (documentation, Obsidian documents as Markdown) to Teams messages. [[Daily 2026-11-17]] |
| 18 Nov | Chris: LO3 should be pragmatic and explain the "why"; ask for feedback every week. | This document, and a weekly feedback request. [[Chris - Portfolio_2 Review]] |
| 18 Nov | Role-based screens: two activities, one activity with visibility changes, or one host with fragments. | Fragments chosen; navigation graph updated the same day. [[Role-based screens]] |

### 3.1 MoSCoW for Sprint 3 (proposed 13 Nov)

| Priority | Blocks | Why |
| --- | --- | --- |
| Must | Roles · Views per role · Logout · Documentation | Without roles, the other blocks have no meaning. |
| Should | Landlord: create houses · IoT: analyse data and endpoint | Needed, but IoT depends on someone else's data. |
| Could | Expenses | Part of it already works ([[HouseMate]]). |
| Next sprint | IoT logic and chart | Depends on data that does not exist yet. |

Whatever moves to Sprint 4 is written as a decision in the sprint's "MoSCoW changes", not as "no time".

## 4. Was the scope right?

**Not for Sprint 3 as planned.** Three things show it:

- The views block needs roles to be saved first. The role column was only working on 17 Nov, so by 18 Nov five days were left for three blocks.
- The group had four integrations in one week. Frank had warned about this on 10 Nov, and I did not put the warning into my own plan.
- The IoT block depended on another person's data from the start. I wrote this down on 13 Nov but did not turn it into a step with a date.

**What I would change:** decide the Must and Should blocks on the first day of the sprint, and give every dependency its own step with an owner and a date.

## 5. What I looked at and where the information came from

| Source | Type | What it gave me | Used in |
| --- | --- | --- | --- |
| Frank (10 Nov) | Feedback session | Group rules; scope; the portfolio can contain shared documents | §3, §4 |
| Martin (13 Nov) | Feedback session | Diagrams (C4); integrate early; the endpoints document was clear | §3, §6 |
| Chris (16 and 18 Nov) | Feedback and questions | LO3 should be concrete and explain the why; weekly feedback | §3, §8 |
| c4model.com (recommended by Martin) | Website | Levels of diagrams: a general view, then zoom in by layer | [[Diagrams]] |
| Android Developers: SharedPreferences | Documentation | How to save small data between sessions | [[SharedPreferences session]] |
| Android Developers: Navigation, start destination | Documentation | How the start screen is chosen | [[Role-based screens]] |
| Android Developers: Kotlin and Java | Documentation | How the two languages work together | [[Java instead of Kotlin]] |
| Spring Security and OWASP: password storage | Documentation | Why passwords must be stored as hashes | [[BCrypt for passwords]] |
| Baeldung: Retrofit tutorial | Tutorial | How Retrofit turns API calls into Java methods | [[Retrofit for API calls]] |
| howtodoinjava: NotBlank vs NotNull | Article | Why a new field fails on old rows | [[Null enum in DB]] |
| My own code | Code check (16 Nov) | What the backend already does with roles | [[Role type]] |
| Trello board | Board | Who does what, and the workload | [[Group_sprint 3]] |
| Daily notes | My logs | What happened each day | [[Daily 2026-11-16]], [[Daily 2026-11-17]], [[Daily 2026-11-18]] |

## 6. Decisions and how I checked them

Each decision has its own note with the options, the reason and the checks. Here is the summary.

### 6.1 Role type
- **Question:** how to store whether a user is a tenant or a landlord.
- **Options:** boolean column · number code · Java enum · two tables.
- **Chosen:** Java enum `RoleType`, stored as text. It is easy to read in the database, and a new role only needs a new value.
- **Checked:** code check on 16 Nov; the fix worked in the database on 17 Nov ([[Role type]]).
- **Status:** taken.

### 6.2 Where the role is saved
- **Question:** when to save the role on the phone, so the app knows the user's view after restarting.
- **Options:** save at registration · pass it between screens with Intents · save at login.
- **Chosen:** save at login. Registration does not start a session, so the login response is the moment the app knows the role ([[Rol saved from Login]]).
- **Checked:** **[TODO: conflict, see §8.]**
- **Status:** taken.

### 6.3 Role-based screens
- **Question:** how to show different screens to tenants and landlords.
- **Options:** hide buttons inside each screen · two activities · one host activity with fragments.
- **Chosen:** one host activity with fragments. The role decides the start screen and the menu. Login and registration stay as activities.
- **Why:** two activities would copy login, registration and the profile screen, and a new role would mean a new activity.
- **Checked:** not yet. The plan is to log in with a tenant and a landlord account and to check that the backend refuses a landlord-only action for a tenant ([[Role-based screens]]).
- **Status:** the note still says "proposed". I decided it on 18 Nov ([[Daily 2026-11-18]]). **[TODO: update the status.]**

### 6.4 Keeping the session
- **Question:** how the app remembers the user and the role after closing the app.
- **Options:** keep the data only while the app runs · pass it with Intents · save it with SharedPreferences.
- **Chosen:** SharedPreferences, under one file name, with Intents still used to pass the role to the next screen ([[SharedPreferences session]]).
- **Why:** Intents only last while the screens are open, and I need the role after a restart. The password is never saved.
- **Checked:** **[TODO: conflict, see §8.]**
- **Status:** taken.

### 6.5 BCrypt for passwords
- **Question:** how to store passwords so a leak does not reveal them.
- **Options:** plain text · a fast hash without salt · BCrypt · Argon2 or scrypt (not compared in depth).
- **Chosen:** BCrypt, because Spring Security already provides it, and it adds a random part to each password.
- **Checked:** **[TODO: confirm, see the decision note.]**
- **Status:** taken ([[BCrypt for passwords]]).

### 6.6 PostgreSQL as shared database
- **Question:** where the group's data is stored.
- **Options:** H2 · SQLite · MySQL · PostgreSQL on the shared server.
- **Chosen:** PostgreSQL on the shared server. Daniel already set it up, and one database avoids copies that do not match.
- **Checked:** the backend starts and connects (18 Nov). A schema change worked on the shared database (17 Nov). **[TODO: check that one member's data is visible to the others.]**
- **Status:** taken ([[PostgreSQL as shared database]]).

### 6.7 Retrofit for API calls
- **Question:** how the Android app calls the API.
- **Options:** `HttpURLConnection` · OkHttp alone · Retrofit.
- **Chosen:** Retrofit, with one interface per area of the API: `UserApi`, `HouseApi`, `ExpenseApi`.
- **Checked:** the endpoints the app uses are listed in [[Endpoints]]. **[TODO: device test.]**
- **Status:** taken ([[Retrofit for API calls]]).

### 6.8 Java instead of Kotlin
- **Question:** which language to use for the app and the back end.
- **Options:** Kotlin · Java.
- **Chosen:** Java. The team's back end is in Java, and one language is easier to share. Kotlin would be the better choice for an Android app on its own.
- **Checked:** the backend starts in Java (18 Nov). **[TODO: confirm the Android part.]**
- **Status:** taken ([[Java instead of Kotlin]]).

## 7. Assumptions I challenged

| My assumption | What challenged it | What I changed |
| --- | --- | --- |
| A yes/no field is enough for two roles. | A new role would mean a new column. | A Java enum with named values ([[Role type]]). |
| Two activities, one per role, are simpler. | Login and the profile would be copied, and the navigation graph still pointed to placeholder screens. | One host with fragments ([[Role-based screens]]). |
| The role is only needed at login. | After closing the app, the role was lost. | Saved on the phone and cleared at logout ([[SharedPreferences session]]). |
| A new required field is safe to add. | Existing users had no role, so the change failed. | A required field, a value for old users, and the fix recorded ([[Null enum in DB]]). |
| Creating houses for landlords is new work. | The app already creates houses. | **[TODO: did you adapt the existing feature or rebuild it?]** |
| Integration can be left to the end. | Martin's warning, and the shared database was not ready on 16 Nov. | Integration became a step with a dependency on Daniel. |
| Passwords can be stored in a simple way. | A simple hash can be broken quickly. | BCrypt ([[BCrypt for passwords]]). |
| Kotlin is the obvious choice for Android. | The back end is in Java, and the team has to share one language. | Java for both sides ([[Java instead of Kotlin]]). |
| Feedback at the end of the project is enough. | Chris asked for feedback during the project. | A weekly feedback request, starting with this document (§8). |

## 8. Validation and feedback

### 8.1 What has been checked

| Item | Evidence | Status |
| --- | --- | --- |
| Role enum and database column | Code check 16 Nov; column in the database 17 Nov ([[Role type]]) | Checked |
| Role at login with two accounts | [[Pendientes Android]] marks "test with User and Landlord accounts" as done. The 18 Nov daily note says the same test is **not checked yet** ([[Daily 2026-11-18]]). The session note says it was done ([[SharedPreferences session]]). | **Conflict: [TODO: give the date of the test, or leave it open.]** |
| Views per role | Not yet tested | Pending |
| Backend connects to the shared database | Backend starts on 18 Nov ([[Diario 2026-11-18]]) | Checked |
| Java on both sides | Backend starts. Android build status conflicts between notes. | **[TODO]** |

### 8.2 Weekly validation

Chris suggested asking for feedback every week, not only at the end. From the next session, I will bring one decision and one plan change, and note what the feedback changed in this document.

## 9. Evidence

| Evidence | Status |
| --- | --- |
| Trello board, Sprint 3 | Available ![[Images/Trello_Sprint3_1.png]] |
| Role column in the database | Available ![[Images/Role_Column_DB.png]] |
| Role selector in the app | Available ![[Images/RolType_Selector.png]] |
| Enum class in Spring | Available ![[Images/Enum_Class_Spring.png]] |
| Group FeedPulse | Available ![[Images/Feedpulse_1.png]] |
| Second FeedPulse (Martin's feedback) | Available ![[Images/FeedPulse_2.png]] |
| Structure diagram | Available ![[Images/Structure Diagram.png]] |
| Feature map photo (11 Nov) | **Missing** |
| Five activities | **Missing** |
| Tenant and landlord home screens | **Missing** (needs the role test) |
| Backend starting without connection errors | **Missing** |

## 10. Before hand-in

- [ ] Resolve the role test conflict in §8.1.
- [ ] Update the status of [[Role-based screens]] to taken.
- [ ] Write the goals and closes of Sprints 1 and 2.
- [ ] Fill in the close of [[Sprint 3]] on Friday 20 Nov.
- [ ] Confirm the group decision about Website ↔ Spring Boot (§3).
- [ ] Fill in every **[TODO]** in §2–§8 with evidence you actually have.
- [ ] Take the missing screenshots (§9).
- [ ] Decide whether the duplicated decision notes in `Claude/Decisions` should be merged into `Projects/HouseMate/Decisions`.
