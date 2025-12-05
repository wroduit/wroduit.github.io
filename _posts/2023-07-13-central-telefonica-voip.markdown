---
layout: post
title: "Central Telefônica VoIP"
date: 2023-07-13 21:00:00 -0300
categories: [Docs, Artigos]
tags: [linux, voip, config, tcc]
---

Em 2011 ingressei em um curso técnico de informática no *campus* do Instituto Federal da minha cidade. Foi o início da jornada profissional no TI. Posto aqui meu artigo de conclusão de curso.

> O conteúdo está na íntegra. Tentei moldar conforme as normas ABNT exigidas na época, mas o `markdown` tem algumas limitações que impedem a formatação.
{: .prompt-info }

___

# <center>CENTRAL TELEFÔNICA VOIP</center>

William Roduit [^1]  
Marcelo Rios Kwecko [^2]

## RESUMO

<div style="text-align: justify">

Este trabalho apresenta a implementação de uma central telefônica VoIP (voz sobre Protocolo de Internet) com suporte PABX. Na implantação do sistema, foram utilizados os recursos livres oferecidos pelo software Asterisk, que é uma ferramenta de código aberto (Open Source), capaz de implementar, por meio de software, os recursos convencionais de um PABX. O principal objetivo do trabalho consiste em mostrar, através da simulação de um ambiente corporativo, as vantagens oferecidas pela tecnologia VoIP em relação às opções disponíveis na telefonia tradicional, visando à redução de custos. Sendo a voz o principal e mais primitivo meio de comunicação da humanidade, é natural o progresso tecnológico que envolve o meio
de comunicação em questão. Através do áudio é possível expressar emoções e sentimentos, tornando a telefonia, por consequência, um dos maiores e mais eficientes meios de comunicação globalizados. Com o progresso da tecnologia e o advento da internet, houve a evolução de vários serviços, dentre eles, destacam-se os meios físicos propriamente ditos. A possibilidade de utilização de um mesmo cabo, por exemplo, para transmitir dados de telefonia e internet reflete diretamente um novo conceito tecnológico chamado de redes convergentes. A tecnologia VoIP deriva dessa tendência, que tem por objetivo, e maior desafio, interligar diversos serviços utilizando para isso um meio, ou seja, usar a mesma infraestrutura para vários serviços diferentes. No desenvolvimento deste trabalho foi realizada a configuração dos elementos necessários para demonstrar o funcionamento de uma central telefônica VoIP, assim como a implementação dos recursos que englobam o ambiente corporativo simulado. Com o servidor VoIP em funcionamento, percebeu-se a vantagem que o sistema proporciona em relação ao custo e à manutenção, pois aproveita a infraestrutura existente, tornando possível para as corporações integrar um sistema de telefonia alternativo e de semelhante qualidade à telefonia tradicional.</div>  
---
**Palavras-chave:** VoIP; Asterisk; Central Telefônica; PABX.

## ABSTRACT

<div style="text-align: justify">
This study presents the implementation of a telephone exchange VoIP (Voice over Internet Protocol) with PABX support. In order to implement the system, open resources offered by the Asterisk software were used. Asterisk is an open source tool
that is able to implement the required resources of a PABX. The main objective of this study is to show, by simulating a corporate environment, the advantages of VoIP technology in relation to the other options available in traditional telephony, with the purpose of reducing costs. The voice is the main and the most primitive means of communication and it seems natural that the technological progress involves it.
Through audio it is possible to express emotions and feelings and because of that the telephone is one of the biggest and most efficient means of communication in this globalized world. With the progress of technology and the advent of the internet, many services evolved and among them stand the physical media. The possibility of using a single cable, for example, to transmit data and internet telephony directly reflects a new technological concept called converged networks. The VoIP technology comes from this trend and its objective is to connect various services using this means, that is, to use the same infrastructure for different services. For this study, the configuration of the elements required to demonstrate the operation of a
VoIP telephone exchange was performed. Besides that, resources that that comprise the simulated corporate environment were implemented. With the VoIP server running, the advantage that the system presents was realized. It was noticed that this advantage has to do with cost and with maintenance because it takes advantage of the existing infrastructure, making it possible for corporations to integrate an alternative telephony system with good quality to traditional telephony.</div>  
___

**Key words:** VoIP; Asterisk; Telephone Exchange; PABX.

## INTRODUÇÃO

