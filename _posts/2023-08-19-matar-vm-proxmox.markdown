---
layout: post
title:  "Matar VM no Proxmox"
date:   2023-08-19 18:30:00 -0300
categories: [Linux, Proxmox]
tags: [virtualização]
---


Algo aconteceu no processo de instalação da VM e você precisou forçar o shutdown, mas nada acontece e o status da VM fica igual ao da imagem abaixo e não consegue fazer mais nada? É possível parar a VM via CLI.

![T-568A](/assets/img/vm-nao-desliga.png)
_VM não desliga no Proxmox_

Precisamos conhecer o ID da VM e acessar shell do PVE e entrar com o seguinte comando (no exemplo é a VM com ID 101):

```shell
qm stop 101
```
Após executar o comando a VM desligará e liberará para alterar as configurações necessárias.
