# Integración con servicios externos

## 🎯 Objetivo

Simular una **llamada a un servicio externo** desde una Service Task del proceso.

---

## 🧠 Contexto

Los procesos de negocio suelen interactuar con sistemas externos.

Ejemplos comunes:

```id="z3b3zl"
APIs REST
microservicios
sistemas de pagos
servicios de notificación
```

En Camunda estas integraciones suelen implementarse dentro de **Service Tasks** mediante código Java.

En este ejercicio se simulará una llamada a un servicio externo desde un `JavaDelegate`.

---

# Crear un servicio externo simulado

Crear el archivo:

```id="60nh3v"
backend/src/main/java/com/example/workflow/service/ServicioValidacion.java
```

---

# Implementar el servicio

Añadir el siguiente código:

```java id="fay8vo"
package com.example.workflow.service;

import org.springframework.stereotype.Service;

@Service
public class ServicioValidacion {

    public boolean validarSolicitud(Integer importe) {

        System.out.println("Llamando a servicio externo de validación");

        if (importe < 5000) {
            return true;
        }

        return false;
    }
}
```

Este servicio simula una validación realizada por un sistema externo.

---

# Modificar el delegate

Abrir el archivo:

```id="jq0ze5"
ValidarSolicitudDelegate.java
```

Modificar el delegate para llamar al servicio.

```java id="69kbv9"
package com.example.workflow.delegate;

import com.example.workflow.service.ServicioValidacion;
import org.camunda.bpm.engine.delegate.DelegateExecution;
import org.camunda.bpm.engine.delegate.JavaDelegate;
import org.springframework.stereotype.Component;

@Component
public class ValidarSolicitudDelegate implements JavaDelegate {

    private final ServicioValidacion servicio;

    public ValidarSolicitudDelegate(ServicioValidacion servicio) {
        this.servicio = servicio;
    }

    @Override
    public void execute(DelegateExecution execution) {

        Integer importe = (Integer) execution.getVariable("importe");

        boolean resultado = servicio.validarSolicitud(importe);

        execution.setVariable("estadoSolicitud", resultado ? "VALIDADA" : "RECHAZADA");

        System.out.println("Resultado validación: " + resultado);

    }
}
```

---

# Compilar el proyecto

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar:

```bash id="s7x2h6"
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar el backend:

```bash id="j9b0kp"
mvn spring-boot:run
```

Cuando el proceso llegue a la Service Task se ejecutará el delegate y se llamará al servicio.

---

# Observar la ejecución

En la consola deberían aparecer mensajes similares a:

```id="0xf5fq"
Llamando a servicio externo de validación
Resultado validación: true
```

Esto confirma que el proceso ha interactuado con el servicio.

---

# Flujo del proceso

La integración ocurre dentro del flujo:

```id="hm5e4t"
Proceso BPMN
      │
      ▼
Service Task
      │
      ▼
JavaDelegate
      │
      ▼
Servicio externo
```

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea el servicio `ServicioValidacion`
* el delegate llama al servicio
* el resultado se guarda como variable del proceso
* el mensaje aparece en la consola durante la ejecución.
# Integración con servicios externos

## 🎯 Objetivo

Simular una **llamada a un servicio externo** desde una Service Task del proceso.

---

## 🧠 Contexto

Los procesos de negocio suelen interactuar con sistemas externos.

Ejemplos comunes:

```id="z3b3zl"
APIs REST
microservicios
sistemas de pagos
servicios de notificación
```

En Camunda estas integraciones suelen implementarse dentro de **Service Tasks** mediante código Java.

En este ejercicio se simulará una llamada a un servicio externo desde un `JavaDelegate`.

---

# Crear un servicio externo simulado

Crear el archivo:

```id="60nh3v"
backend/src/main/java/com/example/workflow/service/ServicioValidacion.java
```

---

# Implementar el servicio

Añadir el siguiente código:

```java id="fay8vo"
package com.example.workflow.service;

import org.springframework.stereotype.Service;

@Service
public class ServicioValidacion {

    public boolean validarSolicitud(Integer importe) {

        System.out.println("Llamando a servicio externo de validación");

        if (importe < 5000) {
            return true;
        }

        return false;
    }
}
```

Este servicio simula una validación realizada por un sistema externo.

---

# Modificar el delegate

Abrir el archivo:

```id="jq0ze5"
ValidarSolicitudDelegate.java
```

Modificar el delegate para llamar al servicio.

```java id="69kbv9"
package com.example.workflow.delegate;

import com.example.workflow.service.ServicioValidacion;
import org.camunda.bpm.engine.delegate.DelegateExecution;
import org.camunda.bpm.engine.delegate.JavaDelegate;
import org.springframework.stereotype.Component;

@Component
public class ValidarSolicitudDelegate implements JavaDelegate {

    private final ServicioValidacion servicio;

    public ValidarSolicitudDelegate(ServicioValidacion servicio) {
        this.servicio = servicio;
    }

    @Override
    public void execute(DelegateExecution execution) {

        Integer importe = (Integer) execution.getVariable("importe");

        boolean resultado = servicio.validarSolicitud(importe);

        execution.setVariable("estadoSolicitud", resultado ? "VALIDADA" : "RECHAZADA");

        System.out.println("Resultado validación: " + resultado);

    }
}
```

---

# Compilar el proyecto

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar:

```bash id="s7x2h6"
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar el backend:

```bash id="j9b0kp"
mvn spring-boot:run
```

Cuando el proceso llegue a la Service Task se ejecutará el delegate y se llamará al servicio.

---

# Observar la ejecución

En la consola deberían aparecer mensajes similares a:

```id="0xf5fq"
Llamando a servicio externo de validación
Resultado validación: true
```

Esto confirma que el proceso ha interactuado con el servicio.

---

# Flujo del proceso

La integración ocurre dentro del flujo:

```id="hm5e4t"
Proceso BPMN
      │
      ▼
Service Task
      │
      ▼
JavaDelegate
      │
      ▼
Servicio externo
```

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea el servicio `ServicioValidacion`
* el delegate llama al servicio
* el resultado se guarda como variable del proceso
* el mensaje aparece en la consola durante la ejecución.
