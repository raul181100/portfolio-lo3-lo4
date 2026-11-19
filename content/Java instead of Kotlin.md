---
type: decision
date: 2026-11-18
status: taken
cssclasses:
  - decision
---
# Java instead of Kotlin

## Context
The Android app and the Spring Boot back end are written in one language each. I had to decide the language before most of the code was written. On 13 Nov, after Martin's feedback, the group decided to unify the back end into [[Spring Boot]] ([[Martin -Documentation on software development and useful technologies]]). Kotlin is the language Google recommends for new Android code, so the choice was not obvious to me.

## Options
| Option | For | Against |
| --- | --- | --- |
| Kotlin | Recommended by Google for Android; shorter code; Spring supports it | The back end is already in Java, so the team would have to know two languages. It would also be one more thing to learn in a short project. |
| Java | The back end is already in Java; I already had code written; the team can help me with the same language | Longer code; Google's newest examples are in Kotlin, so I have to translate some of them |

## Chosen, and why
I chose Java because the group needed one language for the whole project, and the back end was already moving to Java. Kotlin would have been the better choice for Android on its own, but it would have split the team's knowledge in two. Since the project has a short deadline, I preferred to spend my time on the features and the process than on learning a new language. I still think Kotlin is the right choice for a future Android project, but not for this one.

What the project already shows: the Android app is written in Java ([[HouseMate]]), the back end is Spring Boot in Java, and the [[Role type]] enum is a Java enum.

## Sources
- [Kotlin and Java interoperability (Android Developers)](https://developer.android.com/kotlin/interop)
- [Kotlin first for Android (Android Developers)](https://developer.android.com/kotlin/first)

## How I validated it
The back end starts with Java and connects to the database (see [[Claude/Diario/2026-11-18]]). The Android app runs with the same language, and I could log in with my test accounts. 

## Consequences
- Java is more verbose, so some code takes more lines than it would in Kotlin.
- When I read Android examples in Kotlin, I have to translate them. That takes time, but it also made me read the code more carefully.

## Review
