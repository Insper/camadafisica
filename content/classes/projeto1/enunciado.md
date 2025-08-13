# Projeto 1: Loop-back

## Objetivo

Implementar um sistema de comunicação serial loop-back utilizando a porta USB do computador. O sistema deve ser capaz de transmitir e receber dados através de um cabo USB, demonstrando os conceitos básicos de comunicação serial.

## Descrição

Neste projeto, você irá desenvolver um programa que:

1. Estabelece uma comunicação serial através da porta USB
2. Envia dados de um terminal para outro
3. Recebe os dados enviados e os exibe no terminal de destino
4. Implementa um protocolo básico de comunicação

## Requisitos

- Python 3.x
- Biblioteca pyserial
- Cabo USB
- Dois terminais de computador

## Entregáveis

1. Código fonte do programa implementado
2. Relatório técnico contendo:
   - Descrição da implementação
   - Análise do protocolo de comunicação
   - Resultados dos testes realizados
   - Discussão sobre possíveis melhorias

## Avaliação

O projeto será avaliado considerando:

- Funcionalidade do sistema implementado
- Qualidade do código e documentação
- Relatório técnico
- Apresentação oral

## Datas

- Entrega: [Data a ser definida]
- Apresentação: [Data a ser definida]

## Recursos Adicionais

- [Link para documentação da biblioteca pyserial]
- [Link para tutoriais sobre comunicação serial]
- [Link para exemplos de código]

## Detalhes Técnicos

### Estrutura da Camada de Enlace

O maior desafio e objetivo do projeto 1 é que você entenda como as funções das classes fazem o trabalho de envio e recebimento full-duplex representado nesse esquema. Você deve seguir as funções envolvidas no envio e recebimento de um bytearray. Se familiarizar com elas. Ser capaz de utiliza-las, modifica-las e responder a algumas perguntas sobre elas.

### Imagens em Python

Você terá que transformar uma imagem em uma lista de bytes. No mesmo modo, salvar a lista de bytes recebida, como imagem. Para isso pode se basear nos seguintes trechos de código:

```python
# Caminhos das imagens
# Lista de bytes com a imagem a ser transmitida

# Escreve arquivo cópia
```

### Conceitos de Avaliação

#### Conceito C
- Mostrar a transmissão e recepção da imagem ocorrendo corretamente.

#### Conceito B
- Responder as questões feitas pelo seu professor (no momento da apresentação) a respeito das seguintes funções:
  - getBufferLen
  - getAllBuffer
  - getBuffer
  - getNData
  - sendBuffer

#### Conceito B+
- Além dos conceitos C e B, entender o que significa cada um dos 10 termos presentes na comunicação UART:
  1. Transmissão assíncrona
  2. UART – Start bit
  3. UART – Stop bit
  4. UART – TX, RX, GND
  5. UART – Baud rate
  6. UART – Bit rate
  7. UART – Buffer
  8. UART – Frame
  9. UART – Bit de Paridade
  10. UART – CRC

#### Conceito A+
- A função getStatus não está funcionando corretamente. Verifique o que essa função deveria retornar e encontre uma solução para corrigi-la.

### Data Limite
- 13/02 - Após esse período sua nota terá uma redução de 25% a cada semana.

# PROJETO 1 - LOOP BACK

#### Neste projeto você deverá construir um código em Python para transmissão e recepção serial simultâneas!

O software será uma camada entre o usuário e o chip UART, que irá sequenciar os bits de cada byte seguindo o
devido protocolo. Para isso voce usará os 5 arquivos fornecidos. Por ora, você deverá apenas editar o arquivo
"aplicação.py". Os demais arquivos farão o trabalho de fornecer ao chip UART do seu computador os bytes que você deseja enviar através da função de envio e também disponibilizar os dados recebidos.

Os arquivos fornecidos já estão prontos para o envio e recebimento de uma pequena mensagem de 4 bytes, ou seja,
se voce rodar o main, 4 bytes serão enviados, rebatidos pelos arduínos (conforme explicado em aula) e recebido pela aplicação, sendo printados.

Leia com atenção os comentários no código.

### Objetivo:

Ao rodar seu arquivo aplicação, o seu software deve:

```
1) Enviar uma imagem (a menor possível) através da porta de comunicação serial.
2) Receber a imagem simultaneamente ao envio e salvá-la como uma cópia. Para isso a recepção do Arduino ( pino rx ) deve estar curto-circuitada com o pino de transmissão ( pino tx ).
3) Adquirir compreensão do código base de transmissão UART.
```
### Material:

