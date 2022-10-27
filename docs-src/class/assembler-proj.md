# G - Assembler

> O projeto tem letra G para manter compatibilidade com Elementos de Sistemas, que possui o projeto F.

| Entrega      |
|--------------|
| 4/10 - Sexta |

![Assembly](figs/H-Assembler/sistema-assembler.png)

Nesse projeto iremos criar o programa *assembler* que é responsável por traduzir os códigos escrito em Assembly para a linguagem de máquina.

## Instruções 

As instruções técnicas de como começar o projeto estão no laboratório 14.

### Conceito C

O conceito C deve ser:

- a implementaćão completa do Assembler, com todo os testes passando.

!!! info
    Atencão com os testes, existem mais de uma maneira de realizar a mesma instruções (por exemplo o nop), então se falhar, não assuma imediatamente que a sua implementaćão está errada.

## Rubrica

| Conceito |                                                                                     |
|----------|-------------------------------------------------------------------------------------|
| A        | - Insere automaticamente um NOP após instrução de JUMP que não é seguida de nop.    |
|          | - Realiza pequenas otimizaćões no código assembly (descrever no readme)             |
|          | - Proponha alguma outra melhoria e converse com o professor para saber se é valida. |
|          |                                                                                     |
| B        | - Verifica se instrução de jump é seguida de NOP, caso contrário dá erro            |
|          | - Possibilita carregar um valor negativo: `leaw $-5, %A`                            |
|          |                                                                                     |
| C        | - Criado assembler a partir de estrutura de código disponibilizada                  |
|          | - Todos os testes unitários passam no teste                                         |
|          | - Actions configurado corretamente                                                  |
|          |                                                                                     |
| D        | - Teste unitário ou Teste integração não passa                                      |
|          |                                                                                     |
| I        | - Menos da metade dos módulos funcionando                                           |

