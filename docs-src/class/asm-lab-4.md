# Lab 13: (nasm) Praticando

| Lab 13                                                                          |
|---------------------------------------------------------------------------------|
| **Data limite para entrega**: =={{lab_nasm_4_deadline}}==                       |
| Entregue o código pelo repositório do ==[Classroom]({{lab_nasm_4_classroom}})== |
| Pontos: {{lab_nasm_4_points}}                                                   |

Ao final desse lab você deve ser capaz de:

- Fazer programas mais complexos em assembly 

Os seguintes programas são contemplados nesse lab:

- max
- abs
- mult ==(muito importante estudar!)==
- div ==(muito importante estudar!)==

Os problemas desse lab possuem teste unitário, sugerimos utilizarem o simulador junto com os testes para melhor entendimento do programa.

!!! exercise "💰 Pontos"
    - File: `max.nasm`
    - Test: `pytest -k max`
    
    O maior valor que estiver, ou em R0 ou R1 sera copiado para R2 
    Estamos considerando número inteiros:
    
    `RAM2 = max(RAM[0], RAM[1])`
 
!!! exercise "💰 Pontos"
    - File: `abs.nasm`
    - Test: `pytest -k abs`
   
    Copia o valor de RAM[1] para RAM[0] deixando o valor sempre positivo.

!!! exercise "💰 Pontos"
    - File: `mult.nasm`
    - Test: `pytest -k mult`
 
    Multiplica o valor de RAM[1] com RAM[0] salvando em RAM[3]

!!! exercise "💰 Pontos"
    - File: `div.nasm`
    - Test: `pytest -k div`
    
    Realiza uma divisão de inteiros entre R0 e R1 valores e armazena R2 
