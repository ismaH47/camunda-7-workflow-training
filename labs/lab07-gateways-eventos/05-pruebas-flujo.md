# Pruebas del flujo del proceso

## 🎯 Objetivo

Ejecutar varias instancias del proceso y comprobar cómo el motor gestiona:

* temporizadores
* eventos de mensaje
* decisiones del gateway

---

## 🧠 Contexto

En los ejercicios anteriores se han añadido varios elementos al proceso:

* **Timer Event**
* **Message Event**
* **Exclusive Gateway con condiciones**

Esto hace que el proceso tenga ahora un comportamiento más complejo.

El flujo actual es aproximadamente:

```
Inicio
   │
   ▼
Timer Event
   │
   ▼
Message Event
   │
   ▼
Validar solicitud
   │
   ▼
Aprobar solicitud
   │
   ▼
Exclusive Gateway
   ├── Aprobada → Fin
   └── Rechazada → Fin
```

En este ejercicio se probará el comportamiento completo del flujo.

---

# Arrancar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Ejecutar la aplicación:

```bash
mvn spring-boot:run
```

Esto iniciará una instancia del proceso.

---

# Observar el Timer Event

Abrir **Camunda Cockpit**:

```
http://localhost:8081/camunda
```

Abrir el proceso:

```
approval-process
```

Entrar en una instancia activa.

Durante los primeros segundos el proceso estará detenido en el **Timer Event**.

Después de 10 segundos continuará automáticamente.

---

# Observar el Message Event

Una vez superado el temporizador el proceso llegará al **Message Event**.

En ese momento la instancia quedará esperando el mensaje:

```
validacion-recibida
```

Esto se puede observar en Cockpit.

---

# Enviar el mensaje al proceso

Enviar el mensaje desde código Java utilizando:

```java
runtimeService.correlateMessage("validacion-recibida");
```

Después de enviar el mensaje el proceso continuará.

---

# Completar la tarea humana

Abrir **Tasklist**:

```
http://localhost:8081/camunda/app/tasklist
```

Buscar la tarea:

```
Aprobar solicitud
```

Completar el formulario.

Probar dos casos diferentes.

---

# Caso 1 — Solicitud aprobada

Formulario:

```
Solicitud aprobada = true
```

El flujo será:

```
Gateway → camino aprobado → Fin
```

---

# Caso 2 — Solicitud rechazada

Formulario:

```
Solicitud aprobada = false
```

El flujo será:

```
Gateway → camino rechazado → Fin
```

---

# Verificar el resultado en Cockpit

Volver a **Cockpit** y abrir el proceso.

Revisar:

```
Process Instances
History
```

Se podrán observar:

* instancias completadas
* camino seguido por cada instancia
* variables utilizadas

---

# Qué se ha comprobado

Durante esta prueba se han validado varios comportamientos del motor:

```
Timer Event
      │
      ▼
espera programada

Message Event
      │
      ▼
espera de evento externo

Exclusive Gateway
      │
      ▼
decisión basada en variables
```

---

# Comprobación

El ejercicio se considera completado cuando:

* el temporizador retrasa la ejecución del proceso
* el proceso se detiene en el evento de mensaje
* el mensaje permite continuar el flujo
* el gateway selecciona correctamente el camino según el formulario.
