# Escaneo de puertos TCP y UDP en Metasploitable Ubuntu

Estado: escaneos TCP/UDP y detección de servicios documentados. Investigación de vulnerabilidades pendiente.

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

## Prueba complementaria: puerto UDP 53

Se realizó una segunda prueba propia sobre el mismo objetivo:

```bash
sudo nmap -sU 192.168.32.130 -p 53
```

`-sU` selecciona un escaneo UDP y `-p 53` limita esta prueba al puerto 53. No es una repetición del escaneo TCP: se evalúa un protocolo diferente.

![Escaneo UDP del puerto 53 en Ubuntu](evidencias/nmap-udp-53-ubuntu.png)

| Dato | Resultado observado |
|---|---|
| Objetivo | 192.168.32.130 |
| Puerto | 53/udp |
| Estado | open\|filtered |
| Etiqueta SERVICE | domain |
| Estado del host | Activo |
| Duración | 4.89 segundos |

Nmap no pudo distinguir entre un puerto UDP abierto y uno filtrado. Este resultado no confirma un servicio DNS activo. La etiqueta `domain` es una asociación habitual del puerto 53, no una identificación verificada del servicio. La captura no determina la causa concreta del estado ambiguo; no se atribuye a un firewall específico.

## Identificación de servicio y versión en 21/TCP

Se ejecutó desde Kali:

```bash
sudo nmap -sV 192.168.32.130 -p 21
```

La opción `-sV` solicita detección de servicios y versiones. `-p 21` limita el análisis al puerto 21.

![Detección de ProFTPD en el puerto 21](evidencias/nmap-servicio-ftp.png)

| Dato | Resultado informado por Nmap |
|---|---|
| Puerto | 21/tcp |
| Estado | open |
| Servicio | ftp |
| Producto y versión | ProFTPD 1.3.5 |
| Información adicional | Service Info: OS: Unix |
| Duración | 15.61 segundos |

En el escaneo SYN inicial, `ftp` era una etiqueta asociada al puerto. Esta segunda prueba identifica mediante detección de servicio el producto ProFTPD y la versión 1.3.5. Se registra como identificación informada por Nmap, no como verificación local del paquete instalado. La indicación Unix procede de la información del servicio; no equivale a una detección completa del sistema operativo.

## Detección de servicios en el escaneo TCP general

Se amplió la identificación con el siguiente comando, sin limitar puertos mediante `-p`:

```bash
sudo nmap -sV 192.168.32.130
```

![Detección de servicios en los puertos TCP abiertos](evidencias/nmap-servicios-tcp.png)

La salida vuelve a mostrar 7 puertos abiertos, 2 cerrados y 991 filtrados sin respuesta. La ejecución tardó 19.67 segundos.

| Puerto TCP abierto | Servicio informado | Producto o versión informados |
|---|---|---|
| 21 | ftp | ProFTPD 1.3.5 |
| 22 | ssh | OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0) |
| 80 | http | Apache httpd 2.4.7 |
| 445 | netbios-ssn | Samba smbd 3.X - 4.X (workgroup: WORKGROUP) |
| 631 | ipp | CUPS 1.7 |
| 3306 | mysql | MySQL (unauthorized) |
| 8080 | http | Jetty 8.1.7.v20120910 |

Los puertos 3000/TCP y 8181/TCP siguen cerrados. No se les atribuyen aplicaciones activas.

### Comparación e incertidumbres

- En 445/TCP, la etiqueta inicial `microsoft-ds` pasa a `netbios-ssn`, con producto Samba. El rango `3.X - 4.X` no identifica una versión exacta.
- En 8080/TCP, la etiqueta inicial `http-proxy` pasa a `http`, con Jetty identificado. La primera etiqueta no confirmaba que fuera un proxy.
- En 3306/TCP, Nmap informa MySQL con `unauthorized`, sin versión. Esto no demuestra acceso a la base de datos ni una vulnerabilidad.
- ProFTPD 1.3.5 coincide con la prueba específica anterior del puerto 21.
- La línea `Service Info` informa Unix/Linux y los nombres `127.0.0.1` y `UBUNTU`. Es información recopilada de los servicios, no una prueba independiente de detección del sistema operativo.

Estas identificaciones remotas orientan la investigación posterior; no verifican por sí solas el estado de parches ni la configuración local.

## Interpretación y siguiente fase

El producto y la versión permiten buscar vulnerabilidades candidatas en fuentes públicas y comparar los requisitos de posibles pruebas de concepto con el laboratorio. La coincidencia de versión, por sí sola, no demuestra una vulnerabilidad explotable: deben verificarse las condiciones relevantes, como configuración, módulos y parches.

Todavía no se ha investigado ni validado una vulnerabilidad concreta en este caso, ni se ha ejecutado un exploit. La investigación y eventual validación en el objetivo propio se documentarán como una fase separada con sus evidencias, impacto y mitigación.

## Continuación pendiente

Quedan pendientes la investigación de vulnerabilidades y, si resulta necesario para ella, precisar la versión de Samba y MySQL. No es necesario asumir versiones que la evidencia no muestra.

La variante con `-v --reason` y exportación XML queda pendiente para la revisión final del portafolio, por decisión del autor.
