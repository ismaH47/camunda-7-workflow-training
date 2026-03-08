# Expresiones EL

## 🎯 Objetivo

Utilizar **expresiones EL (Expression Language)** dentro del modelo BPMN para acceder a variables del proceso.

---

## 🧠 Contexto

Camunda permite utilizar **expresiones EL** dentro de los modelos BPMN.

Las expresiones permiten:

* acceder a variables del proceso
* invocar beans de Spring
* realizar evaluaciones simples

Las expresiones se escriben utilizando la sintaxis:

```id="i6t6xn"
${ ... }
```

Por ejemplo:

```id="u9t5xg"
${importe}
${solicitante}
${estadoSolicitud}
```

Estas expresiones se evalúan durante la ejecución del proceso.

---

# Abrir el modelo BPMN

Abrir el archivo:

```
model/approval-process.bpmn
```

Editar el modelo con **Camunda Modeler**.

---

# Seleccionar la User Task

Seleccionar la tarea:

```
Aprobar solicitud
```

---

# Configurar el nombre dinámico de la tarea

En el panel de propiedades localizar el campo:

```
Name
```

Modificar el nombre de la tarea utilizando una expresión.

Cambiar el valor por:

```id="p5t7j9"
Aprobar solicitud de ${solicitante}
```

Esto hará que el nombre de la tarea incluya el nombre del solicitante.

---

# Guardar el modelo

Guardar el archivo:

```
model/approval-process.bpmn
```

---

# Copiar el modelo al backend

Actualizar el modelo desplegado en el backend:

```bash id="v4x8po"
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

---

# Ejecutar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Ejecutar la aplicación:

```bash id="k8j5rb"
mvn spring-boot:run
```

Esto iniciará una nueva instancia del proceso.

---

# Verificar la tarea en Tasklist

Abrir:

```
http://localhost:8081/camunda/app/tasklist
```

Localizar la tarea creada.

El nombre de la tarea debería aparecer como:

```id="3t7mzd"
Aprobar solicitud de juan
```

Esto indica que la expresión EL ha sido evaluada utilizando la variable del proceso.

---

# Qué ha ocurrido

Durante la ejecución del proceso:

```id="5zq2nh"
variable solicitante
      │
      ▼
expresión EL en BPMN
      │
      ▼
nombre dinámico de la tarea
```

El motor evalúa la expresión utilizando las variables disponibles en la instancia del proceso.

---

# Comprobación

El ejercicio se considera completado cuando:

* el nombre de la tarea contiene una expresión EL
* la tarea aparece en Tasklist con el nombre dinámico
* la expresión utiliza correctamente la variable `solicitante`.

---

## 📚 Referencia

[Expresiones EL en Camunda – referencia](../../docs/referencia/expresiones-el.md)
