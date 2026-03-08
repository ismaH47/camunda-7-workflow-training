# Simulación de un worker externo

## 🎯 Objetivo

Crear un **worker externo simple** que consulte tareas del motor Camunda, las ejecute y marque la tarea como completada.

---

## 🧠 Contexto

En el ejercicio anterior se configuró una **External Task** con el topic:

```id="jkgp1y"
validar-solicitud
```

Cuando el proceso llega a esa tarea, el motor crea una **External Task** y espera a que un **worker externo** la procese.

Un worker externo realiza normalmente tres pasos:

```id="1bb5ua"
1. solicitar tareas al motor
2. ejecutar la lógica de negocio
3. marcar la tarea como completada
```

En este ejercicio se simulará ese worker mediante llamadas REST.

---

# Arrancar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Arrancar el servidor:

```bash id="n9j08b"
mvn spring-boot:run
```

---

# Crear un worker simple con curl

El worker solicitará tareas utilizando el endpoint:

```id="9rmcgl"
/engine-rest/external-task/fetchAndLock
```

Ejecutar el siguiente comando:

```bash id="9e4baj"
curl -X POST http://localhost:8081/engine-rest/external-task/fetchAndLock \
-H "Content-Type: application/json" \
-d '{
  "workerId": "worker-1",
  "maxTasks": 1,
  "topics": [
    {
      "topicName": "validar-solicitud",
      "lockDuration": 10000
    }
  ]
}'
```

---

# Respuesta del motor

El motor devolverá una tarea externa similar a:

```json id="1b1y2s"
[
  {
    "id": "externalTaskId",
    "topicName": "validar-solicitud",
    "workerId": "worker-1",
    "lockExpirationTime": "...",
    "processInstanceId": "...",
    "executionId": "..."
  }
]
```

El campo importante es:

```id="7h4y9t"
id
```

Este identificador representa la tarea que el worker debe completar.

---

# Completar la tarea

Una vez ejecutada la lógica de negocio, el worker debe indicar al motor que la tarea ha finalizado.

Ejecutar:

```bash id="jqdf44"
curl -X POST http://localhost:8081/engine-rest/external-task/{id}/complete \
-H "Content-Type: application/json" \
-d '{
  "workerId": "worker-1"
}'
```

Sustituir `{id}` por el identificador de la tarea obtenida anteriormente.

---

# Qué ocurre después

Cuando el worker completa la tarea:

```id="fl7pxd"
worker ejecuta tarea
        │
        ▼
envía complete
        │
        ▼
Camunda continúa el proceso
```

El flujo BPMN avanzará a la siguiente actividad.

---

# Verificar el resultado

Abrir **Cockpit**:

```id="9avszn"
http://localhost:8081/camunda
```

Abrir el proceso:

```id="tfu1nd"
approval-process
```

La instancia del proceso debería haber avanzado después de la External Task.

---

# Flujo completo del patrón

```id="l3y3dz"
Proceso BPMN
      │
      ▼
External Task creada
      │
      ▼
Worker solicita tarea
      │
      ▼
Worker ejecuta lógica
      │
      ▼
Worker completa tarea
      │
      ▼
Proceso continúa
```

Este patrón permite ejecutar tareas desde **microservicios independientes del motor**.

---

# Comprobación

El ejercicio se considera completado cuando:

* el worker obtiene una tarea con `fetchAndLock`
* se obtiene el `externalTaskId`
* el worker completa la tarea mediante `/complete`
* el proceso continúa su ejecución.
