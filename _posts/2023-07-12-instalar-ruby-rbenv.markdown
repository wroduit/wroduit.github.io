---
layout: post
title:  "Instalar Ruby com rbenv"
date:   2023-07-12 13:05:00 -0300
categories: [Dev, Ruby]
tags: [linux, environment, config]
---

De acordo com a [documentação oficial](https://www.ruby-lang.org/pt/documentation/installation/#rbenv), o **`rbenv`** permite gerenciar versões instaladas do Ruby. Ele não suporta a instalação do Ruby, mas existe um plugin popular chamado *`ruby-build`* para isso. Ambas ferramentas estão disponíveis para macOS, Linux ou outros sistemas operacionais do tipo UNIX.

Seguindo os passos abaixo instalaremos o *`rbenv`* juntamente com o *`ruby-build`* em uma distribuição Debian like.


```shell
cd $HOME
sudo apt update 
sudo apt install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev libffi-dev

git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source .bashrc

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
source .bashrc

rbenv install 2.3.1         # instala a versão 2.3.1 
rbenv global 2.3.1          # define a versão como "titular"
ruby -v                     # verifica a versão
```

> No exemplo acima está sendo instalada a **versão 2.3.1**. Altere para a versão desejada.
{: .prompt-info }

> Se usa ZSH, substituir o **.bashrc** por **.zshrc** nos comandos. Exemplo:
```shell
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
source .zshrc
```
{: .prompt-tip }



Depois instalar o Bundler...
```shell
gem install bundler
rbenv rehash
````

E atualizar o sistema:
```shell
gem update --system
rbenv rehash
````