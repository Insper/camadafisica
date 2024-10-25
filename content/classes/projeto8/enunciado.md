# Modulação AM

## Descritivo

Neste projeto, vamos implementar a transmissão e recepção em Modulação em Amplitude (AM), que permite transmitir sinais de áudio através de diferentes frequências portadoras. Essa prática permitirá compreender os conceitos de modulação e demodulação, além de técnicas de filtragem e análise de sinais.

## Objetivos

- Transmitir um áudio que ocupa bandas de baixas frequências (até 4 kHz) através de um canal de transmissão acústico, utilizando apenas as bandas entre 10 kHz e 18 kHz da placa de áudio do PC.
- Após a transmissão via sinal acústico (alto-falante do PC), o receptor deverá gravar o sinal transmitido, demodular e reproduzi-lo de maneira audível novamente.


## Implementação

Para isso, você deverá construir uma aplicação que executa as seguintes tarefas, sequencialmente:


!!! tip "Dica"
    Em cada etapa da implementação, verifique por meio da Transformada de Fourie se a mesma está corretamente implementada.


### Modulação

1. Faça a leitura de um arquivo de áudio `.wav` de poucos segundos (entre 2 e 5) previamente gravado com uma `taxa de amostragem de 44100 Hz`. Se o áudio for estéreo, utilize apenas um dos canais (esquerdo ou direito) para simplificar a implementação.
2. Aplique um filtro passa baixas com fc em `4kHz`.
3. Reproduza o sinal filtrado e verifique que ele continua audível, embora com menos componentes de alta frequência.
4. Module esse sinal de áudio em AM com uma `portadora de 14.000 Hz`. A portadora deve ser uma senoide começando em zero, gerada com a mesma taxa de amostragem do sinal de áudio.
5. Calcule e normalize o vetor de áudio modulado de modo que todos os pontos do sinal permaneçam `dentro do intervalo [-1, 1]`. Isso pode ser feito dividindo todos os valores do sinal pelo valor máximo absoluto encontrado.
6. Reproduza o sinal modulado e observe que pode não ser audível, devido às altas frequências utilizadas (na faixa superior de audição humana). Isso é esperado e indica que a modulação foi realizada corretamente.

!!! tip "Dica"
    A modulação do sinal poderá ser feita com a multiplicação entre a portadora de amplitude 1 e o sinal importado e normalizado.


### Demodulação

7. No outro computador, grave o áudio transmitido através do microfone, utilizando uma `taxa de amostragem de 44.100 Hz`.
8. Utilize a Transformada de Fourier para verificar que o sinal recebido tem componentes significativas dentro da banda de `10 kHz a 18 kHz`.
9. Demodule em AM o sinal usando a `frequência da portadora`.
10. Aplique um filtro passa-baixas com frequência de corte em `4 kHz` para eliminar as componentes de alta frequência e recuperar o sinal de áudio original.
11. `Reproduza o sinal demodulado` e verifique que ele é audível novamente. Compare a qualidade do áudio com o sinal original filtrado.

!!! tip "Dica"
    A demodulação deverá ser feita com um filtro passa-baixa na frequência de corte do sinal importado. O módulo do sinal poderá ser obtido com a multiplicação do sinal de áudio e a portadora.

#### Filtro passa baixas 

A função a seguir aplica um filtro passa baixas de frequência de corte : *cutoff_hz* e frequência de amostragem *fs* no sinal *signal* passado. O filtro utiliza a janela de Kaiser para projetar um filtro FIR com uma determinada atenuação de ripples na banda de parada (60 dB) e largura de transição.

```
from scipy import signal as sg

def LPF(signal, cutoff_hz, fs):
        #####################
        # Filtro
        #####################
        # https://scipy.github.io/old-wiki/pages/Cookbook/FIRFilter.html
        nyq_rate = fs/2
        width = 5.0/nyq_rate
        ripple_db = 60.0 #dB
        N , beta = sg.kaiserord(ripple_db, width)
        taps = sg.firwin(N, cutoff_hz/nyq_rate, window=('kaiser', beta))
        return( sg.lfilter(taps, 1.0, signal))
```

Exemplo de uso :

``` 
    yDemodFiltrado  = LPF(yDemod, 4000, fs)    
```

Importando um áudio
````
    import soundfile as sf

    audio, samplerate = sf.read('dois.wav')
    yAudio = audio[:,1] # Se o áudio for estério
    samplesAudio = len(yAudio)
````

## Entrega e Avaliação

1. Fazer uma apresentação ao seu professor gravando um áudio, filtrando, modulando e executando esse áudio (antes e depois da modulação). Um segundo computador deve receber esse áudio modulado, demodular e executar o áudio demodulado. Seu professor poderá pedir explicações.

2. Obrigatório: Apresentar os seguintes gráficos, no domínio do tempo e da frequência (Fourier):

    - Gráfico 1: Sinal de áudio original normalizado – domínio do tempo.
    - Gráfico 2: Sinal de áudio filtrado – domínio do tempo.
    - Gráfico 3: Sinal de áudio filtrado – domínio da frequência.
    - Gráfico 4: Sinal de áudio modulado – domínio do tempo.
    - Gráfico 5: Sinal de áudio modulado – domínio da frequência (verifique se as bandas não permitidas não estão sendo ocupadas).
    - Gráfico 6: Sinal de áudio recebido (após transmissão) – domínio da frequência.
    - Gráfico 7: Sinal de áudio demodulado – domínio do tempo.
    - Gráfico 8: Sinal de áudio demodulado – domínio da frequência.
    - Gráfico 9: Sinal de áudio demodulado e filtrado – domínio da frequência.


## Data Limite

- **xx/11** - Após essa data, a nota terá uma redução de 25% a cada semana de atraso.

