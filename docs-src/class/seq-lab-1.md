# Lab 8: Lógica Sequencial

Agora vamos ver como implementamos uma lógica sequencia em MyHDL! Até agora temos utilizado o `decorator`: `@always_comb` para indicar que uma função deve ser interpretada como um trecho combinacional:

```py
@always_comb
def comb():
    led.next = l
```

Agora vamos começar usar um novo `decorator` (`@always_seq`) para indicar que uma função deve ser sequencial e depender do `clock` e do `reset`. O módulo aseguir demonstra como implementar um flip-flop tipo D em MyHDL:

```py
@block
def dff(q, d, clk, rst):
    @always_seq(clk.posedge, reset=rst)
    def seq():
        q.next = d

    return instances()
```

Notem que estamos usando `@always_seq(clk.posedge, reset=rst)`, e indicando que o módulo deve ser acionado na borda de subida do sinal `clk` e que o sinal de `reset` deve ser o `rst`.

Podemos interpretar o `def seq()` da seguinte maneira: Sempre que o sinal clock variar de `0` para `1` a função é acionada e então a saída `q` recebe a entrada `d`. Podemos visualizar isso como um `while True:` 

```py
    while True:
        q.next = d
        time.sleep(1/CLOCK)
```

## dff

!!! exercise
    - File: `seq/seq_modules.py`

    Tarefa:

    Vamos validar o flip-flop, para isso modifique o `toplevel.py`:
    
    ```py
        ic0 = dff(ledr_s[0], sw_s[0], key_s[0], RESET_N)
    ```
    
    E faça o processo completo para obtermos o hardware.
    
    Validando:
    
    Mapeamos o clock para o `KEY[0]` e a entrada do dff para o `SW[0]`, notem que ao mexer a chave `SW[0]` nada acontece, o valor do LED muda apenas após apertar o `KEY[0]` (que é o `clock`)
    
### Clock

O sinal de clock da nossa FPGA é de ==50Mhz==, ou seja: `50 000 000` vezes por segundo! Isso parece muito né? Mas, dependendo do projeto, podemos elevar o clock para 200Mhz ou usar FPGAs mais rápidas que chegam próximo do 1GHz.

## Piscando LED

Agora com o uso da lógica sequencial conseguimos contar 'tempo' e gerar eventos em determinado momento. Ou seja: podemos contar 0.5 segundos e mudar o valor do led, contar mais 0.5 s e mudar novamente (fazer o famoso **pisca led**). Para isso, teremos que conseguir contar eventos de clock, e quando o valor chegar em **25 000 000** inverter o valor do LED e zerar o contador e ficar nesse loop para sempre.

Podemos usar o nosso `adder` do lab anterior como módulo de contador, conectando a saída do `adder` na entrada `x`, mas passando por um registrador antes (para apenas mudar a cada clock). A entrada `y` será conectado ao valor `1`, como resultado teremos: `s = x + 1`. A expressão será executada a cada subida do clock. E `x` será:

``` py
if s < MAX:
    x.next = s
else:
    x.next = 0
```

Se o valor de `s` for menor que o valor máximo (define a velocidade que o LED irá piscar) copiamos a saída do somador para a entrada, e se o valor `MAX` for atingido, iremos zerar o somador, para começarmos novamente. O HW que queremos gerar é algo como:

![](figs/seq/lab-blink.svg)

A ideia de piscar o LED é que temos que mudar uma variável a cada ciclo do contador. 

```
-----------           -------------
           |          |            |           Status
           |          |            |
            -----------            ----------
            
           _ 25000000  _            _
         / |         / |          / |      
      /    |      /    |       /    |          Contador
   /       |   /       |    /       |
/          |/          | /          |
```

A implementação em MyHDL:

```py
@block
def blinkLed(led, clk, rst):
    cnt = Signal(intbv(0)[32:])
    l = Signal(bool(0))

    @always_seq(clk.posedge, reset=rst)
    def seq():
        if cnt < 25000000:
            cnt.next = cnt + 1
        else:
            cnt.next = 0
            l.next = not l

    @always_comb
    def comb():
        led.next = l

    return instances()
```

Alguns detalhes devem ser levados em consideração na implementação do componente:

1. O `seq` acontece a cada mudança do clock
1. O `comb` acontece sempre
1. Não podemos `ler` uma saída

E então atribuímos o valor de `l` para a saída `led` na parte combinacional do módulo:

```py
def comb():
    led.next = l
```

Essa atribuicão poderia ser feita dentro da parte sequencial do componente:

```diff
@always_seq(clk.posedge, reset=rst)
def seq():
    if cnt < 25000000:
        cnt.next = cnt + 1
    else:
        cnt.next = 0
        l.next = not l

    led.next = l
```

!!! exercise 
    File: `toplevel.py`
    
    Modifiquem o toplevel para conter o componente `blinkLed`:
    
    ```py
    ic1 = blinkLed(ledr_s[0], CLOCK_50, RESET_N)
    ```
    
    E façam o fluxo de rodar o módulo na FPGA. Verifiquem que o LED pisca!!

!!! exercise short 
    O `cnt` de 32 bits está bem dimensionado? Esse valor faz alguma diferença?
    
    `cnt = Signal(intbv(0)[32:])`
    
    !!! answer
        - 32 bits = 4294967296
        - 4294967296/50M = 85s
        
        Faz diferença sim! Quando mais bits, mais registradores temos que usar e maior ficar o hardware.
        
        Poderíamos dimensionar o tamanho do vetor de acordo com o `time_ms` que foi passado para o módulo.

!!! exercise
    - File: `seq_modules.py`
    - File: `toplevel.py`
    - Função: `blinkLed`
    
    Vamos deixar o componente mais genérico? Para isso modifique a função `blinkLed` para receber mais um argumento: O valor em `ms` na qual o LED irá piscar:
    
    ```py
    def blinkLed(led, time_ms, clk, rst):
    ```
    
    Depois modifique o toplevel para validar diferentes valores em diferentes leds:
    
    ```py
    ic1 = blinkLed(ledr_s[0], 100, CLOCK_50, RESET_N)
    ic2 = blinkLed(ledr_s[1], 50, CLOCK_50, RESET_N)
    ic3 = blinkLed(ledr_s[2], 1000, CLOCK_50, RESET_N)
    ```
    
    Lembre de validar na FPGA!

!!! exercise 
    - File: `seq_modules.py`
    - Função: `barLed`
    
    Tarefa:

    Vamos praticar mais! Agora faça com que os LEDs da FPGA acendam em sequência: Primeiro o LED0, depois o LED1... (como uma animação), ao chegar no final apague tudo e comece novamente.
    
    Dica:
    
    Você vai precisar de mais um contador indo de 0 a 9
    
!!! exercise
    - File: `seq_modules.py`
    - Função: `barLed`

    Modifique a barLed adicionando:
    
    - SW[0] controla a velocidade dos LEDs: Rápido ou Lento
    - SW[1] controla a direção (esquerda/ direita)
    
    ```py
    def barLed(leds, time_ms, dir, vel, clk, rst):
    ```

!!! exercise
    - File: `seq_modules.py`
    - Função: `barLed2`

    Tarefa:
    
    O barLed2 é similar ao LED porém só um LED aceso por vez!
    
    Dica:
    
    Aplique um shift de `cntLed` ao valor em binário `000000001`, onde `cntLed` é o contador de 0, 9.
    
    ```py
    @always_comb
    def comb():
        leds.next = intbv(1)[10:] << cntLed
    ```

## Desafio

Ideias de LABs com utilidade:

- Ultrasom HC-SR04?
- LED RGB
- StepMotor
- Servo
- ...
