# RuntimeService

## 🎯 Objetivo

Explorar el **RuntimeService** del motor Camunda y utilizarlo para interactuar con procesos en ejecución.

---

## 🧠 Contexto

Camunda expone distintas APIs para interactuar con el motor.

Una de las más importantes es:

```
RuntimeService
```

Este servicio permite trabajar con **instancias de proceso activas**.

Entre sus funciones principales se encuentran:

```
iniciar procesos
consultar instancias activas
enviar mensajes a procesos
gestionar variables de ejecución
```

Se utiliza habitualmente desde aplicaciones Java para controlar la ejecución de procesos.

---

# Localizar RuntimeService en el proyecto

Abrir la clase principal de la aplicación:

```
backend/src/main/java/com/example/workflow/WorkflowAppApplication.java
```

En esta clase ya se utiliza el servicio:

```java
RuntimeService runtimeService
```

Este servicio es proporcionado automáticamente por **Spring Boot y Camunda**.

---

# Crear un componente de prueba

Crear el siguiente archivo:

```
backend/src/main/java/com/example/workflow/service/RuntimeExplorer.java
```

---

# Implementar el componente

Añadir el siguiente código:

```java
package com.example.workflow.service;

import org.camunda.bpm.engine.RuntimeService;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;

@Component
public class RuntimeExplorer {

    private final RuntimeService runtimeService;

    public RuntimeExplorer(RuntimeService runtimeService) {
        this.runtimeService = runtimeService;
    }

    @PostConstruct
    public void exploreRuntimeService() {

        long instanceCount = runtimeService
                .createProcessInstanceQuery()
                .count();

        System.out.println("Instancias activas: " + instanceCount);

    }
}
```

---

# Qué hace este código

Cuando la aplicación arranca:

```
Spring Boot inicia
       │
       ▼
RuntimeExplorer se crea
       │
       ▼
@PostConstruct se ejecuta
       │
       ▼
RuntimeService consulta instancias activas
```

El resultado se mostrará en la consola.

---

# Compilar el proyecto

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar el proyecto:

```bash
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar la aplicación:

```bash
mvn spring-boot:run
```

En la consola debería aparecer un mensaje similar a:

```
Instancias activas: 1
```

---

# Qué es RuntimeService

El **RuntimeService** permite trabajar con el estado actual del motor.

Ejemplos de operaciones posibles:

```
startProcessInstanceByKey()
createProcessInstanceQuery()
setVariable()
correlateMessage()
```

Estas operaciones permiten controlar el flujo de ejecución desde código.

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea el componente `RuntimeExplorer`
* se utiliza `RuntimeService`
* la aplicación muestra en consola el número de instancias activas.

---

## 📚 Referencia

[APIs Java de Camunda – referencia](../../docs/referencia/apis-java.md)
