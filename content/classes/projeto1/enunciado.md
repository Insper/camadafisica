# Projeto 1 – Loop Back


<a href="HandOut.rar" download>Baixar os arquivos do projeto 1</a>


Neste projeto, você deverá construir um código em **Python** para **transmissão e recepção serial simultâneas**.  
O software funcionará como **camada intermediária** entre o usuário e o chip UART, sequenciando os bits de cada byte de acordo com o protocolo.

Você utilizará **5 arquivos fornecidos** e deverá **editar apenas o arquivo `aplicação.py`**.  
Os demais arquivos já estão prontos para enviar bytes ao chip UART e receber dados.



## Objetivo

Ao rodar seu arquivo `aplicação.py`, o software deve:

1. **Enviar** uma imagem (o menor tamanho possível) através da porta de comunicação serial.
2. **Receber** a imagem simultaneamente ao envio e salvá-la como uma cópia.
   - Para isso, o pino RX do Arduino deve estar curto-circuitado com o pino TX.
3. **Compreender** o código-base de transmissão UART.


## Material Necessário

- Arduino  
- Computador  
- 5 arquivos de código fornecidos pelo professor  
- **No console Python:**  
  ```bash
  pip install pyserial
  ```
- Verificar no **Gerenciador de Dispositivos** qual porta COM está o Arduino e ajustar no `aplicação.py`.


## Montagem do Sistema

![alt text](image-9.png)

- Ao conectar o Arduino ao computador:
  - **TX do computador** → **RX do Arduino**
  - **TX do Arduino** → **RX do computador**
- Para criar o loopback:
  - Conecte o **pino TX do Arduino** ao **pino RX do próprio Arduino**.
- Para o Arduino UNO, você deve:
  - Ficar com o **botão RESET pressionado**  
  - Ou **pino RESET aterrado**.

![alt text](image-12.png)


## Funcionamento Esperado

- Enviar uma sequência de bytes ou bytearray para o **RX do Arduino**  
- Receber a mesma sequência de bytes de volta no computador (**espelho**)
- O envio e recepção acontecem **full-duplex**.

---

## Estrutura da Camada Enlace

O maior desafio é compreender como as funções das classes realizam o envio e recepção **full-duplex**.

![alt text](image-11.png)

Você deve:
- Seguir o fluxo das funções no envio e no recebimento.
- Entender e ser capaz de modificar essas funções.
- Trabalhar com **imagem em Python**:
  - Converter imagem → lista de bytes
  - Receber lista de bytes → salvar como imagem

---

## Exemplo de Fluxo para Imagens

1. Definir caminho da imagem.
```python
# Endereco da imagem a ser transmitida
imageR = "./imgs/image.png"

# Endereco da imagem a ser salva
imageW = "./imgs/recebidaCopia.png"
```
2. Ler imagem e converter para `bytearray`.

```python
# Carrega imagem
print("Carregando imagem para transmissão :)")
print(f"- {imageR}")
print("-------------------------")
with open(imageR, 'rb') as f:
    txBuffer = bytearray(f.read())

print(f" - Tamanho do buffer: {len(txBuffer)} bytes")
```

3. Enviar via porta serial.
4. Receber os bytes.
5. Salvar como **arquivo cópia**.

```python
print("Salvando dados no arquivo :")
print(f" - {imageW}")
with open(imageW, 'wb') as f:
    f.write(rxBuffer)
```

6. Verificar se abre corretamente.

### Termos da Comunicação UART

| #  | Termo                  |
|----|------------------------|
| 1  | Transmissão assíncrona |
| 2  | UART – Start bit       |
| 3  | UART – Stop bit        |
| 4  | UART – TX, RX, GND     |
| 5  | UART – Baud rate       |
| 6  | UART – Bit rate        |
| 7  | UART – Buffer          |
| 8  | UART – Frame           |
| 9  | Bit de Paridade        |
| 10 | CRC                    |

--

## O que é esperado na entrega

- Mostrar a transmissão e recepção da imagem ocorrendo corretamente.
- Compreender e responder perguntas sobre as funções principais: `getBufferLen`, `getAllBuffer`, `getBuffer`, `getNData`, `sendBuffer`. 
- Compreender e explicar os termos da comunicação UART.
- Corrigir a função `getStatus` para que funcione corretamente.
