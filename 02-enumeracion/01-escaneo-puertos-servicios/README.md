# Escaneo TCP SYN en Metasploitable Ubuntu

Estado: en curso. Escaneo inicial documentado; identificación de servicios pendiente.

## Objetivo y entorno

Identificar estados de puertos TCP del objetivo propio `192.168.32.130` (Metasploitable Ubuntu) desde Kali. Práctica realizada durante la sección de recopilación activa de información del curso de hacking ético.

- Herramienta: Nmap 7.99, según la captura.
- Objetivo: Metasploitable3 Ubuntu 14.04, previamente comprobado mediante ping.
- Red del laboratorio configurada en modo Sólo host.
- Evidencia relacionada: [configuración y conectividad del laboratorio](https://github.com/gonzalo-rinaldi/cybersecurity-homelab/blob/main/docs/conectividad-kali-ubuntu.md).

## Comando ejecutado

```bash
sudo nmap -sS 192.168.32.130
```

La opción `-sS` selecciona el escaneo TCP SYN. El comando no solicita detección de versiones ni escaneo UDP. Tampoco solicita todos los puertos TCP.

![Resultado del escaneo TCP SYN desde Kali](evidencias/nmap-syn-ubuntu.png)

## Resultados observados

El objetivo respondió como activo. Nmap informó 991 puertos TCP filtrados sin respuesta y mostró los siguientes nueve puertos:

| Puerto TCP | Estado | Etiqueta SERVICE mostrada, sin confirmar |
|---|---|---|
| 21 | open | ftp |
| 22 | open | ssh |
| 80 | open | http |
| 445 | open | microsoft-ds |
| 631 | open | ipp |
| 3000 | closed | ppp |
| 3306 | open | mysql |
| 8080 | open | http-proxy |
| 8181 | closed | intermapper |

Balance de esta ejecución: 7 puertos abiertos, 2 cerrados y 991 filtrados, sobre 1000 puertos TCP evaluados. Duración mostrada: 9.38 segundos.

## Interpretación propia

La columna `SERVICE` no garantiza que el servicio real coincida con el nombre mostrado. En este escaneo inicial las etiquetas se basan en la asociación habitual del número de puerto; no se identificó todavía el software ni su versión mediante sondeos de servicio.

- `open`: el puerto respondió de forma compatible con un puerto TCP abierto durante la prueba.
- `closed`: el puerto respondió como cerrado; su etiqueta no indica que haya un servicio ejecutándose.
- `filtered`: Nmap no pudo determinar si estaba abierto o cerrado. En esta captura se informa ausencia de respuesta; no se identificó la causa concreta.

Un puerto abierto no constituye por sí mismo una vulnerabilidad. El resultado describe lo observado desde Kali en ese momento.

## Continuación pendiente

Se incorporará la siguiente práctica del curso para identificar los servicios y comparar sus resultados con estas etiquetas. Todavía no se han aportado evidencias de detección de versiones, vulnerabilidades, correcciones ni detecciones defensivas para este caso.
