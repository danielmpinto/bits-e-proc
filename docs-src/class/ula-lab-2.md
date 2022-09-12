# Lab 7: Hardware types

Até agora estamos usando **mal** os recursos do MyHDL, o componente `adder` anterior poderia ser muito mais simples se:

1. Pudéssemos tratar sinais como `inteiros` 
1. Não precisássemos implementar o `adder` (x + y)

Para isso o MyHDL possui outros dois tipos de dados além do `bool`: o `intbv` e o `modbv`.

> Hardware design involves dealing with bits and bit-oriented operations. The standard Python type int has most of the desired features, but lacks support for indexing and slicing. For this reason, MyHDL provides the intbv class. The name was chosen to suggest an integer with bit vector flavor.
> 
> Do mamual: http://docs.myhdl.org/en/stable/manual/hwtypes.html

## modbv

!!! info
    A principal diferença entre o `modbv` e o `intbv` é que o sinal do tipo `modbv` trunca o valor da variável para o seu máximo e mínimo, já o `intbv` lança um erro quando isso acontecer. Na implementação do hardware não existe diferença nenhuma. Apenas na execução do módulo a nível de simulação. 

O modbv possibilita trabalharmos com um vetor de bits como se fosse um único bloco de dados, diferente do `bool` na qual os bits não possuem relação entre si. Agora conseguimos trabalhar com valores inteiros (`signed` e `unsigned`) muito similar ao que já estamos acostumados no python:

```py
>>> a = modbv(24)
>>> b = modbv(2)
>>> print(a)
24
>>> print(a + b)
26
>>> print(a == 12)
False
>>> a = b
>>> a
2
```

Notem que conseguimos:

- somar dois vetores de bits `a+b`
- atribuir um vetor a outro `a=b`

O `modbv` não limita a quantidade de bits que será utilizado, isso funciona muito bem na simulação, mas quando formos gerar um hardware temos que definir o tamanho do vetor caso contrário teremos erro na conversão. 

O exemplo a seguir indica como criarmos um sinal `cnt` com 32 bits:

```py
# cnt com 32 bits do tipo modbv
>>> cnt = Signal(modbv(0)[32:])

>>> cnt.max
4294967296

>>> cnt.min
0
```

Outra opcão é definir o tamanho do vetor com base nos valores máximos e mínimos:

```py
a = modbv(12, min=0, max=16)
```

### bits

O `modbv` possibilita acessarmos bits individualmente, assim como fazíamos com o vetor de bits:

```py
>>> from myhdl import bin
>>> a = modbv(24)
>>> bin(a)
'11000'

# Bit indexing

>>> int(a[0])
0
>>> int(a[3])
1
>>> b = modbv(-23)
>>> bin(b)
'101001'
>>> int(b[0])
1
>>> int(b[3])
1
>>> int(b[4])
0
'11000'

# Bit slicing

>>> a[4:1]
modbv(4)
>>> bin(a[4:1])
'100'
>>> a[4:1] = 0b001
>>> bin(a)
'10010'
>>> a
modbv(18)
```

## Add

Usando esse novo tipo, podemos reimplementar o `adder` assumindo que as entradas `x` e `y` e a saída `soma` são vetores, e que `carry` é um `bool`:

```py title="ula_modules.py"
@block
def adderIntbv(x, y, soma, carry):
    @always_comb
    def comb():
        sum = x + y
        soma.next = sum
        if sum > x.max - 1:
            carry.next = 1
        else:
            carry.next = 0

    return comb
```

Note que para o `carry` utilizamos o valor máximo que `x` pode assumir e que isso é dinâmico, de acordo com o tamanho de `x`. Como no exemplo a seguir:

```py title="runAdderIntbv.py"
@block
def runAdder():
    x = Signal(modbv()[2:])
    y = Signal(modbv()[2:])
    s = Signal(modbv()[2:])
    c = Signal(bool())

    dut = adderIntbv(x, y, s, c)
```


!!! exercise
    - File: `ula/ula_modules.py `
    - Módulo: `def adderIntbv(a, b, soma, carry):`
    - Run: `./runAdderIntbv.py`
 

    Implemente o `adderIntbv` como indicado no exemplo anterior e então execute o `runAdderIntbv.py` para testar a implementação.
     
    - Teste com diferentes inputs
    
!!! exercise
    - File: `toplevel.py `
    
    Tarefa: Modifique o `toplevel` para usar o `adderModbv` no lugar do `adder`, e verifique que tudo funciona =).
