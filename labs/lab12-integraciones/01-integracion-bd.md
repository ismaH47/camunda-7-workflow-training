# Integración con base de datos

## 🎯 Objetivo

Integrar el proceso con una **base de datos utilizando Spring Data JPA** para guardar información generada por el workflow.

---

## 🧠 Contexto

En aplicaciones reales los procesos suelen interactuar con sistemas externos.

Uno de los casos más habituales es **guardar información en una base de datos**.

En este ejercicio se modificará el proceso para que, durante la ejecución, se registre una solicitud en la base de datos.

El flujo será:

```id="o1zq1m"
Proceso BPMN
      │
      ▼
Service Task
      │
      ▼
JavaDelegate
      │
      ▼
Repositorio JPA
      │
      ▼
Base de datos H2
```

---

# Crear una entidad JPA

Crear el archivo:

```id="i9p9cz"
backend/src/main/java/com/example/workflow/entity/Solicitud.java
```

---

# Código de la entidad

```java id="sqn1zz"
package com.example.workflow.entity;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
public class Solicitud {

    @Id
    @GeneratedValue
    private Long id;

    private String solicitante;

    private Integer importe;

    private String tipo;

    public Long getId() {
        return id;
    }

    public String getSolicitante() {
        return solicitante;
    }

    public void setSolicitante(String solicitante) {
        this.solicitante = solicitante;
    }

    public Integer getImporte() {
        return importe;
    }

    public void setImporte(Integer importe) {
        this.importe = importe;
    }

    public String getTipo() {
        return tipo;
    }

    public void setTipo(String tipo) {
        this.tipo = tipo;
    }
}
```

---

# Crear el repositorio JPA

Crear el archivo:

```id="cw9e36"
backend/src/main/java/com/example/workflow/repository/SolicitudRepository.java
```

---

# Código del repositorio

```java id="km1d2i"
package com.example.workflow.repository;

import com.example.workflow.entity.Solicitud;
import org.springframework.data.jpa.repository.JpaRepository;

public interface SolicitudRepository extends JpaRepository<Solicitud, Long> {
}
```

---

# Modificar el delegate

Abrir el archivo:

```id="izt2nh"
ValidarSolicitudDelegate.java
```

Actualizar el código para guardar la solicitud.

```java id="th4k8d"
package com.example.workflow.delegate;

import com.example.workflow.entity.Solicitud;
import com.example.workflow.repository.SolicitudRepository;
import org.camunda.bpm.engine.delegate.DelegateExecution;
import org.camunda.bpm.engine.delegate.JavaDelegate;
import org.springframework.stereotype.Component;

@Component
public class ValidarSolicitudDelegate implements JavaDelegate {

    private final SolicitudRepository repository;

    public ValidarSolicitudDelegate(SolicitudRepository repository) {
        this.repository = repository;
    }

    @Override
    public void execute(DelegateExecution execution) {

        String solicitante = (String) execution.getVariable("solicitante");
        Integer importe = (Integer) execution.getVariable("importe");
        String tipo = (String) execution.getVariable("tipoSolicitud");

        Solicitud solicitud = new Solicitud();
        solicitud.setSolicitante(solicitante);
        solicitud.setImporte(importe);
        solicitud.setTipo(tipo);

        repository.save(solicitud);

        System.out.println("Solicitud registrada en la base de datos");
    }
}
```

---

# Compilar el proyecto

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Compilar:

```bash id="r7eokh"
mvn clean package
```

---

# Ejecutar la aplicación

Arrancar el backend:

```bash id="clg3vo"
mvn spring-boot:run
```

Cuando el proceso llegue a la **Service Task**, se guardará una solicitud en la base de datos.

---

# Abrir la consola H2

Abrir el navegador:

```id="u0gmls"
http://localhost:8081/h2-console
```

Configurar:

```id="v6n1gx"
JDBC URL: jdbc:h2:mem:testdb
User: sa
Password: (vacío)
```

---

# Consultar la tabla

Ejecutar la consulta:

```sql id="s6gny1"
SELECT * FROM SOLICITUD;
```

Debería aparecer un registro generado por el proceso.

---

# Qué ocurre internamente

Durante la ejecución:

```id="epw7mu"
Service Task
      │
      ▼
JavaDelegate
      │
      ▼
Spring Data Repository
      │
      ▼
Base de datos H2
```

Esto demuestra cómo un proceso puede interactuar con sistemas externos.

---

# Comprobación

El ejercicio se considera completado cuando:

* se crea la entidad `Solicitud`
* el delegate guarda datos en la base de datos
* los registros aparecen en la consola H2.
