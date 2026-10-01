# Guion de entrevista

> **Proyecto:** Sistema de reservaciones y control de paquetes  
> **Fecha:** 22/09/2026


### Apertura

Hola, este proyecto está enfocado en mejorar la forma en la que se organizan las reservaciones del local dentro de Communa y se lleva el control de los paquetes.

La idea de esta entrevista es entender cómo hacen actualmente este proceso, qué problemas llegan a tener y qué cosas serían importantes mejorar.

También quiero confirmar algunas ideas que tenemos para el sistema y ver si realmente son necesarias.

---

### Contexto

**C1.** Cuéntame un poco cómo funciona actualmente la renta del cuarto.

**C2.** ¿Quiénes utilizan actualmente el cuarto y quién se encarga de organizar sus reservaciones?

**C3.** Cuando una persona quiere utilizar el cuarto, ¿cómo se pone de acuerdo contigo para elegir una fecha y un horario?

**C4.** ¿Cómo llevas actualmente el control de las reservaciones y de los paquetes?

---

### Proceso actual

**P1.** Cuéntame qué pasa normalmente desde que una persona te pide reservar el cuarto hasta que termina su sesión.

**P2.** Cuando alguien quiere reservar, ¿cómo revisas si el horario que quiere está disponible?

**P3.** ¿Cómo registras actualmente una reservación y qué información necesitas guardar?

**P4.** ¿Cómo llevas el control de los paquetes y cómo sabes cuántos usos le quedan a cada persona?

**P5.** ¿Qué pasa cuando una persona llega al último uso de su paquete?

---

### Dificultades del proceso actual

**D1.** ¿Qué es lo que más se te complica al momento de organizar las reservaciones?

**D2.** ¿Alguna vez ha pasado que dos reservaciones se empalmen? Cuéntame qué pasó y cómo lo resolvieron.

**D3.** ¿Te ha pasado que una persona termine los usos de su paquete y no te des cuenta inmediatamente?

**D4.** ¿Qué es lo más complicado de llevar el control de los usos que le quedan a cada persona?

**D5.** Si pudieras mejorar una parte de este proceso, ¿cuál sería?

---

### Excepciones y situaciones especiales

**E1.** ¿Qué hacen cuando una persona necesita cambiar la fecha o el horario de una reservación?

**E2.** ¿Qué pasa cuando una persona cancela una reservación?

**E3.** ¿Qué hacen si una persona tiene una reservación pero no asiste?

**E4.** Si una persona ya utilizó todos los usos de su paquete, ¿qué pasa la siguiente vez que quiere utilizar el cuarto?

**E5.** ¿En qué momento consideran que un uso del paquete ya fue utilizado?

---

### Verificación de supuestos

Estas preguntas se hicieron para revisar algunas de las ideas que teníamos antes de definir los requisitos del sistema y comprobar cuáles realmente eran necesarias.

#### Requisitos funcionales

**Validación 1. Reservaciones**

**Supuesto:** Es necesario tener un registro de las reservaciones del cuarto.

**Pregunta:** ¿Qué información necesitas consultar de una reservación para poder organizar el uso del cuarto?

---

**Validación 2. Horarios disponibles**

**Supuesto:** La persona necesita conocer qué horarios están disponibles antes de hacer una reservación.

**Pregunta:** ¿Cómo sabes actualmente qué horarios están libres y cuáles ya están ocupados?

---

**Validación 3. Empalmes de reservaciones**

**Supuesto:** El sistema debe evitar que dos personas reserven el cuarto en la misma fecha y horario.

**Pregunta:** ¿Qué pasa actualmente cuando dos personas quieren utilizar el cuarto en el mismo horario?

---

**Validación 4. Paquetes**

**Supuesto:** Se manejan paquetes de 5 y 10 usos.

**Pregunta:** ¿Qué tipos de paquetes manejan actualmente y cómo llevas el registro de estos?

---

**Validación 5. Usos disponibles**

**Supuesto:** Es necesario saber cuántos usos le quedan a cada persona.

**Pregunta:** ¿Cómo sabes actualmente cuántos usos le quedan a una persona y qué pasa cuando llega al último?

---

**Validación 6. Consulta de reservaciones**

**Supuesto:** La encargada necesita consultar las reservaciones que ya se encuentran registradas.

**Pregunta:** Cuando necesitas revisar quién utilizará el cuarto, ¿qué información buscas y cómo la consultas actualmente?

---

#### Requisitos no funcionales

**Validación 7. Consistencia de los usos**

**Supuesto:** La cantidad de usos que muestra el sistema debe coincidir con los usos reales que tiene disponibles la persona.

**Pregunta:** ¿Qué problemas podría causar que el número de usos registrados no coincida con los usos que realmente le quedan a una persona?

---

**Validación 8. Facilidad de uso**

**Supuesto:** Registrar una reservación debe ser un proceso sencillo y no debería necesitar capacitación previa.

