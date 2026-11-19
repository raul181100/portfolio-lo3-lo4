---
type: decision
date: 2026-11-16
status: taken
cssclasses:
  - decision
---
# Role type

> [!abstract] 🧭 Context
> For my project [[HouseMate]] I had to change the model where houses are created. Right now there is only one type of user, the normal user.
>
> The problem: a house cannot be owned by a [[User rol]]. It must be owned by a [[Landlord rol]]. A [[Landlord rol]] does not take part in splitting expenses and cannot join any house that is not theirs. They also have the power to remove a [[User rol]] from their house if necessary.
>
> 📅 These are the roles required as of [[2026-11-16]].

## ⚖️ Options

|     | Option                                                  | For ✅                               | Against ❌                                        |
| --- | ------------------------------------------------------- | ----------------------------------- | ------------------------------------------------ |
| 1   | Boolean column (`is_landlord`)                          | Simple                              | Only two roles; a new role needs a schema change |
| 2   | Int role code (1 = user, 2 = landlord)                  | Flexible                            | Magic numbers; easy to mix up                    |
| 3   | ⭐ Java enum `RoleType { User, Landlord }`, stored as string | Readable, type-safe, easy to extend | Slightly more code than a boolean                |
| 4   | Two separate user types/tables                          | Clear separation                    | Duplication; more complexity                     |

## ✅ Chosen, and why

> [!success] Decision: Java enum `RoleType { User, Landlord }`, stored as a string
> I chose a Java enum. I only need two roles at the moment, but an enum makes the code readable: the values have names, the compiler rejects invalid ones, and adding a new role later only means adding one value.
>
> Storing the name with `@Enumerated(EnumType.STRING)` means the database shows `LANDLORD` instead of a number, which makes the data easier to read.
>
> I did not choose two separate user tables because that would duplicate the user data and add more complexity than the app needs.

## ⚠️ Consequences

> [!warning] Rules to remember
> - `House.owner` must reference a user with the `LANDLORD` role, which is the [[Landlord rol]].
> - The business rules for [[Landlord rol]] (no expense splitting, joining only their own houses, removing members) will be enforced in the service layer.
> - Adding a new role later means adding a new value to the `RoleType` enum and defining its rules.
- Code check (16 Nov): `RoleType` lives in `entity/RoleType.java`, and `User` stores it in the `role` field. `CreateUserRequest` requires it at registration, and `UserResponse` returns it.

## 📚 Sources
- 

## 🧪 How I validated it


## 🔍 Review
Would I decide the same today? (fill in at the end of the project)
