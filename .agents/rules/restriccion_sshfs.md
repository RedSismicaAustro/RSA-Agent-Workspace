---
trigger: glob
globs: `montajes/**`
---

**Contexto del Workspace:**
El entorno de trabajo actual contiene múltiples proyectos. Específicamente, el subdirectorio `montajes/` contiene sistemas de archivos de equipos remotos (hardware limitado como Raspberry Pi) montados localmente mediante `sshfs`. 

**Limitación de Entorno:**
Al operar sobre el directorio `montajes/`, el Agente NO tiene una sesión SSH activa ni acceso de ejecución sobre el hardware remoto subyacente. Intentar ejecutar comandos de validación, compilación o manipulación de servicios del sistema directamente en la terminal local producirá errores o afectará a la máquina anfitriona incorrecta.

**Reglas de Comportamiento (Cumplimiento Obligatorio):**

1. **PROHIBICIÓN DE EJECUCIÓN AUTÓNOMA:** Si el contexto de tu tarea actual involucra la ruta `montajes/`, tienes estrictamente prohibido tomar el control de la terminal para ejecutar comandos de forma autónoma (ej. ejecutar scripts, compilar código, reiniciar servicios o revisar logs).
2. **DELEGACIÓN OBLIGATORIA:** Cada vez que tu razonamiento determine que es necesario ejecutar un comando en el equipo para realizar una comprobación, instalar una dependencia o aplicar un cambio en estos sistemas remotos, DEBES detenerte y solicitar al usuario que lo ejecute.
3. **FORMATO DE ENTREGA:** Debes proporcionar el comando exacto en un bloque de código Bash e instruir al usuario para que lo ejecute en su sesión remota.

**Ejemplo de respuesta esperada ante la necesidad de ejecutar un comando:**
"Para verificar el estado del servicio, ejecuta este comando manualmente en la terminal del equipo remoto:"
```bash
sudo systemctl status rsa-acelerografo.service
```
"Esperaré la salida de este comando para continuar con el análisis."