# Projeto 2: Client/Server

## Pré-requisitos (o que você deve ter pronto antes de começar)

### 1) Base do Projeto 1 (arquitetura em camadas)

No Projeto 2, você **reutiliza os arquivos base** do Projeto 1. O ponto principal é que você deve pensar em termos de **camadas**:

- As camadas “de baixo” (Interface Física e Enlace) cuidam de **enviar/receber bytes**.
- A camada “de cima” (sua **aplicação**) deve decidir:
  - **quando** falar
  - **o que** falar
  - **como** organizar os dados (protocolo)
  - **como** detectar erros de comunicação (validação)

!!! warning "Importante"
    O objetivo do Projeto 2 é consolidar o entendimento das camadas.  
    Na prática, tente **evitar alterações** em partes que não pertencem à aplicação (principalmente camadas mais baixas), a menos que o professor peça explicitamente.

### 2) Execução em grupo: 2 PCs (client e server em máquinas diferentes)
O Projeto 2 é em dupla. Isso muda completamente a realidade do teste:

- **PC 1** executa o `server.py` (lado servidor)
- **PC 2** executa o `client.py` (lado cliente)

Por que isso importa?
- A sincronização fica “real”: há atrasos, inicializações em momentos diferentes e variação de tempo.
- Problemas que somem em testes locais aparecem (e você precisa do protocolo para lidar com isso).

!!! exercise choice "Setup do grupo: por que 2 PCs?"
    Qual é o maior risco de testar client e server no **mesmo** computador?

    - [ ] O baud rate muda automaticamente.
    - [X] Você mascara problemas de sincronização/tempo e torna o teste “bom demais para ser verdade”.
    - [ ] Você não consegue imprimir logs no terminal.
    - [ ] O Arduino deixa de funcionar.

    !!! answer "Resposta!"
        Em um único PC você elimina vários atrasos e condições reais (timing, inicialização, concorrência, etc.).
        Isso pode fazer um protocolo “frágil” parecer correto — até o momento em que for testado em 2 PCs.

---

## Contexto e motivação: UART transporta bytes, não significado

A UART é um meio de transmitir **bytes** entre dois dispositivos. Ela **não** define, por si só:

- onde uma mensagem começa e termina
- se o receptor está pronto
- como o emissor sabe que foi entendido
- como representar números de forma padronizada (texto vs binário)

Em outras palavras: a UART é o “caminho”.  
O **protocolo** é o “acordo” que dá significado aos bytes.

!!! exercise
    Dê **3 exemplos** de problemas que podem ocorrer quando dois sistemas apenas “enviam bytes” sem um protocolo de aplicação (sem acordo).

---

## Modelo conceitual: Client/Server e a ideia de protocolo

No Projeto 2, você trabalha com uma comunicação **Client/Server**:

- **Client** (cliente): inicia a comunicação e envia uma solicitação/dados
- **Server** (servidor): espera solicitações e responde com um resultado

Isso implica que a aplicação precisa de um **fluxo previsível** (uma sequência de eventos) para evitar ambiguidade.

### Uma máquina de estados mínima (modelo mental)
Um jeito profissional de pensar nisso é como **estados**:

- `IDLE`: nada acontecendo
- `SYNC`: sincronização entre as pontas (handshake)
- `TX_DATA`: transmissão de dados do client para o server
- `WAIT_RESPONSE`: client aguardando resposta do server
- `DONE` / `ERROR`: encerramento normal ou tratamento de falha

> Nesta aula, o foco é entender **por que** esses estados existem.  
> A implementação detalhada desses estados é parte da prática do Projeto 2.

!!! exercise choice "Quando o client deve começar a enviar os dados?"
    Considerando um desenho clássico de protocolo, o client deve transmitir os dados principais:

    - [ ] Imediatamente, sem sincronização.
    - [X] Depois de algum tipo de confirmação de que o server está pronto.
    - [ ] Somente após o server enviar o resultado.
    - [ ] Apenas se houver paridade par.

    !!! answer "Resposta!"
        A sincronização reduz perda de dados no começo da comunicação e evita que o client envie enquanto o server ainda não está pronto.

---

## Handshake: o que é, para que serve e como desenhar

### Definição
**Handshake** é um mecanismo de **sincronização** entre duas pontas de comunicação para:

- confirmar que as duas aplicações estão “vivas”
- garantir que existe um “momento de início” acordado
- reduzir ambiguidades (ex.: ambos falando ao mesmo tempo)
- estabelecer uma base para timeouts e tratamento de erro

### Tipos comuns (conceitualmente)
1) **1-way**: o server anuncia “READY” e o client começa  
2) **2-way**: client diz “HELLO”, server responde “OK”  
3) **3-way (analogia)**: inspirado no TCP: `SYN → SYN-ACK → ACK`

> Você não precisa implementar TCP, mas a analogia é útil:  
> *uma confirmação extra pode reduzir ambiguidades e falhas de sincronização.*

### Boas práticas de handshake (na camada de aplicação)
- mensagens curtas e inequívocas (poucos bytes)
- estados bem definidos (“o que faço se não recebo resposta?”)
- logs claros (para depuração em dupla)
- um critério de falha (timeout/re-tentativa)

!!! tip "Dica de engenharia"
    Pense no handshake como “o combinado antes do jogo começar”.  
    Sem isso, cada ponta pode interpretar o começo da conversa de um jeito diferente.

