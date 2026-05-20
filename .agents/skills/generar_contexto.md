# Skill: Generar Contexto Técnico de Script

**Descripción de Activación:** Ejecuta este flujo ÚNICAMENTE cuando el usuario te indique la instrucción: **"genera el contexto del script [nombre_script.ext]"** (o variantes como *"crea el contexto para..."*).

**Objetivo:** Analizar el código de un script específico y generar un archivo de contexto técnico estandarizado que sirva como memoria semántica para otros agentes de IA, guardándolo en la ruta del proyecto correspondiente.

---

## Pasos de Ejecución

1. **Localización y Lectura del Script:**
   - Busca el archivo solicitado en el workspace del proyecto.
   - Lee el contenido completo del script para comprender su funcionamiento, dependencias y arquitectura.

2. **Identificación de la Ruta de Salida:**
   - Localiza la raíz del proyecto al que pertenece el script.
   - La ruta de destino debe ser `<raiz_del_proyecto>/docs/context/`. Si los directorios `docs/` o `context/` no existen, créalos.
   - El archivo generado se nombrará siguiendo el patrón: `<nombre_del_script_sin_extension>_context.md`. (Ejemplo: para `mqtt_coordinator.py`, el archivo será `docs/context/mqtt_coordinator_context.md`).

3. **Análisis del Código:**
   - **Metadatos:** Identifica el proyecto, lenguaje, dependencias externas y las líneas de código (LOC).
   - **Descripción**: Redacta una descripción clara y sintética de una línea sobre el propósito principal del script.
   - **Arquitectura**: Diseña un diagrama de flujo o secuencia en **Mermaid** que describa el flujo de datos o la interacción del script con otros componentes.
   - **Configuraciones**: Identifica las variables de entorno, constantes clave o archivos JSON de configuración requeridos.
   - **Funciones/Clases**: Tabula las funciones y clases principales detallando su propósito.
   - **Limitaciones/TODOs**: Identifica de manera objetiva los límites del script (ej. falta de reintentos, validación de datos, etc.).

4. **Escritura del Archivo de Contexto:**
   - Aplica el formato estructurado utilizando la siguiente cabecera YAML y cuerpo Markdown:

   ```markdown
   ---
   proyecto: [nombre_del_proyecto]
   tipo: contexto_tecnico
   repositorio: [nombre_del_repositorio]
   script: [ruta_relativa_del_script]
   temas: [tema1, tema2, tema3]
   ---
   # [Nombre del Script o Módulo] — Contexto para Agentes IA

   > [Descripción de una línea sobre el propósito del script]

   **Ruta**: `[Ruta del script]`
   **LOC**: [Líneas de código] | **Lenguaje**: [ej. Python 3 / C / Bash] | **Dependencias**: [ej. paho-mqtt, obspy]
   **Proceso**: [ej. Daemon gestionado por Supervisor / Cron Job / Ejecución Manual]

   ---

   ## Arquitectura / Flujo de Trabajo

   [Explicación de la arquitectura]

   ```mermaid
   [Diagrama Mermaid del flujo]
   ```

   ---

   ## Configuraciones / Variables de Entorno

   [Detalle de configuraciones]

   ---

   ## Componentes / Clases / Funciones Clave

   | Elemento | Descripción |
   |----------|-------------|
   | `funcion()` | [Descripción] |

   ---

   ## Limitaciones Conocidas / TODOs

   - [Limitación 1]
   - [Limitación 2]
   ```

5. **Actualización del Índice Central (Si Aplica):**
   - Si el archivo `exocortex/indice_tematico.md` está presente en tu workspace actual:
     1. Abre `exocortex/indice_tematico.md`.
     2. Añade la ruta del archivo generado (`docs/context/nombre_context.md`) bajo la línea correspondiente del entorno en la sección `## Contextos Técnicos (Código y Arquitectura)`.
     3. Si el entorno no existe en esa sección, agrégalo.

6. **Confirmación al Usuario:**
   - Reporta al usuario la ruta del archivo de contexto generado y un resumen de las dependencias y arquitectura detectadas.
