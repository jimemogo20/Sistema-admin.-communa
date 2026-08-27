Jimena Morales Gómez
18/agosto/2026

**Repositorio:**

## 1. Descripción del sistema

El sistema permitirá **administrar las reservaciones y el uso de un cuarto que se renta por paquetes de 5 o 10 sesiones**. Permitirá consultar horarios disponibles, reservar el espacio y llevar el control de las sesiones utilizadas y restantes de cada paquete, evitando empalmes y usos sin pago.

**Nombre del sistema:** 
Sistema de citas communa

**Descripción:**

---

## 2. Problema y usuarios

Actualmente existen problemas para **controlar las reservaciones y los paquetes de uso del cuarto**. En ocasiones las citas se empalman y también puede ocurrir que una persona termine las sesiones de su paquete y continúe utilizando el espacio sin que se realice un nuevo cobro.

El sistema servirá principalmente a la administradora, quien necesita controlar las reservaciones y pagos, y a las personas que rentan el cuarto, quienes necesitan consultar disponibilidad, reservar horarios y conocer cuántas sesiones les quedan.

**El problema:**

**Cómo se resuelve hoy sin el sistema:**

Actualmente, el personal se organiza de forma manual, usando mensajes, anotaciones y acuerdos entre ellos para controlar horarios y cobros.

**Usuarios del sistema:**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
| Administradora| Controlar reservaciones, paquetes comprados y sesiones utilizadas.|Que se empalmen citas o alguien utilice el cuarto después de terminar su paquete sin pagar.|
| Persona que renta| Consultar horarios disponibles, reservar y saber cuántas sesiones le quedan.| Llegar y encontrar el cuarto ocupado o no saber cuántos usos le quedan.|


**Un conflicto entre usuarios:**

La persona que renta quiere poder reservar fácilmente el horario que necesita, mientras que la administradora necesita restringir las reservaciones cuando el horario ya está ocupado o cuando el paquete ya no tiene sesiones disponibles

**Visión**

No sabía si era el mismo negocio o no 

---

## 3. Alcance


### Dentro del alcance

- Consultar los horarios disponibles del cuarto.
- Crear, modificar y cancelar reservaciones
- Registrar paquetes de 5 o 10 usos y llevar el control de las sesiones restantes
- Evitar reservaciones empalmadas y avisar cuando un paquete se haya terminado.

### Explícitamente fuera del alcance

- Procesamiento de pagos en línea
- Administración de citas de dermatología o clases de yoga
- Administración de otros espacios o cuartos del negocio

**Por qué queda fuera:**

El sistema se enfocará únicamente en la renta y uso del cuarto, para mantener un alcance manejable. Por ejemplo, integrar pagos en línea agregaría complejidad y no es necesario para solucionar el problema principal, que es controlar las reservaciones y los usos disponibles de cada paquete

---

## 4. Tipo de sistema y restricciones

Sistema de información

**Por qué es de ese tipo:**

Porque permite registrar, consultar y administrar información relacionada con las reservaciones del cuarto y los paquetes de usos de cada persona.

**Atributos de calidad que impone:**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
| Confiabilidad| Las reservaciones y sesiones restantes deben registrarse correctamente.| Podrían empalmarse citas o cobrarse incorrectamente los usos.|
| Usabilidad | Debe ser fácil consultar disponibilidad y hacer una reservación. | Los usuarios podrían preferir seguir organizándose manualmente.|
| Seguridad |No todos los usuarios deben poder modificar paquetes o sesiones. | Un usuario podría modificar información que solo corresponde a la administración.|

**Reglas de negocio que ya identifiqué:**

1. Un cuarto no puede estar reservado por dos personas en el mismo horario.
2. Los paquetes disponibles son de 5 o 10 usos y cada uso debe quedar registrado.
3. Cuando un paquete llega a 0 usos, la persona no puede seguir utilizando el cuarto con ese paquete y debe adquirir uno nuevo.

---

## 5. Ciclo de vida elegido

*Instrucción: este apartado se trabaja en la semana 3, después de ver los modelos de desarrollo. La justificación pesa más que la elección: no hay un modelo correcto, hay uno defendible para tu caso.*

**Modelo elegido:**

**Por qué le conviene a este proyecto:**

*Instrucción: argumenta con las características reales de tu caso. Estabilidad de los requisitos, disponibilidad del cliente, nivel de riesgo, tamaño del equipo, frecuencia de entregas esperada.*

### Alternativas descartadas

**Alternativa 1:**

*Por qué la descarté:*

**Alternativa 2:**

*Por qué la descarté:*

---

## Antes de entregar

Reviso que el documento cumpla lo siguiente:

- [ ] La descripción del apartado 1 se entiende sin ser del área
- [ ] Hay al menos dos tipos de usuario con necesidades distintas
- [ ] Identifiqué un conflicto real entre usuarios
- [ ] El alcance dice qué queda fuera, no solo qué queda dentro
- [ ] Las exclusiones son específicas, no genéricas
- [ ] Identifiqué el tipo de sistema y al menos dos atributos de calidad
- [ ] Anoté al menos tres reglas de negocio no obvias
- [ ] Justifiqué el ciclo de vida contra dos alternativas descartadas
- [ ] El documento está en mi repositorio y se puede leer desde el navegador
- [ ] Borré todas las instrucciones en cursiva de la plantilla