- Você irá utilizar um Arduino, um computador e 5 arquivos código fornecidos.
- No console python, 'pip install pyserial'
- Verificar em gerenciador de dispositivos qual porta COM está o Aduino. Ajustar o arquivo aplicação para
    essa porta!

### Montagem:

Seu sistema operacional irá abrir uma porta de comunicação serial com o Arduino. Através dessa comunicação você
terá acesso a tudo que o Arduino enviar ao seu computador (saindo do pino TX do Arduino e RX da sua porta USB).
Tudo que seu computador enviar ao Arduino (saindo do pino TX da sua USB em seu computador). Desta maneira, ao
conectar o Arduino ao seu computador, o pino de envio do seu computador (TX) estará conectado ao pino de
recepção do Arduino (RX). Da mesma forma, o pino de envio do Arduino (TX) estará conectado ao pino de recepção
do seu computador (RX).

O queremos é que ao enviarmos uma mensagem (lista de bytes ou bytearray) ao Arduino, este responda com os
mesmos bytes. Queremos que o Arduino seja um espelho para os bytes enviados. Para isso basta que conectemos o
pino TX do Arduino ao seu pino RX! Assim, ao enviarmos uma sequência de bytes para o RX do Arduino, a mesma
sequência de zeros e uns são produzidas no pino de envio do Arduino e recebidos de volta em seu computador.
Observe a figura:

Você precisará verificar qual os pinos TX e RX de seu Arduino.

**ATENÇÃO! ALGUNS ARDUINOS (UNO) PRECISAM FICAR COM O BOTAO DE RESET PRESSIONADO. OU O PINO RESET
ATERRADO!**

### A estrutura da camada enlace:

O maior desafio e objetivo do projeto 1 é que você entenda como as funções das classes fazem o trabalho de envio e
recebimento full-duplex representado nesse esquema. Você deve seguir as funções envolvidas no envio e
recebimento de um bytearray. Se familiarizar com elas. Ser capaz de utiliza-las, modifica-las e responder a algumas
perguntas sobre elas. Para isso, não tem outro modo a não ser se debruçar sobre as funções, seguindo todas as
chamadas de métodos envolvidos no recebimento "enlace.get()" e recebimento emlace.send()".

### Imagens em python.

Você terá que transformar uma imagem em uma lista de bytes. No mesmo modo, salvar a lista de bytes recebida,
como imagem. Para isso pode se basear nos seguintes trechos de código:

#### Caminhos das imagens

#### Lista de bytes com a imagem a ser transmitida


#### ENGENHARIA DA COMPUTAÇÃO - Rodrigo Carareto

#### Escreve arquivo cópia

### Pronto! Consegui!

Se você conseguiu fazer o arquivo cópia através da comunicação serial e este arquivo abre normalmente, parabéns!
Vamos aproveitar então para explorar um pouco mais nossas classes. Iremos fazer um estudo mais profundo das
classes na aula 2, mas já é necessário que entendam as funções e estrutura dos arquivos.

### Entrega

Os projetos dessa disciplina serão sempre avaliados presencialmente. Um dos seus professores observar uma breve
apresentação feita por você e sua dupla e lhes fazer algumas perguntas. Isso ocorrerá em um momento solicitado
por você, dentro de uma data limite. Caso você solicite a apresentação após a data limite, você será penalizado.

### Conceito C: Mostrar a transmissão e recepção da imagem ocorrendo corretamente.

### Conceito B: responder as questões feitas pelo seu professor (no momento da apresentação) a respeito das

seguintes funções:

- getBufferLen
- getAllBuffer
- getBuffer
- getNData
- sendBuffer

### Conceito B+: Além dos conceitos C e B, tente entender o que significa cada um dos 10 termos presentes na

```
comunicação UART:
```
1. Transmissão assíncrona
2. UART – Start bit
3. UART – Stop bit
4. UART – TX, RX, GND
5. UART – Baud rate
6. UART – Bit rate
7. UART – Buffer
8. UART – Frame
9. UART – Bit de Paridade
10. UART – CRC

### Conceito A+: A função getStatus não está funcionando corretamente. Verifique o que essa função deveria

retornar e encontre uma solução para corrigi-la.

### Data limite: 13 /0 2 - Após esse período sua nota terá uma redução de 25% a cada semana.



