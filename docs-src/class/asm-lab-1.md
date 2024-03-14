# Lab 8: (nasm) Assembly 

| Lab 8                                                                       |
|-----------------------------------------------------------------------------|
| Entregue o código pelo repositório do ==[Classroom]({{lab_nasm_1_classroom}})== |

!!! info "💰 Laboratório com pontos"
    Algumas tarefas deste laboratório fornecem pontos de nota individual (hardware ou software), os exercícios marcados com 💰 são os que fornecem os pontos. Os pontos apenas são validados quando contabilizados pelo CI do github. Fiquem atentos para o deadline da entrega.
    
    Neste laboratório você pode receber até: **({{lab_nasm_1_points}})**.

Ao final desse lab você deve ser capaz de:

1. Usar o simulador gráfico 
1. Fazer pequenas modificações em um código assembly
1. Depurar a execução do assembly
    
## Simulador

Nosso código assembly pode ser executado em hardware de verdade (FPGA) porém nesse primeiro momento iremos trabalhar em um ambiente simulado que nos dará maior facilidade de programação e depuração.

Um pouco de contexto: O livro texto (The Elements Of Computer System) disponibiliza um simulador da CPU original todo escrito em java, esse código é fechado e não permite nenhuma customização. Em 2017 o Prof. Luciano Pereira iniciou a criação de um simulador Z0 (versão anterior) também em Java, onde teríamos controle total do software.

Percebemos alguns pontos negativos de utilizar um simulador em Java sendo o principal: Qualquer alteração no Hardware iria demandar uma alteração no simulador, sendo necessário mantermos dois projetos independentes e sincronizados.

Nesta versão do curso iremos utilizar um simulador que utiliza uma implementacão em MyHDL como descrição da CPU (e de tudo envolvido), uma alteração no hardware irá automaticamente alterar o simulador e o comportamento do computador.

O simulador possui como entradas (para cada simulação): a arquitetura do computador (hardware); o conteúdo da memória RAM o conteúdo da memória ROM e um tempo de execução.

Após o término da simulação é exportado diversos sinais internos da CPU, o estado final da memória RAM e ROM. Esses sinais são então lidos pela interface gráfica e exibida de uma forma amigável, ou usados nos testes.

## Testando

Temos um pytest para testar a execucao do programa, para executar pasta usar o mesmo padrão dos anteriores: 

```
pytest -s -k MODULO
```

Esse script:

1. Inicializa a memória RAM com valores pré estabelecidos 
1. Converte o `nasm` para `hack` e inicializa a memória ROM
1. Executa o Hardware por um tempo
1. Compara a memória RAM após a simulação com um padrão de testes.

Exemplo de teste:

```py
def test_exe1():
    ram = {0: 0}
    tst = {10: 5}
    assert nasm_test("exe1.nasm", ram, tst)
```

Onde:

- `ram`: É a memória RAM inicial da aplicação
- `tst`: É o teste que será executado na memória RAM ao final do processamento

!!! exercise
    Abra o arquivo `exe1.nasm` e implemente o código a seguir que supostamente faz:
    
    - RAM[10] = 5
    
    Código
    
    ```nasm
    leaw $5, %A
    movw %A, %D
    leaw $10, %A
    movw %D, %A
    ```
    
    Execute o teste: 
    
    ```
    pytest -s -k exe1
    ```
    
    E repare que o código ==falha==.
    
### Entendendo o problema

O código anterior falha, e agora precisamos entender o que está acontecendo com ele, para isso vamos depurar a execução do código assembly, para isso utilize o comando a seguir:

```
bits debug nasm exe1
```
    
> Note que toda teste gera um arquivo com extensão `.lst`, este arquivo possui a execucao passo a passo do código na nossa CPU.

Você deve obter algo assim:

```
┏━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━┳━━━━┳━━━━━┓
┃ pcount ┃ OP           ┃ %A ┃ %D ┃ RAM ┃
┡━━━━━━━━╇━━━━━━━━━━━━━━╇━━━━╇━━━━╇━━━━━┩
│ 1      │ leaw $5, %A  │ 0  │ 0  │     │
│ 2      │ movw %A, %D  │ 5  │ 0  │     │
│ 3      │ leaw $10, %A │ 5  │ 5  │     │
│ 4      │ movw %D, %A  │ 10 │ 5  │     │
└────────┴──────────────┴────┴────┴─────┘
RAM FINAL (APENAS ENDERECOS ALTERADOS)
┏━━━━━━━━━┳━━━━━━━┓
┃ Address ┃ Value ┃
┡━━━━━━━━━╇━━━━━━━┩
└─────────┴───────┘
```

!!! exercise short question
    Consegue entender o que está errado?
    
    !!! answer
        Note que não fazemos nenhuma escrita na memória RAM, a última instrução deveria ser: 
        
        ```diff
        - movw %D, %A
        + movw %D, (%A)
        ```
        
        O `(%A)` indica que deve salvar o resultado de `%D` onde `%A` aponta, ou seja, `RAM[%A]=%D`. 

!!! exercise
    1. Corrija o código anterior
    1. Teste com `pytest -k exe1`
    1. Analise a execução com `bits debug nasm exe1`

## 💰  Praticando

Vamos praticar um pouco agora programar em assembly, no começo parece bem difícil, mas com a prática as coisas vão ficando mais fáceis.

!!! info
    Consulte a teoria e o resumo das instruções: [AssemblyZ1](https://insper.github.io/bits-e-proc/commum-content/z01/z01-Resumo-Assembly/) para saber as instruções disponíveis.


Vamos implementar alguns códigos assembly, a descrição do que eles devem fazer estão no próprio arquivo `.nasm`.

!!! exercise "💰 (0 HW / 1 SW)"
    - File: `add.nasm`
    - Test: `pytest -k add`
    
    Tarefa: Leia o cabeçalho do arquivo e implemente o programa nasm que executa o que está descrito, teste com o `pytest`

!!! exercise "💰 (0 HW / 1 SW)"
    - File: `sub.nasm`
    - Test: `pytest -k sub`
    
    Tarefa: Leia o cabeçalho do arquivo e implemente o programa nasm que executa o que está descrito, teste com o `pytest`

!!! exercise "💰 (0 HW / 1 SW)"
    - File: `mov.nasm`
    - Test: `pytest -k mov`
    
    Tarefa: Leia o cabeçalho do arquivo e implemente o programa nasm que executa o que está descrito, teste com o `pytest`
