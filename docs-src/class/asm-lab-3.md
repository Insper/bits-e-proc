# Lab 9 - (nasm) Saltos

| Lab 9                                                                     |
|-----------------------------------------------------------------------------|
| Entregue o código pelo repositório do ==[Classroom]({{lab_nasm_2_classroom}})== |

!!! info "💰 Laboratório com pontos"
    Algumas tarefas deste laboratório fornecem pontos de nota individual (hardware ou software), os exercícios marcados com 💰 são os que fornecem os pontos. Os pontos apenas são validados quando contabilizados pelo CI do github. Fiquem atentos para o deadline da entrega.
    
    Neste laboratório você pode receber até: **({{lab_11_points}})**.

Ao final desse lab você deve ser capaz de:

- Escrever programas complexos em assembly que envolvem acesso a memória e saltos (condicionais e incondicionais)

!!! tip
    Para fazer esse lab, você deve ter lido a teoria sobre:
    - [mapa de memória](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-Z01-mapadeMemoria/)
    - [jump](https://insper.github.io/bits-e-proc/commum-content/teoria/Teoria-Assembly/)

!!! note
    Dúvidas sobre assembly? [Z01->Resumo Assembly](https://insper.github.io/bits-e-proc/commum-content/z01/z01-Resumo-Assembly/)

## Condicional

Saltos condicionais são utilizados para verificarmos condições no programa, vamos trabalhar um pouco com isso.


!!! exercise "jmp1 💰 (0 HW/ 1 SW)"
    - File: `jmp1.nasm`
    - File: `test_nasm.py`
    - Test: `pytest -k jmp1`
    
    Implemente o pseudo código a seguir em nasm:
    
    ```python
    if RAM[1] == 0: 
        RAM[0] = 1
    else
        RAM[0] = 2
    ```
    
    Esse módulo não possui teste, então vamos modificar o nosso `test_nasm.py` para testar isso, vamos criar dois testes, um para o caso do `if` e outro para o caso do `else`
    
    Para isso iremos simular dois cenários: 
    
    `if`:
    
    - in: `RAM[0] = 0` / `RAM[1] = 0`
    - out: `RAM[0] = 1`
    
    `else`:
    
    - in: `RAM[0] = 0` / `RAM[1] = 3`
    - out: `RAM[0] = 2`
    
    === "resultado esperado"
        - `test_jmp1_if`: RAM[0] = 1
        - `test_jmp1_else`: RAM[0] = 1
        
    === "dica"
        Podemos reescrever o código para ficar:

        ```python
        RAM[0] = 2
        if RAM[1] == 0: 
            RAM[0] = 1
        ```
    
    === "Solução"
    
        ```nasm
        leaw $2, %A
        movw %A, %D
        leaw $0, %A
        movw %D, (%A) ; RAM[0] = 2
        leaw $1, %A
        movw (%A), %D ; busca valor verificar (RAM[1])
        leaw $END, %A ; prepara salto
        jne           ; RAM[1] == 0?
        nop
        leaw $0, %A
        movw $1, (%A) ; RAM[0] = 1
        END:          
        ```


!!! exercise "jmp2 💰 (0 HW/ 1 SW)"
    - File: `jmp2.nasm`
    - File: `test_nasm.py`
    - Test: `pytest -k jmp2`
    
    Implemente o pseudo código a seguir em nasm:
    
    ```python
    if RAM[1] == 3: 
        RAM[0] = 1
    else:
        RAM[0] = 2
    ```
    
    Este exercício também não possui teste, podemos seguir o mesmo formato do anterior:
        
    - Teste 1: RAM[1] = 3
    - Teste 2: RAM[1] = 0
        
    === "dica"
        Não temos uma instrução de jmp que verifica se o valor de `%D` é igual a 3, porém podemos subtrair **3** do calor salvo em RAM[1] e verificar se o resultado é igual a 0:
        
        ```python
        RAM[0] = 2
        if RAM[1] - 3 == 0: 
            RAM[0] = 1
        ```
        
        ```nasm
        leaw $1, %A
        movw (%A), %D
        leaw $3, %A
        subw %D, %A, %D ; %D = RAM[1] - 3
        ```

!!! exercise "💰 (0 HW/ 1 SW)"
    - File: `jmp3.nasm`
    - File: `test_nasm.py`
    - Test: `pytest -k jmp3`
    
    Implemente o pseudo código a seguir em nasm:
    
    ```python
    if RAM[1] + RAM[2] >= 3: 
        RAM[0] = 1
    else
        RAM[0] = 2
    ```
