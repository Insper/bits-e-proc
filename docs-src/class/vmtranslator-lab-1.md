# Lab 17 - VM translator

| Lab 17                                                                      |
|-----------------------------------------------------------------------------|
| **Data limite para entrega**: =={{lab_17_deadline}}==                       |
| Entregue o código pelo repositório do ==[Classroom]({{lab_17_classroom}})== |
| =={lab_17_points}==                                                            |

Neste laboratório iremos implementar parte do código que executa a tradução do VM para NASM.

!!! info
    Lembre de autenticar na telemetria, executando uma única vez no terminal:
    
    - `telemetry auth`

## Estrutura

O VMtranslator já foi fornecido quase todo pronto (ufa!!) vocês só precisam implementar a parte que faz a tradução de um comando `vm` (pilha) em `nasm` (registrador-memória). O único arquivo que vocês vão precisar mexer de todo o repositório é o `Code.py`. Mas se tiver energia, de uma olhada na estrutura geral do projeto.

## LAB

Vamos implementar parte do VMtranslator.

### Aritmética

Vamos comecar o lab implementando a operacoes aritméticas, mais especifica a de `add` (que soma dois elementos na pilha), abra o código do `Code.py` e procure pelas linhas:

```py
if command == "add":
    pass # TODO
```

A variável `command` é um vetor (na verdade ela vai virar um vetor de strings), é nesta variável que iremos adicionar as instruções assembly que irão realizar a operação de `add`, isso deve ser feito da seguinte maneira:

```py
if command == "add":
    commands.append("leaw $SP,%A")
    commands.append("movw (%A),%D")
    commands.append("decw %D")
    ...
    ...
```

No final do método o programa salva as instruções assembly relativos ao comando `vm` no arquivo `.nasm`.

!!! tip ""
    Você pode remover o `pass`, eu só coloco para o pytest não reclamar que o código python está errado.

!!! exercise
    - File: `/Code.py`
    - Command: `add`
    - Test: `pytest -k add`
    
    Termine de implementar o comando `add` e teste com `pytest -k add`

### Como o teste funciona?

Com o teste passando, abra a pasta `test_assets` e repare que vários arquivos foram criados, para cada teste temos um arquivo `.vm` (neste caso `add.vm`) que gera um arquivo `.nasm` (no exemplo `add.nasm`) que possui o comando `VM` traduzido para assembly, este arquivo então é passado pelo assembler que gera o `add.hack`. Com o arquivo de linguagem de máquina, uma simulacão é executada e o teste realizado (analisasse os valores na memória RAM).

## Praticando

Agora vamos praticar um pouco.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Command: `neg`
    - Test: `pytest -k neg`
    
    Implemente o comando `neg` e teste com `pytest -s -k neg`.
    
    Dica: Faça no papel antes e só depois implemente.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Command: `neg`
    - Test: `pytest -k sub`
    
    Implemente o comando `sub` e teste com `pytest -s -k sub`.
    

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writePush`
    - Command: `push constant`
    - Test: `pytest -s -k push_constant`
 
    Agora implemente um comando de uma outra classe, a do push. Procure pelo comando na classe `writePush`.

Os próximos exercícios são de classe diferente da aritméticas.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writePop`
    - Command: `pop local`
    - Test: `pytest -s -k pop_local`
 
    Implemente o comando `pop local`.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writePop`
    - Command: `pop temp`
    - Test: `pytest -s -k pop_temp`
 
    Implemente o comando `pop temp N`.
    
    > Dica: Você vai precisar do argumento `index` que fornece o valor de N.

!!! exercise
    - File: `sw/vmtranlator/Code.py`
    - Method: `writeArithmetic`
    - Command: `gt`
    - Test: `pytest -s -k gt`
 
     Implemente o comando `gt`. 
    
    Dica: Você vai ter que fazer um label para poder saltar, mas o label tem que ser único em todo o código `nasm` criado, para isso, utilize a função `self.getUniqLabel()` que retorna uma string única em todo o programa. 


!!! exercise
    Tem uma infinidade de comandos para implementar, todos possuem teste. Você pode brincar e estudar mais por conta. 
    
    A parte mais díficil é o `call` e o `return`.
