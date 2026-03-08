# Integración SSO (Single Sign-On)

## 🎯 Objetivo

Configurar el acceso a **Cockpit, Tasklist y Admin** mediante un proveedor de identidad externo (SSO), de modo que los usuarios se autentiquen una vez en el IdP y accedan a las aplicaciones web de Camunda sin un segundo login.

---

## 🧠 Contexto

**SSO** permite que la autenticación la gestione un **Identity Provider (IdP)** (Keycloak, Okta, Auth0, Azure AD, etc.) en lugar del usuario/contraseña integrado de Camunda.

Flujo típico:

1. El usuario abre `http://localhost:8081/camunda` (o la URL de Cockpit/Tasklist).
2. La aplicación redirige al IdP para login.
3. Tras autenticarse, el IdP redirige de vuelta con un token (OAuth2/OIDC o SAML).
4. Camunda valida el token y crea la sesión; el usuario queda identificado por el **identity** que Camunda obtiene del token (subject, preferred_username, etc.).
5. Las **autorizaciones** de Camunda (usuarios, grupos, permisos) siguen aplicando: el IdP dice "quién es"; Camunda debe tener ese usuario/grupos configurados para autorizar acceso a recursos.

Para que las tareas y procesos se asignen correctamente, el **userId** que Camunda use debe coincidir con el que está en la base de datos de identidades de Camunda (IdentityService); normalmente se configura un **Identity Provider Plugin** que, a partir del token, proporcione el userId y los grupos a Camunda.

---

## 📋 Opciones de integración en Camunda 7

* **OAuth2 / OpenID Connect**: el IdP expone endpoints de autorización y tokens; la aplicación web de Camunda (o un reverse proxy) valida el token JWT y extrae el usuario. Camunda puede usar un plugin que lea el token (por header o cookie) y establezca la identidad en la sesión.
* **SAML 2.0**: el IdP devuelve aserciones SAML; el mismo concepto: validar la aserción y mapear el sujeto a un usuario de Camunda.

En Spring Boot con Camunda, es habitual:

1. Proteger las rutas `/camunda/**` con OAuth2 Resource Server (Spring Security) o con un gateway que valide el token y pase el userId en un header.
2. Configurar un **ProcessEnginePlugin** (Identity Provider) que en cada petición lea el userId (y opcionalmente grupos) del token o del header y los inyecte en el **IdentityService** o en el contexto de autenticación de Camunda, de modo que Cockpit/Tasklist vean al usuario actual y apliquen autorizaciones.

Documentación oficial de Camunda describe Identity Provider plugins y ejemplos con Keycloak.

---

## 📋 Pasos prácticos recomendados

1. **IdP:** Elige un IdP (por ejemplo Keycloak en Docker) y registra una aplicación cliente OAuth2/OIDC con la URL de callback de tu aplicación Camunda (ej. `http://localhost:8080/login/oauth2/code/keycloak`).
2. **Spring Security:** En el proyecto, la configuración suele ir en **src/main/resources/application.yml** (o application.properties): `spring.security.oauth2.client.*`, issuer-uri, client-id y client-secret. Activa OAuth2 Login o Resource Server y haz que las rutas de Camunda (`/camunda/**`) exijan autenticación OAuth2.
3. **Plugin de identidad:** Configura el plugin de Camunda (en código o en configuración) para que tome el userId (y grupos si aplica) del token o de los claims y los use como identidad actual en el motor.
4. **Usuarios en Camunda:** Abre **Camunda Admin** (si Cockpit está en `http://localhost:8080/camunda`, Admin suele ser esa misma URL con la pestaña o enlace **Admin** en la parte superior, o `.../camunda/app/admin`). Ahí crea el mismo **userId** (y grupos) que devuelve el IdP y asígnale permisos para Cockpit, Tasklist y Admin, para que ese usuario vea procesos y tareas.
5. **Verificar:** Abre la URL de Cockpit en el navegador (por ejemplo `http://localhost:8080/camunda`) sin usar login local; deberías ser redirigido al IdP y, tras iniciar sesión, volver a Cockpit ya autenticado con el usuario del IdP.

---

## 📌 Variables y documentación

En la documentación de Camunda busca *Security - Identity Service*, *Authentication - Single Sign-On* y ejemplos de *Camunda + Keycloak* (o el IdP que uses). Las variables típicas van en **application.yml** (en `src/main/resources/`): `spring.security.oauth2.client.*`, `spring.security.oauth2.resourceserver.*` y la configuración del Identity Provider plugin de Camunda.

---

## 📌 Conclusión

Con SSO, Cockpit, Tasklist y Admin delegan la autenticación en el IdP; Camunda sigue aplicando su modelo de usuarios, grupos y autorizaciones, que debe estar alineado con las identidades que devuelve el IdP.
