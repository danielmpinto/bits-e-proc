# Lab 14: Assembler

O laboratório introduz uma série de conceitos e ferramentas e deve ser realizado individualmente ou em dupla (como indicado no começo de cada parte). 

Ao final do laboratório você deverá ser capaz de:

1. Entender o que é um arquivo `.hack` e `.mif`
1. Ter o método `code.jump` implementando e testado
1. Saber como executar os testes unitários
1. Ter o método `parser.commandType` implementando
1. Saber como extrair informações dos testes unitários
1. Ter o `fillSymbolTable.initialize` implementando

## Antes de começar

Este laboratório será realizado já nos arquivos da entrega do projeto E-Assembler, portanto será necessário:

1. Definir o scrum
1. Atualizar o repositório do grupo com o do upstream
1. Todos atuailizarem o repositório do grupo

!!! warning
    Não seguir sem realizar a etapa anterior.

## Parte 1 - Entendendo

Agora iremos desenvolver um programa em python que será capaz de ler nossos programas escritos em assembly (`.nasm`) e converter eles para `.hack` (binário). Nosso arquivo `.hack` é um arquivo de **texto** que possui apenas `1`s e `0`s. Cada linha desse arquivo `.hack` é uma instrução a ser armazenada na memória ROM e executado pela CPU.

Exemplo de um arquivo `.hack`:

```
000000000000000101
100101100000010000
000000000000000001
100000000000100000
000000000000001011
```

> Você pode abrir seus arquivos .hack, basta ir em `sw/nasm` que vai encontrar seus binários (executáveis) lá.

O arquivo `.hack` é um formato que não conseguimos fazer o download para a FPGA, então é necessário convertemos esse formato em um que o Quartus entenda. Esse formato do Quartus é chamado de `.mif` e é gerado automaticamente pelos scripts de teste, esse arquivo `.mif` é similar ao `.hack` salvo um cabeçalho e a indicação do endereço na qual a linha deve ser salva:

```
WIDTH=18;
DEPTH=5;

ADDRESS_RADIX=UNS;
DATA_RADIX=BIN;

CONTENT BEGIN
  0 : 000000000000000101;
  1 : 100101100000010000;
  2 : 000000000000000001;
  3 : 100000000000100000;
  4 : 000000000000001011;
END;
```

!!! info
    O Assembler de vocês deve gerar um arquivo `.hack`.
    
    ```
        assembler        script python
    .nasm ---------> .hack --------> .mif 
                                    v
                                    |---------> FPGA
                                    |---------> SIMULADOR
    ```

## Assembler

O assembler será um programa escrito em python e que foi estruturado em **quatro classes**:
    
- ASM
    - **Arquivo**: `ASM.py`
    - **Descrição**: Classe responsável por criar o código de máquina, ela que **efetivamente** faz a varredura do arquivo `.nasm` de entrada e escreve o arquivo `.hack` de saída, gerando o código de máquina. 
    - **Dependências**: `ASMcode.py`, `Parser.py`, `SymbolTable.py`

- Code
    - **Arquivo**   : `ASMcode.py`
    - **Descrição** :  Traduz mnemônicos da linguagem assembly para códigos binários da arquitetura Z0.
    - **Dependências** : none

- Parser
    - **Arquivo**: `ASMparser.py`
    - **Descrição** : Encapsula o código de leitura. Carrega as instruções na linguagem assembly, analisa, e oferece acesso as partes da instrução  (campos e símbolos). Além disso, remove todos os espaços em branco e comentários.
    - **Dependências** : none

- SymbolTable
    - **Arquivo**   : `ASMsymbolTable.py`
    - **Descrição** :  Mantém uma tabela com a correspondência entre os rótulos simbólicos e endereços numéricos de memória.
    - **Dependências** : none

Note que o 'orquestrador' da montagem (esse é o termo em português utilizado) é a classe 'Assemble', nela que estará toda a lógica de montagem acessoada pelas demais classes. 

## Parte 2 - ASMCode

!!! warning ""
    Deve ser realizado individual (porém discutindo no grupo)
    
Iremos agora implementar um dos métodos da classe **Code**, a parte responsável por gerar os três bits referentes ao `jump`:

![](figs/H-Assembler/code-jump.png)

No **vscode** abra o código `ASMcode.py` e procure pelo método `jump`:

```python
    # TODO
    def jump(self, mnemnonic):
        """
        Retorna o código binário do mnemônico para realizar uma operação de jump (salto).
        - in mnemnonic: vetor de mnemônicos "instrução" a ser analisada.
        - return bits: (String de 3 bits) com código em linguagem de máquina para a instrução.
        """
        bits = "000"
        return bits
```

Note que o input dessa função é um array de strings, chamado `mnemnonic` e seu retorno é uma string. No mnemnonic será passado a instrução a ser executada da seguinte forma:

