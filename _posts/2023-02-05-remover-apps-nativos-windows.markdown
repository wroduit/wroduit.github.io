---
layout: post
title:  "Desinstalar Apps nativos do Windows"
date:   2023-01-05 09:00:00 -0300
categories: [SO, Windows]
tags: [config, powershell, bloatware]
image:
  path: /assets/img/3-powershell-cim1.jpg
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: PowerShell
---
Executar no powershell como administrador.

Sintaxe do comando:


```powershell
Get-AppxPackage *nomedoapp* | Remove-AppxPackage
```
Desinstalar todos os apps, exceto a loja:

```powershell
Get-AppxPackage | where-object {$_.name –notlike "*store*"} | Remove-AppxPackage
```
O que eu costumo remover:

```powershell
Get-AppxPackage *appconnector* | Remove-AppxPackage
Get-AppxPackage *feedback* | Remove-AppxPackage
Get-AppxPackage *gethelp* | Remove-AppxPackage
Get-AppxPackage *getstarted* | Remove-AppxPackage
Get-AppxPackage *messaging* | Remove-AppxPackage
Get-AppxPackage *3d* | Remove-AppxPackage
Get-AppxPackage *appinstaller* | Remove-AppxPackage
Get-AppxPackage *onenote* | Remove-AppxPackage
Get-AppxPackage *xboxapp* | Remove-AppxPackage
Get-AppxPackage *xboxspeech* | Remove-AppxPackage
Get-AppxPackage *microsoft.xboxgamingoverlay* | Remove-AppxPackage
Get-AppxPackage *people* | Remove-AppxPackage
Get-AppxPackage *windowscommunicationsapps* | Remove-AppxPackage
Get-AppxPackage *microsoft.yourphone* | Remove-AppxPackage
```