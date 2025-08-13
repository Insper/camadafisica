# Transmissão e Recepção Serial UART

## Introdução à Comunicação Serial

A comunicação serial é uma forma de transmitir dados entre dispositivos eletrônicos de forma sequencial, enviando um bit por vez, ao longo de uma única linha de comunicação. Ao contrário da comunicação paralela, onde vários bits são enviados simultaneamente em várias linhas, a comunicação serial utiliza menos cabos, é mais simples e é frequentemente utilizada em dispositivos que precisam enviar informações a longas distâncias ou com recursos limitados.

## O Que é UART?

UART, ou **Universal Asynchronous Receiver-Transmitter**, é um protocolo de comunicação serial assíncrona amplamente utilizado para permitir a troca de dados entre um dispositivo (como um microcontrolador) e um periférico (como um computador). Esse protocolo é assíncrono porque não requer um sinal de clock comum para sincronizar os dispositivos comunicantes.

### Estrutura de Dados na Comunicação UART

A comunicação UART transmite os dados em "frames". Um frame é uma sequência de bits que inclui os dados a serem transmitidos e informações de controle, como bits de início, parada e, opcionalmente, paridade. A estrutura básica de um frame UART é a seguinte:

1. **Start Bit**: Um único bit que indica o início da transmissão de um frame. O start bit é sempre um '0' (nível baixo).
2. **Data Bits**: Entre 5 e 9 bits que representam os dados a serem transmitidos.
3. **Parity Bit (Opcional)**: Um bit adicional utilizado para verificar erros durante a transmissão.
4. **Stop Bit**: Um ou dois bits que indicam o final de um frame. O stop bit é sempre '1' (nível alto).

### Diagrama de um Frame UART:

| Start | Data Bits (5-9) | Paridade (Opcional) | Stop (1-2) |


## Termos Importantes

Aqui estão alguns termos que você precisa entender para compreender a comunicação UART:

1. **Transmissão Assíncrona**: É um tipo de comunicação onde o receptor e o transmissor não compartilham um sinal de clock comum. Em vez disso, o receptor sincroniza com o transmissor através dos bits de start e stop do frame de dados.
   
2. **Start Bit**: Sinaliza o início da transmissão. Normalmente, é um nível lógico baixo (0).
   
3. **Stop Bit**: Indica o fim de uma transmissão. É um nível lógico alto (1) e pode haver um ou dois bits de stop.
   
4. **TX, RX, GND**: TX é o pino de transmissão, RX é o pino de recepção, e GND é o aterramento comum entre os dispositivos.
   
5. **Baud Rate**: A taxa de bits por segundo (bps) transmitidos na comunicação UART. Exemplo: 9600 bps significa que 9600 bits são transmitidos a cada segundo.
   
6. **Bit Rate**: Refere-se à quantidade de dados (bits) transmitidos ou recebidos por unidade de tempo.
   
7. **Buffer**: Área de memória usada temporariamente para armazenar os dados durante a comunicação.
   
8. **Frame**: A estrutura completa de dados transmitidos, composta por bits de início, dados, paridade e parada.
   
9. **Bit de Paridade**: Bit opcional usado para detecção de erros. Pode ser par ou ímpar.
   
10. **CRC (Cyclic Redundancy Check)**: Um método de verificação de erros mais robusto do que a paridade simples, utilizado para garantir a integridade dos dados.

## O Que é Loopback?

O conceito de **loopback** envolve conectar o pino de transmissão (TX) ao pino de recepção (RX) para criar um ciclo fechado de comunicação. Nesse projeto, o loopback é feito para que tudo o que o seu computador enviar ao Arduino seja imediatamente devolvido, espelhando a transmissão de dados. Isso é útil para testar a comunicação sem um segundo dispositivo.


## Leituras Recomendadas

Para se aprofundar na transmissão serial UART, consulte os seguintes links:

- [UART em FreeBSD](https://docs.freebsd.org/pt-br/articles/serial-uart/)
- [Transmissão Serial UART](http://www1.rc.unesp.br/igce/demac/alex/disciplinas/MicroII/EMA864315-Serial.pdf)
- [Transmissão e Recepção Assíncrona](https://www2.pcs.usp.br/~labdig/pdffiles_2012/tx_e_rx_as.pdf)
- [UART Basics](https://ece353.engr.wisc.edu/serial-interfaces/uart-basics/)

# Introdução aos Filtros Digitais

## Visão Geral

Neste projeto, você irá trabalhar com filtros digitais, que são sistemas que processam sinais discretos para modificar suas características em frequência. Os filtros digitais são fundamentais em processamento de sinais e têm aplicações em diversas áreas.

## O que são Filtros Digitais?

Filtros digitais são sistemas que processam sinais discretos para:
1. **Selecionar** frequências específicas
2. **Remover** ruídos indesejados
3. **Modificar** características do sinal
4. **Realizar** análise espectral

## Tipos de Filtros Digitais

### 1. Filtros FIR (Finite Impulse Response)
- Resposta ao impulso finita
- Sem feedback
- Estável
- Linear em fase

### 2. Filtros IIR (Infinite Impulse Response)
- Resposta ao impulso infinita
- Com feedback
- Pode ser instável
- Menor ordem

## Características dos Filtros

### 1. Resposta em Frequência
- Banda passante
- Banda de rejeição
- Frequência de corte
- Ripple

### 2. Resposta ao Impulso
- Duração
- Forma
- Estabilidade
- Causalidade

## Projeto de Filtros

### 1. Especificações
- Tipo de filtro
- Frequências de corte
- Atenuação
- Ripple

### 2. Implementação
- Cálculo dos coeficientes
- Estrutura do filtro
- Quantização
- Otimização

## Aplicações Práticas

### 1. Processamento de Áudio
- Equalização
- Redução de ruído
- Compressão
- Efeitos sonoros

### 2. Processamento de Imagens
- Suavização
- Detecção de bordas
- Realce
- Restauração

### 3. Comunicações
- Modulação
- Demodulação
- Sincronização
- Equalização

## Implementação no Projeto

No seu projeto, você irá:

1. Projetar diferentes filtros
2. Implementar os filtros
3. Analisar a resposta
4. Testar aplicações

## Ferramentas e Recursos

- Python para implementação
- Bibliotecas de processamento de sinais
- Ferramentas de análise espectral
- Visualização de sinais

## Próximos Passos

1. Familiarize-se com os filtros digitais
2. Projete os filtros
3. Implemente as soluções
4. Teste e documente


