# Base Teórica - Representação de Dados e Sistemas Numéricos

## Camada Física da Computação - Aula 1

Esta documentação apresenta os conceitos fundamentais necessários para compreender e realizar os exercícios práticos sobre representação de dados na computação. Durante o estudo, você encontrará exercícios interativos que o ajudarão a fixar os conceitos aprendidos.

[notebook](atividade-aula1.ipynb)

## Sistemas de Numeração Fundamentais

Na computação, trabalhamos constantemente com diferentes sistemas de numeração. Embora estejamos acostumados com o sistema decimal no dia a dia, os computadores operam internamente com o sistema binário, e frequentemente utilizamos o hexadecimal como uma forma mais compacta de representar dados binários.

O **sistema decimal** utiliza 10 símbolos (0-9) e é baseado em potências de 10. Por exemplo, o número 347 representa: 3×10² + 4×10¹ + 7×10⁰ = 300 + 40 + 7 = 347.

!!! exercise choice "Question"
    Qual é o valor posicional do dígito 5 no número decimal 2537?

    - [ ] 5
    - [ ] 50
    - [x] 500
    - [ ] 5000

    !!! answer "Answer!"
        O dígito 5 está na posição das centenas (10²), portanto seu valor posicional é 5 × 100 = 500.

O **sistema binário** é fundamental porque os computadores trabalham com estados ligado/desligado (1/0). Para converter um número decimal para binário, dividimos sucessivamente por 2 e coletamos os restos. Por exemplo, convertendo 12 para binário:

```
12 ÷ 2 = 6, resto 0
6 ÷ 2 = 3, resto 0  
3 ÷ 2 = 1, resto 1
1 ÷ 2 = 0, resto 1
```

Lendo os restos de baixo para cima: 12₁₀ = 1100₂

!!! exercise
    Converta os números 8 e 16 para o sistema binário usando o método de divisões sucessivas. Anote o processo completo!

Para converter de binário para decimal, multiplicamos cada dígito pela potência correspondente de 2. O número 1100₂ equivale a: 1×2³ + 1×2² + 0×2¹ + 0×2⁰ = 8 + 4 + 0 + 0 = 12₁₀.

O **sistema hexadecimal** utiliza 16 símbolos (0-9 e A-F, onde A=10, B=11, C=12, D=13, E=14, F=15) e é muito útil para representar dados binários de forma compacta. Para converter 255 para hexadecimal:

```
255 ÷ 16 = 15, resto 15 (F)
15 ÷ 16 = 0, resto 15 (F)
```

Resultado: 255₁₀ = FF₁₆ = 0xFF

!!! exercise choice "Question"
    Quantos símbolos diferentes são utilizados no sistema hexadecimal?

    - [ ] 8
    - [ ] 10
    - [ ] 15
    - [x] 16

    !!! answer "Answer!"
        O sistema hexadecimal utiliza 16 símbolos: os dígitos 0-9 (10 símbolos) e as letras A-F (6 símbolos), totalizando 16 símbolos diferentes.

## Bits, Bytes e Representação Digital

A menor unidade de informação em computação é o **bit** (binary digit), que pode assumir apenas dois valores: 0 ou 1. Um **byte** é um conjunto de 8 bits e pode representar 2⁸ = 256 valores diferentes (0 a 255). Esta é a unidade padrão para medida de dados.

A relação entre os sistemas é direta: 1 byte = 8 bits = 2 dígitos hexadecimais. Por exemplo, 0xFF = 11111111₂ = 255₁₀. Esta equivalência torna o hexadecimal muito prático para representar dados binários de forma compacta.

!!! exercise
    Complete a tabela de equivalências:
    
    | Decimal | Binário (8 bits) | Hexadecimal |
    |---------|------------------|-------------|
    | 15      | ?                | ?           |
    | ?       | 01000001         | ?           |
    | ?       | ?                | 0x2A        |

Quando trabalhamos com números que podem ser negativos, utilizamos diferentes representações. Em números **sem sinal (unsigned)**, todos os bits representam magnitude, permitindo valores de 0 a 2ⁿ-1 para n bits. Em números **com sinal (signed)**, o bit mais significativo indica o sinal, e o método mais comum é o complemento de dois, que permite valores de -2ⁿ⁻¹ a 2ⁿ⁻¹-1.

!!! exercise choice "Question"
    Em um sistema de 8 bits com representação signed, qual é o intervalo de valores possíveis?

    - [ ] 0 a 255
    - [x] -128 a +127
    - [ ] -127 a +128
    - [ ] -255 a +255

    !!! answer "Answer!"
        Com 8 bits em representação signed (complemento de dois), temos valores de -2⁷ a 2⁷-1, ou seja, -128 a +127.

## Ordem de Bytes e Organização de Dados

A **ordem de bytes (byte order)** é crucial quando trabalhamos com dados que ocupam mais de um byte. No formato **big endian**, o byte mais significativo vem primeiro (ordem "natural" para humanos), enquanto no **little endian**, o byte menos significativo vem primeiro (comum em processadores x86).

Por exemplo, o número 0x1234:
- Big endian: [0x12] [0x34]
- Little endian: [0x34] [0x12]

Esta diferença é fundamental em comunicação entre sistemas diferentes e manipulação de arquivos binários.

