# Enumeración de Metasploitable Windows

Estado: escaneo dirigido a 139/TCP y 445/TCP documentado; enumeración SMB y SNMP pendiente.

## Objetivo y entorno

Comprobar los puertos asociados habitualmente a SMB en el objetivo propio Metasploitable Windows (`192.168.32.132`), desde Kali con Nmap 7.99. El laboratorio está configurado en modo Sólo host.

La [conectividad ICMP](https://github.com/gonzalo-rinaldi/cybersecurity-homelab/blob/main/docs/conectividad-kali-windows.md) se verificó previamente con seis respuestas y ninguna pérdida.

## Comando ejecutado

```bash
sudo nmap -v -sS -p 139,445 192.168.32.132
```

- `-v`: muestra el progreso con mayor detalle.
- `-sS`: selecciona escaneo TCP SYN.
- `-p 139,445`: limita la prueba a esos dos puertos; la p es minúscula.

![Escaneo dirigido a los puertos 139 y 445](evidencias/nmap-smb-puertos.png)

## Resultados observados

| Puerto | Estado | Etiqueta SERVICE |
|---|---|---|
| 139/tcp | open | netbios-ssn |
| 445/tcp | open | microsoft-ds |

La salida confirma que se escanearon únicamente dos puertos. El objetivo está activo y la duración total informada es de 5.70 segundos.

## Interpretación y límites

Ambos puertos están abiertos desde la perspectiva de Kali. El resultado permite continuar con la enumeración SMB, pero todavía no identifica versiones del protocolo, usuarios, recursos compartidos ni permisos. Un puerto abierto no demuestra una vulnerabilidad.

No se utilizó `-sV`; las etiquetas SERVICE son asociaciones habituales de los puertos y no una identificación confirmada del software que responde.

## Exploración local de scripts NSE relacionados con SMB

Se navegó al directorio de scripts de Nmap y se listaron los archivos cuyo nombre comienza con `smb`:

```bash
cd /usr/share/nmap/scripts
ls smb*
```

![Acceso al directorio de scripts](evidencias/nse-directorio.png)

![Listado de scripts SMB y SMB2](evidencias/nse-listado-smb.png)

El listado incluye scripts como `smb-enum-shares.nse`, `smb-enum-users.nse`, `smb-os-discovery.nse`, `smb-protocols.nse`, `smb2-security-mode.nse` y otros orientados a comprobaciones de vulnerabilidades o acciones más intrusivas.

NSE (Nmap Scripting Engine) permite automatizar tareas de descubrimiento, enumeración y detección de vulnerabilidades; algunos scripts también implementan explotación. No todos los scripts SMB realizan la misma tarea y comprobar una vulnerabilidad no equivale necesariamente a explotarla. Referencia técnica: [documentación oficial de NSE](https://nmap.org/book/nse.html).

Estos comandos únicamente inspeccionan archivos locales: no ejecutan scripts contra Windows ni demuestran vulnerabilidades del objetivo. La enumeración remota sigue pendiente. Antes de usar un script se revisará su función y sus requisitos; no se ejecutará indiscriminadamente todo el conjunto mostrado.

## Pendientes

- Incorporar la enumeración SMB con su comando y resultados.
- Evaluar SNMP mediante una prueba específica: este escaneo TCP no verifica su disponibilidad por UDP.
