# Diagramas Mermaid — Communna

## Introducción

Communna es una propuesta de sistema web para administrar las reservaciones de una sala compartida y los paquetes de 5 o 10 usos. Busca facilitar la consulta de horarios, evitar reservaciones empalmadas y mostrar los usos disponibles de cada paquete.

> **Alcance de los diagramas:** Los diagramas describen una propuesta de diseño, no un sistema ya implementado. La arquitectura web/API/base de datos y el inicio de sesión por rol son decisiones propuestas que deben validarse con el equipo y el cliente. No se asumen reglas definitivas de cancelación ni de descuento de usos.

---

## 1. Diagrama de contexto

### Descripción

Presenta a Communna como un sistema único y a las personas que interactúan con él: la persona que renta la sala, la recepcionista y el administrador. La persona que renta consulta disponibilidad y solicita reservaciones; la recepcionista gestiona las reservaciones y paquetes; el administrador consulta la información general.

```mermaid
flowchart TD
    persona([Persona que renta la sala])
    recep([Recepcionista])
    admin([Administrador])
    sistema[Communna - Sistema de reservaciones y paquetes]

    persona -->|consulta horarios y solicita reservaciones| sistema
    recep -->|registra reservaciones y paquetes| sistema
    admin -->|consulta reservaciones y usos| sistema

    style sistema fill:#ff5d00,color:#fff
```

### Explicación

El diagrama identifica a los usuarios principales y las funciones que realizan, sin entrar en detalles tecnológicos. No se agregan servicios externos porque no forman parte del alcance confirmado.

---

## 2. Diagrama de contenedores

### Descripción

Propone separar el sistema en una aplicación web, una API y una base de datos. La tecnología específica aún no está definida.

```mermaid
flowchart TD
    persona([Persona que renta la sala])
    recep([Recepcionista])
    admin([Administrador])

    subgraph communna[Communna]
        web[Aplicacion web - interfaz de usuarios]
        api[API - reglas de reservaciones y paquetes]
        bd[(Base de datos - usuarios, reservaciones y paquetes)]
    end

    persona -->|usa| web
    recep -->|usa| web
    admin -->|usa| web
    web -->|solicitudes HTTPS| api
    api -->|consulta y guarda datos| bd

    style api fill:#ff5d00,color:#fff
```

### Explicación

La aplicación web permite a los usuarios interactuar con Communna. La API procesa las solicitudes y verifica las reglas de negocio; la base de datos conserva la información. Es una arquitectura propuesta, no una implementación existente.

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

Muestra los mensajes entre la persona que renta, la aplicación web, los módulos de reservaciones y disponibilidad, y la base de datos al crear una reservación.

```mermaid
sequenceDiagram
    actor Persona as Persona que renta
    participant Web as Aplicacion web
    participant Res as Reservaciones
    participant Disp as Disponibilidad
    participant BD as Base de datos

    Persona->>Web: Selecciona fecha y horario
    Web->>Res: Solicitar reservacion
    Res->>Disp: Verificar disponibilidad
    Disp->>BD: Consultar reservaciones existentes
    BD-->>Disp: Horarios registrados
    Disp-->>Res: Resultado de disponibilidad
    alt Horario libre
        Res->>BD: Guardar reservacion
        BD-->>Res: Reservacion guardada
        Res-->>Web: Confirmacion
        Web-->>Persona: Muestra reservacion exitosa
    else Horario ocupado
        Res-->>Web: Horario no disponible
        Web-->>Persona: Solicita otro horario
    end
```

### Explicación

El sistema consulta los horarios existentes antes de guardar una nueva reservación. El diagrama también muestra qué ocurre cuando el horario solicitado ya está ocupado.

---

## 6. Diagrama de clases

### Descripción

Propone las clases principales para representar a las personas usuarias, las reservaciones, la sala y los paquetes. Sus atributos y operaciones son orientativos.

```mermaid
classDiagram
    class Usuario {
        +int id
        +string nombre
        +string rol
    }

    class Sala {
        +int id
        +string nombre
    }

    class Reservacion {
        +int id
        +date fecha
        +string horaInicio
        +string horaFin
        +string estado
    }

    class Paquete {
        +int id
        +int usosTotales
        +int usosDisponibles
        +consultarUsos() int
    }

    Usuario "1" --> "0..*" Reservacion : realiza
    Sala "1" --> "0..*" Reservacion : recibe
    Usuario "1" --> "0..*" Paquete : tiene
    Paquete "0..1" --> "0..*" Reservacion : puede asociarse
```

### Explicación

Una persona puede tener varias reservaciones y paquetes. Cada reservación corresponde a una sala. La relación opcional con el paquete representa una propuesta de diseño que debe validarse según cómo se registren y descuenten los usos.

---

## 7. Diagrama de estados

### Descripción

Representa los estados propuestos para una reservación. Se limita al registro y la atención; no se establecen reglas de cancelación porque todavía no están confirmadas.

```mermaid
stateDiagram-v2
    [*] --> Registrada: se guarda la reservacion
    Registrada --> Atendida: se utiliza la sala
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

Un usuario puede registrar varias reservaciones y tener varios paquetes. Una sala puede tener varias reservaciones en horarios distintos. La asociación entre reservación y paquete es opcional y está sujeta a confirmación.

---

## Conclusión

Estos ocho diagramas muestran distintas perspectivas de Communna: sus usuarios, la estructura tecnológica propuesta, sus componentes, el flujo de reservaciones, la comunicación interna, las clases, los estados y los datos. En conjunto ayudan a revisar el diseño antes de implementarlo y a detectar decisiones que todavía deben confirmarse con el cliente.
