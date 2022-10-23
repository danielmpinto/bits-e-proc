# E - Assembly

| Entrega      |
|--------------|
| 24/10 - Segunda |

![Assembly](figs/F-Assembly/sistema-assembly.svg)

Nesse projeto cada grupo terá que implementar diversos códigos em assembly a fim de entendermos a linguagem e as limitações do hardware propostos.

## Instruções 

Seguir as instruções a seguir para desenvolvimento do projeto.

### Entendendo a Organização do Projeto

Agora iremos trabalhar na pasta `sw/nasm/` do repositório de entregado grupo. A pasta possui diversos arquivos `.nasm` assim como o arquivo `nasm_test.py` que executa os testes.

### Executando o Script de Teste 

Abra o terminal na pasta `sw/nasm/` e execute o pytest

```bash
$ pytest -k MODULO
```

Lembre que o módulo é o programa `nasm` que deseja testar.

## Projeto

Deve-se implementar diversos programas na linguagem de máquina do Z01 que irão manipular a memória RAM a fim de implementar o que é pedido. **A descrição a seguir está classificada em ordem de dificuldade, começando pelos mais simples.**

### Módulos 

A descrição de cada módulo está localizada no cabeçalho do arquivo.**
 
- abs
    - **Arquivo**   : `abs.nasm` (==lab 13==)
- max
    - **Arquivo**   : `max.nasm` (==lab 13==)
- mult
    - **Arquivo**   : `mult.nasm` (==lab 13==)
- mod
    - **Arquivo**   : `mod.nasm`
- div
    - **Arquivo**   : `div.nasm` 
- pow
    - **Arquivo**   : `pow.nasm`
- É par 
    - **Arquivo** : `isEven.nasm`
- String length 
    - **Arquivo** : `stringLength.nasm`
- Chaves e Leds 
    - **Arquivo** : `SWeLED.nasm`
- Linha
    - **Arquivo**   : `LCDlinha.nasm`
    - Edite o arquivo para desenhar uma linha completa no lcd

#### Conceito B

- Palíndromo 
    - **Arquivo** : `palindromo.nasm`
- Fatorial
    - **Arquivo**   : `fatorial.nasm`    
- Vector Mean
    - **Arquivo** : `vectorMean.nasm`
- LCD Quadrado
    - **Arquivo**   : `LCDquadrado.nasm`
    
#### Conceito A

- Multiplo de dois:
    - **Arquivo** : `multiploDeDois.nasm`
- MatrizDeterminante:
    - **Arquivo** : `matrizDeterminante.nasm`
- Chaves e Leds 2
    - **Arquivo** : `SWeLED2.nasm`
- Letra Grupo
    - **Arquivo**   : `LCDletraGrupo.nasm`

#### Extra

Criar um programa em python que converte um tabela do excel (onde cada célula equivale a um px pintado) em um código nasm que executa no Z01 e gera a imagem da tabela

