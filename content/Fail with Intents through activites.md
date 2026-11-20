---
type: bug
date: 2026-11-20
status: solved
area: "Intents between LoginActivity and UserActivity"
time_lost: 
cssclasses:
  - bug
---
# Fail with Intents through activites

## What happened

> [!info] Expected
> When I press the "House" button in UserActivity, HouseActivity opens and shows my house, or the buttons to join or create one.

> [!failure] Actual
> A toast "Please check the data you entered" appears and HouseActivity closes straight away. This happens before any network call, so the backend never receives a request.

## What I tried (in order)
1. Checked the backend for join-code and role errors (`HouseService`, `HouseController`). Not the cause: the app closes before it sends anything.
2. Checked the database hypothesis (`User.role` as NOT NULL with `ddl-auto: update`). The backend log showed no SQL or Hibernate errors.
3. Read the Logcat from the emulator. The only message was the guard in HouseActivity, not a crash in the network code.
4. Traced `HouseActivity.onCreate()`: if `userId == -1` it shows `invalid_data` and calls `finish()`.
5. Traced where the `-1` comes from: `UserHomeFragment` and `LandlordHomeFragment` read `EXTRA_USER_ID` from `requireActivity().getIntent()`, with `-1` as the default.
6. Checked `LoginActivity.openUserWindow()`: it saved the data in SharedPreferences but never called `putExtra`, so the Intent to UserActivity was empty.

## Real cause

> [!warning] Real cause
> SharedPreferences and Intent extras are different things. At login the data was saved in SharedPreferences, but the Intent that opens UserActivity carried no data. The fragments read the user id from the Intent, got the default `-1`, and HouseActivity rejected it.

## Solution

> [!success] Solution
> In `LoginActivity.openUserWindow()` send the four values in the Intent before `startActivity()`:
> ```java
> intent.putExtra(UserActivity.EXTRA_USER_ID, user.id);
> intent.putExtra(UserActivity.EXTRA_USERNAME, user.username);
> intent.putExtra(UserActivity.EXTRA_EMAIL, user.email);
> intent.putExtra(UserActivity.EXTRA_ROLE, user.role);
> ```
> The SharedPreferences writes stay, because HouseActivity reads the role from there.

## Source that helped
- My own step-by-step trace of the code and the Logcat. No external source.

## Evidence
- Code: `app/src/main/java/com/example/housemate/ui/LoginActivity.java` lines 125–141 (`openUserWindow`).
- Logcat from the emulator at 10:09:19 (LoginActivity → UserActivity), showing the guard message.
- Compiled OK. Emulator check still pending: press House and confirm HouseActivity opens.

## Reusable lesson

> [!tip] Lesson
> Data saved in SharedPreferences is not visible to an Activity or Fragment that reads `getIntent()`. If the next screen reads from the Intent, send the values with `putExtra()`.
> → to add to Knowledge: Android Intents (no note exists yet)
