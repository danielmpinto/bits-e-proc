# Mundo Real

!!! warning ""
    Entregar até dia 23/11

| HW | SW |
|----|----|
| 15 | 10 |

Esse projeto extra optativo (individual) fornece **15 pontos** 
extras de **Hardware** e **10 pontos extras** de **Software**. 

## Processadores

Você deverá escolher um dos processadores listados a seguir:

!!! warning 
    Não pode repetir. Ao escolher um processador, coloque o seu nome na planilha:
    
    - https://docs.google.com/spreadsheets/d/14MBWYusOTiBsR9gXlFhh964Hi1ULSdAOSlLffCnFaP0/edit?usp=sharing 
    

- [ARM Cortex M0](https://en.wikipedia.org/wiki/ARM_Cortex-M)
- [RISC V](https://en.wikipedia.org/wiki/RISC-V)
- [AVR](https://www.google.com/search?q=avr+microcontroller+wiki): Arduino UNO
- [Microchip PIC ](https://en.wikipedia.org/wiki/PIC_microcontrollers)
- [PowerPC](https://en.wikipedia.org/wiki/PowerPC)
- [SPARC V8](https://en.wikipedia.org/wiki/SPARC)
- [ZIP CPU](https://zipcpu.com/)
- [OpenRISC](https://openrisc.io/)
- [Intel 8051](https://en.wikipedia.org/wiki/8051)
- [ESP8266](https://en.wikipedia.org/wiki/ESP8266)
- [ESP32 RISC](https://en.wikipedia.org/wiki/ESP32)
- [Motorola S08](https://en.wikipedia.org/wiki/Motorola_S08)
- [Motorola 68hc12](https://en.wikipedia.org/wiki/Motorola_S08)
- [XC800](https://en.wikipedia.org/wiki/XC800_family)
- [LEON 3](https://www.gaisler.com/index.php/products/processors/leon3)
- [LatticeMico32](https://en.wikipedia.org/wiki/LatticeMico32)
- [PIC16x](https://en.wikipedia.org/wiki/PIC16x84)
- [PIC32M](https://en.wikipedia.org/wiki/PIC_microcontrollers#PIC32M_MIPS-based_line)
- [dsPIC](https://en.wikipedia.org/wiki/PIC_microcontrollers#PIC24_and_dsPIC)
- [CompactRISC](https://en.wikipedia.org/wiki/CompactRISC)
- [NXP LPC](https://en.wikipedia.org/wiki/NXP_LPC)
- [RP2040](https://en.wikipedia.org/wiki/RP2040)
- [Renesas RL78](https://en.wikipedia.org/wiki/RL78)
- [Renesas V850](https://en.wikipedia.org/wiki/V850)
- [6502](https://en.wikipedia.org/wiki/MOS_Technology_6502)
- [Ricoh 5A22](https://en.wikipedia.org/wiki/Ricoh_5A22): Usado no Super Nintendo e Apple IIGS
- [STM ST6](https://en.wikipedia.org/wiki/ST6_and_ST7)
- [Texas Instruments TMS100](https://en.wikipedia.org/wiki/Texas_Instruments_TMS1000)
- [Texas Instruments MSP430](https://en.wikipedia.org/wiki/TI_MSP430)
- [Texas instruments TMS320](https://en.wikipedia.org/wiki/Texas_Instruments_TMS320)
- [WDC 65C02](https://en.wikipedia.org/wiki/WDC_65C02)
- [WDC 65c816](https://en.wikipedia.org/wiki/WDC_65C816)
- [Xilinx MicroBlaze](https://en.wikipedia.org/wiki/MicroBlaze)
- [Xilinx PicoBlaze](https://en.wikipedia.org/wiki/PicoBlaze)
- [Zilog Z8](https://en.wikipedia.org/wiki/Zilog_Z8)
- [Zilog Z80](https://en.wikipedia.org/wiki/Zilog_Z80): Muito popular em 1976
- [Fujitsu FR-V](https://en.wikipedia.org/wiki/FR-V_(microprocessor))

## Entrega

Você deve entregar um vídeo que explica a CPU em questão, este vídeo ==de 10 minutos== deve conter:

- Explicativo do hardware
- Código Assembly Comentado

A entrega deve ser realizada pelo link a seguir, o vídeo deve estar no youtube (lembre de deixar acessível para qualquer um com o link):

- [Link para entrega](https://docs.google.com/forms/d/e/1FAIpQLSeTF5fCUlGqZBWhO6w_9HVgQ5nIxPIgawWLaW3n7M1L_bKaew/viewform?usp=sf_link)

!!! warning
    ==Muito importante que sempre que possível realizar uma comparação com a nossa CPU==
    
### (**15 HW**) CPU

- Histórico
    - [ ] História da arquitetura
    - [ ] Pessoas/ empresas responsáveis
    - [ ] Impacto histórico, impacto nos concorrentes/ comunidade/
    - [ ] Curiosidades
    
- Dispositivos, produtoes e empresas que fazem ou fizeram uso da CPU
    
- Arquitetura: Descreva a arquitetura interna da CPU
 
    - [ ] Quantos bits de largura? 8/16/32/..
    - [ ] Quantidade de registradores
    - [ ] Operações da ULA (se for muitas, pode pegar algumas)
    - [ ] A arquitetura é CISC ou RISC?
    - [ ] Qual tipo da CPU? 
        - [Stack Register](https://en.wikipedia.org/wiki/Stack_register), [Processor register](https://en.wikipedia.org/wiki/Processor_register), [Accumulator](Accumulator Register))
    - [ ] Como o Program Counter (PC) funciona? 
    - [ ] Como é realizado o acesso a memória nessa arquitetura? 
        - registrador-registrador, registrador-memória, memória-memória
        - Pode fazer operações direto na memória? Ou temos que carregar para os registradores antes?

- Instruções
    - [ ] Descritivo das instruções e seus padrões
    - [ ] Quantidade total de instruções
    - [ ] Diferença com relação ao Z01.1 

### (**10 SW**) Comentar código

Você deve pegar um código de exemplo do assembly da CPU escolhida e comentar ele no vídeo, explicando o que está fazendo.

- Explicar o que cada instrução está fazendo
- O impacto dela no hardware
- Muitas arquitetura possuem simulador! Interessante usar, mas não é necessário
