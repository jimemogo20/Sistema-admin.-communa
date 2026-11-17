**ADR-001: Utilizar un monolito modular para Communna**

Se propone desarrollar Communna mediante una arquitectura de monolito modular, separando las responsabilidades de reservaciones, disponibilidad y gestión de paquetes.

Esta arquitectura permite mantener las funciones organizadas dentro de un mismo sistema, sin la complejidad de administrar múltiples servicios independientes.

La principal ventaja es que facilita el desarrollo y mantenimiento de un sistema pequeño. Como consecuencia negativa, los módulos comparten un mismo despliegue y un problema en la aplicación podría afectar varias funciones.
