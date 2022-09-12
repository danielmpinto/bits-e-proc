# B - Lógica Combinacional

| Data da entrega |
|-----------------|
| 11/09 - Domingo |

- Arquivo: `hw/components.py`

![](figs/LogiComb/sistema-comb.svg)

!!! tip "Antes de começar"
    Siga os passos em:
    
    - https://insper.github.io/bits-e-proc/commum-content/util/Util-Comecando-novo-projeto/

!!! tip "Vixi Sou scrum master"
    Você é o scrum do projeto? Leia:
    
    - https://insper.github.io/bits-e-proc/commum-content/util/Util-vixi-sou-scrum/

!!! tip "Vixi! Sou desenvolvedor"
    Seu papel é o de desenvolvedor? Leia:
    
    - https://insper.github.io/bits-e-proc/commum-content/util/Util-vixi-sou-dev/

Esse projeto tem como objetivo trabalhar com portas lógicas e sistemas digitais combinacionais (sem um clock) em FPGA e MyHDL. Os elementos lógicos desenvolvidos nessa etapa serão utilizados como elementos básicos para a construção do computador. 

## Instruções

O desenvolvimento será na linguagem MyHDL, o grupo deve se organizar para implementar todos os elementos propostos. O facilitador escolhido será responsável pela completude e consistência do branch master do grupo.

### Integrantes
    
Tarefas devem ser criadas no **Issues** e atribuídas aos demais colegas.
As tarefas devem ser resolvidas individualmente! Utilize a ajuda de seus colegas, mas resolva o que foi atribuído a vocês, essa é sua tarefa/ responsabilidade! 
    
!!! warning
    Este  projeto é para ser realizado por todos os integrantes do grupo em seus próprios computadores, quem não participar, não implementar os módulos que foram atribuídos, ou não realizar pull-request não ganhará nota de participação individual.
    
### Controle de Tarefas e Repositório

Nas discussões com os outros colegas o scrum master deve definir os módulos que cada um do grupo irá desenvolver. Crie uma rotina para commits e pull-request. Sempre teste os módulos e verifique se está fazendo o esperado.

=== "Facilitador (Scrum Master)"
    - Fazer a **atualização** do fork com o upstream
    - Organizar o **github + issues + project**
    - Gerenciar o grupo (atribuir tarefas)
    - **Gerenciar os pull-requests**
    - Criar relatório da performance de cada um do grupo
    - Entregar/Apresentar o projeto no final 

=== "Desenvolvedores"
    - Realizar as tarefas atribuidas pelo scrum-master
    - Ajudar na entrega final 
    - Testar os códigos
    - Realizar os pull-requests

### Testes

Cada módulo da entrega possui um teste de unidade (similar ao dos labs), para executar o teste rode:

```py
pytest -k hw/componentes.py -k MODULO
```

- MODULO: Módulo a ser testado

### Configurando Testes CI

Cada desenvolvedor além de editar o arquivo `hw/components.py` deve editar o arquivo `.github/workflows/ components.yml` adicionando o teste referente ao modulo que implementou.

!!! example
    Exemplo de como testar o componente `and16`.

    ``` yml title=".github/workflows/componentes.yml"
    - name: Test and16
      run: |
        pytest hw/test_components.py -k and16
    ```
    
    Para testar mais módulos basta replicar o bloco anterior:
    
    ``` yml title=".github/workflows/componentes.yml"
    - name: Test and16
      run: |
        pytest hw/test_components.py -k and16

    - name: Test or16
      run: |
        pytest hw/test_components.py -k or16
    ```

## Entrega

A entrega **final** deve ser feita no ramo `master` do git.

- [ ] Implementar todos os módulos listados
- [ ] Todos os módulos devem passar nos testes
- [ ] Actions deve estar configurado e funcionando

### Rubricas para avaliação do projeto

Cada integrante do grupo irá receber duas notas: Uma referente ao desenvolvimento total do projeto (Projeto) e outra referente a sua participação individual no grupo.

### Conceito C

- `and16(a, b, q)`
- `or8way(a, b, c, d, e, f, g, h, q)`
- `orNway(a, q)`
- `barrelShifter(a, dir, size, q)`
- `mux2way(q, a, b, sel)`
- `mux4way(q, a, b, c, d, sel)`
- `mux8way(q, a, b, c, d, e, f, g, h, sel)`
- `deMux2way(a, q0, q1, sel)`
- `deMux4way(a, q0, q1, q2, q3, sel)`
- `deMux8way(a, q0, q1, q2, q3, q4, q5, q6, q7, sel)`

### Conceito B

- `bin2bcd(b, bcd1, bcd0)`
- `test_bin2bcd`
- `toplevel.py`

Para o conceito B vocês devem desenvolver um módulo e seu teste que converte um valor binário (`b`) para
BCD (não é necessário testar na FPGA), a ideia de uso deste componente é: Poder exibir um valor de 00 até 99 nos displays de 7segmentos.

Além de desenvolverem o módulo  `components.py bin2bcd` vocês devem criar um teste que irá ajudar vocês verificar se o componente foi implementando corretamente. A entrega final deve ser o `bin2bcd` e o teste `test_components.py test_bin2bcd`, eu já dei um template do teste pronto no arquivo `test_components.py`, o teste deve tentar ser genérico e validar vários cenários.

Exemplo:

```
dig1 = Signal(modbv(0))
dig2 = Signal(modbv(0))
bin2bcd(72, dig1, dig0)
print(dig1)
>> 7
print(dig0)
>> 2

bin2bcd(84, dig1, dig0)
print(dig1)
>> 8
print(dig0)
>> 4
```

!!! tip
    Você pode implementar usando uma [look-up-table](https://en.wikipedia.org/wiki/Lookup_table) com uma [ROM em MyHDL](http://docs.myhdl.org/en/stable/manual/conversion_examples.html?highlight=rom#rom-inference), ou se preferir é possível fazer uma tabela verdade e encontrar as equações (vai dar um certo trabalho). Mas podem usar o [SymPy](https://docs.sympy.org/latest/modules/logic.html) que encontra uma equação booleana de uma tabela verdade (e você gera a tabela de um script...). Existe outra solucão que seria usar um algorítimo chamada de [Double dabble](https://en.wikipedia.org/wiki/Double_dabble).

### Conceito A

Para validar vocês devem programar a FPGA e gravar um vídeo do mesmo funcionando (mudando as chaves sw exibindo o valor nos dois hex).

![](figs/comb/comb-proj-b.svg){width=300}

- Vocês devem copiar o módulo `bin2hex` que desenvolveram no laboratório 5 para o `components.py`.

O `toplevel.py` já está configurado para testar na FPGA, usando as chaves SW como input:

```py
    bc0 = Signal(intbv[4])
    bc1 = Signal(intbv[4])
    hex0 = Signal(intbv[7:])
    hex1 = Signal(intbv[7])

    ic1 = bin2bcd(SW[8:], bc1, bc0)
    ihex1 = bin2hex(hex1, bc1)
    ihex0 = bin2hex(hex0, bc0)
```

### Formulários

- O scrum deve preencher este: https://docs.google.com/forms/d/e/1FAIpQLScf_G8nLvN45edhR7o043xig2aAWB8jb9ZSM6yCvbHP7DziZA/viewform?usp=sf_link

- Os desenvolvedores devem preencher este: https://docs.google.com/forms/d/e/1FAIpQLScYtzwG9xI6Aef3hWBJSD6GocEyhZC05NsEXzCVK3C7aKGZ-Q/viewform?usp=sf_link
