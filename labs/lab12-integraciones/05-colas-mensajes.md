# Integración con colas de mensajes

## 🎯 Objetivo

Conectar el proceso BPMN con una **cola de mensajes**: el proceso envía eventos a la cola o reacciona a mensajes recibidos (por ejemplo para desbloquear un evento de mensaje o alimentar una External Task).

---

## 🧠 Contexto

En arquitecturas reales los procesos suelen integrarse con:

* **Colas (RabbitMQ, Apache Kafka, JMS)**: para desacoplar productores y consumidores, garantizar entrega o procesar picos de carga.
* Flujo típico: el proceso publica un mensaje (ej. "Solicitud creada") o una **External Task** es completada por un worker que a su vez consume de una cola; alternativamente, un consumidor de la cola llama a la **REST API** de Camunda para correlacionar un mensaje con un proceso (message event) o completar una tarea.

Patrones habituales:

1. **Proceso → cola**: una Service Task (o delegate) publica en la cola; un sistema externo procesa.
2. **Cola → proceso**: un worker consume de la cola y, según el mensaje, inicia un proceso o envía un mensaje de correlación a una instancia en espera (`RuntimeService.createMessageCorrelation()`).
3. **External Task + cola**: el worker que completa la External Task obtiene el trabajo desde una cola (en lugar de solo desde Camunda); el motor sigue siendo quien crea la tarea y el worker la completa tras procesar el mensaje.

---

## 📋 Opción A: Worker que consume de cola y completa External Task

1. El proceso tiene una **External Task** con un topic (ej. `procesar-solicitud`).
2. Un worker (en la misma app o en otro servicio) en bucle:
   * Consume un mensaje de la cola (RabbitMQ, Kafka, JMS).
   * Llama a `fetchAndLock` para esa topic, recibe la External Task.
   * Procesa el mensaje y la tarea juntos (ej. actualiza BD, llama a API).
   * Completa la tarea con `complete()`.

Así la cola alimenta al worker y el motor sigue controlando el flujo del proceso.

---

## 📋 Opción B: Cola dispara correlación con proceso

1. El proceso tiene un **Message Event** (intermedio o en el límite) con un nombre (ej. `solicitud-recibida`).
2. Una instancia queda en espera en ese evento.
3. Un consumidor de cola, al recibir un mensaje, obtiene el id de proceso o de negocio (business key) y llama a la API REST o Java:

   ```java
   runtimeService.createMessageCorrelation("solicitud-recibida")
     .processInstanceBusinessKey(businessKey)
     .setVariable("payload", mensajeDeCola)
     .correlate();
   ```

4. La instancia continúa con el flujo.

---

## 📌 Configuración práctica

Para un ejercicio en el curso:

* **Sin cola real:** Simula el consumidor con un endpoint REST (en un controlador de tu app, por ejemplo en el mismo módulo donde arranca Camunda) o un scheduler que lea de una lista en memoria y llame a `createMessageCorrelation` o complete una External Task. El objetivo es entender el flujo proceso ↔ cola. La URL del endpoint o la lógica del scheduler la defines tú; lo importante es que en algún momento se invoque la API de Camunda (RuntimeService o REST) para correlacionar el mensaje o completar la tarea.
* **Con cola real:** Añade RabbitMQ (o Kafka) en Docker; en el proyecto, la configuración de la conexión al broker suele ir en **src/main/resources/application.yml** (o application.properties): URL, usuario, cola o topic. La dependencia (spring-boot-starter-amqp o kafka) va en el **pom.xml**. El listener `@RabbitListener` o `@KafkaListener` ponlo en una clase de tu aplicación (por ejemplo en un paquete `listener` o `consumer`); en el callback invoca `RuntimeService.createMessageCorrelation(...)` o el cliente REST de Camunda para completar la tarea.

---

## 📌 Comprobación

Inicia un proceso que quede en espera en un message event; envía un mensaje a la cola (o llama al endpoint/simulador que hayas hecho). Abre **Cockpit** (normalmente en `http://localhost:8080/camunda` o el puerto de tu app) y en la vista de procesos verifica que la instancia avanza. Si usas External Task: comprueba que el worker consume de la cola y completa la tarea y que en Cockpit el proceso continúa.

---

## 📌 Conclusión

La integración con colas permite que procesos BPMN se disparen o avancen desde sistemas asíncronos; el motor mantiene el estado del proceso y la cola aporta escalabilidad y desacoplamiento.
