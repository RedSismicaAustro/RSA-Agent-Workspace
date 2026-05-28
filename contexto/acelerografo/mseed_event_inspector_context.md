---
proyecto: generalized-phase-detection
tipo: contexto_tecnico
archivo: scripts/gui/mseed_event_inspector.py
temas: [visualizacion, gui, miniseed, obspy]
---
# mseed_event_inspector.py — Contexto para Agentes IA

> GUI simple interactiva para la visualización, inspección y análisis estadístico de archivos miniSEED.

**Ruta**: `scripts/gui/mseed_event_inspector.py`  
**LOC**: 416 | **Lenguaje/Formato**: Python 3 | **Dependencias/Imágenes**: obspy, matplotlib, tkinter, python-dotenv  
**Proceso**: Ejecución manual (GUI Interactiva de Escritorio)

---

## Arquitectura / Estructura de Servicios

El script está diseñado bajo un esquema simple de separación de responsabilidades:
1. **DataProcessor**: Carga de datos, remuestreo, cálculo estadístico e impresión de metadata en consola.
2. **PlotManager**: Encapsulamiento del graficado con matplotlib interactuando con canvas de Tkinter.
3. **SimpleViewerGUI**: Gestión del ciclo de vida de la ventana y los controles Tkinter.

```mermaid
graph TD
    A[Usuario (GUI)] -->|Abre archivo| B[SimpleViewerGUI]
    B -->|Usa| C[DataProcessor]
    C -->|Lee miniSEED| D[obspy.read]
    C -->|Remuestrea a 100Hz| E[Stream.resample]
    C -->|Extrae e imprime| F[Metadata por Consola]
    B -->|Actualiza| G[Widgets de Información en GUI]
    B -->|Solicita Graficar| H[PlotManager]
    H -->|Genera Subplots por Canal| I[matplotlib.pyplot]
    I -->|Embebe en Tkinter| J[FigureCanvasTkAgg]
    H -->|Monitorea cursor| K[lbl_pos / Muestra tiempo absoluto]
```

---

## Configuraciones / Variables de Entorno

El script lee las siguientes variables de configuración desde el archivo `.env` del proyecto:

| Variable | Propósito | Fallback |
|----------|-----------|----------|
| `GPD_LOCAL_ROOT` | Raíz local del proyecto para resoluciones de ruta. | `os.getcwd()` (directorio actual) |
| `GPD_DATA_DIR` | Directorio por defecto en donde se abre el explorador de archivos. | `os.getcwd()` |

---

## Componentes / Clases / Funciones Clave

| Elemento | Tipo | Descripción |
|----------|------|-------------|
| `TimeHandler` | Clase | Contiene utilidades estáticas para formatear objetos datetime con precisión de milisegundos. |
| `DataProcessor` | Clase | Lee los archivos `.mseed` usando ObsPy, clona los datos originales y remuestrea la copia a 100 Hz para su visualización. Extrae estadísticas detalladas (mínimo, máximo, media, desviación estándar). |
| `DataProcessor._print_metadata` | Método | Imprime en consola un reporte detallado con la metadata de la red sismológica, estación, canales y estadísticas físicas de la señal. |
| `PlotManager` | Clase | Administra el canvas de matplotlib incrustado en Tkinter (`FigureCanvasTkAgg`). Grafica cada canal en un subplot individual compartiendo el eje de tiempo en horas. |
| `SimpleViewerGUI` | Clase | Construye el layout principal de la GUI, conecta los eventos y controla los widgets de visualización (fecha, inicio, fin, duración). |

---

## Limitaciones Conocidas / TODOs

- **Solo Visualización**: No cuenta con capacidades de recorte, filtrado o guardado de datos (herramienta exclusivamente de inspección).
- **Consumo de Memoria**: Al cargar archivos muy grandes completos a memoria mediante ObsPy, puede haber problemas de rendimiento o consumo excesivo si la duración del registro es muy extensa.
- **Frecuencia Fija**: Remuestrea internamente todo a 100.0 Hz de forma automática para simplificar el despliegue gráfico.
