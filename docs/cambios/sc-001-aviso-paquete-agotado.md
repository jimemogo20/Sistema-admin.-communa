# SC-001: Avisar a la administradora cuando a una persona se le termina el paquete

---

## Estado

Propuesta · 12/noviembre/2026

## Quién la pide

<César Méndez, dupla de revisión del proyecto "Sistema de reservaciones y control de paquetes" de Jimena Morales Gómez.

## Qué se pide

Quiero que a la administradora le salga un aviso cuando a una persona se le
termina el paquete (se queda en cero usos), con el nombre de la persona y el
tipo de paquete que terminó, para que no tenga que ir revisando paquete por
paquete. Y que el aviso se quite cuando se registre el paquete nuevo de esa
persona.

## Por qué

En la entrevista con la encargada apareció un problema que nadie esperaba:
una persona puede llegar al último uso de su paquete y la encargada no se
entera en ese momento (D3 del guion, y "Información que apareció y no
esperábamos" en la especificación). La regla de negocio ya dice que al
terminar el último uso la persona debe comprar un paquete nuevo, pero hoy
nada le avisa a la administradora de que ese momento llegó.

Además hay una diferencia entre lo que se promete y lo que se especifica:
la visión del producto dice, en el alcance, que el sistema "notifica cuando un
paquete llega a cero usos", pero en la especificación de requisitos ninguna
ficha lo pide. RF-005 solo muestra "agotado" cuando alguien consulta el
paquete, es decir, depende de que la administradora se acuerde de mirar.

Es justo la preocupación principal de la clienta: que alguien siga usando el
cuarto sin haber pagado un paquete nuevo (RNF-CON-001 lo menciona como
pérdida de dinero).

## Qué pasa si no se hace

La administradora sigue dependiendo de su memoria o de revisar a mano para
darse cuenta de que un paquete se terminó, que es básicamente el problema que
el sistema quería quitar. El sistema funciona sin este cambio (se puede
consultar el paquete), pero puede seguir habiendo renovaciones sin cobrar.
No es grave ni bloquea nada, pero sí deja sin resolver una parte del problema
original.

## Tipo de mantenimiento

- [ ] **Correctivo** · algo está mal y hay que repararlo
- [ ] **Adaptativo** · el entorno cambió y hay que ajustarse
- [x] **Perfectivo** · funciona, pero puede ser mejor
- [ ] **Preventivo** · todavía no falla, pero va a fallar

**Justificación:** hoy se puede consultar si un paquete se agotó (RF-005) y eso funciona; el cambio hace que el sistema avise por sí solo en lugar de esperar a que alguien consulte.

## Criterio de aceptación

1. Cuando un paquete queda en 0 usos disponibles, la siguiente vez que la
   administradora abre el sistema ve un aviso con el nombre de la persona y
   el tipo de paquete (5 o 10 usos). ¿Sí o no?
2. Si a la persona todavía le quedan 1 o más usos, no aparece ningún aviso
   sobre su paquete. ¿Sí o no?
3. El aviso sigue visible mientras la persona no tenga un paquete nuevo
   registrado. ¿Sí o no?
4. Al registrar un paquete nuevo para esa persona, el aviso deja de aparecer.
   ¿Sí o no?
5. La persona que renta el cuarto no ve avisos de otras personas. ¿Sí o no?

## Prioridad que sugiere el solicitante

**Media.** Toca la preocupación central de la clienta (perder dinero por
paquetes no renovados), pero hoy existe una forma manual de saberlo (RF-005) y
el cambio depende de que primero se defina en qué momento se descuenta un uso,
que sigue pendiente de validar con la encargada. Quien analice el impacto
puede subirla si considera que el riesgo económico pesa más.

---

*La solicitud describe qué se quiere, nunca cómo hacerlo. El cómo se decide
en el análisis de impacto, y lo decide quien conoce el diseño.*
