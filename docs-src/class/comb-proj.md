# B - Lógica Combinacional

| Data da entrega |
|-----------------|
| ??              |

- Arquivo: `hw/components.py`

![](figs/LogiComb/sistema-comb.svg)

!!! tip "Scrum Master"
    Você é `Scrum Master` e não sabe por onde começar? De uma olhada nessas dicas: [Vixi! Sou Scrum Master](https://insper.github.io/Z01.1/Util-vixi-sou-scrum/)

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

### Testes CI

!!! info
    preparar os testes..

Cada desenvolvedor além de editar o arquivo `hw/components.py` deve editar o arquivo `.github/workflows/ components.yml` adicionando o teste referente ao modulo que implementou.

!!! example
    Exemplo de como testar o componente `and16`.

    ```yml
    - name: Test Projeto B
      run: |
        pytest hw/test_components.py -k and16
    ```

## Entrega

A entrega **final** deve ser feita no ramo `master` do git.

- [ ] Implementar todos os módulos listados
- [ ] Todos os módulos devem passar nos testes
- [ ] Actions deve estar configurado e funcionando

### Rubricas para avaliação do projeto

Cada integrante do grupo irá receber duas notas: Uma referente ao desenvolvimento total do projeto (Projeto) e outra referente a sua participação individual no grupo.

=== "Grupo"
    Para atingir os objetivos A e B, deve-se antes atingir o C.
    
=== "Individual"
    As rubricas a serem seguidas serão comuns a todos os projeto e está descrito no link:

    - [Rubricas Scrum e Desenvolvedor](/Z01.1/Sobre-Rubricas/)

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

### Conceito A

### Formulários
