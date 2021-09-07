---
title: "Uma_rede_local_mais_segura_parte1"
date: 2021-09-07T08:17:32-03:00
draft: false
---


Sempre fui muito ligado em assuntos relacionados em privacidade e segurança.
Talvez depois de ter ido em algumas [cryptorave](https://cryptorave.org/) eu
tenha começado a olhar o que era até então pra mim um de meus milhares hobbies,
como algo mais sério.


Com a chegada do home office em minha vida, pude olhar com um pouco mais com
carinho para a minha rede local.


## DNS


No geral, as pessoas costumam usar o DNS que já vem configurado no roteador
entregue pela operadora de LINK. O ponto positivo disso é que o cliente acaba
sendo beneficiado com melhores rotas e melhores PoPs das CDNs.


Já os pontos negativos e generalizando aqui, os DNSs das operadoras são muito instáveis,
me fazendo mostrar [esse caso aqui de 2008](https://super.abril.com.br/blog/bruno-garattoni/o-que-provocou-o-apagao-da-internet/). Fazendo justiça, a estabilidade melhorou bastante desde este último apagão
da internet em 2008.


Outro ponto negativo de se usar o DNS da operadora e este ponto aqui questiona
até mesmo o positivo do início, já que mostra a fragilidade da privacidade, já que
utilizando estes DNSs, a gente corre o risco de cair em filtro
[como este aqui](https://tecnoblog.net/461579/claro-oi-tim-e-vivo-bloqueiam-the-pirate-bay-no-brasil-apos-operacao-404/) que tirou o piratebay do ar aqui no BR. Outra questão neste mesmo tópico,
é que no geral as operadoras não ativam o suporte ao [DNSSEC](https://registro.br/tecnologia/dnssec/dns-e-dnssec/por-que-utilizar/).


Então olhando para esses pontos resolvi colocar um Raspberry pi zero para ficar
responsável pelo DNS local da minha rede.
O Raspberry zero deve ser o mais barato da linha, com 512MiB de ram e um ARM11
de 1GHz, deu conta do recado. Após instalar o [raspibian](https://www.raspberrypi.org/software/operating-systems/) nele, configurei um [Unbound](https://en.wikipedia.org/wiki/Unbound_(DNS_server)
para ser usado como DNS recursivo.


No unbound, não modifiquei muito as suas configurações, só ativei o suporte a IPv6,
fixei quais redes estavam liberadas para consulta-lo, ativei o suporte ao DDNS
e adicionei quais servidores de DNS ele iria consultar. No começo eu usei os
[root servers](https://en.wikipedia.org/wiki/Root_name_server), porém com um
número crescente de ataques de phishing, abri mão um pouco da privacidade e
adicionei os DNSs gratuitos com [bloqueio de Malware da cloudflare](https://blog.cloudflare.com/introducing-1-1-1-1-for-families/).


Com um DNS configurado e com o incentivo de um amigo do trampo (vlw luiz!)
decidi colocar o [pihole](https://pi-hole.net/) no pi zero. O pihole é um
software opensource que oferece um monte de recursos diretamente para a sua
rede como por exemplo bloqueio de tracking e ads, monitoramento da rede e
otimização e performance. Ele faz isso com base uma lista de URLs e regex que
você pode gerar ou pegar alguma lista da comunidade, tem milhares, inclusive,
fiz [esse projeto aqui](https://github.com/thiago-scherrer/go-pihole) para gerar
e atualizar todo dia a minha lista de [bloqueio que jogo aqui](https://github.com/thiago-scherrer/pi-hole-block-list).


Depois de tudo pronto com meu pizero, coloquei ele como único dns em DHCP/Roteador da minha rede.
E pronto, a mágica começou. No começo, deu um pouco de trabalho para ir liberando as páginas que estavam bloqueadas
(obrigado esposa pela paciência haha).
Mas isso foi culpa minha, com a lista que eu gerei, muita coisa foi bloqueada então foi um trabalho de formiguinha no começo.


Em meus testes, parando de usar os DNSs do meu provedor e usando o meu pi
zero com unbound e pihole, a velocidade de lookup aumentou em mais de 70%! O
tráfego total bloqueado pelo pihole até agora foi de 11.5%, o que além de trazer
segurança, impacta do consumo de banda da minha internet.


O pizero não tem ethernet, ou seja, utiliza o wireless para comunicação, mas
mesmo assim, atendeu minhas expectativas.
