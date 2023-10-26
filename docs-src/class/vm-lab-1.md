# Lab 16: VM

| Lab 16                                                                      |
|-----------------------------------------------------------------------------|
| **Data limite para entrega**: =={{lab_16_deadline}}==                       |
| Entregue o código pelo repositório do ==[Classroom]({{lab_16_classroom}})== |
| =={lab_16_points}==                                                            |

!!! info "💰 Laboratório com pontos"
    Algumas tarefas deste laboratório fornecem pontos de nota individual (hardware ou software), os exercícios marcados com 💰 são os que fornecem os pontos. Os pontos apenas são validados quando contabilizados pelo CI do github. Fiquem atentos para o deadline da entrega.
    
    Neste laboratório você pode receber até: **({{lab_16_points}})**.

!!! tip
    - Realizar o laboratório individualmente. Mas trabalhar no grupo e trocar ideias.


No laboratório iremos praticar a linguagem VM para o nosso Z01.1, essa entrega é individual e **vale nota**. Esse laboratório mistura exercícios com leitura de teoria, é essencial que você realize as leituras recomendadas para cada secção e então voltar para fazer os exercícios. 

## Treinando RPN

Primeiro iremos praticar o conceito básico da linguagem VM, que é a notação RPN. Abra o simulador online da calculadora [hp48](http://www.poleyland.com/hp48/) e realize os seguintes cálculos:

1. `12 + 34 + 56 – 78 + 90 – 12`
1. `(12 × 34) + (56 × 78) – (90 × 12)`
1. `3 × (4 + (5 × (6 + 7)))`   (Dica: comece pelo parêntese mais interno)
1. $1/\sqrt{121}$
1. `23^2 – (13 × 9) + (5/7)`

> Exercícios extraídos de: https://hansklav.home.xs4all.nl/rpn/ , no site tem várias dicas muito legais!

## VM 

!!! info "TEORIA"
    Leia:
    
    - [Teoria/VM](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-vm/) antes de seguir.
    - [Teoria/VM - Segmentos](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-vm-segmentos/) antes de seguir.

Agora vamos trabalhar com a nossa vm, vocês terão que implementar os programas a seguir e testar com o pytest:

!!! exercise "💰 (00 HW/ 01 SW) add"
    - File: `1a-add.vm`
    - Teste: `pytest -k 1a`

    A descrição do que deve ser feito está nos comentários dos arquivos.
    
    ==Tip: Para salvar em `temp 0` use: `pop temp 0`.==

!!! exercise "💰 (00 HW/ 01 SW) calc"
    - File: `1b-calc.vm`
    - Teste: `pytest -k 1b`

Você notou que nesses códigos pedimos para salvar o resultado em `temp 0`, fazemos
isso pela operação de `pop temp 0`. Vamos estudar um pouco a respeito disso:

## goto (jump)

Nossa linguagem vm suporta realizar condições e loops, vamos ver como isso é feito e praticar um pouco!

!!! info "TEORIA"
    Leia a [Teoria/VM - jump](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-vm-jump/) antes de seguir.
    
!!! exercise "💰 (00 HW/ 01 SW) loop"
    - File: `1c-loop.vm`
    - Teste: `pytest -k 1c`
    
!!! exercise "💰 (00 HW/ 04 SW) div"
    - File: `1d-div.vm`
    - Teste: `pytest -k 1d`
    
!!! exercise "💰 (00 HW/ 01 SW) mult"    
    - File: `1e-mult.vm`
    - Teste: `pytest -k 1e`

## Funções

Vamos agora fazer o uso de funções em VM, o que irá nos permitir fazer as seguintes operações: $10/2 + 15*3*\sqrt{121}/2^5$, lembre que no nosso hardware não possuímos os operadores de multiplicação, divisão, raiz quadrada e muito menos exponencial. Mas com o uso de funções podemos implementar isso em código e usar para implementar a equação anterior.

```
div(10,2) + div(mult(mult(15,3), sqrt(121.2))), exp(2,5))
``` 

- note que os operadores viraram chamadas de funções.

!!! info "TEORIA"
    Leia a [Teoria/VM - Funções](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-vm-funcoes/) antes de seguir.
    
Vamos agora trabalhar com funções na nossa VM, implementem os códigos a seguir:

!!! exercise "💰 (00 HW/ 01 SW) call"
    - File: `2a-calculadora/Main.vm`
    - Teste: `pytest -k 2a`
    
    Neste exercício a funções `mult` já foi dada pronta, você deve agora apenas fazer uso dela na função `main`.
    
!!! exercise "💰 (00 HW/ 02 SW) div function"
    - File: `2b-calculadora/div.vm`
    - Teste: `pytest -k 2b`

    Neste exercício você deve implementar uma funções `div` que recebe dois argumentos e faz a divisão. Para isso, declare no comeco do arquivo: `function div X` onde X é o número de variáveis temporária que deseja utilizar.

!!! exercise "💰 (00 HW/ 04 SW) pow"
    - File: `2c-calculadora/pow.vm`
    - Teste: `pytest -k 2c`

    Neste exercício você deve implementar uma funções `pow` que recebe dois argumentos e faz `x^y`, onde **x** é o primeiro argumento e **y** o segundo. Para isso, declare no comeco do arquivo: `function pow X` onde X é o número de variáveis temporária que deseja utilizar. Note que na pasta existe a funçõe `mult`, faća uso dela!