**Pregunta:** ¿Qué parte del proceso actual te parece más tardada o complicada y cómo te gustaría que fuera?

---

**Validación 9. Permanencia de las reservaciones**

**Supuesto:** Las reservaciones registradas deben seguir disponibles para consultarlas después.

**Pregunta:** Este punto no se preguntó directamente durante la entrevista, por lo que queda pendiente de confirmar.

---

### Cierre

Para terminar, repasamos los puntos principales sobre cómo se hacen actualmente las reservaciones, cómo funcionan los paquetes y cuáles son los problemas que se presentan.

También quedaron algunas situaciones que todavía necesitamos definir mejor.

¿Hay algo importante sobre las reservaciones o los paquetes que no hayamos mencionado?

Gracias por tu tiempo y por ayudarme a entender mejor cómo funciona actualmente este proceso.

---

# 2. Bitácora de la entrevista

## Supuestos confirmados

- **Paquetes:** Se confirmó que se manejan paquetes de 5 y 10 usos.

- **Control de usos:** Es importante saber cuántos usos le quedan disponibles a cada persona.

- **Empalmes:** Se confirmó que uno de los problemas es que las reservaciones pueden llegar a empalmarse.

- **Consulta de reservaciones:** La encargada necesita saber qué reservaciones están registradas para poder organizar los horarios del cuarto.

- **Último uso del paquete:** Cuando una persona está utilizando su último uso puede terminar esa sesión normalmente. Para continuar utilizando el cuarto después necesita comprar otro paquete.

---

## Supuestos que resultaron falsos o se modificaron

- **Alcance del sistema:** Al principio se habían considerado otros problemas del negocio, como inventario y otros procesos administrativos. Después se decidió que el sistema no necesita cubrir todo el negocio y que el proyecto se enfocará solamente en las reservaciones del cuarto y el control de paquetes.

Esto ayudó a hacer el alcance más específico y evitar agregar funciones que no están relacionadas directamente con el problema principal.

---

## Hallazgos inesperados

- **Fin del paquete:** Se identificó que una persona puede llegar al último uso de su paquete sin que se detecte inmediatamente que necesita comprar uno nuevo.

- **Relación entre reservaciones y paquetes:** No solamente es importante organizar los horarios. También es necesario tener claro cuántos usos le quedan a cada persona.

- **Situaciones especiales:** Durante el análisis aparecieron casos como cancelaciones, inasistencias y cambios de horario que necesitan reglas más claras antes de incluirlos como requisitos definitivos.

---

## Supuestos que no se verificaron en la entrevista

- **Cancelaciones:** No se confirmó qué debe pasar con el uso del paquete cuando una persona cancela una reservación.

- **Inasistencias:** No se preguntó qué debe pasar cuando una persona reserva pero no asiste.

- **Cambio de horario:** No quedó definida la regla que se debe seguir cuando una persona quiere cambiar una reservación.

- **Momento en que se descuenta un uso:** No se confirmó si el uso debe descontarse al reservar, al llegar o al terminar la sesión.

- **Permanencia de las reservaciones:** No se preguntó directamente si las reservaciones deben permanecer disponibles después de salir y volver a entrar al sistema.

Estos puntos quedan pendientes de confirmar antes de convertirlos en reglas definitivas del sistema.

---

# 3. Ficha de dominio

### Omar Enrique Buenrostro Islas   

### QUIÉN ERES

Eres la encargada de un negocio donde se renta un cuarto que actualmente utilizan dos personas.

Tú te encargas de organizar las reservaciones y también de llevar el control de los paquetes que compra cada persona a quien le rentas en local.

---

### Cómo es tu día

Durante el día necesitas saber quién va a utilizar el local, en qué fecha y en qué horario.

También necesitas llevar el control de los usos que le quedan a cada persona para saber cuándo termina su paquete.

Actualmente se manejan paquetes de 5 y 10 usos.

---

### Reglas que conocemos
- Los paquetes son de 5 o 10 usos.
- No deberían existir dos reservaciones para el cuarto en el mismo horario.
- Necesitas saber cuántos usos le quedan a cada persona.
- Cuando una persona utiliza el último uso de su paquete puede terminar esa sesión normalmente.
- Para seguir utilizando el cuarto después debe comprar otro paquete.
- Necesitas consultar las reservaciones para saber qué horarios ya están ocupados.

---

### Excepción que ocurre

Puede pasar que una persona termine los usos de su paquete y no se detecte inmediatamente.

También pueden presentarse cambios de horario, cancelaciones o personas que no asisten a una reservación. Algunas de estas situaciones todavía no tienen una regla completamente definida.

---

### Lo que molesta

Uno de los principales problemas es que las reservaciones pueden llegar a empalmarse.

También es complicado llevar el control de cuántos usos le quedan a cada persona, ya que puede pasar que alguien llegue al final de su paquete y no se detecte inmediatamente.

Lo que buscas es tener una forma más clara de consultar las reservaciones y los usos disponibles.

