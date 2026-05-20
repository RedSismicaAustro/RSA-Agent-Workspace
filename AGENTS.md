# Guía para Agentes de IA en RSA-Agent-Workspace

¡Bienvenido! Este repositorio centraliza la memoria técnica, reglas y automatizaciones para los desarrollos en la **Red Sísmica del Austro (RSA)**. Está diseñado para actuar como un **exocortex** (un sistema de memoria externa) que expande tu contexto de trabajo.

Como agente de IA, debes leer este archivo para entender cómo interactuar con el repositorio, cómo catalogar la información y qué reglas de seguridad debes seguir estrictamente.

---

## 📂 Estructura del Exocortex

El conocimiento de la RSA está organizado en dos tipos de memoria:

1. **Memoria Semántica (Documentación de Código)**:
   - Se ubica en [contexto/](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/contexto/).
   - Contiene la arquitectura, flujos de datos, dependencias y limitaciones de los scripts actualmente en producción (agrupados por entorno, ej: `contexto/acelerografo/`).
   
2. **Memoria Episódica (Bitácora de Cambios)**:
   - Se ubica en [sesiones/](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/sesiones/).
   - Contiene los registros técnicos cronológicos detallados de las sesiones de chat con IAs y sesiones de programación asistida en el IDE (agrupados por año y mes).

3. **Índice Maestro**:
   - El archivo [exocortex/indice_tematico.md](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/exocortex/indice_tematico.md) es la fuente única de verdad para el mapeo de temas, entornos, contextos y sesiones.

---

## ⚙️ Habilidades y Flujos de Trabajo (Skills)

Bajo el directorio `.agents/skills/` se encuentran las automatizaciones nativas del entorno agéntico:

- **Guardar/Actualizar Memoria**:
  - Se activa con el comando del usuario: **"ejecuta el volcado de bitácora"** o **"actualiza la bitácora"**.
  - Sigue las instrucciones de [volcado_bitacora.md](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/.agents/skills/volcado_bitacora.md).
  - **Nota Crítica**: Cuando agregues una nueva sesión al índice, añádela únicamente en las categorías de `## Historial de Sesiones por Entorno` o `## Historial de Sesiones por Tema`. **NUNCA** modifiques la sección `## Contextos Técnicos (Código y Arquitectura)` durante el volcado de bitácoras.

- **Consulta de Conocimiento Pasado**:
  - Se activa cuando el usuario realiza preguntas sobre el pasado de un proyecto o el funcionamiento de un script.
  - Sigue las instrucciones de [consulta_historica.md](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/.agents/skills/consulta_historica.md).
  - **Estrategia de Carga**: Primero, lee el **Contexto Técnico** en `contexto/` para entender las especificaciones y arquitectura del script. Segundo, lee las **Sesiones** relacionadas en `sesiones/` para entender los últimos cambios/decisiones cronológicas.

---

## 🛡️ Reglas de Comportamiento Críticas

Debes respetar estas reglas en todas tus respuestas y ejecuciones:

1. **Restricción de Comandos Remotos (SSHFS)**:
   - Está estrictamente prohibido ejecutar comandos automáticos (`run_command`) sobre cualquier ruta que coincida con montajes del sistema de archivos remoto (`montajes/**`).
   - Si necesitas ejecutar algo en hardware remoto (ej. una Raspberry Pi), debes preparar el comando en texto y pedirle al usuario que lo ejecute manualmente.
   - Consulta los detalles en [restriccion_sshfs.md](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/.agents/rules/restriccion_sshfs.md).

2. **Formato de Commits**:
   - Si el usuario te pide un mensaje de commit o una propuesta de commit, **no intentes ejecutarlo tú mismo en la terminal**. Muestra el texto.
   - El mensaje debe redactarse en **español** bajo la estructura:
     `tipo: descripción corta` seguido de un guion alto (`-`) y detalles específicos en viñetas y sub-viñetas (con sangría de dos espacios).
   - Consulta los detalles en [commits.md](file:///c:/Users/miltonrsa/Documents/Proyectos-RSA/Git/RSA-Agent-Workspace/.agents/rules/commits.md).

3. **Idioma**:
   - Todas tus interacciones, reportes y códigos de documentación en este repositorio deben realizarse en **español**.
