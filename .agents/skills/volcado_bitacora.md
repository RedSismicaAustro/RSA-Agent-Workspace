# Skill: Volcado de Bitácora RSA

**Descripción de Activación:** Ejecuta este flujo ÚNICAMENTE cuando el usuario te indique el comando exacto: **"ejecuta el volcado de bitácora"** o **"actualiza la bitácora"**. 

**RESTRICCIÓN CRÍTICA (ANTI-PROMPT):** Tienes estrictamente prohibido utilizar el sistema nativo de "Knowledge Items", "Agent Memory" o cualquier base de datos interna del IDE para esta tarea. Esta habilidad consiste **exclusivamente** en la escritura de archivos de texto plano (`.md`) en el sistema de archivos local.

**Directorio Base:** `/home/rsa/git/rsa/RSA-Agent-Workspace/sesiones`

**Pasos de Ejecución:**

1. **Determinación del Origen Temporal:**
   - Identifica la fecha exacta en la que se inició el primer mensaje de esta conversación.
   - Usa esa fecha (YYYY-MM-DD) para calcular la ruta: `[Directorio Base]/YYYY/MM/`.
   - Genera el nombre del archivo basado en el tema inicial y la fecha de apertura (ej: `2026-04-20_migracion_kicad.md`).

2. **Reconstrucción Cronológica:**
   - Analiza el historial completo de la sesión actual.
   - Agrupa los avances, decisiones de arquitectura y fragmentos de código por cada día calendario detectado.

3. **Escritura en Sistema de Archivos (Local):**
   - Si el archivo `.md` no existe en la ruta calculada, créalo.
   - No incluyas la ejecucion de rules y skills, solo los cambios realizados en los archivos del proyecto.
   - Para cada día de actividad detectado, inserta un bloque con el siguiente formato, asegurándote de usar `append` para no sobreescribir:

     ```markdown
     # Actividad del [FECHA DEL DÍA DETECTADO]
     
     **Hitos de la jornada:**
     [Resumen detallado técnico]
     
     **Decisiones y Cambios:**
     - [Cambio 1]
     
     **Scripts/Comandos relevantes:**
     ```bash
     [Código clave]
     ```
     ---
     ```

4. **Sincronización Final:**
   - Informa al usuario la ruta del archivo Markdown local que ha sido actualizado.