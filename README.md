# Sistema de Agencia de Viajes

![commits](https://badgen.net/github/commits/UR-CC/lp2-taller1?icon=github) 
![last_commit](https://img.shields.io/github/last-commit/UR-CC/lp2-taller1)

- ver [badgen](https://badgen.net/) o [shields](https://shields.io/) para otros tipos de _badges_

## Autor

- Luz Carolina Hernandez Vega
https://github.com/LCarolina811

## Descripción del Proyecto

TODO: Corregir la descripción - Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam ut quam dolor. Quisque elementum est sed massa gravida convallis. Donec volutpat turpis eget lectus feugiat congue. Morbi rutrum auctor eleifend. Etiam iaculis libero tellus, vel aliquet erat tempor sed. Duis efficitur quam vel sapien luctus, sed semper lacus mollis. Suspendisse non nunc eleifend, aliquet elit eget, condimentum augue.

Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Vivamus vel nibh fringilla, porta elit vel, consequat libero. Nulla et libero ac nulla ultricies sollicitudin. Sed viverra non nulla id convallis. Morbi vel varius lacus, in maximus nunc. Praesent sed semper diam. Pellentesque vehicula nulla augue, ut porta dolor consequat at.

## Documentación

Revisar la documentación en [`./docs`](./docs)

### Requerimientos

# Sistema de Agencia de Viajes

## 🎯 Alcance
El sistema permitirá:
- Registrar hoteles y habitaciones con toda su información relevante.
- Gestionar disponibilidad, precios, temporadas y estados de servicio.
- Permitir a los clientes buscar, reservar, cancelar y pagar habitaciones.
- Ofrecer herramientas de calificación y comentarios para retroalimentación.

---

## 👥 Usuarios del Sistema
- **Administrador**: gestiona hoteles, habitaciones, promociones y calendarios.  
- **Cliente**: busca, reserva, paga y deja opiniones.

---

## ✅ Requerimientos Funcionales

### 1. Gestión de Hoteles
- RF1: Registrar hoteles con nombre, dirección, teléfono, correo, ubicación geográfica, descripción y fotos.  
- RF2: Activar o inactivar hoteles según su disponibilidad.  
- RF3: Gestionar ofertas y promociones de hoteles.  

### 2. Gestión de Habitaciones
- RF4: Registrar habitaciones con tipo, descripción, precio, capacidad, servicios y fotos.  
- RF5: Asignar estado a una habitación (activa, en mantenimiento, remodelación o limpieza).  
- RF6: Manejar un calendario por habitación con disponibilidad y reservas.  
- RF7: Definir precios dinámicos según temporada y ocupación.  

### 3. Reservas
- RF8: Realizar reservas en línea seleccionando fechas y habitaciones disponibles.  
- RF9: Confirmar reservas mediante pago (en línea o al llegar, según política).  
- RF10: Gestionar cancelaciones de reservas aplicando políticas de reembolso.  
- RF11: Bloquear habitaciones mientras estén reservadas o inactivas.  

### 4. Clientes
- RF12: Registrar clientes con nombre completo, teléfono, correo y dirección.  
- RF13: Permitir búsqueda de habitaciones por fecha, ubicación, precio y calificación.  
- RF14: Mostrar información detallada de cada habitación (servicios, fotos, comentarios, calificación).  

### 5. Opiniones y Calificaciones
- RF15: Permitir que los clientes califiquen y comenten su experiencia tras una estancia.  
- RF16: Calcular calificaciones promedio por habitación y generales por hotel.  

---

## ⚙️ Requerimientos No Funcionales
- RNF1: **Usabilidad** → Interfaz intuitiva y adaptable a dispositivos móviles.  
- RNF2: **Disponibilidad** → Acceso 24/7 con mínimo tiempo de inactividad.  
- RNF3: **Seguridad** → Protección de datos personales y financieros con cifrado.  
- RNF4: **Escalabilidad** → Soporte para múltiples hoteles, clientes y reservas concurrentes.  
- RNF5: **Rendimiento** → Respuesta en búsquedas y reservas en menos de 3 segundos.  

Diagrama de clases:

classDiagram
    %% =====================
    %% Clases principales
    %% =====================

    class Hotel {
        +int id
        +string nombre
        +string direccion
        +string telefono
        +string correo
        +string ubicacion
        +string descripcion
        +list~string~ fotos
        +bool activo
    }

    class Habitacion {
        +int id
        +string tipo
        +string descripcion
        +float precioBase
        +int capacidad
        +list~string~ servicios
        +list~string~ fotos
        +EstadoHabitacion estado
    }

    class Reserva {
        +int id
        +date fechaInicio
        +date fechaFin
        +string estado
        +float monto
        +string metodoPago
    }

    class Cliente {
        +int id
        +string nombre
        +string telefono
        +string correo
        +string direccion
    }

    class Opinion {
        +int id
        +int calificacion
        +string comentario
        +date fecha
    }

    class Promocion {
        +int id
        +string descripcion
        +float descuento
        +date fechaInicio
        +date fechaFin
    }

    class Calendario {
        +int id
        +list~Disponibilidad~ disponibilidad
    }

    class Disponibilidad {
        +date fecha
        +bool disponible
        +float precio
    }

    %% =====================
    %% Enumeraciones
    %% =====================

    class EstadoHabitacion {
        <<enumeration>>
        activa
        mantenimiento
        remodelacion
        limpieza
    }

    %% =====================
    %% Relaciones
    %% =====================

    Hotel "1" --> "*" Habitacion : tiene >
    Hotel "1" --> "*" Promocion : ofrece >
    Habitacion "1" --> "1" Calendario : gestiona >
    Calendario "1" --> "*" Disponibilidad : define >
    Habitacion "1" --> "*" Reserva : asociada >
    Cliente "1" --> "*" Reserva : realiza >
    Cliente "1" --> "*" Opinion : escribe >
    Hotel "1" --> "*" Opinion : recibe >

### Tárifas

|destino|pasajes|silver|gold|platinum|
|:---|---:|---:|---:|---:|
|Aruba|418|134|167|191|
|Bahamas|423|112|183|202|
|Cancún|350|105|142|187|
|Hawaii|858|210|247|291|
|Jamaica|380|115|134|161|
|Madrid|496|190|230|270|
|Miami|334|122|151|183|
|Moscu|634|131|153|167|
|NewYork|495|104|112|210|
|Panamá|315|119|138|175|
|Paris|512|210|260|290|
|Rome|478|184|220|250|
|Seul|967|205|245|265|
|Sidney|1045|170|199|230|
|Taipei|912|220|245|298|
|Tokio|989|189|231|255|

## Instalación

TODO: Corregir la explicación de la instalación - Morbi quam lectus, tempus sit amet mi non, facilisis dignissim erat. Aenean tortor libero, rhoncus eu eleifend ut, volutpat id nisi. Ut porta eros at ante rutrum pharetra. Integer nec nulla dictum, vestibulum ligula id, hendrerit ex. Morbi eget tortor metus.

1. Clonar el proyecto
```bash
git clone https://github.com/UR-CC/lpa1-taller-requerimientos.git
```

2. Crear y activar entorno virtual
```bash
cd lpa1-taller-requerimientos
python -m venv venv
venv/bin/activate
```

3. Instalar librerías y dependencias
```bash
pip install -r requirements.txt
```
    
## Ejecución

TODO: Corregir la explicación de la ejecución - Maecenas sed lorem at arcu varius mollis. Sed eleifend nulla ut blandit interdum. Donec sollicitudin nunc at orci facilisis dignissim. Donec at arcu luctus, commodo magna eget, blandit leo.

1. Ejecutar el proyecto
```bash
cd lpa1-taller-requerimientos
python app.py
```

