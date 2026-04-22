---
trigger: always_on
---

# Reglas para mensajes de Commit

Cada vez que se solicite generar un commit, no debes tratar de ejecutarlo directamente en la terminal, limitate solo a mostrar el texto,

El texto del commit generado debe seguir ESTRICTAMENTE estas reglas:

1. **Idioma:** Todo el texto generado para el commit debe estar en español.
2. **Estructura:** Debes usar la convención de "tipo: descripción corta" seguida de un guion alto.
3. **Detalles:** A continuación del guion, debes listar los cambios específicos utilizando viñetas (`-`).
4. **Sub-viñetas:** Si un cambio involucra múltiples elementos dentro del mismo archivo o componente, utiliza viñetas anidadas con dos espacios de sangría (`  -`).

Ejemplo estricto de formato esperado:

feat: mejora de métricas de salud y refactorización de heartbeat
- Se implementaron métricas detalladas de hardware en mqtt_coordinator.py:
  - Porcentaje de espacio en disco (reemplaza GB).
  - RAM disponible en MB.
  - Load Average de 15 minutos.
  - Temperatura del CPU usando 'vcgencmd'.
  - Estado de Throttling/Undervoltage del sistema.
- Se eliminó la lógica de publicación de heartbeat del script coordinador.