- `{"jmp"}`
- `{"jge", "S"}`
- `{"jg", "%D"}`
- ...

E deve retornar o binário correspondente aos bits j2, j1 e j0 do comando de jump :

- `111`, `011`, `010`, ....

> Note que aesa classe não precisa se preocupar com a origem do jump (%A, %D, ...) apenas com o seu tipo `jmp`, `jge`, ...

!!! exercise
    - File: `sw/assembler/ASMcode.py`
    - Teste: `pytest -k test_jump`
    
    Implemente a classe `jump` e teste sua implementação.

    Dica: Lembre que a disciplina utiliza da metodologia TDD, onde vocês devem basear o desenvolvimento no testes. Abra o arquivo de teste `test_asmcode.py` e analise como o `test_jump` é realizado.
    
## Parte 3 - Parser

[Desenvolvimento baseado em testes](https://en.wikipedia.org/wiki/Test-driven_development) é uma técnica que temos utilizado até agora para os nosso projetos, nesse método fragmentando o desenvolvimento em pequenos módulos que são testados de forma individual, por testes unitários. O desenvolvimento é focado em fazer com que os módulos passem nos testes.

Como os testes não são perfeitos e não conseguem cobrir toda a funcionalidade do módulo, é necessário realizarmos o teste de integração, onde juntamos todas as peças e testamos o sistema como um todo.

Dentro da pasta do novo projeto, temos um arquivo de teste para cada módulo, desenvolvido em pytest:

- `test_asm.py`
- `test_asmcode.py`
- `test_asmparser.py`
- `test_symboltable.py`

E alguns arquivos que ajudam na realizacão dos testes, localizados em `test_assets`. Os testes são uma guia do que cada método deve fazer, e eles servirão como complemento da documentação do módulo. Iremos seguir o fluxo:

1. Ler descrição do método
1. Abrir teste unitário e entender o que é passado e o que é esperado
1. Desenvolver método
1. Testar
   - Falhou? Volte para 1.

Vamos pegar como exemplo o método `commandType` do `sw/assembler/ASMparser.py`:

```python
    # TODO
    def commandType(self):
        """
        Retorna o tipo da instrução passada no argumento:
         - self.commandType['A'] para leaw, por exemplo leaw $1,%A
         - self.commandType['L'] para labels, por exemplo Xyz: , onde Xyz é um símbolo.
         - self.commandType['C'] para todos os outros comandos
        @param  command instrução a ser analisada.
        @return o tipo da instrução.
        """
        pass
```

E seu teste unitário:

```py
def test_commandType():
    fnasm = open('test_assets/mult.nasm', 'r')
    ptest = Parser(fnasm)

    ptest.currentCommand = ['leaw', '$2', '%A']
    assert ptest.commandType() == ptest.CommandType['A']

    ptest.currentCommand = ['movw', '$1', '%A']
    assert ptest.commandType() == ptest.CommandType['C']

    ptest.currentCommand = ['WHILE:']
    assert ptest.commandType() == ptest.CommandType['L']

    ptest.currentCommand = ['leaw', '$31', '%A']
    assert ptest.commandType() == ptest.CommandType['A']

    ptest.currentCommand = ['addw', '%D', '%A', '%D']
    assert ptest.commandType() == ptest.CommandType['C']

    ptest.currentCommand = ['rsubw', '%D', '%A', '%D']
    assert ptest.commandType() == ptest.CommandType['C']
```

- Nesse teste é passado o vetor `["leaw", "$2",  "%A"]` para o método `parser.commandType` e esperasse na saída `A_COMMAND`, .... .

Com essa informação complementar conseguimos iniciar o desenvolvimento dessa classe.

!!! exercise
    - File: `sw/assembler/ASMparser.py`
    - Teste: `pytest -k test_commandType
    
    Implemente a classe `commandType` e teste sua implementação.
    
    ==NOTA:== O teste verifica apenas alguns casos, você deve tentar generalizar a implementacão da classe, lembre que instruções do tipo C podem ser das mais diversas.

!!! exercise
    - File: `sw/assembler/test_asmparser.py`
    - Teste: `pytest -k test_commandType`

    Adicione mais algumas linhas ao teste do `commandType` e verifique se sua implementação continua funcionando:
    
    ```py
    ptest.currentCommand = ['negw', '%D']
    assert ptest.commandType() == ptest.CommandType['C']
    
    ptest.currentCommand = ['subw', '%D', '%A', '(%A']
    assert ptest.commandType() == ptest.CommandType['C']
    ```
    
    - Adicione você mais 3 testes do tipo `C`, `L` e  `A`

## Parte 4 - Symboltable

Implemente o método `init` da classe `SymbolTable` utilizando os conceitos visto nos outros labs. 


!!! exercise
    - File: `sw/assembler/ASMsymbolTable.py`
    - Teste: `pytest -k test_init`
    
    Implemente o método `init` do `SymbolTable` e teste.
