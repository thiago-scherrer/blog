---
title: "Queda_de_energia"
date: 2021-08-19T15:24:41-03:00
draft: false
---

## Impressão 3d e a falta de energia

Mesmo morando na capital de São Paulo, as quedas de energia por aqui são
constante, isso muito antes de estourar a crise hídrica (2021 aqui).

Perdi muitas impressões e a primeira coisa que pensei em comprar foi um nobreak.
Fiz uma lista de modelos e os mais recomendados para impressoras
3d em minhas pesquisas são modelos senoidal puro.

O preço me assustou, modelos SMS saem por uns R$1200,00 e então desisti por hora
e tentei usar a função `POWER_LOSS_RECOVERY` no Marlin `2.0.x`.

## Configuration_adv.h

O código que usei na minha ender3 v1 com um SKR Mini v2.0 + bltouch, foi esse
aqui:

```c
  #define POWER_LOSS_RECOVERY
  #if ENABLED(POWER_LOSS_RECOVERY)
  #define PLR_ENABLED_DEFAULT   true  // Power Loss Recovery enabled by default. (Set with 'M413 Sn' & M500)
  //#define BACKUP_POWER_SUPPLY       // Backup power / UPS to move the steppers on power loss
  #define POWER_LOSS_ZRAISE       2 // (mm) Z axis raise on resume (on power loss with UPS)
  #define POWER_LOSS_PIN         -1 // Pin to detect power loss. Set to -1 to disable default pin on boards without module.
  #define POWER_LOSS_STATE     HIGH // State of pin indicating power loss
  //#define POWER_LOSS_PULLUP         // Set pullup / pulldown as appropriate for your sensor
  //#define POWER_LOSS_PULLDOWN
  //#define POWER_LOSS_PURGE_LEN   20 // (mm) Length of filament to purge on resume
  //#define POWER_LOSS_RETRACT_LEN 10 // (mm) Length of filament to retract on fail. Requires backup power.
  #define POWER_LOSS_MIN_Z_CHANGE 0.05 // (mm) Minimum Z change before saving power-loss data

```

## POWER_LOSS_RECOVERY e OctoPrint

Não funciona :/
Primeira coisa que tentei foi fazer o power loss funcionar junto com meu
OctoPrint, que está rodando em Pi3.

O problema maior é o buffer, como a impressão é enviada através da conexão USB
(console), o GCODE é bufferizado, acaba que perde o sincronismo da impressão e o
OctoPrint.

## POWER_LOSS_RECOVERY e SDCard

Funcionou :)

Fiz um teste com o [Cali Cat](https://www.thingiverse.com/thing:1545913), removi
o cabo da impressora no meio da impressão e quando voltei o cabo, pude resumir a
impressão de onde parou.

O único problema que percebi é que o bico por estar quente na hora da "queda de
energia", ele acabou danificando um pouco a superficie onde parou. No final, não
deu para perceber pois as outras camadas da impressão acabou tapando o dano.

Vale lembrar que a função faz com que o GCODE seja escrito constantemente no
SDCard, ou seja, é bem possível que a vida dele acabe antes do que você imagina.

## Conclusão

Se as quedas de energia forem muuuito comuns por ai e você puder comprar um
nobreak, é sucesso.

Mas vale a pena tentar um pouco mais com o `POWER_LOSS_RECOVERY`.
