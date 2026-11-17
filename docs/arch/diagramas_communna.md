# Diagramas Mermaid — Communna

## Introducción

Communna es una propuesta de sistema web para administrar las reservaciones de una sala compartida y los paquetes de 5 o 10 usos. Busca facilitar la consulta de horarios, evitar reservaciones empalmadas y mostrar los usos disponibles de cada paquete.

> **Alcance de los diagramas:** Los diagramas describen una propuesta de diseño, no un sistema ya implementado. La arquitectura web/API/base de datos y el inicio de sesión por rol son decisiones propuestas que deben validarse con el equipo y el cliente. No se asumen reglas definitivas de cancelación ni de descuento de usos.

---

## 1. Diagrama de contexto

### Descripción

Presenta a Communna como un sistema único y a las dos personas que interactúan con él, las mismas que aparecen como actores en los casos de uso: la persona que renta el local y la administradora. La persona que renta consulta disponibilidad, reserva y revisa sus usos; la administradora registra paquetes y consulta reservaciones y usos.

```mermaid
flowchart TD
    persona([Persona que renta el local])
    admin([Administradora])
    sistema[Communna - Sistema de reservaciones y paquetes]

    persona -->|consulta horarios, reserva y revisa sus usos| sistema
    admin -->|registra paquetes y consulta reservaciones y usos| sistema

    style sistema fill:#ff5d00,color:#fff
```

### Explicación

El diagrama identifica a los usuarios principales y las funciones que realizan, sin entrar en detalles tecnológicos. Communna no se comunica con ningún sistema externo: los pagos, el correo y las notificaciones por WhatsApp quedaron fuera del alcance a propósito, y los avisos de paquete agotado (SC-001) se muestran dentro del propio sistema.

---

## 2. Diagrama de contenedores

### Descripción

Propone separar el sistema en una aplicación web, una API y una base de datos, cada una con su tecnología.

```mermaid
flowchart TD
    persona([Persona que renta el local])
    admin([Administradora])

    subgraph communna[Communna]
        web["Aplicacion web<br/>[React]<br/>interfaz de usuarios"]
        api["API - monolito modular<br/>[Node.js + Express]<br/>reglas de reservaciones y paquetes"]
        bd[("Base de datos<br/>[PostgreSQL]<br/>usuarios, reservaciones y paquetes")]
    end

    persona -->|usa desde el navegador| web
    admin -->|usa desde el navegador| web
    web -->|"solicitudes HTTPS / JSON"| api
    api -->|"lee y escribe (SQL)"| bd

    style api fill:#ff5d00,color:#fff
```

### Explicación

La aplicación web permite a los usuarios interactuar con Communna. La API procesa las solicitudes y verifica las reglas de negocio; la base de datos conserva la información. Es una arquitectura propuesta, no una implementación existente.

**Por qué estas tecnologías:** React y Node.js usan el mismo lenguaje (JavaScript) en la interfaz y en la API, lo que reduce lo que tiene que dominar un equipo pequeño. PostgreSQL es una base de datos relacional con transacciones, lo que ayuda a cumplir RF-003 (evitar empalmes) y RNF-CON-001 (usos disponibles siempre correctos), porque las reservaciones, los paquetes y los usos están relacionados entre sí.

---

## 3. Diagrama de componentes

### Descripción

Muestra los componentes propuestos dentro de la API: disponibilidad, reservaciones, paquetes y consulta de usos.

```mermaid
flowchart TD
    web[Aplicacion web]

    subgraph api[API de Communna]
        disp[Disponibilidad - horarios libres]
        reservas[Reservaciones - registro y consulta]
        paquetes[Paquetes - registro de paquetes]
        usos[Usos - consulta de usos disponibles]
    end

    bd[(Base de datos)]

    web --> disp
    web --> reservas
    web --> paquetes
    web --> usos
    reservas -->|verifica horario libre| disp
    usos -->|consulta paquete asociado| paquetes
    disp --> bd
    reservas --> bd
    paquetes --> bd
    usos --> bd

    style reservas fill:#ff5d00,color:#fff
```

### Explicación

Antes de guardar una reservación, el módulo de reservaciones consulta la disponibilidad para evitar empalmes. Los módulos de paquetes y usos permiten registrar paquetes y conocer cuántos usos quedan. El momento exacto del descuento de un uso está pendiente de definir.

