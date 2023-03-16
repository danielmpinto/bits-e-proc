# Lab 14: (nasm) Praticando

Ao final desse lab você deve ser capaz de:

- Fazer programas complexos em assembly 

Os seguintes programas são contemplados nesse lab:

- max
- abs
- mult ==(muito importante estudar!)==

Os problemas desse lab possuem teste unitário, sugerimos utilizarem o simulador junto com os testes para melhor entendimento do programa.


!!! exercise "max.nasm" 
    - File: `max.nasm`
    - Test: `pytest -k max`
    
    O maior valor que estiver, ou em R0 ou R1 sera copiado para R2 
    Estamos considerando número inteiros:
    
    `RAM2 = max(RAM[0], RAM[1])`
 
!!! exercise "abs.nasm" 
    - File: `abs.nasm`
    - Test: `pytest -k abs`
   
    Copia o valor de RAM[1] para RAM[0] deixando o valor sempre positivo.

!!! exercise "mult.nasm" 
    - File: `mult.nasm`
    - Test: `pytest -k mult`
 
    Multiplica o valor de RAM[1] com RAM[0] salvando em RAM[3]
