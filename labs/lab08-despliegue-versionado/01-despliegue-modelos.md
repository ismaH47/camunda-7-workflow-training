# Despliegue de modelos BPMN

## 🎯 Objetivo

Comprender cómo **Camunda despliega automáticamente los modelos BPMN** y verificar qué ocurre cuando se añade o modifica un proceso.

---

## 🧠 Contexto

Cuando se utiliza **Camunda con Spring Boot**, el motor escanea automáticamente el directorio:

```
src/main/resources
```

Dentro de este directorio existe una carpeta especial utilizada por el starter de Camunda:

```
src/main/resources/processes
```

Todos los archivos BPMN que se encuentren en esta carpeta se **desplegarán automáticamente al arrancar la aplicación**.

Esto permite que los procesos estén versionados junto al código.

---

# Verificar el directorio de procesos

Abrir el directorio del backend:

```
backend/src/main/resources
```

Debería existir el directorio:

```
processes
```

Listar su contenido:

```bash
ls backend/src/main/resources/processes
```

Debería aparecer el modelo creado anteriormente:

```
approval-process.bpmn
```

---

# Arrancar la aplicación

En la **terminal**, desde la **raíz del repositorio** ejecuta `cd backend`. Luego:

Ejecutar la aplicación:

```bash
mvn spring-boot:run
```

Durante el arranque Camunda detectará los modelos BPMN.

---

# Observar el despliegue en los logs

En la consola deberían aparecer mensajes similares a:

```
ENGINE-08024 Found 1 process definitions.
ENGINE-08024 Deployment successful
```

Esto indica que el modelo BPMN ha sido desplegado correctamente.

---

# Verificar el despliegue en Cockpit

Abrir el navegador:

```
http://localhost:8081/camunda
```

Entrar en **Cockpit**.

Ir a la sección:

```
Deployments
```

Aquí se pueden observar todos los despliegues realizados por el motor.

Cada despliegue incluye:

* el archivo BPMN
* la fecha de despliegue
* la versión del proceso

---

# Explorar el proceso desplegado

Ir a:

```
Processes
```

Seleccionar:

```
approval-process
```

En esta pantalla se puede ver:

* el diagrama BPMN
* el número de instancias activas
* estadísticas del proceso

---

# Qué ocurre durante el despliegue

Cuando la aplicación arranca ocurre lo siguiente:

```
Spring Boot inicia
        │
        ▼
Camunda escanea resources/processes
        │
        ▼
Encuentra archivos BPMN
        │
        ▼
Crea un Deployment
        │
        ▼
Registra el proceso en el motor
```

---

# Experimento práctico

Modificar el nombre del proceso en el modelo BPMN.

Abrir:

```
model/approval-process.bpmn
```

Cambiar el nombre del proceso a:

```
Approval Process V2
```

Guardar el archivo.

Copiar nuevamente el modelo al backend:

```bash
cp model/approval-process.bpmn backend/src/main/resources/processes/
```

Reiniciar la aplicación.

---

# Observar el nuevo despliegue

Entrar en **Cockpit → Deployments**.

Debería aparecer **un nuevo despliegue** del mismo proceso.

Esto demuestra que cada vez que se despliega un modelo, Camunda crea una nueva versión.

---

# Comprobación

El ejercicio se considera completado cuando:

* el proceso BPMN aparece en **Deployments**
* el motor despliega el modelo automáticamente
* al modificar el modelo se genera un nuevo despliegue.
