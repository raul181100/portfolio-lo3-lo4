---
type: decision
date: 2026-11-18
status: taken
cssclasses:
  - decision
---
# PostgreSQL as shared database

## Context
The Spring Boot API stores all the data of HouseMate: users, houses, expenses and roles. The group needs one database that every member can reach, and not a copy on each laptop. The server is shared and managed by Daniel (see [[Group_sprint 3]]). The connection is made from Spring with JPA/Hibernate ([[Spring Boot]]).

On 16 Nov I could not connect to the shared database from eduCloud, because the database had not been set up correctly ([[Daily 2026-11-16]]). On 18 Nov the backend started against PostgreSQL, using the container password passed as an environment variable.

## Options
| Option | For | Against |
| --- | --- | --- |
| H2 (embedded) | No setup; starts with the app | Each member has their own data; not shared |
| SQLite (single file) | Simple, no server | Not designed for several clients writing at once |
| MySQL / MariaDB | Widely used | **Different DB than my group** |
| PostgreSQL on a shared server | One shared database for the group; Daniel already set it up; supports the data types we use | Needs the VPN and the server to be up; a shared password to manage |

## Chosen, and why
The group needed one place where everyone's data would end up, and the server was already there. Choosing PostgreSQL meant that Daniel could set it up once and we could all use it, instead of each of us running a local database that would never match. I also did not want to change the database in the middle of the project, so keeping PostgreSQL was the simplest option for the team. The 16 Nov problem showed me that depending on a shared server means depending on the people who manage it, and I need to plan around that.

## Sources
- The server details and the connection in [[Endpoints]] and my notes from [[Group_sprint 3]]
- My daily notes on the connection attempts ([[Daily 2026-11-16]])

## How I validated it
- 18 Nov: the backend starts and connects to PostgreSQL.
- 17 Nov: a schema change (`ALTER TABLE users ADD COLUMN role …`) worked on the shared database, which fixed the bug in [[Null enum in DB]].

## Consequences
- The app needs the VPN and the server to be up.
- The password is not in the repository. It is passed as an environment variable (`SPRING_DATASOURCE_PASSWORD`), so it stays out of the code the team shares.

## Review

