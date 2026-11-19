---
type: decision
date: 2026-11-18
status: taken
cssclasses:
  - decision
---
# BCrypt for passwords

## Context
Users register and log in with an email and a password (`POST /users` and `POST /users/login`, see [[Endpoints]]). When I started writing the registration, I realised that whatever I saved in the database would be visible to anyone who got access to it. That made me stop and think about how the passwords should be stored, before the feature grew any further.

## Options
| Option | For | Against |
| --- | --- | --- |
| Plain text | Trivial to implement | Anyone with database access reads every password |
| Fast hash (e.g. SHA-256) without salt | Simple, one line | Identical passwords get identical hashes; fast to brute-force |
| BCrypt | Salted by default; the cost can grow as computers get faster; built into Spring Security | Slower on purpose; the stored value is longer than the password |
| Argon2 / scrypt | Modern, memory-hard | I did not compare them in depth. I chose a tool I could find in the framework I already use. |

## Chosen, and why
I chose BCrypt because it is the one that fit my project best without adding complexity. Spring Security already provides it, so I did not need to set up a password system from scratch. I also liked that it adds a random part to each password, so two users with the same password do not end up with the same stored value. Writing it down made me realise that the choice was partly practical: I was looking for something safe enough that I did not have to maintain myself.

## Sources
- [Spring Security: password storage](https://docs.spring.io/spring-security/reference/features/authentication/password-storage.html)
- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)

## How I validated it
I checked that the password is not stored as I typed it: what the database keeps is a long, unreadable value. I also checked that a wrong password does not log the user in, and that the message returned does not say which of the two fields was wrong (see [[Endpoints]]). 

## Review
Would I decide the same today? (fill in at the end of the project)
