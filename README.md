[README_HADES.md](https://github.com/user-attachments/files/28574253/README_HADES.md)
```
    ██╗  ██╗ █████╗ ██████╗ ███████╗███████╗
    ██║  ██║██╔══██╗██╔══██╗██╔════╝██╔════╝
    ███████║███████║██║  ██║█████╗  ███████╗
    ██╔══██║██╔══██║██║  ██║██╔══╝  ╚════██║
    ██║  ██║██║  ██║██████╔╝███████╗███████║
    ╚═╝  ╚═╝╚═╝  ╚═╝╚═════╝ ╚══════╝╚══════╝

    🔱 GUARDIAN DEL INFRAMUNDO DIGITAL 🔱
       Por los Hijos del Vudú — Netrunners del Tártaro
```

# HADES — Guardian del Inframundo Digital

**HADES** (`v1.0.0-TARTARUS`) es una herramienta de **vigilancia OSINT pasiva** de dominios y cuentas de email. Realiza reconocimiento pasivo, comprobación de brechas de seguridad, búsqueda de secretos expuestos en repositorios públicos e integración con plataformas de Threat Intelligence — todo sin interacción activa con los objetivos y con un informe de texto generado al finalizar.

> ⚠️ Esta herramienta solo realiza escaneos de información **pública**. Diseñada para vigilancia defensiva, OSINT ético y monitorización de exposición de datos propios.

---

## Características

- **Reconocimiento pasivo** con WHOIS y resolución DNS para cualquier dominio o email
- **Comprobación de brechas** vía HaveIBeenPwned API v3
- **Búsqueda de secretos expuestos** en repositorios públicos de GitHub
- **Búsqueda en Pastes** (Pastebin — requiere API key)
- **Threat Intelligence** integrable con VirusTotal y Shodan mediante API keys
- Acepta múltiples objetivos en el mismo ritual (dominios y emails mezclados)
- **Informe `.txt` automático** generado en el Escritorio al finalizar con todos los hallazgos
- Verificación de dependencias al arrancar con sugerencias de instalación

---

## Requisitos

- Linux / macOS con Bash
- `curl` — peticiones HTTP
- `jq` — parseo de respuestas JSON
- `whois` — consultas WHOIS
- `dig` — resolución DNS
- `nmap` — detección de red (opcional según uso)

### Instalación de dependencias

```bash
# Debian / Ubuntu / Kali
sudo apt install curl jq whois dnsutils nmap

# macOS
brew install curl jq whois bind nmap
```

---

## Instalación

```bash
git clone https://github.com/tuusuario/hades.git
cd hades
chmod +x hades_script.sh
./hades_script.sh
```

---

## Uso

HADES funciona de forma completamente interactiva. Al ejecutarlo solicita los objetivos uno a uno y lanza todos los módulos en secuencia:

```bash
./hades_script.sh
```

Ejemplo de sesión:

```
🔱 Alma: empresa.com
🔱 Alma: usuario@empresa.com
🔱 Alma: (enter vacío para finalizar)
```

Acepta tanto **dominios** (`empresa.com`, `sub.dominio.org`) como **direcciones de email** (`usuario@dominio.com`). Algunos módulos (HIBP) solo se activan si el objetivo contiene `@`.

---

## Módulos

### 🌊 Reconocimiento pasivo

Para cada objetivo ejecuta:

- **WHOIS**: registros de registro del dominio, titular, fechas de creación/expiración, servidores de nombres
- **DNS**: resolución de registros A, CNAME y demás mediante `dig`

No realiza ninguna conexión directa al objetivo.

---

### 💧 HaveIBeenPwned (HIBP)

Consulta la API v3 de [HaveIBeenPwned](https://haveibeenpwned.com) para cada email introducido y detecta si aparece en brechas de datos conocidas.

Muestra el nombre de las brechas donde aparece la cuenta (máx. 5 por objetivo).

> **Nota**: La API v3 de HIBP requiere una API key para uso automatizado. Obtén la tuya en [haveibeenpwned.com/API/Key](https://haveibeenpwned.com/API/Key).

---

### 🗝️ Búsqueda en GitHub

Busca en el índice público de código de GitHub menciones del objetivo asociadas a la palabra `password`, detectando posibles secretos o credenciales expuestas en repositorios públicos.

Devuelve el número total de resultados encontrados como indicador de exposición.

> La GitHub Search API tiene límites de tasa sin autenticación. Para búsquedas más intensivas, configura un token personal.

---

### 🕸️ Búsqueda en Pastes (Pastebin)

Rastrea menciones del objetivo en pastes públicos. Módulo preparado para integración con la API de Pastebin.

> Requiere API key de [pastebin.com/doc_api](https://pastebin.com/doc_api) para búsqueda profunda.

---

### 🔮 Threat Intelligence

Módulo de integración con plataformas externas de inteligencia de amenazas:

| Plataforma | Función | API |
|---|---|---|
| **VirusTotal** | Reputación de dominio/IP, detecciones AV | [virustotal.com/gui/my-apikey](https://www.virustotal.com/gui/my-apikey) |
| **Shodan** | Servicios expuestos, puertos abiertos, banners | [account.shodan.io](https://account.shodan.io/) |

Ambos módulos están preparados en el código — requieren configurar las API keys correspondientes para activarse.

---

## Configuración de API keys

Para activar los módulos que lo requieren, edita las variables al inicio del script:

```bash
HIBP_API_KEY="tu-api-key-aqui"
GITHUB_TOKEN="ghp_tutoken"
VIRUSTOTAL_API_KEY="tu-api-key"
SHODAN_API_KEY="tu-api-key"
PASTEBIN_API_KEY="tu-api-key"
```

---

## Informe generado

Al finalizar se genera automáticamente un informe en texto plano en el Escritorio:

```
~/Desktop/HADES_REPORT_20241215_143022.txt
```

El informe incluye:

- Cabecera con operador, hostname, sistema y timestamp de la sesión
- Lista de todos los objetivos analizados
- Resultados de cada módulo por objetivo (WHOIS, DNS, brechas, GitHub, Threat Intel)
- Sección de recomendaciones con los enlaces a las APIs
- Timestamp de inicio y fin + duración total de la sesión

---

## Estructura de salida

```
~/Desktop/
└── HADES_REPORT_20241215_143022.txt
```

---

## Recomendaciones de uso

1. Configura todas las API keys antes de ejecutar para obtener resultados completos
2. Ejecuta HADES periódicamente para vigilancia continua de tus dominios y emails
3. Revisa las brechas detectadas y cambia credenciales comprometidas de inmediato
4. Usa los resultados de GitHub como punto de partida para una revisión manual de los repositorios encontrados
5. Complementa con herramientas como `theHarvester`, `Maltego` o `Recon-ng` para OSINT más profundo

---

## Disclaimer

HADES realiza consultas exclusivamente sobre información **pública y legalmente accesible**. No realiza ningún tipo de escaneo activo, intrusión ni acceso no autorizado.

**Úsala únicamente para vigilar tus propios activos o en entornos donde tengas autorización explícita. El autor no se hace responsable del uso indebido.**

---

## Créditos

Desarrollado por **los Hijos del Vudú — Netrunners del Tártaro**.

---

## Licencia

MIT License — libre para usar, modificar y distribuir con atribución.
