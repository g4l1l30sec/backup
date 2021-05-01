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

## Enumeration

### Nmap scan

Apuntamos la IP de la VM 10.10.10.219 hacia sharp.htb en nuestro /etc/hosts

Empiezo mi enum con Nmap  

| `Flag` | Uso |
| :--- | :--- |
| `-p-` | Para escanear todos los puertos.  |
| `-vvv` | Proporciona una salida muy detallada para ver los resultados a medida que se encuentran. |
| `-sC` | Es equivalente a `--script=default` y ejecuta una serie de scripts de enum contra el target |
| `-sV` | Proporciona info de los servicios |


