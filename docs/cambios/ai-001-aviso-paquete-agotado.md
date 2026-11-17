# Análisis de impacto de SC-001

> Plantilla de análisis de impacto · Ingeniería de Software I · SIS3407  
> Proyecto: Communna – Sistema de reservaciones y control de paquetes  
> Elaborado por: Jimena Morales Gómez, responsable del sistema.

---

## Solicitud que se analiza

**Referencia:** `sc-001-aviso-paquete-agotado.md`

**Solicitante:** César Méndez, dupla de revisión del proyecto Communna.

**Fecha de solicitud:** 12 de noviembre de 2026.

**Descripción:** Se solicita que la administradora reciba un aviso dentro del sistema cuando una persona agote los usos de su paquete. El aviso debe mostrar el nombre de la persona y el tipo de paquete, ya sea de 5 o 10 usos.

El aviso debe permanecer visible mientras no se registre un paquete nuevo y desaparecer cuando se realice la renovación.

**Tipo de mantenimiento:** Perfectivo.

**Prioridad propuesta:** Media.

---

## Traducción a términos del sistema

La solicitud busca que la administradora no tenga que revisar manualmente los paquetes para identificar cuáles se encuentran agotados.

Dentro de Communna, esto significa realizar los siguientes cambios:

- **Clase Paquete:** utilizar el atributo `usosDisponibles` para identificar cuándo un paquete llega a cero.
- **Clase UsoPaquete:** después de registrar el uso de la sala, actualizar la cantidad de usos disponibles del paquete.
- **Componente de gestión de paquetes:** incorporar una función que identifique los paquetes agotados.
- **Panel de administración:** agregar una sección donde se muestren los avisos de paquetes agotados, incluyendo el nombre de la persona y el tipo de paquete.
- **Registro de paquetes:** al registrar un paquete nuevo para la persona, el aviso anterior debe dejar de aparecer.

No se necesita integrar WhatsApp, correo electrónico ni servicios externos, porque los avisos aparecerán únicamente dentro de Communna.

---

## Impacto directo

Lo que la solicitud toca por definición: los elementos que deben modificarse para incorporar los avisos de paquetes agotados.

| Artefacto | Unidad | Qué hay que cambiar |
|---|---|---|
| Requisito RF-005 | 2 | Ampliar la consulta de usos disponibles para contemplar la identificación de paquetes agotados. Agregar un requisito específico para mostrar los avisos a la administradora. |
| Caso de uso | 2 | Agregar el caso de uso "Consultar avisos de paquetes agotados", indicando cuándo aparece el aviso y cuándo desaparece. |
| Diagrama de clases | 4 | Incorporar una operación para identificar paquetes agotados en la gestión de paquetes. Revisar las responsabilidades de `Paquete` y `UsoPaquete`. |
| Diagrama de secuencia | 4 | Representar cómo se registra el uso, se actualizan los usos disponibles y se muestra el aviso cuando el paquete llega a cero. También debe contemplarse la renovación del paquete. |

---

## Impacto indirecto

Se revisaron los artefactos relacionados para identificar cuáles podrían verse afectados como consecuencia del cambio.

| Artefacto | Unidad | Por qué se ve afectado |
|---|---|---|
| Registro de decisión ADR de arquitectura | 3 | Sin impacto en la decisión de utilizar un monolito modular. La funcionalidad puede incorporarse al módulo de paquetes sin crear servicios independientes. Se puede agregar una nota para documentar esta decisión. |
| Diagrama de contenedores C4 | 3 | Sin impacto estructural. Se mantienen la aplicación web, la API y la base de datos. No se necesita incorporar un servicio externo de notificaciones. |
| Máquina de estados | 4 | Se debe revisar el estado del paquete para representar correctamente cuándo se considera agotado y cuándo se registra uno nuevo. No es necesario modificar los estados de las reservaciones. |

---

## Lo que queda sin tocar

La solicitud de cambio no modifica las siguientes partes de Communna:

- **Registro de reservaciones:** las personas podrán continuar registrando sus reservaciones de la misma manera.
- **Consulta de horarios disponibles:** no cambia la forma en que se consultan los horarios.
- **Prevención de empalmes:** se mantienen las validaciones para evitar reservaciones simultáneas.
- **Administración de la sala:** no cambia la información ni el funcionamiento de la sala.
- **Arquitectura general:** se conserva la estructura propuesta de aplicación web, API y base de datos.
- **Inicio de sesión:** no se propone modificar su funcionamiento, aunque los avisos deberán ser visibles únicamente para la administradora.
- **Regla de descuento:** los usos continúan descontándose después de utilizar la sala, no al realizar una reservación.

Esto permite incorporar la nueva funcionalidad sin modificar las operaciones principales del sistema.

---

## Riesgos

**1. Avisos que no aparecen cuando se agota un paquete.**