---

## 4. Diagrama de flujo con decisiones

### Descripción

Representa el proceso básico de registrar una reservación y comprobar que el horario solicitado no se encuentre ocupado.

```mermaid
flowchart TD
    ini([Inicio])
    elegir[Seleccionar fecha y horario]
    valido{Datos completos?}
    consultar[Consultar disponibilidad]
    libre{Horario disponible?}
    error[Solicitar datos faltantes]
    ocupado[Mostrar horario no disponible]
    guardar[Registrar reservacion]
    confirmar[Mostrar confirmacion]
    fin([Fin])

    ini --> elegir
    elegir --> valido
    valido -->|No| error
    error --> elegir
    valido -->|Si| consultar
    consultar --> libre
    libre -->|No| ocupado
    ocupado --> elegir
    libre -->|Si| guardar
    guardar --> confirmar
    confirmar --> fin

    style guardar fill:#ff5d00,color:#fff
```

### Explicación

Si faltan datos o el horario está ocupado, se solicita una corrección. Si la fecha y hora están disponibles, se registra la reservación y se muestra una confirmación.

---


## 5. Diagrama de secuencia

### Descripción

Representa el proceso de registrar una reservación en Communna. Muestra cómo el sistema verifica que no existan empalmes antes de guardar una nueva reservación.

```mermaid
sequenceDiagram
    actor Persona as Persona que renta
    participant Web as Aplicacion web
    participant Gestor as GestorReservaciones
    participant Sala
    participant Reserva as Reservacion
    participant BD as Base de datos

    Persona->>Web: Selecciona fecha y horario
    Web->>Gestor: registrarReservacion(usuario, sala, fecha, inicio, fin)
    Gestor->>Gestor: verificarEmpalme(fecha, inicio, fin)
    Gestor->>Sala: consultarDisponibilidad(fecha, inicio, fin)
    Sala->>BD: Consultar reservaciones existentes
    BD-->>Sala: Horarios registrados
    Sala-->>Gestor: Disponibilidad

    alt Horario disponible y sin empalmes
        Gestor->>Reserva: registrar()
        Reserva->>BD: Guardar reservacion
        BD-->>Reserva: Reservacion guardada
        Reserva-->>Gestor: Registro exitoso
        Gestor-->>Web: Confirmacion
        Web-->>Persona: Muestra reservacion exitosa
    else Horario ocupado
        Gestor-->>Web: Horario no disponible
        Web-->>Persona: Solicita otro horario
    end
```

### Explicación

La persona que renta selecciona una fecha y un horario. La aplicación web envía la solicitud a GestorReservaciones, que verifica si existe un empalme y consulta la disponibilidad de la sala.

Si el horario está disponible, se ejecuta la operación registrar() de la clase Reservacion y se guarda la información en la base de datos.

Si el horario está ocupado, el sistema solicita seleccionar otro.

### Consistencia con el diagrama de clases

Los mensajes registrarReservacion() y verificarEmpalme() corresponden a operaciones de GestorReservaciones. El mensaje consultarDisponibilidad() corresponde a la clase Sala y registrar() a la clase Reservacion.

Esto permite comprobar que las operaciones utilizadas en el diagrama de secuencia también están definidas en el diagrama de clases.

---


## 6. Diagrama de clases

### Descripción

El diagrama presenta las clases principales de Communna y sus relaciones. Incluye las operaciones necesarias para registrar reservaciones, verificar empalmes y controlar los usos de los paquetes. Es una propuesta de diseño que debe validarse con el cliente.

