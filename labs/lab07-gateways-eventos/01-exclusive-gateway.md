# Exclusive Gateway

## 🎯 Objetivo

Añadir un **Exclusive Gateway** al proceso para que el flujo pueda tomar diferentes caminos en función de una variable.

---

## 🧠 Contexto

En BPMN un **Gateway** permite controlar el flujo del proceso.

El **Exclusive Gateway** se utiliza cuando el proceso debe elegir **una sola ruta entre varias posibles**.

Este tipo de decisión suele basarse en:

* variables del proceso
* resultados de tareas anteriores
* datos introducidos por el usuario

En este ejercicio utilizaremos la variable creada en el formulario:

```id="7h4lzn"
aprobada
```

---

# Abrir el modelo BPMN

Abre **model/approval-process.bpmn** en **Camunda Modeler** (File → Open, carpeta model del repo).

---

# Insertar un Exclusive Gateway

En la **paleta de la izquierda** busca **Exclusive Gateway** (rombo con una X). **Arrástralo** al diagrama y colócalo después de la tarea:

```id="r7u0ds"
Aprobar solicitud
```

---

# Modificar el flujo del proceso

Actualmente el flujo termina directamente en el evento **Fin**.

Modificar el proceso para que el flujo sea:

```id="q8o6hi"
Inicio
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

# Crear dos caminos posibles

Desde el **Exclusive Gateway** crear dos flujos diferentes.

Primer flujo:

```id="h0q4sy"
Solicitud aprobada
```

Segundo flujo:

```id="b9m3wa"
Solicitud rechazada
```

Cada flujo puede terminar en un evento **End Event**.

---

# Nombrar los flujos

Asignar nombres a los flujos de salida.

Flujo aprobado:

```id="p3d9cu"
Aprobada
```

Flujo rechazado:

```id="d2v8xq"
Rechazada
```

---

# Guardar el modelo

Guardar el archivo:

```id="3r6mvo"
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Actualizar el modelo desplegado en el backend:

```bash id="k7f4sa"
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Ejecutar la aplicación

En la **terminal**, desde la raíz del repo: `cd backend`. Luego:

Arrancar la aplicación:

```bash id="l9s3pu"
mvn spring-boot:run
```

---

# Qué ocurre ahora

El flujo del proceso ha cambiado.

Ahora el proceso puede tomar **dos caminos diferentes**.

Representación del flujo:

```id="v6k2qy"
Inicio
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

---

# Comprobación

El ejercicio se considera completado cuando:

* se añade un **Exclusive Gateway**
* el gateway tiene dos flujos de salida
* cada flujo termina en un evento de fin.

---

## 📚 Referencia

[Gateways BPMN – referencia](../../docs/referencia/gateways-bpmn.md)
