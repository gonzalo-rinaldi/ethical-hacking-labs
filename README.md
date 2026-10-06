# Ethical Hacking Labs

Prácticas de hacking ético en entornos de laboratorio, orientadas a comprender vulnerabilidades, evaluar su impacto y proponer medidas de detección y corrección.

## Estado

Primera práctica en curso: escaneo de puertos TCP en Metasploitable Ubuntu. El escaneo inicial está documentado; la identificación de servicios queda pendiente.

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

- [Escaneo TCP SYN e identificación de servicios](02-enumeracion/01-escaneo-puertos-servicios/README.md) — En curso: resultados del escaneo inicial publicados; identificación de servicios pendiente.

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
