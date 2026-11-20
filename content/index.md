---
title: Portfolio LO3 · HouseMate
cssclasses:
  - portfolio
---
# Portfolio LO3 · Planning and process in HouseMate

> [!abstract] At a glance
> **Project:** HouseMate, an app to share a house: members, shared expenses, and tenant and landlord roles.
> **My part:** the Android app (Java) and the Spring Boot REST API.
> **Team:** Anushree (website) · Daniel (database) · Nikolay (website–API connection and IoT).
> **Hand-in:** 11 December 2026. This version covers Sprint 3 (16–22 November) and the planning that led to it.

> [!info] What this document shows
> For each part of the project I show **what I did**, **what I looked at** to decide, and **why** I chose it. Each decision links to its own note, so the reasoning can be followed step by step.

## 1. The plan

### 1.1 Sprint 3 goal

> [!success] Goal · 16–22 November
> Tenant and landlord roles, landlord views and logout.

### 1.2 Sprint 3 in blocks

The sprint has seven blocks and 19 steps. Each block has a "done when" sentence, so I can tell when it is finished ([[Sprint 3]]).

| Block | Done when | Progress |
| --- | --- | --- |
| 📝 Documentation and planning | Tasks split by person; role decision and endpoints documented | 🟩🟩⬜ 2 of 3 |
| 🎭 Roles | Every user has a role in the database and the app receives it at login | 🟩🟩🟩 3 of 3 |
| 🖥️ Views per role | Tenant and landlord see different screens after login | 🟩🟩🟩 3 of 3 |
| 🏠 Landlord: create houses | A landlord creates a house; a tenant cannot | 🟩🟩 2 of 2 |
| 💶 Expenses | List, add and open the detail of an expense | ⬜⬜⬜ 0 of 3 |
| 📊 IoT | The app shows IoT data in a chart | ⬜⬜⬜⬜ 0 of 4 |
| 🚪 Logout | Logout returns to login, and back does not re-enter | ⬜ 0 of 1 |

**Progress: 10 of 19 steps done.** The IoT block depends on data from another team member, so I planned it as a dependency rather than a step I control ([[Group_sprint 3]]).

### 1.3 Group split

| Member | Tasks in Group Sprint 3 | Note |
| --- | --- | --- |
| Raul | IoT ↔ Android, roles | Roles is my block. |
| Nikolay | IoT ↔ Android, website ↔ Spring Boot | IoT depends on his data. |
| Anushree | Website ↔ Spring Boot | |
| Daniel | Group tasks | Owns the shared database. |

Source: [[Group_sprint 3]].

## 2. How the plan came together

The plan changed after each input. This is the timeline.

> [!quote] 10 November · Frank
> Avoid an ambitious project with little time, and set clear group rules.
>
> **What I did:** group rules and regular meetings, each with a focus. Commitment improved and is still in progress. [[Frank - team rules and scope]]

> [!quote] 13 November · Martin
> Do not leave integration to the end, and document the project with diagrams, starting from a general view and zooming into each layer.
>
> **What I did:** I unified the back end into [[Spring Boot]], and I made diagrams per layer ([[Diagrams]]). [[Martin -Documentation on software development and useful technologies]]

> [!warning] 13 November · My review of Sprint 3
> Seven blocks in one week, and the IoT block depends on data I did not have yet.
>
> **What I did:** a MoSCoW proposal for the sprint (section 2.4).

> [!warning] 13 November · Group review
> Four integrations in one week.
>
> **What I did:** Website ↔ Spring Boot became the candidate to move to Sprint 4. [[Group_sprint 3]]

> [!info] 16 November · Chris
> Explain the documentation with concrete steps and evidence, not with opinions.
>
> **What I did:** I restructured the documentation around the decisions and the knowledge I used. [[Daily 2026-11-16]]

> [!failure] 16 November · Shared database
> I could not connect to the shared database from eduCloud.
>
> **What I did:** I ran the backend against the database on my own machine, and I recorded the dependency on Daniel. [[PostgreSQL as shared database]]

> [!bug] 17 November · Role column
> Existing users had no role, so the new required column failed. This cost 90 minutes.
>
> **What I did:** I found the root cause, applied the fix and recorded the lesson. [[Null enum in DB]]

> [!info] 17 November · Frank
> The planned talk did not happen.
>
> **What I did:** I moved the topics (documentation and Obsidian documents as Markdown) to Teams messages. [[Daily 2026-11-17]]

> [!tip] 18 November · Chris
> Explain the "why" of each decision, and ask for feedback every week, not only at the end.
>
> **What I did:** I started this document and a weekly feedback routine.

> [!success] 18 November · Role-based screens
> Choosing between two activities, hiding views inside each activity, or one host with fragments.
>
> **What I did:** I chose one host with fragments, and I updated the navigation graph the same day. [[Role-based screens]]

> [!example] 19 November · Evidence
> Screenshots of the backend running, the database running in Docker, the five activities, and the tenant and landlord home screens.

