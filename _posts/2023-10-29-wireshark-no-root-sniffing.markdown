---
layout: post
title:  "Utilizar Wireshark sem privilégios root (sudo)"
date:   2023-10-29 10:45:00 -0300
categories: [Redes, Infraestrutura]
tags: [linux]
---

<script language="JavaScript" type="text/javascript" src="http://meuip.eu/ip.php"></script>

Às vezes ao instalar o Wireshark no Linux, mesmo permitindo, a possibilidade de capturar pacotes sem utilizar o usuário `root` ou o utilitário `sudo` não funciona.

![Permissão](/assets/img/non-superuser.png)
_Opção que permite usuário comum a capturar pacotes_

Erro que pode acontecer:


![Erro](/assets/img/non-superuser-error.png)
_Erro, mesmo permitindo na instalação_

Para ajustar é simples, basta entrar utilizar os comandos abaixo:

```shell
$ sudo groupadd wireshark
$ sudo adduser $USER wireshark
$ sudo chgrp wireshark /usr/bin/dumpcap
$ sudo chmod 750 /usr/bin/dumpcap
$ sudo setcap cap_net_raw,cap_net_admin=eip /usr/bin/dumpcap
$ sudo getcap /usr/bin/dumpcap
$ sudo reboot
```
> O comando `sudo reboot` irá reiniciar a máquina!
{: .prompt-info }

Depois de reiniciar a máquina podemos ver que o Wireshark já passa a enxergar as interfaces de rede e já se torna possível capturar pacotes com usuário comum.

![Sucesso](/assets/img/wireshark-captures.png)
_Sucesso na captura!_
