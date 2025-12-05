---
layout: post
title:  "O WinRAR e a pirataria"
date:   2023-07-29 17:00:00 -0300
categories: [Windows, Utilitários]
tags: [software]
---

# Todo mundo sabe que todo mundo já usou software pirata

Mas nem todo mundo sabe que existe um semelhante grátis para quase todo software pago; portanto é perfeitamente possível evitar a pirataria. Esse assunto abre tangentes de pensamentos e pisa em alguns terrenos de filosofia melindrosa sobre software livre e ética. Será que não é imoral ganhar dinheiro usando software pirata? Fica a reflexão.

Não uso mais software pirata há anos. A última lembrança que tenho de rodar um keygen no meu PC é de 2016. Desde essa época tenho encarado de forma diferente o relacionamento com minha área de atuação (TI) e gosto de pensar que não é só o meu tempo/trabalho que vale alguma coisa. Hoje compro aplicativos e assino alguns serviços, mas não sou o íntegro dessa equação. Como disse no início do parágrafo, não uso mais software pirata, mas tenho alguns dos quais não paguei. Também acho um pouco imoral, mas todos somos moderadamente hipócritas, não é mesmo? Não é difícil dar um google e encontrar chaves de ativação dos mais variados softwares, assim possibilitando instalar o software totalmente original sem pagar por ele.

# O WinRAR

O WinRAR é engraçado. Não é grátis, mas ao mesmo tempo é. Você instala e usa ele em sua totalidade por alguns dias, até que um aviso começa a brotar na tela. A cortesia acabou. Mas é só fechar o alerta e seguir o jogo… Todas as funcionalidades permanecem. Pois bem, ainda assim há quem se incomode de tal maneira com o aviso que precisa piratear. Eu penso “puts, essa gente deve usar muito o WinRAR pra esse aviso virar um problema!”. Já vi esse tipo e admito, já fiz o mesmo lá nos anos 2000. Hoje uso o [7-Zip](https://www.7-zip.org/), que considero melhor, mais completo e é open-source (ou seja, totalmente gratuito).

Mas se você não abre mão do bom e velho WinRAR e não quer o aviso, vamos à solução.

## Instalação do WinRAR

Não tem erro. Acesse o site, baixe o instalador e instale no Windows. Não importa a versão, não importa o idioma.

## Ativação do WinRAR

Não será usado nenhum keygen e nenhum crack. Abra o **Bloco de notas** em **`modo administrador`** e cole o seguinte conteúdo:

```plaintext
RAR registration data
WinRAR
Unlimited Company License
UID=4b914fb772c8376bd87d
6412212250d87d9866ad12eb9f900ed7d7e188202a9fa9b82a3338
975de352c447ddb7f3a860fce6cb5ffde62890079861be57638717
7131ced835ed65cc743d9777f2ea71a8e32c7e593cf66794343565
b41bcf56929486b8bcdac33d50ecf773996045fd75874651c6978c
51c8cc27fc9d4066fd160eedf53540db55a7033771aa5d7c51d35e
661121f949cfd6a07b6fa5389e79fe7f0503b10704621ade60e40a
d679c8255cbc8336f8e23c4b3f478a52561b8633b4601362349773
```
Use a opção **`Salvar como`** e navegue até a pasta de instalação padrão do WinRAR. Normalmente localizado em `C:\Program Files\WinRAR`{: .filepath} e salve com o nome `rarreg.key`.

Após salvar o arquivo abra o WinRAR e vá no `Sobre` para ver o software devidamente registrado.

![WinRAR](/assets/img/winrar.png)
_WinRAR registrado._


> Como pode ser visto na imagem acima, a licença aplicada é uma **licença ilimitada** do próprio WinRAR. Esse código circula na internet há muitos anos e está funcional até hoje. Talvez o povo do WinRAR nem se dê ao trabalho de derrubar, pois o software funciona de qualquer jeito, sendo licenciado ou não.
{: .prompt-info }