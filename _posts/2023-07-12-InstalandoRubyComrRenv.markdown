---
layout: post
title:  "Instalar Ruby com rbenv"
date:   2023-07-12 13:05:00 -0300
categories: Programação Ruby
#pin: true
tags: linux dicas
---

Instalando o Ruby via rbenv

```shell
cd $HOME
sudo apt-get update 
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev libffi-dev

git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source .bashrc

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
source .bashrc

rbenv install 2.3.1
rbenv global 2.3.1
ruby -v
```

> Se usa ZSH, substituir o ./bashrc por ./zshrc
{: .prompt-tip }

Depois instalar o Bundler:
```shell
gem install bundler
rbenv rehash
````