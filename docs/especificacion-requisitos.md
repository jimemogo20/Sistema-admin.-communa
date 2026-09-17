# Especificación de requisitos

## 1. Requisitos funcionales

### RF-001 — Registrar reservación

**Descripción:**  
El sistema registra una reservación del cuarto indicando usuario, fecha y horario.

**Origen:**  
Problema identificado en el proceso actual del negocio.

**Prioridad:**  
Imprescindible.

**Criterio de aceptación:**  
Al registrar una reservación con usuario, fecha y horario válidos, esta aparece registrada en el sistema.

**Relacionado con:**  
RF-002 y RF-003.

---

### RF-002 — Consultar disponibilidad

**Descripción:**  
El sistema muestra los horarios disponibles y ocupados del cuarto para una fecha seleccionada.

**Origen:**  
Necesidad identificada a partir de los empalmes que ocurren actualmente.

**Prioridad:**  
Imprescindible.

**Criterio de aceptación:**  
Al seleccionar una fecha, el sistema muestra qué horarios se encuentran disponibles y cuáles están ocupados.

**Relacionado con:**  
RF-001 y RF-003.

---

### RF-003 — Evitar empalmes

**Descripción:**  
El sistema impide registrar una reservación cuando el cuarto ya se encuentra reservado en el mismo horario.

**Origen:**  
Problema identificado en el proceso actual del negocio.

**Prioridad:**  
Imprescindible.

**Criterio de aceptación:**  
Si existe una reservación para un horario determinado y se intenta registrar otra que coincide con ese horario, el sistema rechaza la nueva reservación.

**Relacionado con:**  
RF-001 y RF-002.

---

### RF-004 — Registrar paquetes

**Descripción:**  
El sistema registra paquetes de 5 o 10 usos asociados a un usuario.

**Origen:**  
Regla actual del negocio.

**Prioridad:**  
Imprescindible.

**Criterio de aceptación:**  
Al registrar un paquete para un usuario, el sistema permite seleccionar un paquete de 5 o 10 usos y lo asocia al usuario correspondiente.

**Relacionado con:**  
RF-005.

---

### RF-005 — Consultar usos disponibles

**Descripción:**  
El sistema muestra la cantidad de usos disponibles del paquete asociado a cada usuario.

**Origen:**  
Problema identificado en el control actual de los paquetes.

**Prioridad:**  
Imprescindible.

**Criterio de aceptación:**  
Al consultar la información de un usuario con un paquete activo, el sistema muestra la cantidad de usos que tiene disponibles.

**Relacionado con:**  
RF-004.

---

## 2. Requisitos no funcionales

### RNF-CON-001 — Confiabilidad

**Atributo de calidad:**  
Confiabilidad.

**Descripción:**  
Una reservación confirmada permanece registrada hasta que sea modificada o cancelada mediante una acción autorizada.

**Métrica:**  
El 100% de las reservaciones confirmadas deben permanecer registradas mientras no exista una acción de modificación o cancelación.

**Origen:**  
Derivado del tipo de sistema de información y del atributo de confiabilidad identificado en la Visión del producto.

**Prioridad:**  
Imprescindible.

**Por qué importa:**  
La pérdida de una reservación podría provocar que un horario aparezca disponible cuando realmente ya está ocupado, generando un empalme.

**Afecta a:**  
RF-001, RF-002 y RF-003.

---

### RNF-USA-001 — Usabilidad

**Atributo de calidad:**  
Usabilidad.

**Descripción:**  
Un usuario nuevo completa el registro de una reservación sin capacitación previa.

**Métrica:**  
El usuario debe completar el registro de una reservación sin recibir instrucciones adicionales durante la prueba.

**Origen:**  
Derivado del atributo de usabilidad identificado en la Visión del producto.

**Prioridad:**  
Importante.

**Por qué importa:**  
Si el proceso de reservación resulta difícil de entender, los usuarios podrían continuar utilizando métodos externos para organizar sus horarios.

**Afecta a:**  
RF-001 y RF-002.

---

### RNF-CON-002 — Confiabilidad

**Atributo de calidad:**  
Confiabilidad.

**Descripción:**  
Los usos disponibles mostrados para un paquete coinciden con los usos registrados para ese paquete.

**Métrica:**  
En el 100% de las consultas, la cantidad mostrada debe coincidir con la cantidad de usos disponibles registrada para el paquete.

**Origen:**  
Derivado del atributo de confiabilidad identificado en la Visión del producto.

**Prioridad:**  
Imprescindible.

**Por qué importa:**  
Un conteo incorrecto puede provocar que una persona continúe utilizando el cuarto después de terminar su paquete o que se le indique incorrectamente que ya no tiene usos disponibles.

**Afecta a:**  
RF-004 y RF-005.

---

## 3. Verificación de los requisitos

Los ocho requisitos fueron redactados de manera que puedan convertirse en pruebas concretas.

Por ejemplo:

- Para RF-003 se puede registrar primero una reservación y después intentar registrar otra en el mismo horario. El sistema debe rechazar la segunda.
- Para RF-004 se puede registrar un paquete y comprobar que quede asociado al usuario correspondiente.
- Para RF-005 se puede consultar a un usuario con un paquete registrado y comprobar que aparezca la cantidad de usos disponibles.
- Para RNF-CON-001 se puede registrar una reservación, volver a consultarla y comprobar que la información permanezca registrada.
- Para RNF-USA-001 se puede pedir a un usuario nuevo que registre una reservación sin darle capacitación previa.

---

## 4. Supuestos por validar

Durante la elaboración de los requisitos se identificaron aspectos que todavía necesitan ser confirmados con los usuarios del sistema. Estos puntos no se consideran reglas definitivas hasta realizar la entrevista de elicitación.

- ¿En qué momento se descuenta un uso del paquete: al reservar, al comenzar la sesión o al terminarla?
- ¿Qué sucede con el uso si una reservación es cancelada?
- ¿Qué ocurre si la persona no se presenta a su reservación?
- ¿Una reservación ya registrada puede cambiarse de horario?
- ¿Quién tiene autorización para modificar o cancelar una reservación?
- ¿Existe una duración definida para cada uso del cuarto?
- ¿Los paquetes siempre serán únicamente de 5 y 10 usos?
- Después de terminar un paquete, ¿en qué momento debe registrarse la compra del siguiente paquete?
