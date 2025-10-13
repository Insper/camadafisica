# PROJETO 6 – Identificador de acordes (prática Fourier)

> Antes de apresentar o projeto, a dupla deverá mostrar a **resolução dos exercícios propostos**.
>
> [Exercício de Fourier](Fourier.pdf)
> [Código python de referência](FFT.py)


Nesse projeto, você deverá implementar dois softwares em dois diferentes computadores. Um computador deverá reproduzir, por alguns segundos, um áudio composto por 3 frequências específicas (3 notas musicais) que compõemuma tríade (acorde com 3 notas). Na cultura ocidental, a música é composta por 12 frequências e múltiplos inteiros dessas frequências. Claro que instrumentos produzem uma gama enorme de frequências, mas a maior parte da energia está concentrada na produção de algumas dessas 12 frequências. Para produzir o som com as 3 frequências desejadas você deverá usar funções da biblioteca sounddevice. Para isso, você deverá gerar 3 senoides de frequências desejadas, soma-las e executá-las através da função sd.play. A variável tone deve conter o sinal, ou seja, as senoides a serem executadas. A variável fs contém a frequência de amostragem (mesma que a de execução).

```python 
import numpy as np
import sounddevice as sd

sd.play(tone, fs)
# aguarda até o fim do audio
sd.wait()
```

O lado emissor deverá produzir então um dos acordes listados abaixo, com suas 3 respectivas frequências:

| Tom (Escala)     | Notas (Frequências em Hz)                |
|------------------|------------------------------------------|
| Dó maior         | 523.25 Hz · 659.25 Hz · 783.99 Hz        |
| Ré menor         | 587.33 Hz · 698.46 Hz · 880.00 Hz        |
| Mi menor         | 659.25 Hz · 783.99 Hz · 987.77 Hz        |
| Fá maior         | 698.46 Hz · 880.00 Hz · 1046.50 Hz       |
| Sol maior        | 783.99 Hz · 987.77 Hz · 1174.66 Hz       |
| Lá menor         | 880.00 Hz · 1046.50 Hz · 1318.51 Hz      |
| Si menor (5b)    | 493.88 Hz · 587.33 Hz · 698.46 Hz        |



Esse sinal de áudio deve ser executado pela sua placa de som e captado por outro computador. O computador que receberá o áudio deverá identificar o acorde reproduzido através da transformada de Fourirer. Para detectar o acorde, a segunda aplicação deve capturar o sinal de áudio gerado por outro computador, identificar os picos através da transformada de Fourier. A transformada de Fourier terá vários picos, os 3 relativos às frequências do acorde escolhido pelo emissor e outras frequências introduzidas pelos ruídos do ambiente. Procure funções para identificar picos em Python! Há várias disponíveis. Você deverá identificar os picos na resposta da transformada de Fourier. Na mesma lista utilizada para fazer o gráfico.


Para captar o áudio, você poderá usar a função rec

```python
# agora para graver, utilize
audio = sd.rec(int(numamostras), freqDeAmostragem, chanels=1)
sd.wait()
print("... FIM")
```

**Muitas vezes a gravação retorna uma lista de listas. Você poderá ter que tratar o sinal gravado para ter apenas uma lista!**

## Requisitos do Código

### Lado Emissor

- Perguntar ao usuário qual **acorde** será executado.  
- Emitir, por alguns segundos, as **3 frequências** relativas ao acorde escolhido.  
- Plotar o **gráfico no domínio do tempo** com a soma das duas frequências: `x(t)`.  
- Plotar o **gráfico no domínio da frequência** do sinal emitido (Transformada de Fourier `X(f)`).  

### Lado Receptor

- Captar o **sinal de áudio** emitido pela aplicação do emissor através do microfone.  
  > Tente não gravar silêncio — inicie a gravação logo após o início da execução.  

- Verificar se a gravação ficou com **bom volume**.  
  > Você pode ajustar o volume multiplicando ou dividindo todos os pontos do sinal por um valor.  

- Calcular a **Transformada de Fourier** do sinal captado.  
- **Identificar os picos** no espectro:  
  > Se houver mais de 4 picos, ajuste a sensibilidade da função usada para detecção até ter **no mínimo 5 picos**.  

- **Identificar as frequências** correspondentes aos acordes e, assim, **reconhecer o acorde**.  
- Plotar o **gráfico no tempo** do sinal recebido.  
- Plotar o **gráfico da transformada de Fourier** do sinal recebido.  


## Rubrica de Avaliação

| Conceito | Critério de Desempenho |
|-----------|------------------------|
| **D** | Produz o sinal corretamente, mas **não reconhece** o acorde. |
| **C** | Reconhece o acorde no lado do receptor **de maneira intermitente** (não funciona todas as vezes). |
| **B** | Reconhece o acorde no lado do receptor **em todas as tentativas**. |
| **A / A+** | Reconhece o acorde **e plota todos os gráficos corretamente** (avaliação final depende da apresentação e organização). |

> Antes de apresentar o projeto, a dupla deverá mostrar a **resolução dos exercícios propostos**.