<div style="text-align: justify">
&emsp;&emsp;Nos dias atuais, a comunicação se tornou o principal meio de integração entre as pessoas em diversas atividades, tanto profissionais como pessoais. Através dela, é possível a troca mútua de experiências, fazendo da voz a principal e mais importante ferramenta utilizada no desenvolvimento da comunicação global, pois expressa os sentimentos e o estado de espírito de quem fala. As novas tecnologias proporcionaram uma maior integração entre as nações, uma vez que, através dos meios de comunicação, sofisticaram a forma como que as pessoas se correspondiam.</div>  
<div style="text-align: justify">
&emsp;&emsp;O início desse processo teve a participação ativa da telefonia, porque, através desta, revolucionou-se a forma como a informação era processada e o meio em que a mesma era transmitida, mostrando assim, através da evolução, a importância da comunicação em um meio social.</div>
<div style="text-align: justify">
&emsp;&emsp;Centrais telefônicas fazem parte da vida cotidiana dos cidadãos há um tempo considerável. Diretamente ou não, todas as corporações utilizam serviços de direcionamento de voz fornecidos por empresas de telecomunicações. Redes corporativas geralmente possuem vários pontos ramificados da linha externa de telefonia, que são denominados ramais. Estes, independente se partem ou não de uma linha digital (linhas especiais que contém uma variedade de ramais), são gerenciados por uma central denominada PABX (Private Automatic Branch Exchange), que é responsável pela troca automática dos ramais privados. Para este fim, existe também a opção do gerenciamento através de uma central VoIP (Voz sobre Protocolo de Internet), que consiste em uma tecnologia que utiliza o protocolo TCP/IP para transportar a voz digitalizada em pacotes e enviar os dados através de uma rede local, com a possibilidade de transmissão pela internet. Assim sendo, com o intuito de aproveitar a infraestrutura já estabelecida e reduzir custos com linhas analógicas, centrais telefônicas VoIP com suporte PABX são ótimas alternativas para ambientes corporativos, tanto em empresas de médio como também de grande porte. Diante deste cenário, o objetivo deste trabalho é implementar, configurar e gerenciar uma central telefônica VoIP que seja compatível com entroncamento PABX e que proporcione a perfeita compatibilidade entre as linhas internas analógicas e digitais.</div>

## 1 REFERENCIAL TEÓRICO

### 1.1 A tecnologia VoIP

<div style="text-align: justify">
&emsp;&emsp;Por consequência do crescimento da Internet, algumas tecnologias recentes vêm substituindo outras já existentes, como o VoIP, por exemplo. Para Keller (2011, p. 19), a tecnologia possibilita a realização de chamadas telefônicas através de conexões banda larga e redes internas, independentemente dos serviços de telefonia convencionais.</div>
<div style="text-align: justify">
&emsp;&emsp;Segundo os autores: Davidson, Peters, Bathia, Kalidindi e Mukherjee (2007, p. 396), “a Voz sobre IP (VoIP) tornou-se um importante fator nas redes de comunicação, prometendo custos operacionais mais baixos, maior flexibilidade e uma variedade de aplicações avançadas”.</div>  
<div style="text-align: justify">
&emsp;&emsp;A tecnologia VoIP traz alguns benefícios específicos, principalmente no que diz respeito ao custo, porém, como afirma Gonçalves (2005, p. 99), este não deve ser o único a ser observado:</div>

> <font size="2"><div style="text-align: justify"> O benefício chave do VoIP é combinar redes de voz e dados para reduzir
custos. Se você olhar estritamente em custo por minuto, a economia com
VoIP pode não ser suficiente para justificar o investimento neste tipo deserviço. Em alguns países onde o custo de uma ligação telefônica pode
chegar a um dólar por minuto, certamente é justificável. Em outros lugares
onde os custos de telecomunicações estão caindo dia-a-dia, isto pode não
ser suficiente. Entretanto existem outros benefícios associados ao VoIP,
como o uso de uma única infra-estrutura, adição, mudança e remoção de
pontos são mais simples do que em telefonia tradicional, até porque o
número do telefone passa a ser uma configuração da linha e não do
telefone. Algumas pessoas têm dito que escolheram telefonia IP usando
Asterisk pela liberdade de fazer as configurações elas mesmas sem ter de
depender de um serviço externo, o que é comum com centrais telefônicas
tradicionais. (GONÇALVES, 2005, p. 99)<div>

<div style="text-align: justify">
&emsp;&emsp;De acordo com Keller (2011, p. 19), o VoIP é considerado um protocolo de redes composto de normas e regras que visam o tráfego da voz através de dados pelo protocolo TC/IP (Transmission Control Protocol). Dessa forma, a voz é emitida pela origem e dividida em pacotes. Quando esses pacotes chegam ao destino, são reorganizados para reconstruir em voz os dados que o emitente recebeu através da conexão. Ou seja, como afirma Davidson (2007, p. 24), o VoIP possibilita a quebra da voz em pequenos pedaços (denominados como amostras) e coloca os mesmos dentro de um pacote IP.</div>  
<div style="text-align: justify">
&emsp;&emsp;Com a constante evolução da tecnologia, surgiu um novo conceito denominado redes convergentes, que tem como maior objetivo e desafio unir, em um número reduzido de infraestrutura, os mais diversos serviços, ou seja, unir em um único meio mais de uma possibilidade de comunicação, como sugere o autor:</div>

