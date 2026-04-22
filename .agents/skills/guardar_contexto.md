# Skill: Registro de Sesión RSA (Estructura Dinámica)

**Descripción:** Ejecuta este flujo cada vez que el usuario solicite "guarda el contexto", "registra la sesión" o proporcione una fecha para un registro atrasado. Esta habilidad organiza la memoria episódica del trabajo en el repositorio de gestión.

**Directorio Base:** `rsa/RSA-Agent-Workspace/sesiones/`

**Pasos de Ejecución:**

1. **Determinación de la Fecha:**
   - **Prioridad 1 (Manual):** Si el usuario menciona una fecha específica en su instrucción (ej. "guarda el contexto del lunes pasado" o "para el 2026-04-20"), extrae esa fecha y úsala para el registro.
   - **Prioridad 2 (Sistema):** Si no se especifica, ejecuta `date "+%Y-%m-%d"` y `date "+%H:%M:%S"` para obtener el timestamp actual.

2. **Cálculo de Ruta Dinámica:**
   - Basado en la fecha (manual o de sistema), genera la ruta: `[Directorio Base]/YYYY/MM/`.
   - Ejemplo: Para una sesión del 22 de abril de 2026, la ruta es `.../sesiones/2026/04/`.
   - Ejecuta `mkdir -p` para asegurar que la estructura de carpetas exista.

3. **Gestión del Archivo:**
   - **Identificación:** Busca si ya existe un archivo Markdown para la sesión actual en esa carpeta.
   - **Creación:** Si es nuevo, genera un nombre descriptivo basado en el tema (ej: `calibracion_acelerografo_dev00.md`).
   - **Anexo:** Si ya existe, prepárate para añadir al final del archivo.

4. **Redacción del Registro:**
   - Extrae los hitos, decisiones de arquitectura (ej. cambios en el firmware o restructuracion de topics mqtt) y scripts generados.
   - Formato de inserción (Append):
     ```markdown
     ## Registro del [FECHA] a las [HORA]
     
     **Resumen Técnico:**
     [Resumen de los últimos avances]
     
     **Contexto de Hardware/Software:**
     - Cambios en: [Archivos o componentes]
     - Comandos clave: [Comandos ejecutados/recomendados]
     ---
     ```

5. **Finalización:**
   - Notifica la ruta exacta del archivo actualizado para que el usuario pueda verificarlo o realizar el commit.