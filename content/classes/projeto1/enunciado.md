# Projeto Loopback

## Introdução

Neste projeto, você irá construir um código em Python para realizar transmissões e recepções seriais simultâneas utilizando um Arduino. O objetivo é enviar uma imagem através da porta serial e receber simultaneamente uma cópia dessa imagem.

## Objetivos

1. Enviar uma imagem (a menor possível) através da porta de comunicação serial.
2. Receber a imagem simultaneamente ao envio e salvá-la como uma cópia.
3. Adquirir compreensão do código base de transmissão UART.

## Materiais Necessários

- **Hardware:**
  - Arduino (verificar modelo compatível)
  - Cabo USB para conexão com o computador
  - Jumpers para curto-circuitar os pinos RX e TX

- **Software:**
  - Python instalado no computador
  - Biblioteca `pyserial` (instalar com `pip install pyserial`)
  - Arquivos de código fornecidos (5 no total)

## Montagem

### Configuração do Hardware

!!! exercise
    Conecte o Arduino ao computador via USB. Em seguida, curto-circuite os pinos RX e TX do Arduino:

    - **Passo 1:** Identifique os pinos RX e TX no seu modelo de Arduino.
    - **Passo 2:** Utilize um jumper para conectar o pino RX ao pino TX.

!!! warning "Atenção!"
    Em alguns modelos de Arduino (como o UNO), é necessário manter o botão de reset pressionado ou aterrar o pino reset.

### Configuração do Software

1. **Instalação da Biblioteca PySerial:**

   ```bash
   pip install pyserial
   ```

1. **Configuração da Porta Serial:***


!!! exercise
    - Verifique em seu gerenciador de dispositivos qual porta COM o Arduino está utilizando.
    - Ajuste o arquivo de aplicação Python para utilizar essa porta.

## Implementação

### Manipulação de Imagens em Python

Para transformar uma imagem em uma lista de bytes e vice-versa, você pode usar os seguintes trechos de código:

```python
# Caminho da imagem original
img_origin = "original_image.jpg"

# Leitura da imagem e conversão para bytes
with open(img_origin, 'rb') as f:
    img_bytes = f.read()

# Salvando a imagem recebida como uma cópia
img_copy = "copy_image.jpg"
with open(img_copy, 'wb') as f:
    f.write(img_bytes)
```

## Transmissão e Recepção Serial

!!! exercise
    Utilize as funções fornecidas nos arquivos de código para enviar e receber os bytes da imagem através da comunicação serial.


## Entrega e Avaliação

### Conceito C

- Demonstrar a transmissão e recepção da imagem ocorrendo corretamente.

### Conceito B

- Responder às perguntas feitas pelo professor sobre as seguintes funções:

  - `getBufferLen`
  - `getAllBuffer`
  - `getBuffer`
  - `getNData`
  - `sendBuffer`

### Conceito B+

- Entender e explicar os seguintes termos da comunicação UART:

  1. **Transmissão assíncrona**
  2. **UART – Start bit**
  3. **UART – Stop bit**
  4. **UART – TX, RX, GND**
  5. **UART – Baud rate**
  6. **UART – Bit rate**
  7. **UART – Buffer**
  8. **UART – Frame**
  9. **UART – Bit de Paridade**
  10. **UART – CRC**

### Conceito A+

- Corrigir a função `getStatus`, que não está funcionando corretamente, e apresentar uma solução.

## Data Limite

- **15/08** - Após essa data, a nota terá uma redução de 25% a cada semana de atraso.

