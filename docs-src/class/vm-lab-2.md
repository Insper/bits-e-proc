# Lab 13: VM

| Lab 13                                                                        |
|-------------------------------------------------------------------------------|
| **Data limite para entrega**: =={{lab_vm_2_deadline}}==                        |
| Entregue o código pelo repositório do ==[Classroom]({{lab_vm_2_classroom}})== |
| =={lab_vm_2_points}==                                                         |


## Funções

Vamos agora fazer o uso de funções em VM, o que irá nos permitir fazer as seguintes operações: $10/2 + 15*3*\sqrt{121}/2^5$, lembre que no nosso hardware não possuímos os operadores de multiplicação, divisão, raiz quadrada e muito menos exponencial. Mas com o uso de funções podemos implementar isso em código e usar para implementar a equação anterior.

```
div(10,2) + div(mult(mult(15,3), sqrt(121.2))), exp(2,5))
``` 

- note que os operadores viraram chamadas de funções.

!!! info "TEORIA"
    Leia a [Teoria/VM - Funções](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-vm-funcoes/) antes de seguir.
    
Vamos agora trabalhar com funções na nossa VM, implementem os códigos a seguir:

!!! exercise "💰 (0 HW/ 2 SW) call"
    - File: `2a-calculadora/Main.vm`
    - Teste: `pytest -k 2a`
    
    Neste exercício a funções `mult` já foi dada pronta, você deve agora apenas fazer uso dela na função `main`.
    
!!! exercise "💰 (0 HW/ 2 SW) div function"
    - File: `2b-calculadora/div.vm`
    - Teste: `pytest -k 2b`

    Neste exercício você deve implementar uma funções `div` que recebe dois argumentos e faz a divisão. Para isso, declare no comeco do arquivo: `function div X` onde X é o número de variáveis temporária que deseja utilizar.

!!! exercise "💰 (0 HW/ 4 SW) pow"
    - File: `2c-calculadora/pow.vm`
    - Teste: `pytest -k 2c`

    Neste exercício você deve implementar uma funções `pow` que recebe dois argumentos e faz `x^y`, onde **x** é o primeiro argumento e **y** o segundo. Para isso, declare no comeco do arquivo: `function pow X` onde X é o número de variáveis temporária que deseja utilizar. Note que na pasta existe a funçõe `mult`, faća uso dela!