```mermaid
classDiagram
    direction LR

    class Usuario {
        -int idUsuario
        -string nombre
        -string rol
        +consultarReservaciones() List~Reservacion~
        +consultarPaquetes() List~Paquete~
    }

    class Sala {
        -int idSala
        -string nombre
        +consultarDisponibilidad(fecha: Date, inicio: string, fin: string) bool
    }

    class Reservacion {
        -int idReservacion
        -Date fecha
        -string horaInicio
        -string horaFin
        -EstadoReservacion estado
        +registrar() bool
        +marcarAtendida() void
        +consultarEstado() EstadoReservacion
    }

    class Paquete {
        -int idPaquete
        -int usosTotales
        -int usosDisponibles
        +consultarUsos() int
        +descontarUso() bool
    }

    class UsoPaquete {
        -int idUso
        -Date fechaUso
        +registrarUso() bool
    }

    class GestorReservaciones {
        +verificarEmpalme(fecha: Date, inicio: string, fin: string) bool
        +registrarReservacion(usuario: Usuario, sala: Sala, fecha: Date, inicio: string, fin: string) bool
    }

    class EstadoReservacion {
        <<enumeration>>
        REGISTRADA
        ATENDIDA
    }

    Usuario "1" --> "0..*" Reservacion : realiza
    Sala "1" --> "0..*" Reservacion : recibe
    Usuario "1" --> "0..*" Paquete : tiene
    Paquete "1" --> "0..*" UsoPaquete : registra
    Reservacion "1" --> "0..1" UsoPaquete : genera
    GestorReservaciones "1" --> "0..*" Reservacion : administra

    note for UsoPaquete "Se registra despues de utilizar la sala"
```

### Explicación

El diagrama representa las clases principales de Communna: Usuario, Sala, Reservacion, Paquete, UsoPaquete y GestorReservaciones, además de la enumeración EstadoReservacion.

GestorReservaciones se encarga de verificar que no existan empalmes antes de registrar una reservación.

La clase Paquete permite consultar los usos disponibles y descontar un uso cuando corresponde. La clase UsoPaquete registra cada utilización de la sala.

Una decisión importante es que los usos no se descuentan al realizar una reservación, sino después de que la sala haya sido utilizada. Esto permite conservar un registro de las reservaciones y controlar correctamente los paquetes.

La enumeración `EstadoReservacion` contiene solo los estados REGISTRADA y ATENDIDA, igual que el diagrama de estados. No se incluyen estados de cancelación ni de inasistencia porque esas reglas siguen pendientes de validar con la encargada.

**Patrón Controlador (GRASP):** `GestorReservaciones` recibe la solicitud desde la aplicación web y coordina las validaciones (verificar empalmes y consultar disponibilidad) antes de pedirle a `Reservacion` que se registre. Así la interfaz no contiene reglas de negocio y las validaciones quedan en un solo lugar. Esta clase se agregó al hacer el diagrama de secuencia: sin ella, no había una clase responsable de verificar empalmes entre varias reservaciones.

---

## 7. Diagrama de estados

### Descripción

Representa los estados propuestos para una reservación, se limita al registro y la atención; no se establecen reglas de cancelación porque todavía no están confirmadas.


```mermaid
stateDiagram-v2
    [*] --> Registrada: Se guarda la reservacion
    Registrada --> Atendida: Se utiliza la sala
    Atendida --> [*]
```


### Explicación

Una reservación pasa a Registrada cuando se guarda en el sistema y a Atendida cuando se utiliza la sala. Son estados propuestos que deben revisarse con el cliente.

---

## 8. Diagrama entidad-relación

### Descripción

Presenta una propuesta inicial de tablas para almacenar usuarios, sala, reservaciones y paquetes. No representa todavía un diseño físico definitivo.

```mermaid
erDiagram
    USUARIO ||--o{ RESERVACION : realiza
    SALA ||--o{ RESERVACION : recibe
    USUARIO ||--o{ PAQUETE : tiene
    PAQUETE o|--o{ RESERVACION : puede_asociarse

    USUARIO {
        int id PK
        string nombre
        string rol
    }

    SALA {
        int id PK
        string nombre
    }

    RESERVACION {
        int id PK
        int usuario_id FK
        int sala_id FK
        int paquete_id FK
        date fecha
        string hora_inicio
        string hora_fin
        string estado
    }

    PAQUETE {
        int id PK
        int usuario_id FK
        int usos_totales
        int usos_disponibles
    }
```

### Explicación

Un usuario puede registrar varias reservaciones y tener varios paquetes, una sala puede tener varias reservaciones en horarios distintos. La asociación entre reservación y paquete es opcional y está sujeta a confirmación.

---

## Conclusión

Estos ocho diagramas muestran distintas perspectivas de Communna: sus usuarios, la estructura tecnológica propuesta, sus componentes, el flujo de reservaciones, la comunicación interna, las clases, los estados y los datos. En conjunto ayudan a revisar el diseño antes de implementarlo y a detectar decisiones que todavía deben confirmarse con el cliente.
