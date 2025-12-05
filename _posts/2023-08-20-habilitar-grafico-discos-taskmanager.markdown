---
layout: post
title:  "Habilitando discos no Task Manager no Windows Server"
date:   2023-08-20 20:00:00 -0300
categories: [SO, Windows]
tags: [config, powershell, server]
---

Por padrão, no Windows Server, os gráficos de discos não vem habilitados no Task Manager. É uma feature interessante para monitorar a leitura e escrita e a velocidade dos dados nos discos.

![TaskManager](/assets/img/tasknodisk.jpg)
_Task Manager sem discos_

Para habilitar, basta abrir o prompt do `PowerShell` em modo administrador e entrar com o comando:

```powershell
diskperf -y
```
Resultado:

![TaskManager](/assets/img/taskdisk.jpg)
_Task Manager com discos_