# Lab 12 (nasm) Saltos

| Lab 12                                                                      |
|-----------------------------------------------------------------------------|
| **Data limite para entrega**: =={{lab_12_deadline}}==                       |
| Entregue o código pelo repositório do ==[Classroom]({{lab_11_classroom}})== |

!!! info "💰 Laboratório com pontos"
    Algumas tarefas deste laboratório fornecem pontos de nota individual (hardware ou software), os exercícios marcados com 💰 são os que fornecem os pontos. Os pontos apenas são validados quando contabilizados pelo CI do github. Fiquem atentos para o deadline da entrega.
    
    Neste laboratório você pode receber até: **({{lab_11_points}})**.

Ao final desse lab você deve ser capaz de:

- Escrever programas complexos em assembly que envolvem acesso a memória e saltos (condicionais e incondicionais)

!!! tip
    Para fazer esse lab, você deve ter lido a teoria sobre:
    
    - [mapa de memória](https://insper.github.io/Z01.1/Teoria-Z01-mapadeMemoria/)
    - [jump](https://insper.github.io/Z01.1/Teoria-nasm-jump/)

!!! note
    Dúvidas sobre assembly? [Z01->Resumo Assembly](https://insper.github.io/Z01.1/Util-Resumo-Assembly/)

Esse lab deve ser feito no Z01Simulador, para abrir o programa basta digitar no terminal, `bits gui nasm` com o **env ativado!**

## Incondicional

<!--
!!! exercise "lcd1.nasm" 
    - File: `lcd1.nasm`
    - Test: Visual no simulador
    
    Task: Preencha todos os px do LCD de preto!
    
    === "resultado esperado"
        ![](figs/F-Assembly/lab2-jmp1.png){width=350}
        
    === "solucão"
        
        Irei usar o RAM[0] para salvar o contador, que será incrementado a partir do endeço base do LCD `16384` até a onde o programa executar.
        
        > Neste exemplo, o valor final do loop não está sendo controlado!!
        
        ```nasm
        leaw $16384, %A
        movw %A, %D
        leaw $0, %A
        movw %D, (%A)
        
        LOOP:
          leaw $0, %A
          movw (%A), %D
          addw $1, %D, (%A)
          movw %D, %A
          movw $-1, (%A)
          leaw $LOOP, %A
          jmp
          nop
        ```
-->

## Condicional

Saltos condicionais são utilizados para verificarmos condições no programa, vamos trabalhar um pouco com isso.


!!! exercise "jmp1.nasm" 
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
    
    ```py
    # modifique o test_nasm.py incluindo:
    
    @pytest.mark.telemetry_files(source('jmp1.nasm'))
    def test_jmp1_if():
        ram = {0: 0, 1: 0}
        tst = {0: 1}
        assert nasm_test("jmp1.nasm", ram, tst)

    @pytest.mark.telemetry_files(source('jmp1.nasm'))
    def test_jmp1_else():
        ram = {0: 0, 1: 3}
        tst = {0: 2}
        assert nasm_test("jmp1.nasm", ram, tst)
    ```
    
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
        leaw $1, %A
        movw $1, (%A) ; RAM[=] = 1
        END:          
        ```
        
!!! exercise "jmp2.nasm" 
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
        
    Modifique o `test_nasm.py`:
    
    ```py
    # modifique o test_nasm.py incluindo:
    
    @pytest.mark.telemetry_files(source('jmp2.nasm'))
    def test_jmp2_if():
        ram = {0: 0, 1: 3}
        tst = {0: 1}
        assert nasm_test("jmp2.nasm", ram, tst)

    @pytest.mark.telemetry_files(source('jmp2.nasm'))
    def test_jmp2_else():
        ram = {0: 0, 1: 5}
        tst = {0: 2}
        assert nasm_test("jmp2.nasm", ram, tst)
    ```
        
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

!!! exercise "💰 ({{lab_11_points}})"
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
    
    Modifique o `test_nasm.py` incluindo:
    
    ```py
    # modifique o test_nasm.py incluindo:
    
    @pytest.mark.telemetry_files(source('jmp3.nasm'))
    def test_jmp3_if_equal():
        ram = {0: 0, 1: 1, 2: 2}
        tst = {0: 1}
        assert nasm_test("jmp3.nasm", ram, tst)

    @pytest.mark.telemetry_files(source('jmp3.nasm'))
    def test_jmp3_if_gt():
        ram = {0: 0, 1: 2, 2: 2}
        tst = {0: 1}
        assert nasm_test("jmp3.nasm", ram, tst)

    @pytest.mark.telemetry_files(source('jmp3.nasm'))
    def test_jmp3_else():
        ram = {0: 0, 1: 2, 2: 0}
        tst = {0: 2}
        assert nasm_test("jmp3.nasm", ram, tst)
    ```

        
<!--

!!! example "jmp4.nasm" 
    - File: `jmp4.nasm`
    - Test: Visual
    
    Task: Acione a metade superior dos pxs do LCD de preto.
    
    ![](figs/F-Assembly/lab2-jmp5.png){width=350}
-->
