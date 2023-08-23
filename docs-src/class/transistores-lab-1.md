# Lab 4: Transistores / CI

Esse laboratório tem como objetivo trabalhar com os conceitos básicos de portas lógicas do tipo RTL realizadas a base de transistores discretos do tipo BJT e também trabalhar com componentes integrados (CI) da família CMOS.

Existem basicamente três níveis de simulação de componentes eletrônicos: a primeira, puramente lógica utiliza de portas lógicas "ideais" (https://simulator.io/board). Um simulador mais preciso irá utilizar transistores para a implementação dessas portas lógicas porém não leva em consideração todos os fatores físicos-eletrônicos dos componentes (http://falstad.com/circuit/). Já um simulador que leva em consideração as propriedades dos componentes é chamado de SPICE e irá gerar uma simulação mais precisa em termos físicos do circuito original (http://circuitlab.com).

## Parte 1 - Circuito misterioso

Vamos usar o simulador do site falstad para implementar um circuito feito com transistores que implementa uma equação booleana. 

1. Abra o site: http://www.falstad.com/circuit/
1. :arrow_right: Arquivo :arrow_right: Importar Arquivo Texto :arrow_right: Copiar e colar o texto a seguir

- [code.txt](transistores-lab-1-exe1.txt)

Vocês devem obter o seguinte diagrama:

![](figs/A-Transistores/simulacao.gif){width=400}

Com o circuito carreado no site, encontre:

!!! example "Tarefa"
    1. Encontre a tabela verdade do circuito.
        - Faça todas as combinações possíveis de entradas (H/L) e verifique o valor da saída (H/L)
    1. A partir da tabela verdade encontre a equação lógica.
    1. Desenhar o diagrama da equação (simplificado).


## Outro circuito misterioso

Implementar o outro circuito feito com transistores que implementa uma equação booleana no simulador do site falstad. 

1. Abra o site: http://www.falstad.com/circuit/
1. :arrow_right: Arquivo :arrow_right: Importar Arquivo Texto :arrow_right: Copiar e colar o texto a seguir

[circuito](transistores-lab-1-exe2.txt)

!!! exercise
    1. Encontre a tabela verdade do circuito.
        - Faça todas as combinações possíveis de entradas (H/L) e verifique o valor da saída (H/L)
    1. A partir da tabela verdade encontre a equação lógica.
    1. Desenhar o diagrama da equação (simplificado).

## Parte 2 - RTL

Iremos implementar portas lógicas e equações booleanas com transistores BJT. Para isso vamos utilizar o [TinkerCad](https://www.tinkercad.com/), que irá permitir realizarmos uma montagem similar a que seria feito no laboratório.

### Material

Cada grupo receberá:

- Duas protoboards
- Duas baterias 9V
- Jumpers macho-macho
- 12 transistores [BJT-N BC337](https://www.onsemi.com/pub/Collateral/BC337-D.PDF)
- 24 resistores de 2k
- 6 LEDs coloridos (Vermelho, amarelo e verde)

![](figs/A-Transistores/materiais.jpg)

### Trabalhando

O grupo deve se organizar e executar da melhor forma possível (com todos participando) os módulos a seguir, utilizando:

- Entradas: Utilizar como entrada do sistema (A,B,C,...) **jumpers** que estarão hora conectados em **GND (0)** ou **VCC (1)**. 
- Saídas: A saída final do sistema deve ser representada com um LED, sendo aceso indicando lógica `1` e apagado lógica `0`.
- Validação: Uma tabela verdade do circuito deve ser apresentada e em aula demonstrado que o circuito representa a tabela.

----------------------

### a - NOT

!!! info
   **Cada grupo deve realizar duas** implementações do circuito a seguir que representa uma NOT:

Iremos implementar uma porta lógica do tipo NOT usando transistores BJT. 

![RTL Not](figs/A-Transistores/rtl-notNEW.png){width=500}

Para isso vocês deverão:

1. Entrar no site [TinkerCad](https://www.tinkercad.com/)
1. Logar (com google) e criar conta **pessoal**
1. **Circuis** :arrow_right: **Criar novo Circuito**
1. Fazer a implementação a seguir

![Protoboard](figs/A-Transistores/rtl-not-protoboard.png)

!!! warning
    Se você perceber que algum transistor está aquecendo,
    desconecte a bateria e verifique novamente a montagem.
    Isso é um sinal que alguma coisa está errada.

!!! Exercise
    Levante a tabela verdade do circuito recém montado e verifique se é mesmo uma NOT.

!!! tip
    - Utilize o [datasheet](https://www.onsemi.com/pub/Collateral/BC337-D.PDF) do transistor para entender a montagem

    - Mexa na chave para aplicar `0` ou `1` na entrada do circuito.

!!! note "Solução"
    https://www.tinkercad.com/things/bnWLvsuRvp6-neat-lappi-snicket/editel?sharecode=QlWtWTyxH18eCaVwphNPVTpzdXW9IlssdNUmgLUOtAU

!!! tip
    O fio 'rosa' da imagem anterior representa a entrada do seu circuito, você deve colocar ela em `GND` para simular uma entrada `0` e em `VCC` para simular uma entrada `1`.

    
### 1b - NOT NOT

Agora que as duas `NOT` foram implementadas, testadas e estão funcionado, conecte a saída de uma na entrada da outra. Isso vai fazer com que a saída siga o valor de referência da entrada.

![not not A](figs/A-Transistores/notnot.png){width=300}

!!! exercise
    Levante a tabela verdade do circuito recém montado

!!! exercise
    1. Levante a tabela verdade do circuito recém montado.
    1. Qual porta lógica é essa?

----------------------

### b - OR

!!! exercise
    Implemente uma porta lógica do tipo OR usando transistores BJT. Essa porta terá duas entradas e uma saída, cada entrada deve ser uma chave e a saída um LED.

    Utilize a página a seguir para ter ideias de como implementar as portas lógicas em RTL:
    
    -  http://hyperphysics.phy-astr.gsu.edu/hbase/Electronic/trangate.html#c2

----------------------

### c - Equação

!!! exercise
    Implemente a equação lógica a seguir em um circuito do tipo RTL, faca no simulador e se sobrar tempo implemente com transistores na protoboars. 

    ```
    Q = A.(A.(A+B)+A.C)
    ```

    1. Implemente a equação no TinkerCad
    1. Para validar valide com tabela verdade do circuito 
        - **As duas tabelas precisam ser idênticas!** 

## Circuitos Integrados - CI

Circuitos integrados são componentes eletrônicos que possuem internamente dezenas a milhares de transistores que implementam circuitos eletrônicos, facilitando e possibilitando o desenvolvimento de projetos de hardware mais complexos.

Existem várias 'famílias' de CI que implementam portas lógicas, iremos trabalhar com uma versão chamada de série [TTL 7400](https://pt.wikipedia.org/wiki/S%C3%A9rie_7400). Exemplos de componentes dessa famílias:

- 7400: Quatro portas NAND de duas entradas
- 7401: Quatro portas NAND de duas entradas com coletor aberto
- 7402: Quatro portas NOR de duas entradas
- 7403: Quatro portas NAND de duas entradas com coletor aberto
- 7404: Seis inversores (porta NOT)

> Para a lista completa acesse: https://pt.wikipedia.org/wiki/Lista_dos_circuitos_integrados_da_s%C3%A9rie_7400

Vamos continuar no [TinkerCad](https://www.tinkercad.com/).

### a - NOT

Vamos usar o componente [7404](https://pt.wikipedia.org/wiki/TTL_7404) que possui 6 NOTs para fazer a mesma coisa que fizemos com os transistor discreto:

![](figs/A-Transistores/7404-pcb.png)

!!! note "7404"
    Para mais informações, acesse:  https://pt.wikipedia.org/wiki/TTL_7404
   
    ![](.figs/A-Transistores/7404.png)

!!! note "Solução"
    - https://www.tinkercad.com/things/5didIR3U6qY-sizzling-jaban-jarv/editel?tenant=circuits?sharecode=2N6uVn_CZekje82phPIUcZu_24lOLu1_oeEenH-htT8

----------------------

### b - Equação

Implemente a equação a seguir com CIs da família 74xx.

```
Q = (A xor B) or not(C)
```

!!! tip
    1. Identifique os componentes
    1. Procure na [lista](https://pt.wikipedia.org/wiki/Lista_dos_circuitos_integrados_da_s%C3%A9rie_7400) qual o seu nome
    1. Analise os pinos desse componente
    1. Faça a ligação e teste por parte