- Probabilidad: Media.
- Impacto: Alto.
- Consecuencia: La administradora podría no darse cuenta de que una persona necesita renovar su paquete.
- Mitigación: Realizar pruebas cuando los usos disponibles cambien de 1 a 0.

**2. Avisos que permanecen después de renovar un paquete.**

- Probabilidad: Media.
- Impacto: Medio.
- Consecuencia: La administradora podría recibir información incorrecta.
- Mitigación: Verificar que el aviso desaparezca cuando se registre un paquete nuevo.

**3. Descuento incorrecto de usos.**

- Probabilidad: Media.
- Impacto: Alto.
- Consecuencia: Podrían aparecer avisos antes de tiempo o no aparecer cuando corresponde.
- Mitigación: Comprobar que cada uso se descuente una sola vez y únicamente después de utilizar la sala.

**4. Acceso a información de otras personas.**

- Probabilidad: Baja.
- Impacto: Alto.
- Consecuencia: Una persona que renta la sala podría visualizar información que corresponde a la administradora.
- Mitigación: Restringir la visualización de avisos al rol de administración.

**5. Riesgo de no implementar el cambio.**

La administradora continuará dependiendo de la revisión manual de paquetes. Esto puede provocar que una persona siga utilizando la sala sin renovar su paquete, generando posibles pérdidas económicas.

---

## Alternativas consideradas

**1. Opción A: Avisos automáticos dentro del panel de administración**

Consiste en incorporar una sección que muestre automáticamente los paquetes que tengan cero usos disponibles.

El sistema consultará los paquetes agotados y mostrará el nombre de la persona y el tipo de paquete. Cuando se registre un paquete nuevo, el aviso dejará de mostrarse.

**Ventajas:**
- La administradora identifica rápidamente los paquetes agotados.
- No necesita revisar cada paquete individualmente.
- No requiere servicios externos.
- Responde directamente a la solicitud de cambio.

**Desventajas:**
- Requiere modificar la interfaz y la lógica de gestión de paquetes.
- Se necesitan pruebas para garantizar que los avisos aparezcan y desaparezcan correctamente.

**Esfuerzo estimado:** 12 horas.

**2. Opción B: Agregar un filtro de paquetes agotados**

Consiste en agregar un filtro en la pantalla de consulta de paquetes para mostrar únicamente aquellos que tengan cero usos disponibles.

**Ventajas:**
- Es más sencillo de implementar.
- Reutiliza la funcionalidad de consulta existente.
- Requiere menos modificaciones.

**Desventajas:**
- La administradora debe entrar a consultar los paquetes.
- No cumple completamente con la solicitud de recibir un aviso automático.
- Mantiene parte del problema de depender de una revisión manual.

**Esfuerzo estimado:** 6 horas.

**Alternativa seleccionada:** Opción A, porque permite identificar los paquetes agotados sin necesidad de revisarlos manualmente y responde mejor al problema identificado durante la entrevista.

---

## Estimación de esfuerzo

| Concepto | Esfuerzo |
|---|---|
| Cambios de diseño y documentación | 3 horas |
| Implementación | 6 horas |
| Pruebas | 3 horas |
| **Total** | **12 horas** |

**De dónde sale este número.**

La estimación se realizó considerando que Communna ya contempla el registro de paquetes y la consulta de usos disponibles.

Para los cambios de diseño y documentación se estiman 3 horas, destinadas a actualizar los requisitos, el caso de uso y los diagramas afectados.

Para la implementación se consideran 6 horas, distribuidas entre la lógica para identificar paquetes agotados, la visualización de avisos en el panel de administración y la actualización de los avisos cuando se registre un paquete nuevo.

Finalmente, se estiman 3 horas de pruebas para comprobar que los avisos aparezcan cuando un paquete llegue a cero, no aparezcan cuando todavía existan usos disponibles y desaparezcan después de una renovación.

La estimación supone que se reutilizarán los componentes existentes y que no será necesario contratar servicios externos ni modificar la arquitectura general. No incluye despliegue en producción ni cambios adicionales que puedan solicitarse posteriormente.

Las 12 horas son una estimación inicial de trabajo, no un tiempo medido durante una implementación.

---

## Recomendación

**Se recomienda aceptar la solicitud de cambio SC-001.**

La funcionalidad propuesta responde directamente a uno de los problemas principales identificados en Communna: la falta de seguimiento cuando una persona termina los usos de su paquete.

La alternativa de mostrar avisos automáticos en el panel de administración permite reducir la dependencia de revisiones manuales y facilita que la encargada identifique cuándo es necesario registrar un paquete nuevo.

Además, el cambio puede incorporarse dentro de la arquitectura propuesta sin agregar servicios externos ni modificar el funcionamiento principal de las reservaciones.

Aunque requiere actualizar documentación, diseño y lógica del sistema, el esfuerzo estimado de 12 horas se considera razonable frente al beneficio esperado.

Antes de implementarlo, se deberá confirmar con la encargada el procedimiento para registrar la finalización de cada uso, de manera que los avisos se generen correctamente.

---
