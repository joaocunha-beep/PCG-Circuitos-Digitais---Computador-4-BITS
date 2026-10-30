# Computador de 4 bits

Este projeto implementa um computador simples de 4 bits, construído no simulador de circuitos digitais a partir de portas lógicas básicas. O sistema é composto por uma ULA (Unidade Lógica e Aritmética) de 4 bits, um registrador acumulador de 4 bits, um contador de programa, uma memória ROM de 16 posições, um decodificador de instruções e um clock. A cada pulso de clock o contador avança, a ROM entrega a próxima instrução, o decodificador interpreta o código da operação e a ULA executa o cálculo, guardando o resultado no acumulador até que uma instrução de parada (HLT) seja encontrada.

## ULA de 4 bits

A ULA é capaz de realizar operações aritméticas e lógicas: adição, subtração, multiplicação, divisão, AND, OR, XOR, NOT e verificação de igualdade. Um sinal de controle de 4 bits seleciona a operação executada por meio de um multiplexador de 16 entradas, e a ULA fornece o resultado correspondente na saída.

| Operação | Como foi implementada |
|---|---|
| Adição | Somador de 4 bits em cascata (ripple carry), formado por quatro somadores completos de 1 bit |
| Subtração | A + NOT(B) + 1, reaproveitando o somador de 4 bits e o circuito NOT |
| Multiplicação | Multiplicador combinacional 4x4 com resultado de 8 bits, usando portas AND e somadores completos |
| Divisão | Divisor combinacional de 4 bits, com somadores completos e multiplexadores |
| AND, OR, XOR, NOT | Portas lógicas aplicadas bit a bit sobre os 4 bits das entradas |
| Igualdade | Quatro comparadores de 1 bit (XNOR) combinados por uma porta AND de 4 entradas |

## Componentes

- **ULA 4BITS**: reúne todas as operações acima. Entradas: A, B (4 bits), C, Cin e o Sinal de Controle (4 bits). Saída: resultado de 4 bits.
- **Flip Flop D**: flip-flop montado com portas NAND, com entradas D, EN e CLR.
- **FF D MS**: flip-flop D mestre-escravo, feito com dois Flip Flop D. É a base dos registradores e contadores.
- **4 bit register**: registrador de 4 bits com entradas de dados (Din0 a Din3), sinais de escrita (WR), leitura (RD) e clock (CLK), e saídas Dout0 a Dout3. Funciona como acumulador.
- **Contador**: contador síncrono de 4 bits (Q0 a Q3) com CLK e RST. Funciona como contador de programa (PC).
- **Contador Async**: versão assíncrona do contador de 4 bits, disponível no projeto como circuito de estudo.
- **Decodificador**: recebe o código da operação (OP, 4 bits) e gera os sinais LDI (carga imediata), HLT (parada) e RUN (execução).
- **ROM**: memória de 16 posições que armazena o programa, uma palavra de 8 bits por endereço.
- **Computador de 4 bits**: circuito principal que conecta todos os blocos. Possui as saídas ACC (acumulador), PC (contador de programa) e um indicador de parada.
- **Circuitos auxiliares**: 1 Bit Add, 4 BITS ADD, SUB, AND, OR, XOR, NOT, 1BIT Equal, 4 BIT Equal, Mult e Div, usados dentro da ULA.

## Como funciona o ciclo de execução

1. O clock gera os pulsos que fazem o contador de programa (PC) avançar a cada ciclo.
2. O PC endereça a ROM, que devolve a instrução da posição atual.
3. A palavra de 8 bits é separada em duas partes de 4 bits: o código da operação e o operando.
4. O decodificador identifica se a instrução é uma carga imediata (LDI), uma parada (HLT) ou uma operação da ULA.
5. A ULA executa a operação escolhida pelo sinal de controle e o resultado é gravado no acumulador.
6. Ao encontrar HLT, o sinal RUN é desativado e o computador para de executar.

## Como usar

1. Abra o arquivo `COMPUTADOR_4BITS.cv` no simulador de circuitos digitais.
2. Vá até a aba **Computador de 4 bits**.
3. Grave o programa desejado na ROM (a ROM do arquivo está zerada).
4. Ative o clock e acompanhe os valores de ACC e PC nas saídas.

Cada bloco também pode ser testado de forma isolada na sua própria aba, alterando as entradas manualmente.

## Ferramentas

- Simulador de circuitos digitais (arquivo `.cv`)
- Projeto desenvolvido na disciplina de Circuitos Digitais, Ciência da Computação, Unisantos
