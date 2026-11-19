---
type: feedback
date: 2026-11-13
from: Martin
asked_by_me: Raul
acted_on: Yes
cssclasses:
  - feedback
---
# Martin - Documentation on software development and useful technologies

> [!info] Context
> On Friday I had a personal feedback session with Martin, followed by a group feedback meeting. In the personal one we talked about how to document software development without overloading the documentation with lines of code. He also recommended several useful tools for creating diagrams, such as https://c4model.com. In the group feedback we gave him context on each person's role and how we are structuring the organization of the app, plus several things we need to keep in mind for group development.
>

> [!quote] What they said
> - Individual feedback: He told me that the best way to focus my documentation clearly, without overloading it with code, is to use diagrams. These [[Diagrams]] show the organization of my app more visually, as in ![[Images/Structure_Diagram.png]]. He suggested an interesting approach: start with a very general view and then zoom into different layers of the project to show how it works internally. I also asked him whether a document focused on how Front-end, Back-end and DataBase connect would be useful for the complete picture of the project. We also reviewed my Endpoints document, and he said it was very complete and very interesting.
> - Group feedback: We updated Martin on the roles each of us has in the project: what responsibilities each person has and what structure we are following to organize ourselves. We also explained what our project is about. A very important piece of advice from Martin was to be careful not to leave the integration of the parts each teammate builds until the last moment, because that is always what causes the main problems.

> [!todo] What I did with it
> With this information, I reviewed the different types of [[Diagrams]] I could apply to my project on https://c4model.com. I also decided to keep expanding and documenting different parts of my project in separate documents, such as Endpoints. Finally, as a group, we decided that the best approach was to unify the Back-end into a single technology, [[Spring Boot]], to avoid having to unify different systems. Related decision: Java instead of Kotlin.

> [!success] What changed
> **Before:** No [[Diagrams]], which made it harder for my coaches to quickly see how the project is organized.
> **After:** Diagrams of the project's different layers, zooming into the specific parts where it is useful to see how they work internally.

> [!example] Evidence
> ![[Images/FeedPulse_2.png]]
