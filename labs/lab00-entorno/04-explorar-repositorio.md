# Explorar el repositorio

## 🎯 Objetivo

Comprender la estructura del repositorio que se utilizará durante todo el curso.

Antes de empezar a trabajar con Camunda es importante identificar dónde se encuentran:

* los laboratorios
* el backend de la aplicación
* los modelos BPMN
* los archivos de infraestructura

---

## 📁 Ver estructura del repositorio

Abre una **terminal** en VS Code (menú **Terminal** → **New Terminal**). Asegúrate de estar en la **raíz del repositorio** (la carpeta donde está el **README.md** del proyecto; si acabas de abrir el repo, ya estarás ahí). Ejecuta:

```bash
tree
```

Deberías ver una estructura similar a esta:

```
.
├── README.md
├── backend
├── docs
├── infra
├── labs
└── model
```

---

## 📦 Descripción de los directorios principales

### README.md

Archivo principal del repositorio.

Describe:

* el objetivo del curso
* las tecnologías utilizadas
* cómo ejecutar los laboratorios

---

### backend

Contiene la **aplicación Spring Boot** donde se ejecutará el motor Camunda.

Aquí se encuentra:

* código Java
* configuración del proyecto
* dependencias Maven
* lógica de negocio

Durante el curso iremos modificando este directorio.

---

### docs

Documentación de referencia del curso: elementos BPMN, arquitectura de Camunda, expresiones EL, gateways, APIs Java, etc.

Ver el índice completo en [docs/README.md](../../docs/README.md).

---

### infra

Contiene archivos relacionados con el entorno o infraestructura.

Por ejemplo:

* configuraciones
* scripts de entorno
* archivos de despliegue

---

### labs

Este es el directorio más importante del curso.

Contiene **todos los laboratorios** organizados de forma secuencial.

Ejemplo:

```
labs/
 ├── lab00-entorno
 ├── lab01-bpmn-introduccion
 ├── lab02-arquitectura-camunda
 ├── lab03-instalacion-motor
 └── ...
```

Cada laboratorio contiene varios archivos `.md` con instrucciones paso a paso.

Los laboratorios deben ejecutarse **en orden**.

---

### model

Este directorio almacenará los **modelos BPMN** que se crearán durante el curso.

Los procesos de negocio diseñados con **Camunda Modeler** se guardarán aquí.

Los archivos tendrán extensión:

```
.bpmn
```

---

## 🔎 Explorar el directorio labs

En el **explorador de archivos** de VS Code (barra lateral **izquierda**), haz clic en la carpeta **labs** para expandirla. Verás los distintos laboratorios (lab00-entorno, lab01-bpmn-introduccion, etc.).

Cada laboratorio incluye varios archivos con pasos numerados.

Por ejemplo:

```
lab00-entorno
├── 01-instalar-extensiones-vscode.md
├── 02-verificar-java.md
├── 03-verificar-maven.md
├── 04-explorar-repositorio.md
├── 05-compilar-proyecto.md
├── 06-arrancar-aplicacion.md
└── README.md
```

Esto indica el orden en el que deben ejecutarse los pasos.

---

## ✅ Comprobación

Antes de continuar asegúrate de poder:

* navegar por el repositorio en VS Code
* abrir archivos `.md`
* localizar el directorio `labs`
* localizar el directorio `backend`

Una vez entendido el repositorio podemos continuar con el siguiente paso del laboratorio.
