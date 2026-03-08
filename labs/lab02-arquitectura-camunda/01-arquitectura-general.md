# Arquitectura general de Camunda

## 🎯 Objetivo

Comprender la arquitectura general de Camunda explorando los componentes que se inicializan al arrancar la aplicación.

---

## 🧠 Contexto

Camunda es un **motor de ejecución de procesos**.

Su función es:

* ejecutar procesos BPMN
* gestionar el estado del workflow
* coordinar tareas humanas y automáticas
* persistir la información del proceso

Para entender cómo funciona Camunda es importante identificar los **componentes principales del sistema**.

---

## ▶️ Arrancar la aplicación

Abre una **terminal** (menú **Terminal** → **New Terminal**). Desde la **raíz del repositorio** (donde están **labs** y **backend**), ejecuta:

```bash
cd backend
```

Luego ejecuta la aplicación:

```bash
mvn spring-boot:run
```

Durante el arranque aparecerán mensajes en la terminal.

---

## 🔎 Buscar mensajes del motor Camunda

En la salida de la aplicación buscar líneas que contengan:

```id="camunda_engine_log"
ENGINE-00001 Process Engine default created
```

Este mensaje indica que el **motor de procesos se ha inicializado correctamente**.

---

## 🔎 Identificar componentes del sistema

Durante el arranque también se inicializan varios componentes importantes.

Buscar en la salida mensajes relacionados con:

### Motor de procesos

```id="engine_component"
Process Engine
```

El motor es el componente encargado de **ejecutar los procesos BPMN**.

---

### Base de datos

Camunda necesita una base de datos para almacenar:

* estado de los procesos
* tareas
* historial de ejecución

En este proyecto se utiliza:

```id="h2_database"
H2 Database
```

---

### Servidor web

Spring Boot arranca un servidor web embebido.

Buscar en los logs un mensaje similar a:

```id="server_started"
Tomcat started on port(s): 8080
```

Esto indica que la aplicación está disponible en el puerto **8080**.

---

## 📊 Relacionar componentes

A partir de lo observado durante el arranque, podemos identificar la arquitectura básica del sistema:

```
BPMN Model
      │
      ▼
Spring Boot Application
      │
      ▼
Camunda Process Engine
      │
      ▼
Database
```

---

## 🔎 Verificar que la aplicación responde

Abrir un navegador y acceder a:

```
http://localhost:8080
```

Esto confirma que el servidor web está funcionando.

---

## ✅ Comprobación

El ejercicio se considera completado cuando:

* la aplicación se inicia correctamente
* aparece el mensaje de creación del **Process Engine**
* el servidor web arranca en el puerto **8080**
* se comprende qué componentes forman la arquitectura básica de Camunda.

---

## 📚 Referencia

[Arquitectura de Camunda – referencia](../../docs/referencia/arquitectura-camunda.md)
