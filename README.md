# Ethical Hacking Labs

Portafolio de Gonzalo Rinaldi: prácticas guiadas sobre máquinas propias, con evidencias de enumeración, análisis de vulnerabilidades e interpretación de resultados.

**Versión cerrada — 13 de octubre de 2026.** Esta entrega reúne siete casos documentados. El alcance final comprende descubrimiento de servicios, enumeración SMB/SNMP, evaluaciones con Nmap y Nessus y contraste de MS17-010 mediante un escáner auxiliar de Metasploit.

## Recorrido recomendado

| Caso | Trabajo documentado |
|---|---|
| [Nmap y Nessus en Windows](03-analisis-vulnerabilidades/01-windows-nmap-nessus/README.md) | Lectura de resultados SMB/TLS, informe HTML, análisis básico y propuestas de remediación |
| [Evaluación avanzada con Nessus](03-analisis-vulnerabilidades/02-nessus-avanzado/README.md) | Cuatro hallazgos seleccionados, comparación de políticas y límites de cobertura |
| [Contraste de MS17-010](03-analisis-vulnerabilidades/03-contraste-ms17-010/README.md) | Segunda detección con Metasploit y distinción entre detección y explotación |
| [Escaneos TCP/UDP y servicios](02-enumeracion/01-escaneo-puertos-servicios/README.md) | Identificación de puertos y servicios en Ubuntu |
| [Detección de sistema operativo](02-enumeracion/02-deteccion-sistema-operativo/README.md) | Estimación de Nmap y contraste con la consola |
| [Enumeración de Windows](02-enumeracion/03-enumeracion-windows/README.md) | Identificación por SMB y enumeración parcial de recursos compartidos |
| [Enumeración SNMP](02-enumeracion/04-enumeracion-snmp/README.md) | Comparación TCP/UDP, inventario de software y usuarios del laboratorio |

## Competencias practicadas

- Interpretar puertos, servicios, sistemas operativos y respuestas de herramientas.
- Seleccionar evidencias y redactar resultados reproducibles a partir de prácticas guiadas.
- Diferenciar detecciones, errores, comprobaciones incompletas y acceso efectivamente conseguido.
- Priorizar la revisión de hallazgos y proponer medidas de corrección sin atribuirles una validación inexistente.
- Resolver la presentación local de un informe XML de Nmap mediante conversión a HTML.

## Resultado y límites del cierre

Se conserva lo demostrado por las capturas. **No se consiguió demostrar explotación exitosa, sesión remota ni ejecución de comandos en el objetivo.** El contraste con Metasploit refuerza la detección de MS17-010, pero sigue siendo una comprobación de escáner.

Las correcciones, las pruebas posteriores a remediación y una auditoría autenticada completa no forman parte de esta entrega. Los puntos pendientes de los informes se conservan como límites técnicos, sin comprometer nuevas etapas. Los contadores de Nessus no se presentan como CVE únicos; los avisos de autenticación, DNS y plugins quedan documentados.

## Entorno y metodología

[Cybersecurity Homelab](https://github.com/gonzalo-rinaldi/cybersecurity-homelab) reúne las pruebas de conectividad y el contexto de las máquinas VMware, Kali, Metasploitable Ubuntu y Windows.

Las prácticas se realizaron como parte de una formación guiada. Este repositorio presenta la documentación de las pruebas y sus evidencias; no acredita experiencia profesional ni una auditoría de producción. La [plantilla](plantillas/practica.md) se conserva como recurso reutilizable.

## Alcance

Pruebas sobre sistemas propios de laboratorio. Las direcciones privadas de las capturas pertenecen al entorno de práctica. No se incluyen credenciales, material audiovisual del curso ni resultados inventados.
