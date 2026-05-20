# Skill: Consulta Histórica de Bitácoras

**Descripción de Activación:** Ejecuta este flujo cuando el usuario realice preguntas sobre el estado pasado de un proyecto, resúmenes de semanas anteriores o solicitudes de información sobre temas específicos (ej. "en qué trabajamos la semana pasada", "busca información sobre mqtt").

**Objetivo:** Minimizar el consumo de tokens cargando únicamente los archivos estrictamente necesarios.

**Pasos de Ejecución (Cumplimiento Estricto):**

1. **Consulta del Índice (Fase de Enrutamiento):**
   - Tienes prohibido usar comandos como `grep`, `find` o leer archivos dentro de `sesiones/` directamente.
   - Tu primera acción OBLIGATORIA es leer el contenido del archivo `/home/rsa/git/rsa/RSA-Agent-Workspace/exocortex/indice_tematico.md`.

2. **Selección de Archivos:**
   - Cruza la consulta del usuario con las categorías del índice (`Contextos Técnicos`, `Historial de Sesiones por Entorno`, `Historial de Sesiones por Tema`).
   - Si la consulta se refiere a un entorno o script específico, extrae el archivo de **Contexto Técnico** relevante (por ejemplo, `contexto/acelerografo/mqtt_coordinator_context.md`) y las bitácoras de **Sesiones** relacionadas con ese tema/entorno.
   - Si la consulta es sobre un historial de cambios o fechas (ej. "qué se hizo la semana pasada"), prioriza los archivos de `sesiones/`.
   - Si la consulta es sobre la funcionalidad de un código en producción (ej. "cómo funciona el extractor de miniSEED"), prioriza el archivo correspondiente en `contexto/`.

3. **Carga de Archivos (Fase de Lectura):**
   - Para consultas técnicas de código, lee primero el archivo de **Contexto Técnico** para establecer la base semántica de la arquitectura y el comportamiento esperado del script.
   - Lee a continuación los archivos de **Sesiones** correspondientes (máximo 3 a 5 archivos en total para evitar desbordar el contexto de la IA) para entender los cambios o decisiones de diseño más recientes que afectan a dicho código.

4. **Síntesis y Respuesta:**
   - Sintetiza la información integrando la explicación técnica actual (del contexto) con las decisiones/cambios históricos (de las sesiones).
   - Responde a la pregunta de forma directa, rigurosa y técnica en español.
   - Incluye al final de la respuesta las referencias explícitas a los archivos leídos (ej: *Fuentes consultadas: contexto/acelerografo/mqtt_coordinator_context.md, sesiones/2026/05/2026-05-11_extraccion_remota_mqtt.md*).