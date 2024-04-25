# Mundo Real

| HW | SW |
|----|----|
| 15 | 10 |

Fornece **15 pontos** de **Hardware** e **10 pontos** de **Software**. 

Mini projeto individual de bits e processadores, na qual vocês vão estudar um processador real.

## Processadores

Você deverá escolher um dos processadores listados a seguir:

!!! Info
    Escolher um processador da lista a seguir e coloque o seu nome na planilha:
    
    ==Não pode repetir!==
    
    - https://docs.google.com/spreadsheets/d/1mH5wtVWM12W8EY2jeRJ3-DBCcob1pC0D3yUPiQZnUD4/edit?usp=sharing
    
## Entrega

Você deve entregar um vídeo que explica a CPU em questão, este vídeo ==de aproximadamente 10 minutos== deve conter:

- Explicativo do hardware
- Código Assembly Comentado

A entrega deve ser realizada pelo link a seguir, o vídeo deve estar no youtube (lembre de deixar acessível para qualquer um com o link):

!!! tip
    ==Muito importante que sempre que possível realizar uma comparação com a nossa CPU==
    
### (**15 HW**) CPU

- Histórico
    - [ ] História da arquitetura
    - [ ] Pessoas/ empresas responsáveis
    - [ ] Impacto histórico, impacto nos concorrentes/ comunidade/
    - [ ] Curiosidades
    
- Dispositivos, produtoes e empresas que fazem ou fizeram uso da CPU
    
- Arquitetura: Descreva a arquitetura interna da CPU
 
    - [ ] Quantos bits de largura? 8/16/32/..
    - [ ] Quantidade de registradores
    - [ ] Operações da ULA (se for muitas, pode pegar algumas)
    - [ ] A arquitetura é CISC ou RISC?
    - [ ] Qual tipo da CPU? 
        - [Stack Register](https://en.wikipedia.org/wiki/Stack_register), [Processor register](https://en.wikipedia.org/wiki/Processor_register), [Accumulator](Accumulator Register))
    - [ ] Como o Program Counter (PC) funciona? 
    - [ ] Como é realizado o acesso a memória nessa arquitetura? 
        - registrador-registrador, registrador-memória, memória-memória
        - Pode fazer operações direto na memória? Ou temos que carregar para os registradores antes?

- Instruções
    - [ ] Descritivo das instruções e seus padrões
    - [ ] Quantidade total de instruções
    - [ ] Diferença com relação ao Z01.1 

### (**10 SW**) Comentar código

Você deve pegar um código de exemplo do assembly da CPU escolhida e comentar ele no vídeo, explicando o que está fazendo.

- Explicar o que cada instrução está fazendo
- O impacto dela no hardware
- Muitas arquitetura possuem simulador! Interessante usar, mas não é necessário
