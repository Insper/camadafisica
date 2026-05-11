# Projeto 8: Modulação AM (Amplitude Modulation)

Você deverá nesse projeto gravar `3 arquivos` de áudio de poucos segundos. Esses 3 áudios digitalizados a uma taxa de 44100 Hz (ou 44800) deverão ser modulados em amplitude (AM) cada um dentro de uma das 3 faixas:

- Faixa 1 : de 9 kHz a 12 kHz
- Faixa 2 : de 12 kHz a 15 kHz
- Faixa 3 : de 15 kHz a 18 kHz

Esses sinais modulados representam 3 sinais de e diferentes estações de rádio.

!!!warning "Atenção"
     Verifique que nenhum dos 3 sinais modulados invadiram outras bandas!   


Some os 3 sinais modulados e obtenha um sinal resultante que equivale ao sinal resultante presente no meio físico (superfície) onde receptores captam o sinal.

Utilize filtros digitais (como os do projeto 7) e extraia cada um dos 3 sinais do sinal resultante, como se fosse um rádio receptor, capaz de captar as 3 estações.

Demodule cada um dos 3 sinais, obtendo os áudios originais separados em 3 arquivos.

Você e sua dupla poderão fazer apenas uma aplicação simulando tanto o lado emissor quanto o receptor.

## O que entregar

Você deverá:

- Executar os 3 áudios originais
- Apresentar o gráfico FFT dos 3 áudios modulados.
- Apresente o gráfico FFT do sinal resultante da soma dos 3 sinais modulados.
- Apresente o gráfico FFT dos 3 sinais modulados extraídos do sinal resultante (lado receptor).
- Execute os 3 áudios demodulados no lado receptor.

A nota será atribuída durante a apresentação com base na resolução dos exercícios propostos e clareza e funcionamento dos códigos.