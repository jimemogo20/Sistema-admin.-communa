# Guion de entrevista

## 1. Objetivo de la entrevista

El objetivo de esta entrevista fue entender mejor cómo se manejan actualmente las reservaciones del cuarto y los paquetes de usos. También queríamos conocer cuáles son los problemas que tienen actualmente y confirmar algunas cosas que habíamos pensado al inicio del proyecto.

Con las respuestas de la entrevista pudimos definir mejor qué necesita el sistema y qué cosas realmente vale la pena incluir.

---

## 2. Contexto

Primero hicimos algunas preguntas para conocer mejor cómo funciona actualmente la renta del cuarto.

1. ¿Cómo funciona actualmente la renta del cuarto?
2. ¿Quiénes utilizan el cuarto?
3. ¿Quién se encarga de organizar las reservaciones?
4. ¿Cómo pide una persona una fecha y un horario?
5. ¿Dónde anotan o guardan las reservaciones?
6. ¿Qué información necesitas tener de cada reservación?

---

## 3. Proceso actual

Después preguntamos cómo se hacen normalmente las reservaciones y cómo llevan el control de los paquetes.

1. ¿Qué pasa desde que una persona pide usar el cuarto hasta que termina su sesión?
2. ¿Cómo revisas si un horario está disponible?
3. ¿Cómo registras actualmente una reservación?
4. ¿Cómo sabes cuántos usos le quedan a cada persona?
5. ¿Qué paquetes manejan actualmente?
6. ¿Qué pasa cuando una persona llega al último uso de su paquete?
7. ¿Cómo sabes cuándo alguien necesita comprar otro paquete?
8. ¿Cómo consultas las reservaciones que ya tienes?

---

## 4. Problemas actuales

También preguntamos sobre las cosas que actualmente causan más problemas.

1. ¿Qué es lo que más se te complica al organizar las reservaciones?
2. ¿Ha pasado que dos reservaciones se empalmen en el mismo horario?
3. Si pasa un empalme, ¿qué hacen?
4. ¿Ha pasado que alguien termine su paquete y siga usando el cuarto porque no se dieron cuenta?
5. ¿Se te complica saber cuántos usos le quedan a cada persona?
6. ¿Qué información te gustaría poder consultar más fácilmente?
7. ¿Qué parte de este proceso crees que sería más importante mejorar?

---

## 5. Excepciones

También pensamos en algunas situaciones que pueden pasar fuera del proceso normal.

1. ¿Qué pasa si una persona quiere cambiar su fecha o su horario?
2. ¿Qué pasa si alguien cancela una reservación?
3. ¿Qué pasa si alguien reserva pero no asiste?
4. ¿En qué momento se descuenta un uso del paquete?
5. ¿Qué pasa si alguien ya no tiene usos y quiere hacer otra reservación?
6. ¿Hay algún caso en el que una persona pueda seguir usando el cuarto aunque ya haya terminado su paquete?

Estas preguntas nos ayudaron a darnos cuenta de que todavía hay algunas reglas que necesitamos confirmar, principalmente las cancelaciones, inasistencias, cambios de horario y el momento exacto en el que se descuenta un uso.

---

## 6. Verificación de supuestos

Antes de hacer la entrevista ya teníamos algunas ideas de cómo podía funcionar el sistema, así que hicimos preguntas para saber si realmente eran necesarias.

1. ¿Los paquetes que manejan son de 5 y 10 usos?
2. ¿Necesitas saber cuántos usos le quedan a cada persona?
3. ¿El sistema debería evitar que dos personas reserven el cuarto en el mismo horario?
4. ¿Necesitas poder consultar todas las reservaciones?
5. Cuando una persona usa la última sesión de su paquete, ¿puede terminar esa sesión normalmente?
6. Después de terminar su paquete, ¿necesita comprar otro para poder seguir usando el cuarto?
7. ¿El inventario debería formar parte de este sistema?
8. ¿Lo más importante sería enfocarnos en las reservaciones y en los paquetes?

---

# Bitácora de la entrevista

**Persona entrevistada:** Omar Enrique Buenrostro Islas  
**Fecha:** 22/09/2026  
**Tema:** Reservaciones del cuarto y paquetes

## Supuestos que se confirmaron

Después de la entrevista confirmamos varias cosas que ya habíamos considerado:

- Los paquetes son de 5 y 10 usos.
- Es importante saber cuántos usos le quedan a cada persona.
- No debería haber dos reservaciones en el mismo horario.
- La encargada necesita poder consultar las reservaciones.
- Cuando una persona llega al último uso de su paquete puede terminar esa sesión.
- Después necesita comprar otro paquete si quiere seguir utilizando el cuarto.
- El sistema se debe enfocar principalmente en las reservaciones y en los paquetes.

## Cosas que cambiaron

Al principio habíamos pensado en incluir otros problemas del negocio, como el inventario y otros procesos administrativos.

Después de revisar mejor el problema decidimos hacerlo más específico y enfocarnos solamente en:

- Las reservaciones del cuarto.
- Los paquetes de 5 y 10 usos.

De esta forma el proyecto no se hace demasiado grande y se enfoca en los problemas principales que queremos resolver.

## Cosas que no esperábamos

Una de las cosas que vimos es que una persona puede llegar al último uso de su paquete y no darse cuenta inmediatamente de que ya se terminó.

También vimos que no solamente tenemos que evitar que se empalmen las reservaciones, es importante saber cuántos usos le quedan a cada persona para tener un mejor control.

Además, todavía quedaron algunas cosas por definir, como qué pasa con las cancelaciones, las personas que no asisten, los cambios de horario y en qué momento se descuenta un uso.

## Cambios después de la entrevista

Después de la entrevista hicimos algunos cambios al proyecto:

- Nos enfocamos solamente en las reservaciones y los paquetes.
- Dejamos fuera el inventario y otros procesos del negocio.
- Agregamos que el sistema debe evitar reservaciones en el mismo horario.
- Incluimos paquetes de 5 y 10 usos.
- Agregamos la opción de consultar los usos disponibles.
- Agregamos la consulta de las reservaciones.

Las reglas sobre cancelaciones, inasistencias, cambios de horario y cuándo se descuenta un uso todavía quedan pendientes por confirmar.

---

# Ficha de dominio

## Quién eres

Eres la encargada del negocio y eres quien conoce cómo se organizan las reservaciones del cuarto y los paquetes de las personas que lo utilizan.

## Cómo es tu día

Durante el día necesitas saber quién va a utilizar el cuarto y en qué horario, también necesitas llevar un control de los usos que le quedan a cada persona a quien le rentas, ya que en vez de cobrar por mes, cobras por uso del local en paquetes.

Actualmente hay dos personas que utilizan el cuarto y existen paquetes de 5 y 10 usos.

## Reglas que conoces

- No debe haber dos reservaciones en el mismo horario.
- Los paquetes pueden ser de 5 o 10 usos.
- Se necesita saber cuántos usos le quedan a cada persona.
- Si una persona está usando su último uso, puede terminar esa sesión normalmente.
- Después debe comprar otro paquete para poder seguir utilizando el cuarto.

## Una excepción

Todavía hay algunas situaciones que necesitamos definir mejor, por ejemplo qué pasa cuando alguien cancela, no asiste o quiere cambiar su horario.

## Lo que te molesta

Uno de los principales problemas es que se pueden llegar a empalmar las reservaciones.

También puede pasar que alguien termine todos los usos de su paquete y no se detecte inmediatamente, lo que hace más difícil llevar el control.
