# Lab 6: ULA 

O objetivo desse laboratório é o de trabalharmos com o controle dos sinais da ULA para entendermos as operações da unidade de processamento do nosso computador. Para isso iremos:

1. Programar a ULA na FPGA
1. Responder o google forms usando a FPGA para validar as operações

## Executando na FPGA

Podemos executar a ULA na FPGA, para isso iremos disponibilizar o binário da FPGA com a ULA já implementada. Faća o download do arquivo:

- [Z011-ULA.rbf](https://github.com/Insper/bits-e-proc-lab-6-adders/blob/main/Z011-ULA.rbf)
- Abra o FPGA LOADER
- Programe a FPGA

!!! warning
    Nós já estamos fornecendo uma ULA pronta, não precisam desenvolver ela em myhdl! 

!!! exercise
    Use o programa fpgaLoader para carregar esse projeto na FPGA

Agora basta controlar as chaves da FPGA e ver o resultado da ULA nos LEDS. Note que as entradas X e Y da ula são fixas em:

- X: `01110011`
- Y: `01011111`

Repita algumas operações realizados no simulador.

![](figs/D-ULA/D-ula-fpga-1.png)
![](figs/D-ULA/D-ula-fpga-2.png)

## Controlando ULA

Com o simulador podemos testar a ULA modificando seus sinais de controle. A seguir uma proposta de operações lógicas que devem ser realizadas na ULA, seus sinais de controle e resultados devem ser anotados nas tabelas.

Para cada exercício, anote a operação no papel e entenda o que está acontecendo, use o simulador para validar e testar as operações.

## Simulador

Quer testar em casa? Use simulador da ULA feito em python + Qt. Siga os passos a seguir (execute no seu computador Linux):

```sh
git clone https://github.com/eduardomarossi/z01.1-ula
cd z01.1-ula
pip3 install -r requirements.txt
python3 main.py
```

!!! info "Dica"
   
    Caso o programa não abrir, tente instalar esses pacotes a seguir" 

    ```sh
    sudo apt-get install '^libxcb.*-dev' libx11-xcb-dev libglu1-mesa-dev libxrender-dev libxi-dev libxkbcommon-dev libxkbcommon-x11-dev
    ```

Você deve obter a seguinte interface:

![](https://raw.githubusercontent.com/eduardomarossi/z01.1-ula/master/image.png)
