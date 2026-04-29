# Skill: Consulta Histórica de Bitácoras

**Descripción de Activación:** Ejecuta este flujo cuando el usuario realice preguntas sobre el estado pasado de un proyecto, resúmenes de semanas anteriores o solicitudes de información sobre temas específicos (ej. "en qué trabajamos la semana pasada", "busca información sobre mqtt").

**Objetivo:** Minimizar el consumo de tokens cargando únicamente los archivos estrictamente necesarios.

**Pasos de Ejecución (Cumplimiento Estricto):**

1. **Consulta del Índice (Fase de Enrutamiento):**
   - Tienes prohibido usar comandos como `grep`, `find` o leer archivos dentro de `sesiones/` directamente.
   - Tu primera acción OBLIGATORIA es leer el contenido del archivo `/home/rsa/git/rsa/RSA-Agent-Workspace/exocortex/indice_tematico.md`.

2. **Selección de Archivos:**
   - Cruza la consulta del usuario con las categorías y temas del índice. 
   - Extrae únicamente las rutas de los archivos `.md` que coincidan con la solicitud.
   - Si la consulta es por fechas (ej. "la semana pasada"), verifica los nombres de los archivos en las rutas, ya que contienen la fecha (`YYYY-MM-DD`).

3. **Carga Estrictamente Necesaria (Fase de Lectura):**
   - Una vez identificadas las rutas (máximo 3 a 5 archivos para no desbordar el contexto), lee el contenido de esos archivos específicos.

4. **Síntesis y Respuesta:**
   - Analiza el contenido recuperado.
   - Responde a la pregunta del usuario de forma directa y técnica.
   - Incluye al final de tu respuesta las referencias a los archivos leídos (ej. *Fuentes consultadas: sesiones/2026/04/archivo.md*).