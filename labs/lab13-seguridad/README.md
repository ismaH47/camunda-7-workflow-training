# Lab 13 — Seguridad

## 🎯 Objetivo

Comprender cómo Camunda gestiona **usuarios, grupos y permisos** para controlar el acceso a procesos y tareas.

En este laboratorio se aprenderá a:

* crear usuarios en el sistema
* crear grupos y asignar miembros
* configurar permisos sobre procesos y tareas
* entender cómo funciona el modelo de seguridad de Camunda
* integrar SSO con un IdP externo (OAuth2/OIDC, SAML)

---

# 🧠 Contexto

En sistemas de workflow reales es necesario controlar:

```text id="q1h4v8"
quién puede iniciar procesos
quién puede ver procesos
quién puede completar tareas
quién puede administrar el sistema
```

Camunda gestiona esto mediante tres elementos principales.

```text id="s6n2k3"
Users
Groups
Authorizations
```

---

# 👤 Usuarios

Un **usuario** representa una persona que interactúa con el sistema.

Ejemplos:

```text id="r9d7w2"
juan
maria
pedro
admin
```

Los usuarios pueden:

```text id="b5c8t6"
iniciar procesos
ver tareas
completar tareas
acceder a herramientas del sistema
```

---

# 👥 Grupos

Los **grupos** representan roles dentro de la organización.

Ejemplo:

```text id="p4y9m1"
reviewers
managers
administrators
```

Los usuarios pueden pertenecer a uno o varios grupos.

Las tareas BPMN pueden asignarse a **usuarios o grupos**.

---

# 🔐 Autorizaciones

Las **autorizaciones** controlan qué acciones están permitidas.

Ejemplos de permisos:

```text id="k7z3v5"
READ
UPDATE
CREATE
DELETE
ALL
```

Estos permisos pueden aplicarse a distintos recursos del motor:

```text id="f2x6g8"
procesos
tareas
instancias
usuarios
grupos
```

---

# 🔎 Qué vamos a hacer en este laboratorio

Se configurará el sistema de seguridad de Camunda mediante las herramientas de administración.

Durante los ejercicios se aprenderá a:

```text id="z3k1p7"
crear usuarios
crear grupos
asignar usuarios a grupos
configurar permisos
```

Esto permitirá controlar el acceso a procesos y tareas.

---

# 📘 Ejercicios del laboratorio

### 01 — Usuarios y grupos

Crear usuarios y grupos dentro del sistema.

Archivo:

```text id="v6y5c2"
01-usuarios-grupos.md
```

---

### 02 — Roles y permisos

Configurar permisos básicos sobre procesos.

Archivo:

```text id="w8t3n4"
02-roles-permisos.md
```

---

### 03 — Autorizaciones

Configurar autorizaciones específicas para tareas y recursos.

Archivo:

```text id="m1r9q6"
03-autorizaciones.md
```

---

### 04 — Configuración de seguridad

Configurar usuarios administradores y verificar acceso a las herramientas del sistema.

Archivo:

```text id="s4p8y1"
04-configuracion-seguridad.md
```

---

### 05 — SSO (Single Sign-On)

Integrar Cockpit, Tasklist y Admin con un IdP externo (OAuth2/OIDC o SAML).

Archivo:

```
05-sso.md
```

---

# 🧪 Resultado esperado

Al finalizar este laboratorio se comprenderá cómo funciona el modelo de seguridad de Camunda.

El sistema será capaz de:

```text id="g5x7d3"
gestionar usuarios
organizar usuarios en grupos
controlar permisos sobre procesos
controlar acceso a tareas
```

Esto permite integrar Camunda dentro de organizaciones reales con distintos roles y niveles de acceso.

---

# 🔜 Próximo laboratorio

En el siguiente laboratorio se aprenderá a **probar, depurar y monitorizar procesos BPMN**, permitiendo analizar su comportamiento en ejecución.
