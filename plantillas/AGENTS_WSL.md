# Guía para Agentes de IA en RSA-Agent-Workspace

Como agente de IA, debes leer este archivo para entender cómo interactuar con los repositorios, cómo catalogar la información y qué reglas de seguridad debes seguir estrictamente.

---

## Inicio de coversacion

Al inicio de una nueva conversacion, el usuario te indicara cuales son los directorios de trabajo, con una instruccion del tipo: "nuestro directorio de trabajo exclusivo será [DIRECTORIO]". No modifiques ni busques archivos fuera de esta ruta a menos que el usuario te lo pida.
Paralelamente tendras acceso al directorio rsa/RSA-Agent-Workspace/ para guardar actualizaciones de memoria y consulta de conocimiento pasado.
---

## ⚙️ Habilidades y Flujos de Trabajo (Skills)

Bajo el directorio `.agents/skills/` se encuentran las automatizaciones nativas del entorno agéntico:

- **Guardar/Actualizar Memoria**:
  - Se activa con el comando del usuario: **"ejecuta el volcado de bitácora"** o **"actualiza la bitácora"**.
  - Sigue las instrucciones de [volcado_bitacora.md](.agents/skills/volcado_bitacora.md).
  - **Nota Crítica**: Cuando agregues una nueva sesión al índice, añádela únicamente en las categorías de `## Historial de Sesiones por Entorno` o `## Historial de Sesiones por Tema`. **NUNCA** modifiques la sección `## Contextos Técnicos (Código y Arquitectura)` durante el volcado de bitácoras.

- **Consulta de Conocimiento Pasado**:
  - Se activa cuando el usuario realiza preguntas sobre el pasado de un proyecto o el funcionamiento de un script.
  - Sigue las instrucciones de [consulta_historica.md](.agents/skills/consulta_historica.md).
  - **Estrategia de Carga**: Primero, lee el **Contexto Técnico** en `rsa/RSA-Agent-Workspace/contexto/` para entender las especificaciones y arquitectura del script. Segundo, lee las **Sesiones** relacionadas en `rsa/RSA-Agent-Workspace/sesiones/` para entender los últimos cambios/decisiones cronológicas.

- **Generar Contexto Técnico de Archivo/Componente**:
  - Se activa con el comando: **"genera el contexto de [nombre_archivo.ext]"** o **"genera el contexto del componente [nombre_archivo.ext]"** (o similares).
  - Sigue las instrucciones de [generar_contexto.md](.agents/skills/generar_contexto.md).
  - Analiza el archivo indicado (código C/Python, docker-compose.yml, etc.) y crea un archivo estructurado en la carpeta `rsa/RSA-Agent-Workspace/contexto/` y en la carpeta `docs/context/` del respectivo proyecto, agregando metadatos YAML e indexándolo si corresponde.

---

## 🛡️ Reglas de Comportamiento Críticas

Debes respetar estas reglas en todas tus respuestas y ejecuciones:

1. **Restricción de Comandos Remotos (SSHFS)**:
   - Está estrictamente prohibido ejecutar comandos automáticos (`run_command`) sobre cualquier ruta que coincida con montajes del sistema de archivos remoto (`montajes/**`).
   - Si necesitas ejecutar algo en hardware remoto (ej. una Raspberry Pi), debes preparar el comando en texto y pedirle al usuario que lo ejecute manualmente.
   - Consulta los detalles en [restriccion_sshfs.md](.agents/rules/restriccion_sshfs.md).

2. **Formato de Commits**:
   - Si el usuario te pide un mensaje de commit o una propuesta de commit, **no intentes ejecutarlo tú mismo en la terminal**. Muestra el texto.
   - El mensaje debe redactarse en **español** bajo la estructura:
     `tipo: descripción corta` seguido de un guion alto (`-`) y detalles específicos en viñetas y sub-viñetas (con sangría de dos espacios).
   - Consulta los detalles en [commits.md](.agents/rules/commits.md).

3. **Idioma**:
   - Todas tus interacciones, reportes y códigos de documentación en este repositorio deben realizarse en **español**.
