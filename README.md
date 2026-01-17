# Liga de Fútbol Española 2025 - Angular

Proyecto desarrollado en Angular.
Este proyecto es una evolución de una práctica anterior en TypeScript puro, migrada ahora a un framework moderno aplicando Programación Orientada a Objetos (POO)

## Diagrama de Clases (UML)

A continuación se detalla la estructura de clases del proyecto, mostrando el encapsulamiento y las relaciones entre el Servicio, los Equipos y los Jugadores.

```mermaid
classDiagram

%% --- MODELOS ---
    class Jugador {
        -number _id
        -string _nombre
        -string _posicion
        -number _dorsal
        +constructor(_id, _nombre, _posicion, _dorsal)
        +get id() number
        +set id(number)
        +get nombre() string
        +set nombre(string)
        +get posicion() string
        +set posicion(string)
        +get dorsal() number
        +set dorsal(number)
    }

    class Equipo {
        -string _id
        -string _nombre
        -number _puntos
        +number _partidosJugados
        -number _partidosGanados
        -number _partidosEmpatados
        -number _partidosPerdidos
        -number _golesFavor
        -number _golesContra
        -number _diferenciaGoles
        -string[] _ultimos5
        -string _urlEscudo
        -Jugador[] _jugadores
        +constructor(...)
        +get id() string
        +get nombre() string
        +get puntos() number
        +get jugadores() Jugador[]
        +actualizarEstadisticas(golesFavor, golesContra) void
    }
%% --- SERVICIO ---
    class LigaService {
        -Equipo[] _equipos
        +Subject equiposActualizados
        +getEquipos() Equipo[]
        +getEquipoPorId(id) Equipo
        +registrarPartido(idLocal, idVisitante, golesLocal, golesVisitante) void
    }

%% --- COMPONENTES ---
    class Tabla-clasificacion {
        -Equipo[] equipos
        +ngOnInit()
    }
    class Formulario-partidos {
        -Equipo[] equipos
        +actualizar()
    }
    class Detalle-equipo {
        -Equipo equipo
        +ngOnInit()
    }

%% --- RELACIONES ---
  %% Modelos
    Equipo *-- "0..*" Jugador : Composición 
    LigaService o-- "1..*" Equipo : Agregación (Gestiona)
    
  %% Dependencias (Los componentes usan el servicio)
    Tabla-clasificacion ..> LigaService : Usa
    Formulario-partidos ..> LigaService : Usa
    Detalle-equipo ..> LigaService : Usa



