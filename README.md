# RSA Agent Workspace
Este repositorio centraliza la configuración, las reglas de comportamiento y el historial de sesiones (memoria episódica) para el uso de herramientas asistidas por IA (agentes) dentro de la Red Sísmica del Austro (RSA).

Está diseñado específicamente para utilizarse con entornos de desarrollo agénticos (como Google Antigravity), garantizando que el agente de IA tenga un contexto estructurado, respete las restricciones de seguridad y mantenga un registro persistente del trabajo realizado.

## 📂 Estructura del Repositorio

La estructura base está diseñada para separar la configuración del agente, los registros de chat y los entornos de trabajo remotos:

```text
RSA-Agent-Workspace/
├── .agents/                    # Directorio de configuración nativa del IDE
│   ├── rules/                  # Reglas de comportamiento (ej. restricciones de ejecución)
│   └── skills/                 # Habilidades y flujos de trabajo (ej. guardar contexto)
├── sesiones/                   # Memoria episódica (Historial de chats y contextos)
│   └── YYYY/                   # Subdividido por año y mes
│       └── MM/
└── README.md                   # Este archivo
```

## ⚙️ Uso e Instalación
Para que el entorno agéntico funcione correctamente y las reglas tengan efecto de forma global sobre todos tus proyectos:

### 1. Clona este repositorio:
Lo ideal es tenerlo en la raíz de tu directorio de trabajo principal (por ejemplo, ~/git/).

```Bash
git clone git@github.com:RedSismicaAustro/RSA-Agent-Workspace.git
```
### 2. Configuración del Workspace Raíz:
En lugar de abrir proyectos individuales en el IDE agéntico, abre tu directorio padre (ej. ~/git/) como el entorno de trabajo principal.

### 3. Vinculación de Reglas (Obligatorio):
Para que el agente pueda leer las reglas globales sin importar en qué subdirectorio estés trabajando, debes copiar o enlazar el directorio .agents a la raíz de tu entorno de trabajo (si no has abierto directamente el repositorio como raíz).

```Bash
cp -r ~/git/RSA-Agent-Workspace/.agents ~/git/
```
(Alternativamente, puedes usar enlaces simbólicos ln -s si prefieres mantener una única fuente de verdad).
## 🛡️ Reglas y Restricciones Activas
Actualmente, el agente está configurado para respetar las siguientes reglas principales:

- Restricción SSHFS (restriccion_sshfs.md): El agente tiene estrictamente prohibido ejecutar comandos de forma autónoma dentro de cualquier ruta que coincida con montajes/**. Si necesita ejecutar algo en un hardware remoto (como una Raspberry Pi), deberá generar el texto del comando y solicitar al usuario que lo ejecute manualmente.

- Idioma y Commits: Las interacciones estándar y la generación de mensajes de commit (incluyendo su formato) están forzadas a realizarse en español.

## 💾 Guardado de Contexto (Skills)
El repositorio incluye una habilidad nativa para preservar la memoria de trabajo.

Si necesitas detenerte y respaldar el estado actual de tu tarea, simplemente dile al agente: "Guarda el contexto".
El agente generará automáticamente un resumen técnico y lo almacenará en el directorio sesiones/[AÑO]/[MES]/, permitiéndote retomar el hilo de pensamiento desde cualquier otro equipo sincronizando este repositorio.