> [!failure] 20 November · House button
> Pressing "House" showed "Please check the data you entered" and closed the screen, before any request was sent.
>
> **What I did:** I traced the code and found that the login screen saved the user id in SharedPreferences but did not send it in the Intent to the next screen. I added the values to the Intent, and I recorded the lesson. [[Fail with Intents through activites]]

### 2.4 MoSCoW for Sprint 3 (proposed 13 November)

| Priority | Blocks | Why |
| --- | --- | --- |
| 🔴 Must | Roles · Views per role · Logout · Documentation | Without roles, the other blocks have no meaning. |
| 🟠 Should | Landlord: create houses · IoT: analyse data and endpoint | Needed, but IoT depends on someone else's data. |
| 🟡 Could | Expenses | Part of it already works. |
| 🔵 Next sprint | IoT logic and chart | Depends on data that does not exist yet. |

Anything that moves to Sprint 4 is written as a decision in the sprint's "MoSCoW changes", not as "no time".

## 3. Was the scope right?

> [!warning] Short answer: not for Sprint 3 as planned
> - **The views depend on the roles.** The role column only worked on 17 November, so by 18 November five days were left for three blocks.
> - **The group warning was not in my plan.** Frank had warned about an ambitious plan on 10 November, and I did not turn that warning into a step with a date.
> - **The IoT dependency was known but not managed.** I wrote it down on 13 November, but I did not give it a date.

> [!tip] What I would change
> Decide the Must and Should blocks on the first day of the sprint, and give every dependency its own step, with an owner and a date.

## 4. What I looked at

| Source | Type | What it gave me | Used in |
| --- | --- | --- | --- |
| Frank (10 November) | Feedback session | Group rules, scope, and shared documents in the portfolio | Sections 2 and 3 |
| Martin (13 November) | Feedback session | Diagrams (C4), integrate early, a clear endpoints document | Sections 2 and 6 |
| Chris (16 and 18 November) | Feedback | Concrete LO3 steps, explain the "why", weekly feedback | Sections 2 and 9 |
| c4model.com | Website, recommended by Martin | Levels of diagrams: general view first, then each layer | [[Diagrams]] |
| Android Developers: SharedPreferences | Documentation | How to keep small data between sessions | [[SharedPreferences session]] |
| Android Developers: Navigation, start destination | Documentation | How the start screen is chosen | [[Role-based screens]] |
| Android Developers: Kotlin and Java | Documentation | How the two languages work together | [[Java instead of Kotlin]] |
| Spring Security and OWASP: password storage | Documentation | Why passwords must be stored as hashes | [[BCrypt for passwords]] |
| Baeldung: Retrofit tutorial | Tutorial | How Retrofit turns API calls into Java methods | [[Retrofit for API calls]] |
| howtodoinjava: NotBlank vs NotNull | Article | Why a new field fails on existing rows | [[Null enum in DB]] |
| My own code | Code check (16 November) | What the backend already does with roles | [[Role type]] |
| Trello board | Board | Who does what, and the workload | [[Group_sprint 3]] |
| My own trace of the code and the Logcat (20 November) | Debugging | Why the House button closed before any request | [[Fail with Intents through activites]] |
| Daily notes | My logs | What happened each day | [[Daily 2026-11-16]] · [[Daily 2026-11-17]] · [[Daily 2026-11-18]] |

## 5. Decisions

> [!info] How to read each decision
> Question · options compared · what I chose · why · how I checked it. The full notes are linked from each title.

### 5.1 Role type

> [!success] Java enum `RoleType { User, Landlord }`, stored as text · [[Role type]]
> **Question:** how to store whether a user is a tenant or a landlord.
> **Options:** a yes/no column · a number code · a Java enum · two tables.
> **Why:** an enum has names instead of numbers, the compiler rejects invalid values, and a new role only needs a new value.
> **Checked:** the code check on 16 November, and the fix in the database on 17 November.

### 5.2 Where the role is saved

> [!success] At login, using SharedPreferences · [[Rol saved from Login]]
> **Question:** when to save the role on the phone, so the app knows the user's view after restarting.
> **Options:** save at registration · pass it between screens with Intents · save at login.
> **Why:** registration does not start a session, so the login response is the moment the app learns the role.

### 5.3 Role-based screens

> [!success] One host activity with fragments · [[Role-based screens]]
> **Question:** how to show different screens to tenants and landlords.
> **Options:** hide buttons inside each screen · two activities · one host activity with fragments.
> **Why:** two activities would copy login, registration and the profile screen, and a new role would need a new activity. Fragments keep the role logic in one place.
> **Checked:** the two home screens are captured, one for each role (section 7).

### 5.4 Keeping the session

> [!success] SharedPreferences, with Intents for the next screen · [[SharedPreferences session]]
> **Question:** how the app remembers the user and the role after closing the app.
> **Options:** keep data only while the app runs · pass it with Intents · save it with SharedPreferences.
> **Why:** Intents only last while the screens are open, and the role is needed after a restart. The password is never saved.

