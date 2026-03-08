# Elementos básicos de BPMN

## 🎯 Objetivo

Identificar los **elementos fundamentales de BPMN** observando y modificando un proceso existente.

---

## 🧠 Contexto

En el paso anterior abrimos un proceso BPMN y observamos su estructura.

BPMN utiliza un conjunto pequeño de elementos para representar la mayoría de procesos:

* eventos
* actividades
* flujos
* decisiones

En este ejercicio vamos a **identificar y modificar algunos de estos elementos** dentro del modelo.

---

## 📍 Abrir el modelo BPMN

En el **explorador de archivos** de VS Code (barra lateral izquierda), entra en la carpeta **model** y haz clic en **proceso-ejemplo.bpmn**. Si no existe ese archivo, usa cualquier otro `.bpmn` que tengas en `model/` (por ejemplo el que creaste en el paso 03). Si no tienes ninguno, haz antes el paso 03. Si la extensión BPMN está instalada, se abrirá el diagrama visual; si solo ves XML, cambia a la vista de diagrama que ofrezca la extensión o abre el archivo en Camunda Modeler.

---

## 🔎 Identificar los elementos del proceso

Localizar en el diagrama los siguientes elementos.

### Evento de inicio

Representa el punto donde comienza el proceso.

Símbolo:

```
círculo simple
```

En el modelo corresponde al elemento:

```
Inicio del proceso
```

---

### Actividades

Representan acciones dentro del proceso.

Símbolo:

```
rectángulo con bordes redondeados
```

En el modelo aparecen dos actividades:

```
Revisar solicitud
Aprobar solicitud
```

---

### Flujo de secuencia

Representa el orden de ejecución de las actividades.

Símbolo:

```
flecha
```

Las flechas conectan los elementos del proceso.

---

### Evento de fin

Representa el final del proceso.

Símbolo:

```
círculo con borde más grueso
```

En el modelo corresponde al elemento:

```
Fin del proceso
```

---

## ✏️ Modificar el proceso

Vamos a cambiar el nombre de una actividad. Asegúrate de estar viendo el **diagrama** (no solo el XML): en VS Code la extensión BPMN suele mostrar una vista gráfica; si no la ves, abre el archivo en Camunda Modeler. En el diagrama, **haz doble clic** sobre la actividad que se llama **Revisar solicitud** (o selecciónala con un clic y mira el **panel de propiedades**, que suele estar a la derecha; si no lo ves, en Camunda Modeler prueba **Window** → **Show Properties**). Donde pone "Name" o "Nombre", sustituye por **Validar solicitud**.

Guarda el archivo (**Ctrl + S** en VS Code, o **File** → **Save** en Camunda Modeler).

---

## 🔎 Verificar el cambio

Después de guardar, mira de nuevo el diagrama: la actividad debería mostrar **Validar solicitud** en lugar de "Revisar solicitud".

El proceso ahora debería verse así:

```
Inicio → Validar solicitud → Aprobar solicitud → Fin
```

---

## ✅ Comprobación

El ejercicio se considera completado cuando:

* se ha abierto el archivo BPMN
* se han identificado los elementos del proceso
* se ha modificado el nombre de una actividad
* el modelo BPMN se ha guardado correctamente.

---

## 📚 Referencia

[Elementos BPMN – referencia rápida](../../docs/referencia/elementos-bpmn.md)