> <font size="2"><div style="text-align: justify">O VoIP trouxe diversas novas possibilidades para a comunicação moderna. A principal diferença entre o VoIP e a telefonia como conhecemos tradicionalmente é a forma como a voz é transportada. O protocolo Internet, usado normalmente para enviar e receber e-mails, navegar entre websites, agora está sendo usado também para transportar a nossa voz. (KELLER, 2011, p. 20)</div>

<div style="text-align: justify">
&emsp;&emsp;Ainda baseando-se na afirmação do mesmo autor, é possível dizer que as grandes corporações estão cada vez mais utilizando o VoIP para reduzir os custos das contas telefônicas. Por consequência disso, está ocorrendo, de forma gradativa, a convergência das redes de dados com as redes de telefonia. Isso ocorre devido à substituição das redes baseadas em circuitos TDM (Time Division Multiplexing – Multiplexação por divisão de tempo), por redes com base em pacotes.</div>

### 1.2 Codecs

<div style="text-align: justify">
&emsp;&emsp;A tecnologia VoIP digitaliza a voz, que nada mais é que o som analógico, através de codificadores-decodificadores chamados de codecs. Estes, em grande maioria, são livres e de uso irrestrito, todavia, há alguns, como o G.723.1 e G.729ª, que necessitam de licença para serem implementados. Outros, como o ILBC, por exemplo, não exigem licença de uso, mas os desenvolvedores devem ser contatados em caso de uso comercial.</div>    
<div style="text-align: justify">
&emsp;&emsp;Todos os equipamentos e serviços VoIP possuem suporte a mais de um tipo de codec. Os codecs estão ligados intimamente à qualidade do áudio na chamada. Por exemplo, o codec G.711 tem o payload de 64 Kb porque utiliza 64 Kbps de banda, ou seja, cada pacote transmitido terá 64 Kb reservado à transmissão do áudio digitalizado na chamada. (KELLER, 2011)</div>   
<div style="text-align: justify">
&emsp;&emsp;Outro ponto importante sobre os codecs, segundo Keller (2011), é a capacidade de processamento que cada um demanda. O codec G.711 é o que necessita menor capacidade de processamento, pois não faz uso de compressão da voz. Outro exemplo é o codec G.729ª, que possui payload de 8Kb, mas este necessita de grande processamento, pois é o codec com maior taxa de compressão, chegando a comprimir em até oito vezes o áudio.</div>   
<div style="text-align: justify">
&emsp;&emsp;É possível o gerenciamento e a escolha dos codecs utilizados, como afirma Keller (2011, p. 22):</div>  

> <font size="2"><div style="text-align: justify">Ao utilizar o VoIP, você deve escolher qual Codec será utilizado na comunicação. Essa escolha deve ter como base algumas premissas do seu ambiente, como: tamanho de banda disponível, capacidade de processamento necessária para realizar a digitalização da voz, quantidade de chamadas simultâneas a ser executada, entre outras não menos importantes.</div>

<div style="text-align: justify">
&emsp;&emsp;O mesmo autor ainda afirma que as características principais dos Codecs são:</div>  
* Taxa de bits: quantidade de bits por segundo (Kbps) que precisa ser transmitida.
* Intervalo de amostra: intervalo em tempo (ms) em que o codec opera na codificação.
* Tamanho de amostra: quantidade de bytes capturada em cada intervalo de amostra.
* Tamanho de Payload de Voz: quantidade de bytes preenchida em um pacote de dados. Quanto maior o payload, menor a quantidade de pacotes a ser transmitida e, portanto, maior a quantidade de áudio necessária para compor cada pacote. Maiores valores de payload geram lags e delays, pois quanto maior o pacote, maior o tempo para chegar ao destino.

<div style="text-align: justify">
&emsp;&emsp;Uma boa gerencia dos ramais em relação aos codecs é fundamental para que haja qualidade nas chamadas. Como citado abaixo, o ideal seria a implementação do mesmo codec para todos os ramais:</div>  

> <font size="2"><div style="text-align: justify">O processo de conversão de um Codec em outro, por exemplo, de G.729ª para G.711, é chamado de transcodificação, que causará o aumento no delay e consequentemente na latência, podendo prejudicar a qualidade do áudio da chamada. A situação ideal é que todos os ramais do seu ambiente possuam a mesma implementação de Codec. (KELLER, 2011, p. 24)</div>

#### 1.2.1 Relação codec x qualidade

