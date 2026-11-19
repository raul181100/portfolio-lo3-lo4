---
type: bug
date: 2026-11-17
status: Close
area: "[[Role type]]"
time_lost: 90 minutes
cssclasses:
  - bug
---
# Null enum in DB

## What happened

> [!info] Expected
> I expected that when I passed the text saved in the drop-down menu and sent the role type to the backend, it would be saved directly to the database without any major issues. This is the step that precedes configuring the views for each role type.

> [!failure] Actual
> The system did not save the information even when all the information fell within the expected parameters.

## What I tried (in order)
1. Try saving the information as usual by simply adding the desired role type with a string that would be saved as an enum.
2. When I noticed it wasn't working, I checked to see where in the code the problem was whether it was in the front end, the back end, or when saving to the database. 
3. When I realised the error was occurring in the Back method, I decided to check how the new field was being saved and saw that it was being saved the same way as the others with `NotBlank` instead of `NotNull`. 
4. This last point made me realise that users created before this implementation didn't have this field assigned, so it was null and always caused an error.
5. With this query, I changed all users created before the “User” [[Role type]].
   ```sql
   ALTER TABLE users ADD COLUMN role varchar(255);
   UPDATE users SET role = 'User' WHERE role IS NULL;
   ALTER TABLE users ALTER COLUMN role SET NOT NULL;
   ```

## Real cause

> [!warning] Real cause
> There were two specific issues:
>
> 1. The field was created as “Notblank” instead of “NotNull.”
> 2. Previously created users did not have a role assigned to them.
> 3. `UserService` never passed the role to the `User` entity.
> 4. The `NOT NULL` column could not be added while old rows were null, so the insert failed with a 500, shown as "Please check the data".

## Solution

> [!success] Solution
> - `@NotNull` on `role` in `CreateUserRequest`.
> - Pass `request.role()` to `User` in `UserService`.
> - Add the column and set `User` on old users (SQL above).

## Source that helped

- [NotBlank vs. NotNull ](https://howtodoinjava.com/hibernate/unexpectedtypeexception-error/)

## Evidence

![[Role_Column_DB.png]]

![[Enum_Class_Spring.png]]

![[RolType_Selector.png]]

## Reusable lesson

> [!tip] Lesson
> → added to [[ ]] in Knowledge