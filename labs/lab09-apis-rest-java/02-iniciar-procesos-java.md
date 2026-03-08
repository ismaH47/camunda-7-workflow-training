# Iniciar procesos desde Java

## 🎯 Objetivo

Crear un componente que permita **iniciar instancias del proceso desde código Java** utilizando el `RuntimeService`.

---

## 🧠 Contexto

En Camunda los procesos pueden iniciarse de varias formas:

```
API Java
REST API
Cockpit
Eventos o mensajes
```

Cuando una aplicación backend controla el workflow, lo habitual es iniciar procesos mediante:

```
RuntimeService.startProcessInstanceByKey(...)
```

Esto crea una **nueva instancia del proceso BPMN**.

---

# Crear un servicio para iniciar procesos

Crear el archivo:

```
backend/src/main/java/com/example/workflow/service/ProcessStarter.java
```

---

# Implementar el servicio

Añadir el siguiente código:

```java
package com.example.workflow.service;

import org.camunda.bpm.engine.RuntimeService;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;
import java.util.HashMap;
import java.util.Map;

@Component
public class ProcessStarter {

    private final RuntimeService runtimeService;

    public ProcessStarter(RuntimeService runtimeService) {
        this.runtimeService = runtimeService;
    }

    @PostConstruct
    public void startProcess() {

        Map<String, Object> variables = new HashMap<>();

        variables.put("solicitante", "maria");
        variables.put("importe", 3000);
        variables.put("tipoSolicitud", "compra");

        runtimeService.startProcessInstanceByKey("approval-process", variables);

        System.out.println("Proceso approval-process iniciado");

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
ProcessStarter se crea
        │
        ▼
@PostConstruct se ejecuta
        │
        ▼
RuntimeService inicia una instancia del proceso
```

La instancia del proceso se creará automáticamente.

---

# Compilar el proyecto

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar:

```bash
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar el backend:

```bash
mvn spring-boot:run
```

En la consola debería aparecer:

```
Proceso approval-process iniciado
```

---

# Verificar en Cockpit

Abrir:

```
http://localhost:8081/camunda
```

Entrar en **Cockpit**.

Ir a:

```
Processes
```

Seleccionar:

```
approval-process
```

En **Process Instances** debería aparecer una nueva instancia.

---

# Verificar el flujo

La instancia ejecutará:

```
Timer Event
Message Event
Service Task
User Task
Gateway
```

El proceso se podrá seguir visualmente desde Cockpit.

---

# Qué ocurre internamente

Cuando se ejecuta el método:

```
startProcessInstanceByKey(...)
```

Camunda realiza lo siguiente:

```
crear instancia del proceso
crear contexto de ejecución
asignar variables iniciales
iniciar ejecución del flujo BPMN
```

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea el componente `ProcessStarter`
* el proceso se inicia automáticamente al arrancar la aplicación
* la instancia aparece en **Camunda Cockpit**.

---

## 📚 Referencia

[APIs Java de Camunda – referencia](../../docs/referencia/apis-java.md)
