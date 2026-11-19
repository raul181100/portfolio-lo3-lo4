---
type: decision
date: 2026-11-18
status: Close
cssclasses:
  - decision
---
# Role-based screens

> [!abstract] 🧭 Context
> For my project HouseMate the backend stores each user with a role (`User` or `Landlord`, Java enum `RoleType`, see [[Role type]]). The Android app has to show different things depending on that role: a landlord sees house management, a user sees their expenses.
>
> Right now the app has five activities: LoginActivity, RegisterActivity, HouseActivity, UserActivity and ExpenseActivity. The role does not reach the app yet: the backend `UserResponse` already contains `role`, but the Android `UserResponse` DTO has no role field, and after login the app always opens `UserActivity`.
>
> 📅 Decision needed before Sprint 3 (16–22 Nov).

## ⚖️ Options

|     | Option                                                                                 | For ✅                                                                                                         | Against ❌                                                                                                       |
| --- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| 1   | `View.GONE` / `INVISIBLE` inside each activity, based on role                          | No new structure; fast to do                                                                                  | Role `if`s spread across activities; hiding is not security; gets messy as roles grow                           |
| 2   | Two separate activities (one per role)                                                 | Clear separation; each screen is simple                                                                       | Duplicated code (login, profile, shared lists); login must choose the right one; a role change needs a new flow |
| 3   | ⭐ One host activity with fragments, role decides which fragments and menu items appear | Shared screens are written once; role logic in one place; matches the Navigation graph already in the project | More setup at the start; the activity count drops (see consequences)                                            |

## ✅ Chosen, and why

> [!success] Proposed: option 3, with `.GONE` only for small differences
> I would host the role-specific screens in one activity with fragments, and let the role choose the start destination and the menu items. This keeps role logic in one place instead of in every screen.
>
> Plan:
> 1. The backend already returns the role in the login response; the app adds the field to its DTO, passes it to the next screen and stores it (SharedPreferences) so logout and restarts work.
> 2. One place maps role → what to show (start screen, menu items). Screens do not compare the enum themselves.
> 3. Screens shared by both roles are written once. Small differences inside a shared screen (one extra button) use `.GONE`, driven by that same mapping.
> 4. Roles are checked again on the backend. Hiding a button on Android is only a UI choice.
>
> I did not choose two activities because login, registration and profile would be duplicated, and a new role would mean a new activity.

## ⚠️ Consequences

> [!warning] Things to keep in mind
> - **Activities:** 5 today (declared in AndroidManifest.xml). 
> - **nav_graph.xml:** points to `FirstFragment` / `SecondFragment`, which don't exist. Replace it. DONE
> - **Role storage:** the role isn't saved on the device yet, so it's lost on restart. Save it in SharedPreferences, clear it on logout.
> - **Backend:** the role is stored and returned, but no endpoint checks it. Landlord rules go in the service layer ([[Role type]]).

## 📚 Sources
- Android docs: Navigation component, start destination
- Course evidence list in HouseMate

## 🧪 How I validated it
- Not yet. Plan: log in as a `User` and as a `Landlord` and check that each sees the right screen. Also call the landlord-only endpoint with a `User` account and check the backend returns an error.

## 🔍 Review
