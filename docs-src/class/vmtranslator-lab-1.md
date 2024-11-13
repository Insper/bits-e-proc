# Lab 14 - VM translator

Neste laboratório iremos implementar parte do código que executa a tradução do VM para NASM.

## Estrutura

O VMtranslator já foi fornecido quase todo pronto (ufa!!) vocês só precisam implementar a parte que faz a tradução de um comando `vm` (pilha) em `nasm` (registrador-memória). 

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

### Como o teste funciona?

Com o teste passando, abra a pasta `test_assets` e repare que vários arquivos foram criados, para cada teste temos um arquivo `.vm` (neste caso `add.vm`) que gera um arquivo `.nasm` (no exemplo `add.nasm`) que possui o comando `VM` traduzido para assembly, este arquivo então é passado pelo assembler que gera o `add.hack`. Com o arquivo de linguagem de máquina, uma simulacão é executada e o teste realizado (analisasse os valores na memória RAM).