<div style="text-align: justify">
&emsp;&emsp;Além das principais características dos codecs, o mesmo autor ainda evidencia a qualidade do áudio e aponta alguns elementos considerados críticos, como:</div>  
* Perda de pacotes: geralmente é causada pelos roteadores. Não pode exceder 5% a fim de não deteriorar a qualidade da chamada.
* Delay: tempo decorrido entre a emissão e a recepção da voz. Está ligado à latência, pois demora na recepção dos pacotes d causa o delay.
* Latência: tempo decorrido entre a emissão e a recepção dos pacotes na rede.
* Jitter: é a variação da latência. Devido a certas circunstâncias, o tempo de tráfego dos pacotes é diferente, e essa diferença pode causar distorção no áudio e até mesmo a “queda” da chamada.
* Eco: diversos fatores podem causar eco devido ao delay na rede: codec, transcodificação dos codecs, roteadores, switches, velocidade de banda, etc.
* Supressão de silêncio – Voice Activity Detection (VAD): método aplicado para identificação da ausência de som. Torna o uso da banda mais inteligente, pois, ao identificar a ausência de som, não transmite pacotes. 
* Mean Opinion Score (MOS): “padrão numérico definido pelo International Telecommunication Union (ITU-T), para mensurar e reportar a qualidade da voz. Os valores de MOS estão em uma faixa de 1 (ruim) a 5 (excelente). Esses valores são alcançados de forma subjetiva, de modo que um grupo de ouvintes é submetido a exemplos de áudio e atribui uma nota para cada exemplo”.
* Quality of Service: permite a alocação de prioridade para o pacote de voz, minimizando a sua perda (packet loss) e garantindo, assim, a qualidade do áudio dentro da rede local.

### 1.3 Protocolos

<div style="text-align: justify">
&emsp;&emsp;Toda tecnologia utilizada na arquitetura TCP/IP necessita de um protocolo, que é a linguagem que gerencia a sintaxe, a semântica e a sincronização da conexão, comunicação ou transferência dos dados entre sistemas computacionais. No caso do VoIP não é diferente, por isso existem alguns protocolos de comunicação específicos para garantir o sucesso da comunicação. Dentre eles, existem dois que são usados com mais frequência: SIP e H.323. Ambos possuem a mesma funcionalidade, permitindo a comunicação multimídia ao usuário final e, segundo o autor,</div>  

><font size="2"><div style="text-align: justify"> O transporte da mídia entre os participantes da comunicação é feito por um protocolo específico chamado Real-time Transport Protocol (RTP), responsável pela negociação dos formatos da mídia a ser transferida. (KELLER, 2011, p. 27)</div>

### 1.4 Asterisk

<div style="text-align: justify">
&emsp;&emsp;O Asterisk tem o conceito de ser uma ferramenta open-source capaz de implementar em software os recursos de um PABX convencional. Foi criado e desenvolvido por Mark Spencer, no ano de 1999.</div>  
<div style="text-align: justify">
&emsp;&emsp;De acordo com Roncaglia (2009),</div>  

><font size="2"><div style="text-align: justify"> Mark resolveu montar um negócio de suporte técnico para Linux. Como toda empresa em seu início, sua verba era limitada e insuficiente para comprar uma ferramenta crucial à sua operação: um sistema de PBX. Como já era um desenvolvedor open source, foi autor do GAIM, programa de mensagens instantâneas, entre outros.
Mark publicou seu trabalho e uma comunidade começou a se formar em torno dele. O programa foi batizado de Asterisk, e em pouco tempo já possuía recursos que eram encontrados somente em aparelhos caros de PBX.
Notando que o mercado carecia do hardware necessário para aplicar o sistema efetivamente, Mark montou um negócio para fabricar estas placas e aparelhos. A empresa se chama Digium e se dedica a vender hardware e suporte, para bancar o desenvolvimento do Asterisk, que continua com o código aberto, mudando o rumo de sua empresa de suporte técnico apenas para provedora de soluções em telefonia.</div>  
<div style="text-align: justify">
&emsp;&emsp;O software Asterisk, na sua estrutura, para melhor entendimento, pode ser comparado a outros servidores de recursos, como, por exemplo, o Bind (servidor DNS) e o Apache (servidor de e-mail). Ainda segundo Roncaglia, referindo-se ao Asterisk, “[...] ele embarcou na crescente onda de Voz sobre IP (VoIP) em grande estilo, como fornecedor de uma solução que equivale ao que o Apache foi para a expansão dos servidores na internet.” </div>  
<div style="text-align: justify">
&emsp;&emsp;Portanto, segundo as definições correlacionadas do autor referido acima, é possível atribuir a seguinte definição ao software, de acordo com a definição exposta por Gonçalves (2005, p. 1):</div>  

><font size="2"><div style="text-align: justify"> O Asterisk é um software da PABX que usa o conceito de software livre (GPL), criado pela Digium Inc. e uma base de usuários em contínuo crescimento. A Digium investe em ambos, o desenvolvimento do código fonte do Asterisk e em hardware de telefonia de baixo custo que funciona com o Asterisk. O Asterisk roda em plataforma Linux e outras plataformas Unix com ou sem hardware conectando a rede pública de telefonia, PSTN (Public Service Telephony Network).</div>

