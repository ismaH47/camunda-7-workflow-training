# Camunda 7 Workflow Training

El curso está diseñado como una **cadena de laboratorios progresivos**.
Cada laboratorio introduce nuevos conceptos mientras evoluciona una aplicación de ejemplo.

El objetivo es comprender:

* qué es Camunda
* cómo se modelan procesos BPMN
* cómo se integran con aplicaciones Java
* cómo se despliegan y operan
* cómo se depuran y mantienen

---

# Estructura del curso

El curso está organizado en **laboratorios secuenciales**.

Cada laboratorio amplía el sistema construido en el anterior.

```
labs/
 ├── lab00-entorno
 ├── lab01-bpmn-introduccion
 ├── lab02-arquitectura-camunda
 ├── lab03-instalacion-motor
 ├── lab04-modelado-procesos
 ├── lab05-service-user-tasks
 ├── lab06-variables-expresiones
 ├── lab07-gateways-eventos
 ├── lab08-despliegue-versionado
 ├── lab09-apis-rest-java
 ├── lab10-errores-compensaciones
 ├── lab11-operacion-ui
 ├── lab12-integraciones
 ├── lab13-seguridad
 └── lab14-testing-monitorizacion
```

---

# Herramientas utilizadas

Durante el curso se utilizarán las siguientes herramientas:

* GitHub Codespaces
* Java 17
* Maven
* Spring Boot
* Camunda 7
* Camunda Modeler
* Docker

---

# Arquitectura del sistema de ejemplo

Durante el curso se desarrollará una aplicación basada en la siguiente arquitectura:

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

El motor Camunda gestionará el estado de los procesos mientras la aplicación Java ejecutará la lógica de negocio.

---

# Metodología del curso

El curso sigue el siguiente enfoque:

1. Preparar el entorno de desarrollo
2. Comprender BPMN y modelar procesos
3. Integrar procesos con código Java
4. Ejecutar y monitorizar procesos
5. Gestionar errores y eventos
6. Integrar servicios externos
7. Desplegar y operar el sistema

Cada laboratorio contiene:

* objetivos
* pasos a seguir
* código a implementar
* comprobaciones de funcionamiento

---

# Cómo seguir el curso

1. Abrir el repositorio en **GitHub Codespaces**
2. Ejecutar los laboratorios en orden
3. Modificar la aplicación progresivamente

Los laboratorios están diseñados para ser **completados de forma secuencial**.

---

# Resultado final

Al completar el curso se habrá construido un sistema completo basado en Camunda que incluye:

* procesos BPMN
* lógica Java
* integración con APIs
* gestión de tareas de usuario
* monitorización y operación del motor
