---
description: >-
  G4l1l30 write-up on the medium-difficulty Linux machine Ready from
  https://hackthebox.eu
title: Hack the Box - Ready Writeup
date: 2021-05-15 15:00:00 -0600
categories: [Hack the Box, Writeup]
tags: [htb, hacking, hack the box, redteam, Linux, medium, writeup]     # TAG names should always be lowercase
show_image_post: true
image: /assets/img/Ready/InfoCard.png
---

# Summary

![](/assets/img/Ready/InfoCard.png)

Ready es una VM Medium de la plataforma HackTheBox recientemente retirada(aquí fecha), para realizar esta Box, necesitaremos explotar un RCE en GitLab 11.4.7, aprovechar el flag **privileged** en Docker para escapar del mismo.

## Info de la maquina



| VM column  | Detalles     |
| ---------- | ------------ |
| Nombre     | Ready        |
| Dificultad | Medium       |
| Release    | 12/12/2020   |
| OS         | Linux        |
| IP         | 10.10.10.220 |

Editamos ***/etc/hosts***  y agregamos la IP **10.10.10.220** que apunte hacia **ready.htb** 