#### 1.4.1 O protocolo IAX

<div style="text-align: justify">
&emsp;&emsp;Com o surgimento do Asterisk, foi elaborado um protocolo próprio, o IAX (Inter-Asterisk eXchange), para comunicação direta entre conexões entre servidores Asterisk. Atualmente, o protocolo está na versão 2 (IAX2) e já é utilizado em softphones, ATAs e gateways (Keller, 2011).</div>

| Protocolo | Características |
| --------: | --------------- |
|    SIP       | Aberto e padronizado pela IETF (rfc3261).                 |
|           | Forte adoção pelo mercado.                |
|           | Por utilizar duas portas de comunicação, uma para sinalização (UDP 5060) e outra para o tráfego da mídia (RTP), o SIP apresenta algumas dificuldades e problemas na sua configuração quando há Network Address Translator (NAT) envolvido.                |
|           |                 |
|  IAX2         | Aberto e padronizado pela IETF em fevereiro de 2010 (rfc5456).                |
|           | Ainda tem pouca adoção pelo mercado.                |
|           | Utiliza uma porta única (UDP 4569), tanto para a sinalização quanto para o tráfego de mídia, eliminando qualquer problema existente na comunicação, no caso de haver NAT envolvido.                |
|           | Em modo TRUNK, utilizado apenas para a comunicação entre servidores, faz a multiplexação do áudio das chamadas, utilizando assim significativamente menos banda para o transporte do áudio de um servidor para outro.              |

<div style="text-align: center">Tabela 1 - Resumo dos protocolos SIP e IAX2. (KELLER, 2011, p. 27)</div>

<div style="text-align: justify">
&emsp;&emsp;A figura a seguir ilustra um cenário que utiliza o protocolo IAX2 em um tronco[^3] que interliga dois servidores Asterisk, além de ilustrar o protocolo SIP utilizado nos ramais internos.</div>  
![Figura 1](/assets/img/asterisx.jpg)
_Figura 1 – Exemplo de utilização dos protocolos IAX2 e SIP._

## 2 METODOLOGIA

### 2.1 Recursos
<div style="text-align: justify">
&emsp;&emsp;Tendo como base a bibliografia específica e a revisão de literatura, foram definidos os meios necessários para a implementação do trabalho, sendo utilizados os seguintes recursos na simulação do cenário que compreende o ambiente corporativo:</div>  
* servidor equipado com placa de rede;
* placa VoIP com portas FXS1 e FXO2 (Figura 2);
* aparelhos telefônicos analógicos e softphones equipados com headsets.  

![Figura 2](/assets/img/placa-voip.jpg)
_Figura 2 - Placa VoIP TDM400P+._  
<div style="text-align: justify">
&emsp;&emsp;O servidor necessita de um hardware com capacidade suficiente para executar o sistema operacional adequado, sendo este compatível com o software Asterisk. A máquina utilizada possui um processador com mais de 2GHz de frequência, 8GB de memória e um disco rígido de 500GB de capacidade de armazenamento. A placa VoIP utilizada foi a TDM400P+, fabricada pela Digium Inc., que contém duas interfaces FXS e duas FXO. Alguns telefones analógicos, além de um ATA, também foram disponibilizados para uso no desenvolvimento do trabalho.</div>  


### 2.2 Elastix
<div style="text-align: justify">
&emsp;&emsp;O sistema operacional escolhido foi Linux, com a distribuição Elastix (distribuição desenvolvida para implementação Asterisk), que é considerada um servidor de comunicações unificadas. Dentre as diversas alternativas, como, por exemplo, o FreePBX, o AsteriskNow e o TrixBox, o Elastix foi escolhido por ter alguns pontos a considerar, como suporte ao idioma português, forte e ativa comunidade desenvolvedora além de um forte investimento em certificações.
O Elastix mais recente e estável foi desenvolvido tendo como base a distribuição CentOS 5.9, com a versão 2.6.18-348.1.1e15 do kernel Linux. O servidor implementa suas principais funcionalidades em torno de quatro softwares essenciais: Asterisk, Hylafax, Openfire e Postfix, sendo esses responsáveis pelos respectivos serviços: PABX, fax, mensagem instantânea e correio eletrônico. O Elastix oferece ao administrador a possibilidade de configuração amigável através do navegador, disponibilizando uma página web com todas as funcionalidades do sistema.</div>  
![Figura 3](/assets/img/elastix-gui.jpg)
_Figura 3 - Interface web do Elastix._  

#### 2.2.1 Instalação
<div style="text-align: justify">
&emsp;&emsp;A instalação do sistema foi baseada conforme artigo escrito por (CORREIA, 2012), disponível no site vivaolinux.com.br. </div>  