## Codificação ASCII e Representação de Caracteres

A tabela **ASCII** (American Standard Code for Information Interchange) associa caracteres a números de 0 a 127, permitindo que computadores armazenem e transmitam texto. As faixas mais importantes são:

- **0x00 a 0x1F**: Caracteres de controle (não imprimíveis)
- **0x20 a 0x7F**: Caracteres imprimíveis, incluindo:
  - 0x20: Espaço
  - 0x30-0x39: Dígitos '0'-'9'
  - 0x41-0x5A: Letras maiúsculas 'A'-'Z'
  - 0x61-0x7A: Letras minúsculas 'a'-'z'

Por exemplo: 'A' = 0x41 = 65₁₀, 'a' = 0x61 = 97₁₀, '0' = 0x30 = 48₁₀.

!!! exercise choice "Question"
    Qual é a diferença entre os códigos ASCII de uma letra maiúscula e sua correspondente minúscula?

    - [ ] 16
    - [ ] 26
    - [x] 32
    - [ ] 64

    !!! answer "Answer!"
        A diferença é sempre 32. Por exemplo, 'A' = 65 e 'a' = 97, diferença de 32. Isso acontece porque 32 = 2⁵, então basta alterar o 6º bit para converter entre maiúscula e minúscula.

## Ferramentas Python para Manipulação de Dados

O Python oferece funções nativas poderosas para trabalhar com diferentes sistemas de numeração e manipulação de bytes. As **conversões básicas** incluem:

```python
# Decimal para binário
bin(12)  # Retorna '0b1100'

# Decimal para hexadecimal
hex(255)  # Retorna '0xff'

# Binário/Hex para decimal
int('1100', 2)  # Retorna 12
int('FF', 16)   # Retorna 255
```

!!! exercise
    Teste as funções acima no Python e verifique suas conversões manuais dos exercícios anteriores. Use também as funções para descobrir os valores em decimal de 0b10101010 e 0xAB.

Para **manipulação de bytes**, Python oferece várias ferramentas úteis:

```python
# Criar bytes a partir de lista de inteiros
bytes([65, 66, 67])  # Retorna b'ABC'

# Converter inteiro para bytes
(255).to_bytes(2, byteorder='big')    # b'\x00\xff'
(255).to_bytes(2, byteorder='little') # b'\xff\x00'

# Converter bytes para inteiro
int.from_bytes(b'\x00\xff', byteorder='big')    # 255
int.from_bytes(b'\x00\xff', byteorder='little') # 65280
```

Note como a ordem dos bytes (`byteorder`) afeta significativamente o resultado da conversão. Isso demonstra na prática a importância dos conceitos de big endian e little endian.

!!! exercise choice "Question"
    Qual será o resultado de `int.from_bytes(b'\x12\x34', byteorder='little')`?

    - [ ] 4660
    - [x] 13330
    - [ ] 1234
    - [ ] 3412

    !!! answer "Answer!"
        Em little endian, os bytes são interpretados na ordem inversa: 0x34 (52) + 0x12×256 (18×256) = 52 + 4608 = 13330.

Para trabalhar com **arrays de bytes**, utilizamos:

```python
# Criar bytearray
data = bytearray([1, 2, 3, 4])

# Concatenar bytearrays
combined = bytearray([1, 2]) + bytearray([3, 4])
```

Os bytearrays são úteis quando precisamos modificar sequências de bytes, pois são mutáveis, diferentemente dos objetos bytes que são imutáveis.

## Aplicações Práticas na Computação

Estes conceitos não são apenas teóricos - eles têm aplicações diretas em várias áreas da computação. No **armazenamento de dados**, números são sempre armazenados em binário na memória, caracteres são codificados usando ASCII ou Unicode, e arquivos multimídia como imagens, áudio e vídeo são essencialmente sequências organizadas de bytes.

Na **comunicação de dados**, informações são transmitidas como sequências de bits através de redes, protocolos definem exatamente como interpretar esses bits, e a ordem de bytes torna-se crítica quando sistemas diferentes se comunicam.

Para **depuração e análise**, a representação hexadecimal facilita enormemente a visualização de dados binários, sendo essencial para análise de arquivos corrompidos, protocolos de rede e programação de baixo nível.

!!! exercise
    Pense em uma situação onde você precisa transmitir o texto "Hi!" através de uma rede. Descreva como essa informação seria representada em bytes usando ASCII, e depois em binário.

!!! exercise choice "Question"
    Quantos bits são necessários para representar o número 1024 em binário?

    - [ ] 10 bits
    - [x] 11 bits
    - [ ] 12 bits
    - [ ] 16 bits

    !!! answer "Answer!"
        1024 = 2¹⁰, que em binário é 10000000000 (um 1 seguido de 10 zeros), necessitando de 11 bits para representação.

!!! exercise choice "Final Challenge"
    Qual seria o valor hexadecimal do texto "AB" quando codificado em ASCII?

    - [ ] 0x4142
    - [x] 0x4142
    - [ ] 0x6162
    - [ ] 0x4241

    !!! answer "Answer!"
        'A' = 0x41 e 'B' = 0x42, então "AB" = 0x4142. Note que em little endian seria 0x4241, mas a representação padrão de texto segue a ordem natural (big endian).
