# Qué es BPMN

## 🎯 Objetivo

Comprender qué es **BPMN** observando y analizando un proceso representado mediante un diagrama.

---

## 🧠 Contexto

Antes de crear nuestros propios procesos es útil **ver un proceso BPMN real**.

En este paso vamos a:

1. abrir un modelo BPMN existente
2. observar sus elementos
3. identificar las partes principales de un proceso

---

## 📥 Abrir el modelo de ejemplo

En **VS Code**, en el **explorador de archivos de la izquierda** (si no lo ves, menú **View** → **Explorer** o el icono de la carpeta en la barra lateral), localiza la carpeta **model**. Dentro verás uno o más archivos con extensión **.bpmn**. Haz clic en uno para abrirlo.

**Si la carpeta model está vacía o no tiene ningún .bpmn:** haz primero el paso **03 (Crear primer proceso)** para crear tu primer diagrama; luego vuelve a este paso y ábrelo para identificar los elementos. Si el repositorio trae un archivo de ejemplo con otro nombre, ábrelo.

Si tienes instalada la extensión BPMN, en lugar del XML verás el **diagrama del proceso** (vista gráfica). Si solo ves código, comprueba que la extensión BPMN esté instalada y que el archivo tenga extensión `.bpmn`.

---

## 🔎 Identificar los elementos del proceso

Observar el diagrama y localizar los siguientes elementos:

### Evento de inicio

Representa el **punto donde comienza el proceso**.

En BPMN se representa con un **círculo verde**.

---

### Actividad

Representa una **acción dentro del proceso**.

Se representa con un **rectángulo con bordes redondeados**.

Las actividades pueden representar:

* trabajo realizado por personas
* tareas automáticas
* integraciones con sistemas

---

### Flujo de secuencia

Representa el **orden en el que se ejecutan las actividades**.

Se representa mediante **flechas**.

---

### Evento de fin

Representa el **final del proceso**.

Se representa con un **círculo rojo**.

---

## ✏️ Analizar el flujo del proceso

Intentar responder a las siguientes preguntas observando el diagrama:

* ¿Dónde empieza el proceso?
* ¿Qué actividades se ejecutan?
* ¿En qué orden se ejecutan?
* ¿Dónde termina el proceso?

---

## 📌 Conclusión

Un modelo BPMN describe **cómo fluye un proceso de negocio** desde que empieza hasta que finaliza.

El motor de procesos utilizará este modelo para **ejecutar el workflow paso a paso**.

En el siguiente paso crearemos **nuestro primer proceso BPMN**.

---

## 📚 Referencia

[Elementos BPMN – referencia rápida](../../docs/referencia/elementos-bpmn.md)
