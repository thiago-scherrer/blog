---
title: "Cuidado_com_iot"
date: 2021-08-19T16:53:55-03:00
draft: false
---

## impressora 3d hackeada?

Estava navegando pelo reddit hoje e vi [este post bizarro aqui](https://www.reddit.com/r/3Dprinting/comments/p7jdhi/wake_up_this_morning_and_see_this_on_my_3d/).

Resumindo bem o post, o OP acordou de manha e percebeu que sua impressora 3d
tinha imprimido isto aqui:

```
TSD is not secure I randomly connected sorry had to inform u
```

Traduzindo:
```
TSD não é seguro Eu conectei aleatoriamente desculpe tive que informar você
```

Vou partir do princípio que o post é verdade. Este TSD provavelmente é um plugin
muito usado pela comunidade chamado [thespaghettidetective](https://www.thespaghettidetective.com/).
Basicamente é um software que é conectado em uma camera/celular, pode ser
utilizado em conjunto com o OctoPrint e com a ajuda de IA + IoT + Nuvem, o
programa pode cancelar, avisar, etc, quando sua impressão der ruim, o famoso
espaguete.

## O que é bizarro

Já é bem conhecido coisas como o [shodan](https://www.shodan.io/), mas nunca
tinha visto um ataque voltado a impressão 3d.

Num primeiro momento o que podemos pensar é, "se minha impressora for invadida,
vou perder uma grana com filamento" ou "posso acordar com um monte de coisas
bizarras impressas". Mas a coisa pode ficar feia.

Sabemos que é possível controlar qualquer coisa da impressora via console,
GCODE, etc. Então ativando o modo paranoico aqui, é possível fazer sua
impressora literalmente pegar fogo e com isso, quem sabe, uma casa.

E não é ficção científica, aconteceu com uma [ANET8](https://www.reddit.com/r/3Dprinting/comments/8ah96r/anet_a8_burns_down_half_the_house/).

Imagine forçar o `extruter` ativar o aquecimento para algo em 240C e então
desligar todas as ventilações, por sei lá, HORAS? Caótico!

## Oq fazer então?

Eu prefiro evitar qualquer coisa com IoT + Nuvem por hora ou que sabe pra
sempre.
