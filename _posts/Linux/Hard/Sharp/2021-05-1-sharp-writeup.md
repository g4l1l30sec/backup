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

Empiezo mi enum con Nmap  

| `Flag` | Uso |
| :--- | :--- |
| `-p-` | Para escanear todos los puertos.  |
| `-vvv` | Proporciona una salida muy detallada para ver los resultados a medida que se encuentran. |
| `-sC` | Es equivalente a `--script=default` y ejecuta una serie de scripts de enum contra el target |
| `-sV` | Proporciona info de los servicios |

Acostumbro a empezar por los puertos que me resultan mas familiar :^) 

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
#### SMB Enum.

Empezamos por SMB utilizando `smbmap -H sharp.htb` y obtenemos lo siguiente: 

![](/assets/img/Linux/Sharp/smb_01.png)
