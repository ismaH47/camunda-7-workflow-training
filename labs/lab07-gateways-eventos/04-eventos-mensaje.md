# Eventos de mensaje

## 🎯 Objetivo

Añadir un **Message Event** al proceso para permitir que una instancia de proceso sea **activada mediante un mensaje externo**.

---

## 🧠 Contexto

Los **Message Events** permiten que un proceso:

* espere un mensaje
* se reactive cuando ese mensaje llegue
* interactúe con otros sistemas

Se utilizan habitualmente para integrar procesos con:

* APIs
* microservicios
* colas de mensajería
* sistemas externos

En este ejercicio el proceso esperará un mensaje antes de continuar.

---

# Abrir el modelo BPMN

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open, carpeta model del repo).

Editar el modelo utilizando **Camunda Modeler**.

---

# Añadir un evento de mensaje

Insertar un nuevo evento **entre el Timer Event y la tarea Validar solicitud**.

Seleccionar:

```
Intermediate Event
```

Colocarlo en el flujo.

---

# Convertir el evento en Message Event

**Haz clic** en el evento creado. En el **panel de propiedades a la derecha** (o en el tipo de evento) cámbialo a:

```
Intermediate Message Catch Event
```

Este tipo de evento hace que el proceso **espere un mensaje externo**.

---

# Configurar el nombre del mensaje

En el panel de propiedades localizar:

```
Message Name
```

Introducir:

```id="q9h6et"
validacion-recibida
```

Este será el identificador del mensaje que el proceso espera.

---

# Flujo actualizado del proceso

El proceso ahora debería tener el siguiente flujo:

```id="rj8t0y"
Inicio
   │
   ▼
Timer Event
   │
   ▼
Esperar mensaje "validacion-recibida"
   │
   ▼
Validar solicitud
   │
   ▼
Aprobar solicitud
   │
   ▼
Gateway decisión
```

---

# Guardar el modelo

Guardar el archivo:

```id="b5e4wd"
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Actualizar el modelo desplegado:

```bash id="prkq9b"
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Reiniciar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Arrancar la aplicación:

```bash id="k0jzn4"
mvn spring-boot:run
```

---

# Iniciar una instancia del proceso

El proceso avanzará hasta el **Message Event** y quedará esperando el mensaje.

En **Cockpit** se podrá observar que la instancia está detenida en ese punto.

---

# Enviar el mensaje desde Java

Crear un método para enviar el mensaje al proceso.

Ejemplo:

```java id="zj2t7h"
runtimeService.correlateMessage("validacion-recibida");
```

Esto permitirá que el proceso continúe su ejecución.

---

# Qué ocurre internamente

Cuando el proceso alcanza el evento de mensaje:

```
Proceso llega al Message Event
        │
        ▼
El motor espera el mensaje
        │
        ▼
runtimeService.correlateMessage(...)
        │
        ▼
El proceso continúa
```

---

# Comprobación

El ejercicio se considera completado cuando:

* el modelo contiene un **Message Catch Event**
* el evento tiene el nombre `validacion-recibida`
* el proceso se detiene en ese punto hasta recibir el mensaje.
