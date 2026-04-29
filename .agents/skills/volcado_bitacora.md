# Skill: Volcado de Bitácora RSA

**Descripción de Activación:** Ejecuta este flujo ÚNICAMENTE cuando el usuario te indique el comando exacto: **"ejecuta el volcado de bitácora"** o **"actualiza la bitácora"**. 

**RESTRICCIÓN CRÍTICA (ANTI-PROMPT):** Tienes estrictamente prohibido utilizar el sistema nativo de "Knowledge Items", "Agent Memory" o cualquier base de datos interna del IDE para esta tarea. Esta habilidad consiste **exclusivamente** en la escritura de archivos de texto plano (`.md`) en el sistema de archivos local.

**Directorio Base:** `/home/rsa/git/rsa/RSA-Agent-Workspace`

**Pasos de Ejecución:**

1. **Determinación del Origen Temporal:**
   - Identifica la fecha exacta en la que se inició el primer mensaje de esta conversación.
   - Usa esa fecha (YYYY-MM-DD) para calcular la ruta: `[Directorio Base]/sesiones/YYYY/MM/`.
   - Genera el nombre del archivo basado en el tema inicial y la fecha de apertura (ej: `2026-04-20_migracion_kicad.md`).

2. **Extracción Automática de Metadatos:**
   - **Temas:** Analiza la conversación y extrae entre 1 y 4 palabras clave que definan las tecnologías o conceptos tratados (ej. `mqtt`, `GPD`, `telemetria`, `TIG`).
   - **Entorno:** Identifica en qué directorio de hardware remoto o proyecto local se enfocó el trabajo (ej. `acelerografo-DEV00`, `server-ubuntu`, `rsa-milton`).
   - **Formato YAML:** Prepara el bloque *frontmatter* estrictamente en este formato:
     ```yaml
     ---
     fecha: [YYYY-MM-DD]
     temas: [tema1, tema2]
     entorno: [entorno1]
     ---
     ```

3. **Reconstrucción Cronológica:**
   - Analiza el historial completo de la sesión actual.
   - Agrupa los avances, decisiones de arquitectura y fragmentos de código por cada día calendario detectado.

4. **Escritura o Actualización del Archivo de Bitácora (`.md`):**
   - **Si el archivo NO existe:**
     1. Crea el archivo y escribe el bloque YAML completo en la línea 1.
     2. A continuación, escribe el registro cronológico del día usando el formato: `# Actividad del [FECHA]` seguido de hitos, decisiones y scripts relevantes.
   - **Si el archivo YA existe:**
     1. Lee el bloque YAML existente en la parte superior del archivo.
     2. Combina los `temas` y `entornos` existentes con los nuevos que identificaste hoy. Actualiza el bloque YAML en el archivo sin duplicar elementos.
     3. Utiliza la operación de anexo (*append*) para añadir el registro de la nueva jornada al final del archivo, respetando la siguiente estructura:

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

5. **Actualización del Índice Temático:**
   - Abre el archivo `[Directorio Base]/exocortex/indice_tematico.md`.
   - Verifica las categorías de `temas` y `entorno` extraídas de la sesión actual.
   - Tienes la obligación de mantener ESTRICTAMENTE este formato en el archivo:
     ```markdown
     # Índice de Conocimiento RSA
     
     ## Entornos
     - **acelerografo-DEV00**: sesiones/2026/04/archivo_a.md, sesiones/2026/04/archivo_b.md
     - **server-ubuntu**: sesiones/2026/04/archivo_c.md
     
     ## Temas
     - **mqtt**: sesiones/2026/04/archivo_a.md, sesiones/2026/04/archivo_b.md
     - **GPD**: sesiones/2026/04/archivo_d.md
     ```
   - **Regla de Inserción:** - Si la categoría (ej. `**mqtt**:`) ya existe, simplemente añade una coma, un espacio y la nueva ruta relativa al final de esa misma línea.
     - Si la categoría no existe, crea una nueva línea con la viñeta y la ruta bajo la sección correspondiente (`## Entornos` o `## Temas`).
   - No elimines ni sobrescribas ninguna ruta existente.

6. **Sincronización Final:**
   - Imprime en la terminal del chat un breve resumen indicando:
     - Ruta de la bitácora actualizada.
     - Temas y entorno indexados.
     - Confirmación de actualización del `indice_tematico.md`.