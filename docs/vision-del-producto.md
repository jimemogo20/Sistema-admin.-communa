Jimena Morales Gómez

31/agosto/2026

**Sistema administrativo communa:**

## 1. Descripción del sistema

**Nombre del sistema:** 
Sistema de reservaciones y control de paquetes

**Descripción:**

El sistema permitirá llevar un mejor control de las reservaciones de un cuarto que utilizan diferentes personas para atender a sus clientes. Permitirá consultar los horarios disponibles, registrar reservaciones y evitar que dos personas aparten el cuarto en el mismo horario. Además, llevará el control de paquetes de 5 y 10 usos, descontando las sesiones utilizadas y mostrando cuándo un paquete se ha terminado para que se pueda adquirir uno nuevo.

---

## 2. Problema y usuarios

Actualmente las reservaciones del cuarto no tienen un control centralizado, por lo que existe la posibilidad de que dos personas quieran utilizarlo en el mismo horario. Además, se manejan paquetes de 5 y 10 usos y puede ocurrir que una persona termine las sesiones de su paquete y no se registre o cobre correctamente la compra de uno nuevo.

Esto puede provocar conflictos en los horarios, confusión sobre los usos disponibles y pérdidas económicas por falta de control en la renovación de los paquetes.

**El problema:**

**Cómo se resuelve hoy sin el sistema:**

Actualmente los horarios y los usos de los paquetes se revisan de manera manual, las personas tienen que comunicarse para saber si el cuarto está disponible y llevar por separado el conteo de las sesiones utilizadas. Cuando un paquete termina, también se tiene que revisar manualmente si corresponde comprar uno nuevo.

**Usuarios del sistema:**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
| Administradora| Consultar todas las reservaciones, controlar los paquetes y saber cuándo una persona terminó sus usos.|Que se empalmen citas o alguien utilice el cuarto después de terminar su paquete sin pagar.|
| Persona que renta| Consultar horarios disponibles, reservar y saber cuántas sesiones le quedan.| Llegar y encontrar el cuarto ocupado o no saber cuántos usos le quedan.|


**Un conflicto entre usuarios:**

La persona que utiliza el cuarto busca tener flexibilidad para reservar el horario que más le convenga, pero la administradora necesita mantener un control para evitar que dos personas ocupen el mismo horario y asegurarse de que los paquetes utilizados estén registrados correctamente.

Por esta razón, el sistema debe permitir cierta flexibilidad al reservar, pero sin permitir empalmes ni perder el control de los usos disponibles.

**Visión**

No sabía si era el mismo negocio o no 
No entendía lo de los paquetes 

---

## 3. Alcance


### Dentro del alcance

- Registra reservaciones indicando la persona, fecha y horario.
- Muestra los horarios disponibles y ocupados del cuarto.
- Impide registrar dos reservaciones que utilicen el cuarto en el mismo horario.
- Registra y descuenta los usos correspondientes de los paquetes de 5 o 10 sesiones.
- Notifica cuando un paquete llega a cero usos e indica que corresponde adquirir uno nuevo.

### Explícitamente fuera del alcance

- El sistema no procesa pagos ni realiza cobros bancarios por la compra de paquetes.
- El sistema no administra inventario de productos, materiales o equipo utilizado dentro del negocio.
- El sistema no administra citas personales entre cada profesional y sus propios clientes; únicamente controla la reservación del cuarto compartido

**Por qué queda fuera:**

El procesamiento de pagos queda fuera porque el problema principal que buscamos resolver es el control de reservaciones y de los usos de los paquetes, incluir pagos implicaría agregar funciones financieras y posiblemente servicios externos que aumentarían la complejidad del proyecto sin ser necesarios para solucionar el problema principal.

---

## 4. Tipo de sistema y restricciones

Web y SaaS

**Por qué es de ese tipo:**

Es un sistema Web y SaaS porque las personas necesitan consultar reservaciones, disponibilidad y usos de sus paquetes desde diferentes dispositivos sin depender de una computadora específica. La información se encontraría centralizada y los usuarios autorizados podrían acceder al sistema mediante Internet, ya que, permite que todos consulten la misma información actualizada, lo cual es importante para evitar reservaciones duplicadas

**Atributos de calidad que impone:**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
| Disponibilidad| Las personas necesitan consultar los horarios antes de realizar una reservación| Podrían volver a comunicarse manualmente y existirían problemas para saber si el cuarto está disponible|
| Integridad de los datos | El número de usos disponibles y las reservaciones deben mantenerse correctos | Se podrían descontar usos incorrectamente, permitir reservaciones empalmadas o solicitar un nuevo paquete cuando todavía existen usos disponibles|
| Usabilidad |El sistema será utilizado para acciones sencillas y frecuentes, como consultar horarios y reservar | Si resulta complicado, los usuarios podrían preferir continuar realizando el proceso manualmente|

**Reglas de negocio que ya identifiqué:**

1. Una reservación no puede registrarse si el cuarto ya está reservado por otra persona durante ese mismo horario.
2. Los paquetes disponibles son de 5 o 10 usos y cada sesión realizada descuenta un uso del paquete correspondiente.
3. Cuando una persona utiliza el último uso de su paquete, puede terminar esa sesión normalmente, pero al salir debe adquirir un nuevo paquete para poder continuar utilizando el cuarto posteriormente.
---

## 5. Ciclo de vida elegido

**Modelo elegido:**
Ágil
**Por qué le conviene a este proyecto:**

El modelo ágil le conviene al proyecto porque, aunque ya se identificó el problema principal, algunos requisitos pueden cambiar cuando las personas que realmente utilizan el cuarto comiencen a revisar y probar el sistema.

### Alternativas descartadas

**Cascada:**

La descarté porque cascada funciona mejor cuando los requisitos son estables y conocidos desde el principio. En este proyecto existen reglas que podrían cambiar o aclararse cuando los usuarios vean el sistema funcionando. Por ejemplo, podrían surgir cambios sobre cuándo descontar un uso, cómo manejar una cancelación o qué información mostrar al terminar un paquete.

Si utilizáramos cascada y alguno de estos requisitos cambiara después de terminar el diseño, realizar la modificación podría implicar regresar a etapas anteriores.

**Modelo V:**

El Modelo V sería más adecuado para un sistema con requisitos muy estables y verificables, especialmente cuando existen consecuencias graves ante una falla o se requiere evidencia formal de validación.

En este proyecto no se trata de un sistema crítico ni existe actualmente una necesidad de certificación o auditoría formal. Nuestro principal riesgo está relacionado con entender correctamente las necesidades de los usuarios y adaptar las reglas del negocio, por lo que un modelo con mayor posibilidad de cambios y retroalimentación resulta más adecuado.

---

