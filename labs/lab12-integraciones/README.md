# Lab 12 — Integraciones

## 🎯 Objetivo

Aprender a integrar procesos BPMN con **sistemas externos**, como bases de datos, servicios REST o workers externos.

En este laboratorio se aprenderá a:

* interactuar con una base de datos desde el proceso
* integrar servicios externos mediante código Java
* utilizar el patrón **External Task**
* simular servicios externos que interactúan con el motor
* integrar con colas de mensajes (correlación, workers que consumen de cola)

---

# 🧠 Contexto

En aplicaciones reales los procesos BPMN rara vez funcionan de forma aislada.

Normalmente interactúan con distintos sistemas del ecosistema de la organización.

Ejemplos comunes:

```text id="r7f5v2"
bases de datos
APIs REST
microservicios
sistemas externos
colas de mensajes
```

Camunda permite integrar estos sistemas mediante distintos mecanismos.

---

# 🔧 Mecanismos de integración

Los mecanismos más utilizados para integrar Camunda con otros sistemas son:

```text id="a2q9k6"
Service Tasks
External Tasks
REST API
```

### Service Task

Una Service Task ejecuta código dentro de la propia aplicación.

Ejemplo:

```text id="x8y1p4"
guardar datos en base de datos
llamar a una API REST
validar información
```

---

### External Task

Una External Task delega el trabajo a **un worker externo**.

El motor crea la tarea y un worker independiente la procesa.

Ejemplo:

```text id="g6v2m9"
microservicio que procesa pagos
worker que envía correos
servicio de generación de documentos
```

---

# 🔎 Qué vamos a hacer en este laboratorio

Se ampliará el proceso BPMN para integrar distintos tipos de servicios.

Durante los ejercicios se aprenderá a:

```text id="p3n5t8"
guardar información en base de datos
llamar a servicios externos
ejecutar tareas mediante workers externos
simular integraciones del sistema
```

Esto permitirá entender cómo un proceso BPMN se conecta con otros sistemas.

---

# 📘 Ejercicios del laboratorio

### 01 — Integración con base de datos

Guardar información del proceso en una base de datos utilizando JPA.

Archivo:

```text id="m8k7s1"
01-integracion-bd.md
```

---

### 02 — Servicios externos

Simular la llamada a un servicio externo desde una Service Task.

Archivo:

```text id="d9t6y4"
02-servicios-externos.md
```

---

### 03 — External Tasks

Configurar una tarea BPMN para ser ejecutada por un worker externo.

Archivo:

```text id="z5p1n3"
03-external-tasks.md
```

---

### 04 — Simulación de servicios

Crear un worker simple que procese External Tasks.

Archivo:

```text id="h2v8c6"
04-simulacion-servicios.md
```

---

### 05 — Colas de mensajes

Integrar el proceso con colas (patrones proceso↔cola, correlación de mensajes, worker que consume de cola).

Archivo:

```
05-colas-mensajes.md
```

---

# 🧪 Resultado esperado

Al finalizar este laboratorio se comprenderá cómo integrar procesos BPMN con sistemas externos.

El proceso será capaz de:

```text id="y1s4k9"
guardar datos en base de datos
interactuar con servicios externos
delegar trabajo a workers externos
```

Esto permitirá construir procesos integrados dentro de arquitecturas reales.

---

# 🔜 Próximo laboratorio

En el siguiente laboratorio se estudiará la **gestión de seguridad en Camunda**, incluyendo usuarios, grupos y permisos.
