---
description: >-
  G4l1l30 write-up on the hard-difficulty Linux machine Sharp from
  https://hackthebox.eu
title: Hack the Box - Sharp Writeup
date: 2021-05-1 15:40:00 -0600
categories: [Hack the Box, Writeup]
tags: [htb, hacking, hack the box, redteam, windows,ysoserial, hard, writeup, kaban, dnsspy, remoting_service, smb, wcf]     # TAG names should always be lowercase
show_image_post: true
image: /assets/img/Linux/Sharp/01-Sharp-infocard.png
---

## HTB - Sharp

## Overview

![](/assets/img/Linux/Sharp/01-Sharp-infocard.png)

Esta es una VM Hard de HackTheBox retirada en la 1ra semana de Mayo 2021.

## Escaneo del target

### Nmap scan

Apuntamos la IP de la VM 10.10.10.219 hacia sharp.htb en nuestro /etc/hosts

Empiezo mi scan con Nmap  

| `Flag` | Uso |
| :--- | :--- |
| `-p-` | Para escanear todos los puertos.  |
| `-vvv` | Proporciona una salida muy detallada para ver los resultados a medida que se encuentran. |
| `-sC` | Es equivalente a `--script=default` y ejecuta una serie de scripts de enum contra el target |
| `-sV` | Proporciona info de los servicios |
 
 

```bash
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-05-01 21:10 BST
Nmap scan report for sharp.htb (10.10.10.219)
Host is up (0.35s latency).
Not shown: 65529 filtered ports
PORT     STATE SERVICE            VERSION
135/tcp  open  msrpc              Microsoft Windows RPC
139/tcp  open  netbios-ssn        Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
5985/tcp open  http               Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
8888/tcp open  storagecraft-image StorageCraft Image Manager
8889/tcp open  mc-nmf             .NET Message Framing
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -56m07s
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-05-01T19:24:05
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 603.90 seconds
```
Acostumbro a empezar por los puertos que me resultan mas familiar :^)

#### SMB Enum.

Empezamos por SMB utilizando `smbmap -H sharp.htb` y obtenemos lo siguiente: 

![](/assets/img/Linux/Sharp/smb_01.png)

Tenemos permiso de lectura en el directorio Kaban, podemos acceder al mismo utilizando el el parametro -R

`smbmap -H sharp.htb -R`

![](/assets/img/Linux/Sharp/smb_02.png)

Muchos ficheros ¿no?, vamos a obtenerlos todo con `smbget` de la siguiente forma : `smbget -R smb://sharp.htb/kanban`

![](/assets/img/Linux/Sharp/smb_03.png)

### Kanban

Utilizaremos `ack` para buscar strings que sean de nuestro interes (podemos hacer lo mismo con grep), el uso quedaria asi : `ack -i "password"`

![](/assets/img/Linux/Sharp/kaban_01.png)

Nice :), echemos un vistazo a `PortableKanban.pk3` mas detalladamente y encontraremos dos usuarios : Administrator y Lars.

```text
Administrator
ID: e8e29158d70d44b1a1ba4949d52790a0
Encrypted Password: "k+iUoOvQYG98PuhhRC7/rg=="

Lars
ID: 0628ae1de5234b81ae65c246dd2b4a21
Encrypted Password: "Ua3LyPFM175GN8D3+tqwLA=="
```
Despues de estar estancado un rato, el manual del usuario "User Guide.pdf" es nuestro fichero ideal :)

En la pagina 18 podemos destacar dos cosas importantes: 1. El password del administrador(por defecto) es en blanco y si olvidamos el password, solo movemos el programa (que por cierto, es portable :) ) a otro directorio.

![](/assets/img/Linux/Sharp/kaban_02.png)

Interesante, indagando en el documento en la pagina 20, nos damos cuenta que los password se ocultan por defecto en `Setup/Users tab`

![](/assets/img/Linux/Sharp/kaban_03.png)

Necesitamos una VM con Windows, pasamos los archivos de Kanban ya descargados.