#### 2.2.2 Incompatibilidade de hardware
<div style="text-align: justify">
&emsp;&emsp;Após a instalação do sistema operacional na máquina, foi constatado que o kernel não reconheceu os drivers de rede, impossibilitando a inclusão do servidor na rede do campus, local onde foi implementado o sistema. No decorrer de três semanas, aproximadamente, foram baixados diversos pacotes de atualização, mas nenhum resolveu o problema de incompatibilidade de hardware. Como solução paliativa, foi utilizada uma interface de rede USB compatível com o kernel do sistema, o que possibilitou a verificação do mesmo a partir dos repositórios, sinalizando que a versão do sistema estava desatualizada de tal forma que não havia os drivers do hardware específico nos repositórios. Para resolver de forma definitiva o problema, foi adquirido, via download direto do site oficial Elastix.org, a última versão estável da distribuição. O sistema foi reinstalado e atualizado a partir dos repositórios oficiais, possibilitando assim a solução definitiva para a incompatibilidade de hardware.</div>  

### 2.3 Configurações dos softphones
<div style="text-align: justify">
&emsp;&emsp;Com o servidor atualizado e configurado com IP estático, foi possível dar início aos testes dos ramais. Em um primeiro momento, foi criado um ramal SIP para testes.</div> 
![Figura 4](/assets/img/config-ramal-sip.jpg)
_Figura 4 - Principais configurações do ramal SIP._
<div style="text-align: justify">
&emsp;&emsp;Para esse ramal foi definido o número 1001 e a senha de autenticação, além do nome de exibição para melhor organização. Outro ramal semelhante foi criado, porém, com o número 1002. Para a validação dos ramais criados, foram utilizados dois softphones (softwares que emulam telefones em um dispositivo) diferentes: Zoiper Free e X-Lite. Ambos os softwares foram configurados de acordo com os ajustes dos ramais e testados individualmente. Ambos funcionaram perfeitamente, efetuando e recebendo chamadas de voz entre eles. Após a conclusão dos testes, os ramais foram renomeados e reconfigurados para usuários finais, sendo definida a faixa 1000 para usuários criados e configurados com protocolo SIP.</div>  
![Figura 5](/assets/img/softphones.jpg)
_Figura 5 - Softphones Zoiper e X-Lite configurados, em meio a uma chamada._
![Figura 6](/assets/img/config-softphones.jpg)
_Figura 6 - Telas de configurações dos softphones._

### 2.4 Configurações do ATA
<div style="text-align: justify">
&emsp;&emsp;Após a definição e testes dos ramais SIP, foi configurado um ATA1 (adaptador de terminal analógico) modelo PAP2T, da Linksys, com capacidade para dois ramais. Foi definida no servidor a faixa 3000 para ramais SIP utilizados em ATAs. A configuração desses dispositivos se dá por meio de interface web e é muito semelhante à dos softphones, tendo como principais campos de configuração o Proxy, onde é digitado o IP do servidor VoIP; User ID, onde é definido o número do ramal; Password, que é a senha de autenticação previamente configurada no servidor para determinado ramal e, por último, o campo Display Name, onde é definido o nome do usuário do ramal. Um detalhe importante na configuração do ATA é o codec que o mesmo utilizará. Deverá ser o mesmo para ambas as linhas configuradas no ATA, além de serem compatíveis com os codecs do Asterisk, caso contrário, os ramais não funcionarão no equipamento. Nesta implementação foi utilizado o codec G729a em ambas as linhas do equipamento. Realizado testes e averiguado que as linhas efetuam e recebem ligações entre si e dos demais ramais.</div>  
![Figura 7](/assets/img/ata.jpg)
_Figura 7 - ATA Linksys, modelo PAP2T._
![Figura 8](/assets/img/config-ata.jpg)
_Figura 8 – Interface web de configuração do ATA._

### 2.5 Configurações dos ramais analógicos

#### 2.5.1 Protocolo ZAP x protocolo DAHDI
<div style="text-align: justify">
&emsp;&emsp;Após os testes bem sucedidos dos ramais SIP, outro teste foi realizado a partir das interfaces FXS do servidor. Deu-se início as configurações de um ramal analógico para cada interface disponível. Um telefone comum foi conectado ao servidor em uma das interfaces FXS e, logo após, configurado o ramal de testes com a faixa 2000. A princípio, foi utilizado o protocolo ZAP para a configuração do ramal. Realizado testes e verificado que o telefone analógico efetuava e recebia ligações de outros ramais, aparentando perfeita harmonia do sistema. Depois de definido o nome de usuário do ramal analógico, também foi criado outro ramal semelhante, a partir da outra interface FXS. Neste ramal foi averiguado que havia algo errado, pois era possível efetuar e receber ligações dos ramais SIP em ambas, porém, não era possível efetuar ligação para o outro ramal ZAP. O ramal denominado Analogico 1 (2001) efetuava ligações para o ramal denominado Analogico 2 (2002), mas o ramal 2002 não efetuava ligação para o ramal 2001, emitindo tom de ocupado. Algumas configurações foram alteradas, mas o problema persistiu. Após a realização de alguns testes, foi concluído que havia alguma espécie de incompatibilidade entre hardware e o protocolo ZAP, o que motivou a alteração do protocolo pelo DAHDI (Digium/Asterisk Hardware Device Interface), que é exclusivo dos hardwares da Digium. Realizado novos testes e averiguado que ambos os ramais DAHDI comunicam-se perfeitamente entre si e com os ramais SIP.</div>  
![Figura 9](/assets/img/config-analog-ramal.jpg)
_Figura 9 - Principais configurações do ramal analógico._ 