### 5.5 Password storage

> [!success] BCrypt · [[BCrypt for passwords]]
> **Question:** how to store passwords so a leak does not reveal them.
> **Options:** plain text · a fast hash without salt · BCrypt · Argon2 or scrypt.
> **Why:** Spring Security already provides BCrypt, and it adds a random part to each password, so two equal passwords do not produce the same stored value.
> **Checked:** the stored password is not readable, and a wrong password does not log in ([[Endpoints]]).

### 5.6 Shared database

> [!success] PostgreSQL on the shared server · [[PostgreSQL as shared database]]
> **Question:** where the group's data is stored.
> **Options:** H2 · SQLite · MySQL · PostgreSQL on the shared server.
> **Why:** Daniel had already set up the server, and one database avoids copies that do not match.
> **Checked:** the backend starts and connects (18 November), and a schema change worked on the shared database (17 November).

### 5.7 Calls to the API

> [!success] Retrofit, with one interface per area · [[Retrofit for API calls]]
> **Question:** how the Android app calls the API.
> **Options:** `HttpURLConnection` · OkHttp alone · Retrofit.
> **Why:** each API area is a Java interface, and JSON conversion is built in. The endpoints the app uses are listed in [[Endpoints]].

### 5.8 Java instead of Kotlin

> [!success] Java for the app and the back end · [[Java instead of Kotlin]]
> **Question:** which language to use for the app and the back end.
> **Options:** Kotlin · Java.
> **Why:** the back end is in Java, and one language is easier to share in a team. Kotlin would be the better choice for an Android app on its own, but it would split the team's knowledge.
> **Checked:** the backend starts in Java, and the Android app runs with test accounts.

## 6. Assumptions I challenged

| My assumption | What challenged it | What I changed |
| --- | --- | --- |
| A yes/no field is enough for two roles. | A new role would mean a new column. | A Java enum with named values ([[Role type]]). |
| Two activities, one per role, are simpler. | Login and the profile would be copied, and the navigation graph still pointed to placeholder screens. | One host with fragments ([[Role-based screens]]). |
| The role is only needed at login. | After closing the app, the role was lost. | Saved on the phone and cleared at logout ([[SharedPreferences session]]). |
| A new required field is safe to add. | Existing users had no role, so the change failed. | A value for existing users, and the fix recorded ([[Null enum in DB]]). |
| Integration can be left to the end. | Martin's warning, and the shared database was not ready on 16 November. | Integration became a step with a dependency on Daniel. |
| A simple password hash is enough. | A simple hash can be broken quickly. | BCrypt ([[BCrypt for passwords]]). |
| Kotlin is the obvious choice for Android. | The back end is in Java, and the team needs one language. | Java on both sides ([[Java instead of Kotlin]]). |
| Feedback at the end of the project is enough. | Chris asked for feedback during the project. | A weekly feedback routine, starting with this document. |
| Data saved at login is available on the next screen. | The fragments read the Intent, which was empty, so the House button closed. | The values are sent with `putExtra` as well ([[Fail with Intents through activites]]). |

## 7. Evidence

### 7.1 Tenant and landlord screens

> [!example] The same app, two roles
> The role decides which home screen opens after login.

![[Images/User_Activity.png]]

![[Images/Landlord_Activity.png]]

### 7.2 The five activities and the running backend

> [!example] The app and the backend
> The five activities of the app, the backend running, and the database running in Docker.

![[Images/5_Activities.png]]

![[Images/BackEnd_Running.png]]

![[Images/SQL_Running_Docker.png]]

### 7.3 Roles in the database and the app

> [!example] The role, from the database to the screen
> The role column in the database, the Java enum, and the selector in the registration screen.

![[Images/Role_Column_DB.png]]

![[Images/Enum_Class_Spring.png]]

![[Images/RolType_Selector.png]]

### 7.4 Group work and feedback

> [!example] Group work and feedback
> The Trello board for Sprint 3, the group FeedPulse, and the structure diagram.

![[Images/Trello_Sprint3_1.png]]

![[Images/Feedpulse_1.png]]

![[Images/FeedPulse_2.png]]

![[Images/Structure_Diagram.png]]

## 8. What comes next

> [!tip] Next steps
> - Test the role views and the House button fix on the emulator, with a tenant account and a landlord account.
> - Done: the back end now rejects a tenant creating a house, and a landlord joining one (403).
> - Logout and expenses move to Sprint 4, as recorded in the sprint's MoSCoW changes.

## 9. Feedback loop

> [!quote] What changed after Chris's feedback
> Feedback is now part of the process, not only the final step.
>
> - **Every week:** I ask for feedback on one decision and one change to the plan.
> - **Every change:** I record what the feedback changed in this document.
> - **Every decision:** I keep its options, its reason and its checks in its own note.
