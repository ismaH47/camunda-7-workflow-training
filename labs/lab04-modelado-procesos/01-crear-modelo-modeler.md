# Crear modelo con Camunda Modeler

## 🎯 Objetivo

Crear un nuevo **modelo BPMN** utilizando **Camunda Modeler** y guardarlo dentro del repositorio del proyecto.

---

## 🧠 Contexto

Los procesos que ejecuta Camunda se definen mediante modelos BPMN.

Durante el desarrollo estos modelos se crean normalmente con **Camunda Modeler**, la herramienta oficial para diseñar procesos ejecutables.

En este ejercicio se creará un nuevo modelo BPMN que posteriormente será desplegado en el motor.

---

# Abrir Camunda Modeler

Abre la aplicación **Camunda Modeler** (la que instalaste en el lab01 o en el entorno). Al abrir verás una pantalla inicial o un editor vacío.

En la **parte superior** de la ventana, menú **File**. Haz clic en **File** → **New File** y elige **BPMN Diagram**. Se abrirá un **nuevo diagrama vacío**: canvas en el centro y **paleta de elementos a la izquierda**.

---

# Guardar el modelo en el proyecto

Antes de modelar, guarda el archivo en el repositorio. Menú **File** (arriba) → **Save As**. En el cuadro de guardar, navega hasta la carpeta **model/** del repositorio del curso (la misma raíz donde están **labs** y el **README**). Como nombre de archivo pon: **approval-process.bpmn**. Guarda.

---

# Configurar el identificador del proceso

El **pool principal** es el rectángulo que engloba todo el flujo (a veces tiene una etiqueta "Pool" o el nombre del proceso). **Haz clic en una zona vacía del canvas** (fuera de cualquier tarea o evento) o en el borde del pool para seleccionar el proceso. En el **panel de propiedades a la derecha** (si no lo ves, menú **Window** → **Show Properties**) busca:

* **Process Id** (o "Id"): escribe **approval-process**
* **Name**: **Approval Process**
* **Executable**: márcalo como **true** (o activado). Es importante para que el motor pueda ejecutar el proceso.

---

# Verificar el archivo creado

Abre una **terminal** en VS Code (Terminal → New Terminal). Desde la **raíz del repositorio** (donde están **labs**, **backend** y **model**) ejecuta:

```bash
ls model
```

Debería aparecer el archivo:

```
approval-process.bpmn
```

---

# Abrir el modelo desde VS Code

En el **explorador de archivos** (izquierda), entra en la carpeta **model** y haz clic en **approval-process.bpmn**. O usa **Ctrl+P** y escribe `approval-process`. Si tienes la extensión BPMN instalada, se abrirá la vista del diagrama.

Esto confirma que el modelo está correctamente guardado dentro del repositorio.

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea un nuevo diagrama BPMN
* el proceso tiene el **Process Id `approval-process`**
* el archivo se guarda en el directorio `model`
* el archivo puede abrirse desde VS Code.

---

## 📚 Referencia

[Elementos BPMN – referencia rápida](../../docs/referencia/elementos-bpmn.md)
