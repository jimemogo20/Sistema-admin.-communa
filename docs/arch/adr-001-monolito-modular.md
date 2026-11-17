# ADR-001: Utilizar un monolito modular para Communna

## Contexto

Communna controla las reservaciones de **un local compartido** y los **paquetes de 5 o 10 usos** de las personas que lo rentan. Lo usan dos tipos de usuario: la administradora y las personas que rentan el local.

Datos del caso que condicionan la arquitectura:

- **El alcance es pequeño y está acotado:** seis casos de uso, sin pagos, inventario, contabilidad ni servicios externos.
- **Las funciones comparten la misma información:** para evitar empalmes (RF-003), la reservación tiene que consultar la disponibilidad, y para mantener correctos los usos (RNF-CON-001), el uso de un paquete depende de que la reservación se haya atendido. Reservaciones, disponibilidad, paquetes y usos trabajan sobre los mismos datos.
- **Lo desarrolla y mantiene un equipo de una persona**, sin experiencia operando varios servicios en producción.

## Decisión

Se desarrollará Communna como un **monolito modular**: una sola aplicación (API) con una sola base de datos, organizada internamente en cuatro módulos con responsabilidades separadas:

- **Disponibilidad:** horarios libres y ocupados.
- **Reservaciones:** registro y consulta; verifica empalmes antes de guardar.
- **Paquetes:** registro de paquetes de 5 o 10 usos.
- **Usos:** consulta y descuento de usos disponibles.

## Alternativas consideradas

- **Microservicios:** se descartó. Separar reservaciones y paquetes en servicios con bases de datos distintas obligaría a coordinar datos entre servicios para evitar empalmes y mantener el conteo de usos, y a operar varios despliegues, algo desproporcionado para un cuarto y un equipo de una persona.
- **Monolito sin módulos:** se descartó, porque mezclaría las reglas de reservaciones y de paquetes y dificultaría cambios como SC-001.

## Consecuencias

**Positivas**

- Un solo despliegue y una sola base de datos: más sencillo de construir y de mantener para un equipo pequeño.
- Las validaciones que cruzan módulos (empalmes y descuento de usos) se pueden hacer en una sola transacción, lo que ayuda a cumplir RNF-CON-001.
- Los cambios de alcance limitado se quedan dentro de un módulo: SC-001 (aviso de paquete agotado) solo toca el módulo de Paquetes y no cambia la arquitectura.

**Negativas**

- Todos los módulos comparten el despliegue: un cambio en un módulo obliga a volver a desplegar toda la aplicación.
- Una falla grave en la aplicación puede dejar sin servicio a todas las funciones al mismo tiempo, no solo a una.
- Los límites entre módulos dependen de la disciplina del código; si no se respetan, el sistema puede convertirse en un monolito sin módulos.
- Si en el futuro se agregaran más locales o servicios externos (pagos), habría que revisar esta decisión.
