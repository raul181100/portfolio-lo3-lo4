---
type: sprint
week: 47
start: 2026-11-16
end: 2026-11-22
planned: 7
done: 0
cssclasses:
  - sprint
---
# Sprint 3

> [!goal] Goal · 16–22 Nov
> Tenant and landlord roles, landlord views, logout
>
> Group plan: [[Group_sprint 3]]

## Planned tasks

> [!docs]+ Documentation & planning
> - [ ] Split the [[Group_sprint 3]] tasks by person (note + Trello)
> - [ ] Fill in the [[Role type]] decision and add new endpoints to [[Endpoints]]
> - [ ] Friday: screenshots → Evidence, fill in "Close"

> [!roles]+ Roles — [[Role type]]
> *Done when: every user has a role (tenant / landlord) saved in the database and the app receives it at login.*
> - [ ] Backend: `role` column in `users` (with Daniel) + `Role` enum in the User entity
> - [ ] Accept the role at registration and return it at login
> - [ ] Android: role selector at registration, save the role after login

> [!views]+ Views per role
> *Done when: tenant and landlord see different screens after login.*
> - [ ] Open the landlord or tenant home depending on the role
> - [ ] Layouts for both homes (hide landlord-only buttons for tenants)
> - [ ] Endpoint + display of the specific data for each role

> [!landlord]+ Landlord — create houses
> *Done when: a landlord can create a house and see it in their list; a tenant cannot.*
> - [ ] Backend: only landlords can create houses, linked to their account
> - [ ] Android: "Create house" button only in the landlord view

> [!expenses]+ Expenses
> *Done when: in a house you see the expenses in a list, can add one and open its detail.*
> - [ ] Add expenses to an existing house (endpoint + Android form)
> - [ ] RecyclerView for expenses (adapter + load with Retrofit)
> - [ ] Activity for each expense (tap an item → detail)

> [!iot]+ IoT — [[IoT devices]]
> *Done when: the app shows IoT data from the backend in a chart.*
> ⚠️ **Depends on Nikolay's data**
> - [ ] Get and analyse Nikolay's data → write it in [[IoT devices]]
> - [ ] Endpoint to receive and serve the readings
> - [ ] Logic based on the collected data
> - [ ] Screen with a chart of the data

> [!logout]+ Logout
> *Done when: logout takes you back to login and the back button doesn't let you in again.*
> - [ ] Logout button that clears the session and returns to login

## Review (13 Nov)

> [!abstract]- Summary
> Well organised, but heavy: 7 blocks in one week, with meetings Mon/Wed/Fri and work Fri–Sun. The IoT block depends on data I don't have yet.

> [!example]- Proposal: MoSCoW for this week
> | Priority | Blocks |
> | --- | --- |
> | **Must** | Roles · Views per role · Logout · Documentation |
> | **Should** | Landlord — create houses · IoT: analyse data + endpoint |
> | **Could** | Expenses |
> | **Next sprint** | IoT logic + chart |
> Whatever moves to Sprint 4 goes in "MoSCoW changes" as a decision, not as "no time".

> [!question]- To clarify
> Creating houses and expenses **already work** according to [[HouseMate]]. Check whether "Landlord — create houses" and "Add expenses" mean adapting them, so the work isn't repeated.

> [!todo] Before Monday 16
> - [ ] Close [[Sprint 2]] and fill in [[Sprint 1]] from memory
> - [ ] Ask Nikolay for the IoT data
> - [ ] Fill in the empty notes: [[Role type]] (enum vs roles table), [[Landlord rol]], [[IoT devices]]

## Close & evidence

> [!close]- Close (Friday)
> **Done:** 
> **Not done, and why:** 
> **Deviation from plan and cause:** 
> **Bugs this week:** [[ ]]
> **Decisions this week:** [[ ]]
> **MoSCoW changes:** 
> **What I change next week:** 

> [!example] Evidence
> - Board screenshot: 