!!! exercise
    Proponha um handshake **2-way** para o Projeto 2.  
    Escreva:
    1) a mensagem do client  
    2) a resposta do server  
    3) o que acontece se o client não receber a resposta

!!! exercise choice "2-way vs 3-way"
    Por que um handshake 3-way pode ser mais robusto que um 2-way?

    - [ ] Porque aumenta o baud rate automaticamente.
    - [X] Porque confirma de forma mais forte que *ambas* as pontas concordaram com o início.
    - [ ] Porque elimina a necessidade de logs.
    - [ ] Porque impede erro de paridade.

    !!! answer "Resposta!"
        O 3-way reduz ambiguidades: uma ponta pode confirmar que a outra recebeu a confirmação.
        Isso é útil quando há atrasos, buffers e inicializações em tempos diferentes.

---

## Representação de números: texto vs binário

Antes de falar de IEEE-754, precisamos alinhar uma ideia simples:

### Texto (ASCII)
Você envia algo como:
- `"45.450000"`  
- `"-1.435670"`

Vantagens:
- fácil depurar (você *vê* o número no terminal/serial monitor)
- fácil registrar em log

Desvantagens:
- ocupa mais bytes
- exige parsing (conversão string → número)
- pode ter ambiguidades (separador decimal, sinal, etc.)

### Binário
Você envia o número em bytes diretamente (ex.: float32).

Vantagens:
- mais compacto
- mais rápido de processar
- formato padronizado (se combinado)

Desvantagens:
- mais difícil de depurar “a olho”
- exige acordo de endianness (ordem dos bytes)
- exige conhecer o padrão (IEEE-754)

!!! exercise choice "Debug"
    Qual forma facilita mais depuração rápida via logs/terminal?

    - [X] Texto (ASCII)
    - [ ] Binário
    - [ ] Tanto faz
    - [ ] Depende apenas do cabo

    !!! answer "Resposta!"
        Em texto, você lê diretamente o valor. Em binário, você vê bytes que precisam ser interpretados.

---

## IEEE-754 (float32): como funciona de verdade

O padrão **IEEE-754** define como representar números de ponto flutuante em binário.  
No Projeto 2, o desafio A+ envolve usar **float32** (32 bits).

### Estrutura do float32
Um float32 tem 32 bits divididos em:

- **S**: 1 bit de sinal
- **E**: 8 bits de expoente (com *bias* = 127)
- **F**: 23 bits de fração (mantissa)

Representação:

- `S | EEEEEEEE | FFFFFFFFFFFFFFFFFFFFFFF`

### Interpretação (caso “normalizado”)
Para números normalizados:

- Valor = \((-1)^S\) × \(1.F\) × \(2^{(E - 127)}\)

Onde `1.F` significa “1 ponto (fração)”, com **1 implícito** (não armazenado).

### Exemplo guiado (conceitual): 10,5
1) Em binário:  
   - 10 = `1010`  
   - 0,5 = `0.1`  
   - 10,5 = `1010.1`

2) Normalizando:  
   `1010.1 = 1.0101 × 2^3`

3) Campos:
- S = 0 (positivo)
- Expoente real = 3 → Expoente armazenado = 3 + 127 = 130
- Fração F = bits após o “1.” → `0101...` (completar até 23 bits)

> Nesta aula você não precisa “decorar” o cálculo — precisa entender a **estrutura** e o **porquê**.

### Precisão: por que 0,1 é “problemático”
Nem todo decimal tem representação binária finita.
Ex.: `0.1` em base 10 vira uma dízima em base 2.

Consequência:
- operações podem gerar pequenos erros de arredondamento
- somas sucessivas podem acumular erro

Isso explica o famoso comportamento:
- `0.1 + 0.2` pode não ser exatamente `0.3` em float32/float64

!!! exercise
    Explique, em 4–6 linhas, por que `0.1 + 0.2` pode ser diferente de `0.3` ao usar ponto flutuante.

### Casos especiais (visão geral)
- **Zero**: existe `+0` e `-0` (sinal pode existir mesmo com valor zero)
- **Infinito**: `+Inf` e `-Inf` (overflow)
- **NaN**: “Not a Number” (resultado indefinido, ex.: 0/0)

> Na prática, esses casos importam para robustez e validação do protocolo.

### Endianness (ordem dos bytes)
Mesmo com IEEE-754, você precisa combinar:
- a **ordem** dos bytes na transmissão (little-endian vs big-endian)

Se cada lado interpretar com endianness diferente:
- os 4 bytes recebidos formam **outro número** (e a soma dá errado).

!!! exercise choice "Dobrar um número"
    Quando você dobra um número (ex.: 1,0 → 2,0), qual campo tende a mudar de maneira mais direta em float32?

    - [ ] O bit de sinal
    - [X] O expoente (principalmente)
    - [ ] A mantissa sempre muda e o expoente nunca muda
    - [ ] Nenhum campo muda

    !!! answer "Resposta!"
        Dobrar equivale a multiplicar por 2, o que, em números normalizados, é representado principalmente por um incremento no expoente.

!!! exercise
    Você recebeu 4 bytes e o valor decodificado está completamente fora do esperado (ex.: enorme ou NaN).  
    Liste **2 hipóteses** plausíveis relacionadas a IEEE-754 e transmissão (sem culpar “bug genérico”).

---

## Leituras complementares
- Revisão rápida de ponto flutuante: sinal, expoente (bias) e mantissa
- Erros de arredondamento e comparações (tolerância / epsilon)
- Endianness e representação em bytes