### 2.6 Conclusões da implementação
<div style="text-align: justify">
&emsp;&emsp;Os seguintes ramais foram criados e operam normalmente:</div>  
* ramal 1001 (protocolo SIP), definido e configurado em softphone;
* ramal 1002 (protocolo SIP), definido e configurado em softphone;
* ramal 2001 (protocolo DAHDI), conectado na interface FXS3 da placa VoIP. Utiliza um telefone analógico;
* ramal 2002 (protocolo DAHDI), conectado na interface FXS4 da placa VoIP. Utiliza um telefone analógico;
* ramal 3001 (protocolo SIP, codec G729a), conectado na linha 1 do ATA;
* ramal 3002 (protocolo SIP, codec G729a), conectado na linha 2 do ATA.
<div style="text-align: justify">
&emsp;&emsp;Todos os ramais efetuam e recebem ligações entre si, com satisfatória qualidade de áudio.</div>  
![Figura 10](/assets/img/ramais-server.jpg)
_Figura 10 - Ramais criados no servidor._

## 3 RESULTADOS E DISCUSSÃO
<div style="text-align: justify">
&emsp;&emsp;Partindo do pressuposto de que uma empresa é segmentada em diversos setores e departamentos distintos, organizados fisicamente em ambientes separados por salas e/ou repartições, tem-se, portanto, como principal justificativa para a implementação de serviços de telefonia VoIP a demonstração dos benefícios adquiridos ao utilizar uma central telefônica que não exija grandes alterações na infraestrutura já implantada. Foram utilizados, para este fim, recursos open source, que proporcionaram uma redução considerável de custos em comparação à aquisição de linhas telefônicas digitais.
Uma boa forma de comprovar a economia que a tecnologia oferece é comparando as tarifas de operadoras VoIP com as de operadoras de telefonia tradicional. Como mostra a tabela a seguir, os valores das tarifas da operadora PlugFone foram comparados com os valores das principais concessionárias de telefonia.</div>  
![Figura 11](/assets/img/tarifas.jpg)
_Figura 11 - Comparativo entre tarifas da Operadora PlugFone (VoIP) com as demais operadoras tradicionais. (Fonte: plugfone.com.br/tarifas.php)._




## CONSIDERAÇÕES FINAIS
<div style="text-align: justify">
&emsp;&emsp;A relação custo-benefício da utilização de uma central VoIP configurada em um servidor Asterisk é alta, pois há a flexibilidade e a possibilidade de configuração do software sem a necessidade de alteração da rede telefônica já existente. Outro ponto importante é a infraestrutura, pois, em qualquer ambiente onde haja um computador com acesso à rede, é possível implementar um ramal. Sendo necessário, para isto, apenas um headset e um softphone para utilizar o ramal diretamente no computador, ou uma interface ATA para fazer o link entre aparelhos analógicos com o ramal VoIP. Também existe a opção dos telefones IPs, que podem ser ligados diretamente à rede, deste modo, é perfeitamente possível ter uma linha configurada em cada computador de uma empresa sem fazer grandes alterações na infraestrutura.</div>  
<div style="text-align: justify">
&emsp;&emsp;Há também há o aspecto do custo lógico, já que é possível a utilização da internet para comunicação externa, como por exemplo, duas unidades de uma empresa, situadas em diferentes cidades, utilizando serviços VoIP para comunicação, assim realizando ligações DDD a custo local ou até mesmo a custo zero, o que proporciona uma redução significante de custos com telefonia.</div>
<div style="text-align: justify">
&emsp;&emsp;Uma vez observado que o desenvolvimento do trabalho originou-se de um projeto baseado na simulação de um ambiente corporativo e que, para tal feito, foram utilizados recursos limitados e explorado um número reduzido de funcionalidades do software Asterisk, foi demonstrado e comprovado, através de um meio livre, eficiente e de qualidade, a possibilidade de implementação de uma alternativa à telefonia convencional. </div>

## REFERÊNCIAS

