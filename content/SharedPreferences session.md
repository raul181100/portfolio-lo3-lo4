---
type: decision
date: 2026-11-18
status: taken
cssclasses:
  - decision
---
# SharedPreferences session

## Context
For my system, I needed a way to store information persistently. This information is necessary to keep my user logged in and to determine the user's role. That role will be used to display different views depending on the user's role.

## Options
| Option                                                  | For                                                              | Against                                                                                                    |
| ------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Store the information indefinitely on the user's device | Data is saved across sessions. Access it at any time.            | Anyone with access to the device would have access to the user's credentials even if the app isn't running |
| Send information using intents through activities       | Easy to program. It performs the function of sending information | The need to send the same information multiple times from one activity to another                          |
| Save the information to a SharedPreferences object      | Store the information persistently during the session            | Code that's a little longer than the other options                                                         |

## Chosen, and why
I've decided to use SharedPreferences because it meets the requirements of my project. With SharedPreferences, I can save my user's information when they log in and keep it throughout the session. It can even save the session when the app is closed for a while.

## Sources
- [Android SharedPreferences](https://developer.android.com/training/data-storage/shared-preferences)

## How I validated it
I verified this by creating two types of users and logging into the application with each user's credentials. Both users were shown a different view that had been previously configured for their respective roles.
## Review
For small data types, such as a role type or a single piece of information, I would probably use SharedPreferences again, but to store larger amounts of data, I would use a database directly.