# Lab 16 - VM translator

Este laboratório é uma introdução para o nosso último projeto, o vmtranslator! Neste laboratório iremos aprender como:

1. Modificar o vmtranslator 
1. Realizar testes
1. Ver o teste passar =)

!!! exercise "Antes de começar"

    Este laboratório será realizado já nos arquivos da entrega do projeto `vmtranslator`, portanto será necessário:

    1. Definir o scrum
    1. Atualizar o repositório do grupo com o do upstream
    1. Todos atualizarem o repositório do grupo

!!! warning
    Não seguir sem realizar a etapa anterior.

### Estrutura

O VMtranslator já foi fornecido quase todo pronto (ufa!!) vocês só precisam implementar a parte que faz a tradução de um comando `vm` (pilha) em `nasm` (registrador-memória), o projeto possui estrutura muito similar ao do assembler, os códigos do VM Translator estão localizados em:

- `sw/vmtranlator/....`

O único arquivo que vocês vão precisar mexer de todo o projeto é o `Code.py`. Mas se tiver energia, de uma olhada na estrutura geral do projeto.

### Aritmética

Vamos comecar o lab implementando a operacoes aritméticas, mais especifica a de `add` (que soma dois elementos na pilha), abra o código do `Code.py` e procure pelas linhas:

```py
if command == "add":
    pass # TODO
```

A variável `command` é um vetor (na verdade ela vai virar um vetor de strings), é nesta variável que iremos adicionar as instruções assembly que irão realizar a operação de `add`, isso deve ser feito da seguinte maneira:

```py
if command == "add":
    commands.append("leaw $SP,%A")
    commands.append("movw (%A),%D")
    commands.append("decw %D")
    ...
    ...
```

No final do método o programa salva as intrucões assembly relativos ao comando `vm` no arquivo `.nasm`.

!!! tip ""
    Você pode remover o `pass`, eu só coloco para o pytest não reclamar que o código python está errado.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Command: `add`
    - Test: `pytest -k add`
    
    Termine de implementar o comando `add` e teste com `pytest -k add`

### Como o teste funciona?

Com o teste passando, abra a pasta `test_assets` e repare que vários arquivos foram criados, para cada teste temos um arquivo `.vm` (neste caso `add.vm`) que gera um arquivo `.nasm` (no exemplo `add.nasm`) que possui o comando `VM` traduzido para assembly, este arquivo então é passado pelo assembler que gera o `add.hack`. Com o arquivo de linguagem de máquina, uma simulacão é executada e o teste realizado (analisasse os valores na memória RAM).

### Praticando

Agora vamos praticar um pouco.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Command: `neg`
    - Test: `pytest -k neg`
    
    Implemente o comando `neg` e teste com `pytest -k neg`.
    
    Dica: Fac'a no papel antes e só depois implemente.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writePush`
    - Command: `push constant`
    - Test: `pytest -k push_constant`
 
    Agora implemente um comando de uma outra classe, a do push. Procure pelo comando na classe `writePush`.

Os próximos exercícios são de classe diferente da aritméticas.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writePop`
    - Command: `pop local`
    - Test: `pytest -k pop_local`
 
    Implemente o comando `pop local`.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writePop`
    - Command: `pop temp`
    - Test: `pytest -k pop_temp`
 
    Implemente o comando `pop temp 4`.

Um desafio (e que todo mundo deve conseguir fazer).

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writeArithmetic`
    - Command: `gt`
    - Test: `pytest -k gt`
 
     Implemente o comando `gt`. 
    
    Dica: Você vai ter que fazer um label para poder saltar, mas o label tem que ser único em todo o código `nasm` criado, para isso, utilize a funcão `self.getUniqLabel()` que retorna uma string única em todo o programa. 


Acabou? Organize o projeto no grupo e vá fazer o resto. 
