# ProyectoFinal-POO-Arrua-UML
```mermaid
classDiagram
    %% Relaciones de Herencia y Abstracción
    Coordenada <|-- LecturaMision : Herencia (extends)
    ProcesadorDatos <|.. AnalizadorRF : Implementación (implements)
    
    %% Relaciones de Dependencia (Uso)
    AnalizadorRF ..> LecturaMision : Analiza
    GestorArchivos ..> LecturaMision : Crea una Lista
    VentanaPrincipal ..> GestorArchivos : Llama para leer/guardar
    VentanaPrincipal ..> AnalizadorRF : Llama para calcular

    %% Definición de Clases y sus miembros
    class Coordenada {
        - double latitud
        - double longitud
        - double altitud
        + Coordenada(double latitud, double longitud, double altitud)
        + getLatitud() double
        + setLatitud(double lat) void
        + getLongitud() double
        + setLongitud(double lon) void
        + getAltitud() double
        + setAltitud(double alt) void
    }

    class LecturaMision {
        - int idPaquete
        - double rssi
        - double snr
        + LecturaMision(int idPaquete, double lat, double lon, double alt, double rssi, double snr)
        + getIdPaquete() int
        + setIdPaquete(int id) void
        + getRssi() double
        + setRssi(double rssi) void
        + getSnr() double
        + setSnr(double snr) void
    }

    class ProcesadorDatos {
        <<interface>>
        + procesar(List~LecturaMision~ datos) void
    }

    class AnalizadorRF {
        - double R
        - Coordenada estacionTerrena
        + AnalizadorRF()
        + procesar(List~LecturaMision~ datos) void
        - calcularDistanciaECEF(Coordenada est, Coordenada mod) double
    }

    class GestorArchivos {
        + leerDatosCSV(String ruta) List~LecturaMision~
        + exportarReporteTXT(String ruta, String reporte) void
    }

    class VentanaPrincipal {
        - JButton btnCargar
        - JButton btnAnalizar
        - JTextArea txtConsola
        + VentanaPrincipal()
        - inicializarComponentes() void
    }
