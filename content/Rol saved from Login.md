---
type: decision
date: 2026-11-18
status: Close
cssclasses:
  - decision
---
# Rol saved from Login

> [!abstract] 🧭 Context
> The need to store the user type in order to display different views depending on the user's role. This has made it necessary to consider where that variable should be stored so it can be retrieved later in the code, and how

## ⚖️ Options

| Option                                                    | For ✅                                                    | Against ❌                                                               |
| --------------------------------------------------------- | -------------------------------------------------------- | ----------------------------------------------------------------------- |
| Save the parameter in the registration activity           | Save the parameter in the same moment that it is created | It is not necessary because you could create a user without login later |
| Use intents to share information throughout the activites | The information is not save if you close the phone       | Need of moving parameters all the time                                  |
| Save the information in the login activity                | You save the role when is really useful                  | The user data is saved in the app even when it is closed                |

## ✅ Chosen, and why
> [!success] SharedPreferences as key-value pair data stored
> Select the “Save the information in the login activity” option because the only information that needs to be saved is that of the user who is logging into the application.
> 
>Select this option because the data stored in SharedPreferences is accessible anywhere in the app as a key-value pair.
## Sources
- 

## How I validated it


## Review
Would I decide the same today? (fill in at the end of the project)