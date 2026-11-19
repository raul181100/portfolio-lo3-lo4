# Pendientes Android

- [x] Compilar el proyecto y revisar las marcas rojas de `nav_graph.xml`.
- [x] Añadir `role` al DTO de login de Android (si aún no está).
- [x] Crear `UserHomeFragment` y `LandlordHomeFragment` en `ui/fragments` (ya existen; revisar paquete).
- [x] Layouts `fragment_user_home.xml` y `fragment_landlord_home.xml` (ya existen; revisar contenido).
- [x] Dejar `user_activity.xml` solo con el `FragmentContainerView`.
- [x] Comprobar la dependencia `navigation-fragment` en `build.gradle` (ya aparece en `app/build.gradle`).
- [x] En `UserActivity`: elegir el fragment de inicio según el rol.
- [x] `onViewCreated` de `UserHomeFragment`: vistas, bienvenida y clics.
- [x] Quitar de `UserActivity` los clics que pasen al fragment.
- [x] Decidir: extras del Intent o SharedPreferences para nombre y email.
- [x] Probar con cuentas `User` y `Landlord`.

## Backend
- [x] Ningún endpoint comprueba el rol todavía.
- [ ] Reglas de landlord en la capa de servicio (ver [[Role type]]).
- [ ] Probar que un `User` recibe error en un endpoint de landlord.

## Por revisar
- [ ] Nombres del enum: `RoleType { User, Landlord }` en Java frente al `role` del DTO de Android.
