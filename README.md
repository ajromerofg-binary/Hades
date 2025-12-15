¿QUÉ ES HADES?

HADES es un script de vigilancia digital diseñado para proteger a empresas
y clientes particulares contra la filtración de datos y ciberdelincuencia.
Funciona como un "guardián automático" que busca menciones de tus dominios,
correos electrónicos o datos sensibles en lugares públicos de internet donde
los ciberdelincuentes suelen compartir información robada.

¿QUÉ HACE HADES EXACTAMENTE?

HADES realiza 6 tipos de vigilancia automática:

1. VERIFICACIÓN DE HERRAMIENTAS (Cerbero).
   • Comprueba que tienes instaladas las herramientas necesarias.
   • Te avisa si falta algo.
   • Herramientas: curl, jq, whois, dig, nmap.
   
2.  RECONOCIMIENTO BÁSICO (Río Estigia).
   • Obtiene información pública del dominio (WHOIS).
   • Revisa registros DNS.
   • Identifica servidores y configuraciones.
   • 100% LEGAL - solo info pública.

3.  BÚSQUEDA EN PASTEBIN (Cavernas Oscuras).
   • Busca si tus dominios/emails aparecen en Pastebin.
   • Pastebin es usado por hackers para compartir datos robados.
   • Detecta credenciales filtradas públicamente.
   • Requiere: API de Pastebin (opcional pero recomendado).

4. VERIFICACIÓN DE BRECHAS (Pozo de Almas - HaveIBeenPwned).
   • Comprueba si tus emails están en bases de datos filtradas.
   • Usa HaveIBeenPwned, la mayor base de datos de brechas.
   • Te dice en qué servicios se filtró tu información.
   • Funciona sin API, mejor con API key.

5. ESCANEO DE REPOSITORIOS (GitHub).
   • Busca secretos expuestos accidentalmente en código público.
   • Detecta: contraseñas, API keys, tokens, credenciales.
   • Revisa repositorios públicos de GitHub.
   • Previene robo de credenciales de desarrolladores.

 6. INTELIGENCIA DE AMENAZAS (Oráculo).
   • Consulta bases de datos de amenazas conocidas.
   • Usa VirusTotal para detectar malware asociado.
   • Usa Shodan para ver exposición de servicios.
   • Requiere: APIs de VirusTotal y Shodan.


   
