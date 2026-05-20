# Skill: Generar Contexto Técnico de Archivo/Componente

**Descripción de Activación:** Ejecuta este flujo ÚNICAMENTE cuando el usuario te indique la instrucción: **"genera el contexto de [nombre_archivo.ext]"** o **"genera el contexto del componente [nombre_archivo.ext]"** (o variantes como *"crea el contexto para..."*).

**Objetivo:** Analizar el código/configuración de un archivo o componente específico (scripts Python/Bash, código C, docker-compose.yml, etc.) y generar un archivo de contexto técnico estandarizado que sirva como memoria semántica para otros agentes de IA, guardándolo en la ruta del proyecto correspondiente.

---

## Pasos de Ejecución

1. **Localización y Lectura del Archivo:**
   - Busca el archivo solicitado en el workspace del proyecto.
   - Lee el contenido completo para comprender su funcionamiento, dependencias y arquitectura.

2. **Identificación de la Ruta de Salida:**
   - Localiza la raíz del proyecto al que pertenece el archivo.
   - La ruta de destino debe ser `<raiz_del_proyecto>/docs/context/`. Si los directorios `docs/` o `context/` no existen, créalos.
   - El archivo generado se nombrará siguiendo el patrón: `<nombre_del_archivo_sin_extension>_context.md`. (Ejemplo: para `docker-compose.yml`, el archivo será `docs/context/docker-compose_context.md`).

3. **Análisis del Archivo:**
   - **Metadatos:** Identifica el proyecto, lenguaje/formato, dependencias externas o imágenes y las líneas de código/configuración (LOC).
   - **Descripción**: Redacta una descripción clara y sintética de una línea sobre el propósito principal del archivo.
   - **Arquitectura**: Diseña un diagrama de flujo, relaciones o servicios en **Mermaid** que describa el flujo de datos o la estructura interna (como servicios de Docker).
   - **Configuraciones**: Identifica las variables de entorno, puertos expuestos, constantes clave o volúmenes requeridos.
   - **Componentes/Clases/Funciones/Servicios**: Tabula los elementos principales (funciones/clases en código, servicios en docker-compose) detallando su propósito.
   - **Limitaciones/TODOs**: Identifica de manera objetiva los límites o consideraciones críticas (ej. sin persistencia de volúmenes, dependencias no tolerantes a fallos, etc.).

4. **Escritura del Archivo de Contexto:**
   - Aplica el formato estructurado utilizando la siguiente cabecera YAML y cuerpo Markdown:

   ```markdown
   ---
   proyecto: [nombre_del_proyecto]
   tipo: contexto_tecnico
   archivo: [ruta_relativa_del_archivo]
   temas: [tema1, tema2, tema3]
   ---
   # [Nombre del Archivo o Componente] — Contexto para Agentes IA

   > [Descripción de una línea sobre el propósito del archivo]

   **Ruta**: `[Ruta del archivo]`
   **LOC**: [Líneas de código/configuración] | **Lenguaje/Formato**: [ej. Python 3 / C / YAML (Docker Compose)] | **Dependencias/Imágenes**: [ej. paho-mqtt, python:3.9-slim]
   **Proceso**: [ej. Daemon gestionado por Supervisor / Contenedores Docker / Ejecución Manual]

   ---

   ## Arquitectura / Estructura de Servicios

   [Explicación de la arquitectura o servicios]

   ```mermaid
   [Diagrama Mermaid del flujo o estructura de servicios]
   ```

   ---

   ## Configuraciones / Variables de Entorno

   [Detalle de configuraciones, puertos, volúmenes, etc.]

   ---

   ## Componentes / Funciones / Servicios Clave

   | Elemento | Descripción |
   |----------|-------------|
   | `funcion_o_servicio` | [Descripción] |

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
   - Reporta al usuario la ruta del archivo de contexto generado y un resumen de las dependencias/servicios y arquitectura detectados.
