---
type: decision
date: 2026-11-18
status: taken
cssclasses:
  - decision
---
# Retrofit for API calls

## Context
The Android app has to call the Spring Boot REST API: register, log in, get and create houses, join a house by code, and read expenses ([[Endpoints]]). Each call sends and receives JSON. The app needs an HTTP client that also converts the JSON to Java objects.

## Options
| Option                                   | For                                                                                                              | Against                                                        |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| `HttpURLConnection` (built into Android) | No dependency                                                                                                    | Manual URL building, manual JSON parsing, a lot of boilerplate |
| OkHttp alone                             | Solid HTTP client                                                                                                | Still manual JSON parsing and request code for each call       |
| Retrofit                                 | Each API is a Java interface with annotations; JSON conversion through a converter; works with OkHttp underneath | One more dependency to learn                                   |

## Chosen, and why
**I chose the Retrofit option because it provides me with all the tools I need in a very simple way. It gives me everything OkHttp offers, plus JSON support through the GSON library.


## Sources
- **[Retrofit Tutotrial](https://www.baeldung.com/retrofit)**

## How I validated it
The table in [[Endpoints]] marks each endpoint as used by the Android app: `UserApi` (register, login), `HouseApi` (get, create and join house) and `ExpenseApi` (get expenses). The add-expense endpoint is not called from the app yet.



## Review
Would I decide the same today? (fill in at the end of the project)
