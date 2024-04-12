# Lab 12: VM

| Lab 12                                                                      |
|-----------------------------------------------------------------------------|
| **Data limite para entrega**: =={{lab_12_deadline}}==                       |
| Entregue o código pelo repositório do ==[Classroom]({{lab_12_classroom}})== |
| =={lab_12_points}==                                                            |

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

!!! exercise "💰 (0 HW/ 1 SW) add"
    - File: `1a-add.vm`
    - Teste: `pytest -k 1a`

    A descrição do que deve ser feito está nos comentários dos arquivos.
    
    ==Tip: Para salvar em `temp 0` use: `pop temp 0`.==

!!! exercise "💰 (0 HW/ 1 SW) calc"
    - File: `1b-calc.vm`
    - Teste: `pytest -k 1b`

Você notou que nesses códigos pedimos para salvar o resultado em `temp 0`, fazemos
isso pela operação de `pop temp 0`. Vamos estudar um pouco a respeito disso:

## goto (jump)

Nossa linguagem vm suporta realizar condições e loops, vamos ver como isso é feito e praticar um pouco!

!!! info "TEORIA"
    Leia a [Teoria/VM - jump](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-vm-jump/) antes de seguir.
    
!!! exercise "💰 (0 HW/ 2 SW) loop"
    - File: `1c-loop.vm`
    - Teste: `pytest -k 1c`
    
!!! exercise "💰 (0 HW/ 2 SW) div"
    - File: `1d-div.vm`
    - Teste: `pytest -k 1d`
    
!!! exercise "💰 (0 HW/ 2 SW) mult"    
    - File: `1e-mult.vm`
    - Teste: `pytest -k 1e`