* AMARAL, Italo. VoIP vs Telefonia IP. Disponível em: <https://blog.ccna.com.br/2008/05/14/voip-vs-telefonia-ip/>.   Acesso em: MARÇO DE 2013.  
* ASTERISK GURU. How to install and configure Wildcard TDM400p. Disponível em: <http://www.asteriskguru.com/tutorials/wildcard_tdm400p.html>.   Acesso em: MARÇO DE 2013.  
* ASTERISK PORTUGAL. O que é o Asterisk? Disponível em: <http://www.asterisk.pt/o-que-e-o-asterisk.html>.   Acesso em: MAIO DE 2013.  
* ASTERISK STUFF. Disponível em: <https://sites.google.com/site/allancassaro/asterisk>.   Acesso em: JULHO DE 2013.  
* COLCHER, S. VoIP: Voz sobre IP. 3 Ed. Rio de Janeiro: Elsevier, 2005.  
* CORREIA, Bruno R. Leite. Elastix – Instalando, criando ramais e SIP Trunk Vono. Disponível em: <http://www.vivaolinux.com.br/artigo/Elastix-Instalando-criando-ramais-e-SIP-Trunk-Vono>.   Acesso em: MARÇO DE 2013.  
* DAVIDSON, J., PETERS, J., BHATIA, M., KALIDINDI, S., MUKHERJEE, S. Fundamentos de VoIP. 2 Ed. Porto Alegre: Bookman. 2007.  
* DEVEL SISTEMAS. Codecs vc Consumo de Banda. Disponível em: <http://www.develsistemas.com.br/pt/component/content/article/44-noticias/120-codecs-vs-consumo-de-banda.html>.   Acesso em: ABRIL DE 2013.  
* GONÇALVES, F. Asterisk PBX, Guia de configuração. 2005.  
* INPHONEX. Manuais de Configuração de Equipamentos. Disponível em: <http://www.inphonex.com.br/suporte/configuracao-gateway-trixbox.php>.   Acesso em: MARÇO DE 2013.  
* KELLER, A. Asterisk na Prática. 2 Ed. São Paulo: Novatec Editora. 2011.  
* MALAR, Klaber. Introdução ao Asterisk – O que é, como funciona e como instalar. Disponível em: < http://www.profissionaisti.com.br/2010/10/introducao-ao-asterisk-o-que-e-como-funciona-e-como-instalar/>.   Acesso em: JUNHO de 2013.  
* PBX IN A FLASH: THE LEAN, MEAN ASTERISK® MACHINE. Copyright © Ward Mundy & Associates LLC. Disponível em: <http://pbxinaflash.net/>.   Acesso em: MAIO DE 2013.  
* PLUGFONE. Tarifas. Disponível em: < http://www.plugfone.com.br/tarifas.php>.   Acesso em: JULHO DE 2013.  
* RONCAGLIA, Adriano. História de Mark Spencer e o Open Source Asterisk. Disponível em: < http://mestreasterisk.com.br/artigos-mestre-asterisk/historia-de-mark-spencer-e-o-open-source-asterisk/>.   Acesso em: JUNHODE 2013.  
* SATO, Alberto. Trixbox – Um PABX IP gratuito em apenas 20 minutos. Disponível em: <http://imasters.com.br/artigo/10264/tecnologia/trixbox-um-pabx-ip-gratuito-em-apenas-20-minutos/>.   Acesso em: JUNHO DE 2013.  
* SILICONTECH.Disponível em: <http://www.silicontech.com.br/v2/product_info.php?cPath=43&products_id=140&osCsid=hb2629o2fhtsrhpqb47qonhkv0>.   Acesso em: JULHO DE 2013.  
* SOARES, L. F. G., LEMOS G. e COLCHER, S. Redes de Computadores: das LANs, MANs e WANs às Redes ATM, 2 Ed. Rio de Janeiro: Campus, 1995.  
* TANEMBAUM, A. Redes de Computadores. 4 Ed. Rio de Janeiro: Campus, 2003.  
* VOIP-INFO. Asterisk Codecs. Disponível em: < http://www.voip-info.org/wiki/view/Asterisk+codecs>.   Acesso em: ABRIL DE 2013.  
* VOIPON.Digium Wildcard TDM400P. Disponível em: <http://www.keison.co.uk/digium/digium_wildcard_tdm_400p.htm>.   Acesso em: JULHO DE 2013. 

___

[^1]: Estudante do Curso Técnico em Manutenção e Suporte em Informática do Instituo Federal de Educação, Ciência e Tecnologia Sul-rio-grandense, Campus Camaquã. E-mail: contato@dowilliam.com.
[^2]: Professor Orientador do Instituto Federal de Educação, Ciência e Tecnologia Sul-rio-grandense, campus Camaquã. Mestre em Engenharia Elétrica pela Pontifícia Universidade Católica do Rio Grande do Sul PUCRS, 2005 e Bacharel em Ciências da Computação pela Universidade Católica de Pelotas UCPEL, 2002. E-mail: k****o@ifsul.edu.br.
