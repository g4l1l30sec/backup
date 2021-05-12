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
