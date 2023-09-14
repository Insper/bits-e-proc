# Lab 8: ULA 

O objetivo desse laboratório é o de trabalharmos com o controle dos sinais da ULA para entendermos as operações da unidade de processamento do nosso computador. Para isso iremos:

1. Executando o simulador
1. Controlando ULA para realizar operações específicas (exercícios)
1. Programar a FPGA na ULA e realizar operações.

## Simulador

Iremos utilizar um simulador da ULA feito em python + Qt. Siga os passos a seguir (execute no seu computador):

```sh
git clone https://github.com/eduardomarossi/z01.1-ula
cd z01.1-ula
pip3 install -r requirements.txt
python3 main.py
```

Você deve obter a seguinte interface:

![](https://raw.githubusercontent.com/eduardomarossi/z01.1-ula/master/image.png)

## Controlando ULA

Com o simulador podemos testar a ULA modificando seus sinais de controle. A seguir uma proposta de operações lógicas que devem ser realizadas na ULA, seus sinais de controle e resultados devem ser anotados nas tabelas.

Para cada exercício, anote a operação no papel e entenda o que está acontecendo.

!!! exercise
    ```
    out = X
    ```
    Configure os controles da ULA para fazer com que a saída da ULA seja a entrada **X**
    
!!! exercise 
    ```
    out = Y
    ```
    Configure os controles da ULA para fazer com que a saída da ULA seja a entrada Y

!!! exercise 
    ```
    out = !Y
    ```
    Configure os controles da ULA para fazer com que a saída da ULA seja a entrada a entrada Y negada

!!! exercise 
    ```
    out = 0
    ```
    Faça com que a saída da ULA seja 0

!!! exercise 
    ```
    out = 1
    ```
    Faça com que a saída da ULA seja 1

!!! exercise 
    ```
    out = -1
    ```
    Faça com que a saída da ULA seja -1 (em complemento de 2)

!!! exercise 
    ```
    out = X+Y
    ```
    Faça com que a saída da ULA seja a entrada X + a entrada Y

!!! exercise "(difícil)"
    ```
    out = X or Y
    ```
    Faça com que a saída da ULA seja X ou Y

!!! exercise "(difícil)"
    ```
    out = X - Y
    ```
    Faça com que a saída da ULA seja a entrada X menos a entrada Y

## Executando na FPGA

Podemos executar a ULA na FPGA, para isso iremos disponibilizar o binário da FPGA com a ULA já implementada, o arquivo está dentro da pasta do lab da ula e é chamado de [Z011-ULA.rbf`](https://github.com/Insper/bits-e-proc-lab-6-adders/blob/main/Z011-ULA.rbf). 

!!! exercise
    Use o programa fpgaLoader para carregar esse projeto na FPGA

Agora basta controlar as chaves da FPGA e ver o resultado da ULA nos LEDS. Note que as entradas X e Y da ula são fixas em:

- X: `01110011`
- Y: `01011111`

Repita algumas operações realizados no simulador.

![](figs/D-ULA/D-ula-fpga-1.png)
![](figs/D-ULA/D-ula-fpga-2.png)
