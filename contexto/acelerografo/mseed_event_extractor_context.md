---
proyecto: generalized-phase-detection
tipo: contexto_tecnico
archivo: scripts/gui/mseed_event_extractor.py
temas: [extraccion, gui, miniseed, obspy, numpy]
---
# mseed_event_extractor.py — Contexto para Agentes IA

> GUI interactiva para la selección, previsualización, centrado y extracción de eventos específicos multicanal a partir de archivos miniSEED.

**Ruta**: `scripts/gui/mseed_event_extractor.py`  
**LOC**: 778 | **Lenguaje/Formato**: Python 3 | **Dependencias/Imágenes**: obspy, matplotlib, tkinter, python-dotenv, numpy  
**Proceso**: Ejecución manual (GUI Interactiva de Escritorio)

---

## Arquitectura / Estructura de Servicios

La aplicación sigue una estructura de responsabilidades divididas:
1. **Controladores de Estado y Modos**: `CenteringMode` y `KeepCenterMode` encapsulan la lógica de comportamiento cuando se interactúa con el gráfico de eventos.
2. **Procesamiento de Datos**: `DataProcessor` administra la lectura y la manipulación fina de subventanas de datos (trazas individuales o multicanal).
3. **Visualización y Lienzo**: `PlotManager` maneja la integración de matplotlib en Tkinter y la detección de clics y movimiento de puntero.
4. **Coordinador Principal**: `EventExtractorGUI` unifica las vistas, maneja las configuraciones locales y gestiona los diálogos de guardado de datos.

```mermaid
graph TD
    A[Usuario (GUI)] -->|1. Carga Archivo| B[EventExtractorGUI]
    B -->|Usa| C[DataProcessor]
    C -->|Lee miniSEED y remuestrea a 100Hz| D[obspy.read & Stream.resample]
    
    A -->|2. Previsualiza ventana| B
    B -->|Usa| E[TimeHandler & KeepCenterMode]
    E -->|Calcula ventana y desfases| B
    B -->|Extrae segmento visual| C
    C -->|slice & select| F[Segmento]
    B -->|Grafica| G[PlotManager]
    G -->|Muestra trazas y línea central| H[FigureCanvasTkAgg]
    
    A -->|3. Centrar Evento (Click)| G
    G -->|Captura click / Calcula Delta| I[CenteringMode]
    I -->|Ajusta Desplazamiento| B
    
    A -->|4. Guardar Evento| B
    B -->|Extrae todos los canales| C
    C -->|extract_segment_multi| J[Segmento Multicanal]
    B -->|Normaliza tipo y codifica| K[np.float32 / np.int32]
    K -->|Guarda .mseed| L[ObsPy Stream.write]
```

---

## Configuraciones / Variables de Entorno

El script lee las siguientes variables de configuración desde el archivo `.env` del proyecto:

| Variable | Propósito | Fallback |
|----------|-----------|----------|
| `GPD_LOCAL_ROOT` | Raíz local del proyecto para resoluciones de ruta. | Lanza un error crítico de ejecución si no está definida en el `.env`. |
| `GPD_DATA_DIR` | Directorio por defecto en donde se abre el explorador de archivos. | `os.getcwd()` |

---

## Componentes / Clases / Funciones Clave

| Elemento | Tipo | Descripción |
|----------|------|-------------|
| `TimeHandler` | Clase | Parsea cadenas de tiempo con precisión de milisegundos y calcula marcas temporales absolutas usando `UTCDateTime`. |
| `DataProcessor` | Clase | Carga archivos miniSEED remuestreándolos a 100 Hz. Ofrece recorte de un canal específico (`extract_segment`) o de todos los canales presentes en la subventana (`extract_segment_multi`). |
| `PlotManager` | Clase | Gestiona el lienzo Tkinter de matplotlib y enlaza eventos de movimiento de cursor y clics sobre el gráfico de formas de onda. |
| `CenteringMode` | Clase | Administra el estado de centrado interactivo. Si está activo, calcula la diferencia de tiempo (delta) con respecto al centro del gráfico al hacer clic. |
| `KeepCenterMode` | Clase | Permite mantener el centro de tiempo actual del evento fijo cuando se cambia dinámicamente la duración de la ventana. |
| `EventExtractorGUI` | Clase | Componente maestro. Construye la interfaz, valida las entradas numéricas y de hora de inicio, y maneja el proceso de guardado. |
| `EventExtractorGUI._save_mseed` | Método | Guarda el segmento de tiempo visualizado extrayendo **todos** los canales disponibles en la ventana. Autodetecta tipos de datos para codificar robustamente: si hay valores flotantes usa `FLOAT32` (codificación 4), y si son enteros homogeniza a `int32` bajo `STEIM2` (codificación 11). |

---

## Limitaciones Conocidas / TODOs

- **Dependencia de GPD_LOCAL_ROOT**: A diferencia del visualizador simple, este script se detiene con error si no encuentra la variable de entorno `GPD_LOCAL_ROOT` en el archivo `.env`.
- **Homogeneización de Datos**: Al exportar los segmentos recortados, la función de guardado puede convertir tipos de datos enteros y flotantes a un formato homogéneo (`float32` o `int32`) para evitar inconsistencias en el formato miniSEED, lo que podría alterar ligeramente los dtypes originales si eran mixtos.
- **Rendimiento**: Cargar y manipular en memoria archivos miniSEED extremadamente grandes de 24 horas puede causar ralentización temporal del hilo de Tkinter.
