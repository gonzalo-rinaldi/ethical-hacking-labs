# Ethical Hacking Labs

Prácticas de hacking ético en entornos de laboratorio, orientadas a comprender vulnerabilidades, evaluar su impacto y proponer medidas de detección y corrección.

## Estado

Primera práctica documentada: escaneo TCP, prueba UDP del puerto 53 y detección de servicios en los siete puertos TCP abiertos de Metasploitable Ubuntu. Se registran las versiones informadas y las incertidumbres de Samba y MySQL. Investigación de vulnerabilidades pendiente.

## Temas previstos

| Carpeta que se creará al agregar casos | Tema |
|---|---|
| `01-reconocimiento/` | Información pública y DNS |
| `02-enumeracion/` | Descubrimiento de equipos, puertos y servicios |
| `03-analisis-vulnerabilidades/` | Análisis, validación y priorización de hallazgos |
| `04-seguridad-web/` | Vulnerabilidades en aplicaciones web de laboratorio |
| `05-seguridad-redes/` | Análisis de tráfico y ataques de red en laboratorio |
| `06-explotacion-y-postexplotacion/` | Validación controlada de impacto y medidas defensivas |

## Casos publicados

- [Detección remota del sistema operativo](02-enumeracion/02-deteccion-sistema-operativo/README.md) — Linux estimado por Nmap, sin coincidencia exacta; contraste con la consola de Ubuntu.
- [Escaneos TCP/UDP e identificación de servicios](02-enumeracion/01-escaneo-puertos-servicios/README.md) — Escaneos y detección documentados; investigación de vulnerabilidades pendiente.

## Cómo documentar una práctica

1. Copiar la [plantilla de práctica](plantillas/practica.md) a una carpeta del tema correspondiente, por ejemplo `02-enumeracion/01-descubrimiento-servicios/README.md`.
2. Registrar el entorno, el alcance y los pasos efectivamente realizados.
3. Añadir evidencias seleccionadas dentro de una subcarpeta `evidencias/` del caso.
4. Explicar los resultados, limitaciones, mitigaciones y posibles señales de detección.
5. Actualizar la lista de casos publicados de este README.

## Criterio de documentación

Un resultado de herramienta no constituye por sí solo una vulnerabilidad confirmada. Cada caso distinguirá observaciones, hipótesis y hallazgos verificados. Se indicará si el ejercicio fue guiado y qué aportes se realizaron de forma independiente.

## Alcance y publicación

Usar únicamente entornos propios o autorizados. Publicar explicaciones propias y evidencias revisadas, sin contraseñas, tokens, datos personales ni material del curso redistribuido.

## Formación de referencia

[Curso completo de Hacking Ético y Ciberseguridad — Santiago Hernández](https://www.udemy.com/course/curso-completo-de-hacking-etico-y-ciberseguridad/).
