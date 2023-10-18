# E - Assembly

| Deadline: {{proj_asm_deadline}}                                                   |
|-----------------------------------------------------------------------------------|
| ^^MEDIADOR CRIA PRIMEIRO^^ [Classroom]( {{proj_asm_classroom}}) |
| ^^AO FINAL:^^ Preencher para entregar [==Mediador==]( {{proj_forms_mediador}})    |
| ^^AO FINAL:^^ Preencher para entregar [==Dev==]( {{proj_forms_dev}})              |

Nesse projeto cada grupo terá que implementar diversos códigos em assembly a fim de entendermos a linguagem e as limitações do hardware propostos.

## Descrição

Deve-se implementar diversos programas na linguagem de máquina do Z01 que irão manipular a memória RAM a fim de implementar o que é pedido. **A descrição a seguir está classificada em ordem de dificuldade, começando pelos mais simples.**

### Módulos 

A descrição de cada módulo está localizada no cabeçalho do arquivo.
 
!!! info ""
    - 🧩 indica código com certo grau de dificuldade. 
    - Lembre de executar com `pytest -s -k NOME_ARQUIVO`
    - Se não funcionar, depure usando `bits debug nasm NOME_ARQUIVO`
    
 
- mod 
    - **Arquivo**   : `mod.nasm`
- div 🧩
    - **Arquivo**   : `div.nasm` 
- pow 🧩
    - **Arquivo**   : `pow.nasm`
- É par 
    - **Arquivo** : `isEven.nasm`
- É impar 
    - **Arquivo** : `isOdd.nasm`
- Number of 4 
    - **Arquivo** : `numberOf4.nasm`
- Number of x 
    - **Arquivo** : `numberOfx.nasm`
- Vector Mean 🧩
    - **Arquivo** : `vectorMean.nasm`
- Linha
    - **Arquivo**   : `linha.nasm`
    - Edite o arquivo para desenhar uma linha completa no lcd
- vectorFill 🧩
    - **Arquivo**: `vectorFill.nasm`
    - ==Consulte explicação detalhada no final da página==
    
### Conceito B

- add32
    - **Arquivo**: `add32.nasm`
    - ==Consulte explicação detalhada no final da página==
- Palíndromo 🧩
    - **Arquivo** : `palindromo.nasm`
- Fatorial 🧩
    - **Arquivo**   : `fatorial.nasm`    
- String length 🧩 
    - **Arquivo** : `stringLength.nasm`
- LCD Quadrado
    - **Arquivo**   : `quadrado.nasm`
    
### Conceito A

- Multiplo de dois
    - **Arquivo** : `multiploDeDois.nasm`
- MatrizDeterminante 🧩
    - **Arquivo** : `matrizDeterminante.nasm`
- Letra Grupo
    - **Arquivo**   : `letra.nasm`

## Explicação 

A seguir explicação detalhada para alguns módulos

### Add32.nasm

Todas as operações do nosso computador Z01.1 são de 16 bits (dai que vem o 'w' no final dos comandos, de word). No entanto, queremos utilizá-lo agora para realizar uma operação matemática de 32 bits.

Considere que os 16 bits MAIS significativos (MSB) de um número W estejam armazenados na RAM[0] e os 16 bits MENOS significativos (LSB) estejam armazenados na RAM[0]. Considere também que os 16 bits MAIS significativos de um número T estejam armazenados na RAM[2] e os 16 bits MENOS significativos estejam armazenados na RAM[3].

``` text
| RAM | Variável | byte |
|-----|----------|------|
| 0   | W[15:8]  | MSB  |
| 1   | W[7:0]   | LSB  |
| 2   | T[15:8]  | MSB  |
| 3   | T[7:0]   | LSB  |
| 4   | R[15:8]  | MSB  |
| 5   | R[7:0]   | LSB  |
```

Faça um código em Assembly que:

- calcula: `R = W + T`.
- salve os 16 bits MAIS significativos do resultado na RAM[4] e os 16 bits MENOS significativos na RAM[5]

> DICA:
>
> Simule no papel antes de sair programando, entenda o que deve ser feito!

Testes:

- `noOverflow`: Testa apenas a soma dos termos MSB + MSB e LSB + LSB independente 
- `onlyOverflow`: Testa apenas o estouro de LSB + LSB -> MSB
- `full`: Teste completo

### vectorFill.nasm

Escreva um programa em assembly que preenche um vetor (que está salvo na memória) com uma constante. O vetor começa sempre na RAM[5] e possui tamanho definido pela RAM[4]. O valor da constante (a ser usado) está salvo na RAM[3].

Veja o exemplo a seguir (`-k vectorFill_example`):

```
                INICIAL          FINAL
            -------------------------------------
  valor   ---> RAM[3]: 7   | 
  tamanho ---> RAM[4]: 4   |
          ---  RAM[5]: 0   |     RAM[5]: 7
           |   RAM[6]: 0   |     RAM[6]: 7
     vetor |   RAM[7]: 0  ===>   RAM[7]: 7
          ---  RAM[8]: 0   |     RAM[8]: 7
               RAM[9]: 0   |     RAM[9]: 0
```

Testes:

-  `vectorFill_example`: Testa o exemplo (valor 7 e tamanho 4)
-  `vectorFill_generic`: Teste genérico.
