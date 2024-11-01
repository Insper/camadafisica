# Introdução à Modulação

> **Arquivo PDF do projeto**: [Modulação AM](slides.pdf)

A modulação é um processo fundamental em telecomunicações e engenharia elétrica, permitindo a transmissão eficaz de sinais de informação através de diversos meios físicos. Este documento aborda a modulação em amplitude (AM), fornecendo uma análise técnica detalhada adequada para estudantes de engenharia de computação.

## 1. Conceitos Fundamentais

### 1.1 Sinais e Sistemas

- **Sinal**: Função que representa a variação de uma quantidade física ao longo do tempo ou espaço, como tensão, corrente ou potência.
- **Sistema**: Entidade que processa sinais, podendo ser caracterizado por suas respostas no tempo e na frequência.

### 1.2 Onda Portadora e Sinal Modulante

- **Onda Portadora (\( c(t) \))**: Sinal de alta frequência que serve como meio para transportar o sinal de informação. Geralmente uma senoide pura:

  $$
  c(t) = A_c \cos(2\pi f_c t + \phi_c)
  $$

  Onde:
  - \( A_c \): Amplitude da portadora.
  - \( f_c \): Frequência da portadora.
  - \( \phi_c \): Fase inicial da portadora.

- **Sinal Modulante (\( m(t) \))**: Sinal de informação que se deseja transmitir, geralmente de baixa frequência (como áudio ou dados):

  $$
  m(t): |m(t)| \leq 1
  $$

### 1.3 Parâmetros da Onda

- **Amplitude (\( A \))**: Valor máximo da variação do sinal.
- **Frequência (\( f \))**: Número de ciclos por segundo (Hz).
- **Fase (\( \phi \))**: Deslocamento do início do ciclo em relação ao tempo zero.

## 2. Modulação em Amplitude (AM)

### 2.1 Definição

A modulação em amplitude é um método em que a amplitude da onda portadora é variada proporcionalmente ao sinal modulante, enquanto a frequência e a fase permanecem constantes.

### 2.2 Equação Geral do Sinal AM

O sinal modulado em AM é dado por:

$$
s(t) = [A_c + A_m m(t)] \cos(2\pi f_c t)
$$

Onde:
- \( A_m \): Amplitude máxima do sinal modulante.

Se \( m(t) \) for normalizado tal que \( |m(t)| \leq 1 \), podemos escrever:

$$
s(t) = A_c [1 + m(t)] \cos(2\pi f_c t)
$$

O termo \( [1 + m(t)] \) representa a variação da amplitude da portadora de acordo com o sinal de informação.

## 3. Análise Matemática Detalhada

### 3.1 Índice de Modulação (\( m \))

O índice de modulação quantifica a profundidade da modulação:

$$
m = \frac{A_m}{A_c}
$$

- **Submodulação**: \( 0 \leq m < 1 \)
- **Modulação Total**: \( m = 1 \)
- **Sobremodulação**: \( m > 1 \) (leva a distorções)

### 3.2 Expansão do Sinal AM

Usando \( m(t) = m \cos(2\pi f_m t) \):

$$
s(t) = A_c [1 + m \cos(2\pi f_m t)] \cos(2\pi f_c t)
$$

Expandindo:

$$
s(t) = A_c \cos(2\pi f_c t) + A_c m \cos(2\pi f_m t) \cos(2\pi f_c t)
$$

Aplicando a identidade trigonométrica:

$$
\cos A \cos B = \frac{1}{2} [\cos(A + B) + \cos(A - B)]
$$

Temos:

$$
s(t) = A_c \cos(2\pi f_c t) + \frac{A_c m}{2} \left[ \cos 2\pi(f_c + f_m)t + \cos 2\pi(f_c - f_m)t \right]
$$

### 3.3 Componentes Espectrais

O sinal AM possui três componentes:

1. **Portadora**: \( A_c \cos(2\pi f_c t) \)
2. **Banda Lateral Superior (BLS)**: \( \frac{A_c m}{2} \cos 2\pi(f_c + f_m)t \)
3. **Banda Lateral Inferior (BLI)**: \( \frac{A_c m}{2} \cos 2\pi(f_c - f_m)t \)

## 4. Espectro de Frequência e Largura de Banda

### 4.1 Espectro de Frequência

![Espectro de Frequência AM](am-spectrum.png)

No domínio da frequência, o espectro do sinal AM consiste em:

- **Frequência Portadora**: Pico em \( f_c \)
- **Bandas Laterais**: Simétricas em torno de \( f_c \), em \( f_c \pm f_m \)

### 4.2 Largura de Banda Necessária

A largura de banda total (\( BW \)) requerida é:

$$
BW = 2 f_m^{\text{máx}}
$$

Onde \( f_m^{\text{máx}} \) é a frequência máxima do sinal modulante.

### 4.3 Considerações Espectrais

- **Eficiência Espectral**: AM convencional não é eficiente, pois a portadora e as bandas laterais ocupam espaço espectral significativo.
- **Ocupação de Espectro**: A portadora não carrega informação, mas consome potência e largura de banda.

## 5. Eficiência de Potência

### 5.1 Potência da Portadora e Bandas Laterais

- **Potência da Portadora (\( P_c \))**:

  $$
  P_c = \frac{A_c^2}{2R}
  $$

- **Potência Total (\( P_t \))**:

  $$
  P_t = P_c \left( 1 + \frac{m^2}{2} \right)
  $$

Onde \( R \) é a resistência de carga.

### 5.2 Eficiência da Modulação AM

A eficiência (\( \eta \)) é dada por:

$$
\eta = \frac{\text{Potência nas Bandas Laterais}}{\text{Potência Total}} = \frac{m^2}{2 + m^2}
$$

- **Máxima Eficiência**: Ocorre quando \( m = 1 \), resultando em \( \eta_{\text{máx}} = 33.33\% \)
- **Ineficiente**: Grande parte da potência é desperdiçada na portadora.

## 6. Implementação Prática e Circuitos

### 6.1 Moduladores AM

#### 6.1.1 Modulador de Produto

Multiplica o sinal modulante pela portadora:

$$
s(t) = m(t) \cdot c(t)
$$

#### 6.1.2 Modulador Balanceado

Elimina a portadora, gerando um sinal DSB-SC (Double Sideband Suppressed Carrier).

#### 6.1.3 Modulador em Anel (Ring Modulator)

Utiliza diodos em configuração de ponte para modular o sinal, suprimindo a portadora.

### 6.2 Demoduladores AM

#### 6.2.1 Detector de Envoltória

Extrai a envoltória do sinal AM, recuperando o sinal modulante.

- **Circuito Básico**: Diodo retificador seguido de filtro RC.

#### 6.2.2 Detector Síncrono

Multiplica o sinal recebido por uma portadora local sincronizada.

- **Vantagem**: Melhor rejeição ao ruído.
- **Desvantagem**: Maior complexidade.

## 7. Impacto do Ruído e Interferência

### 7.1 Sensibilidade ao Ruído

- **Amplitude**: Componentes de ruído somam-se ao sinal, afetando a qualidade.
- **Ruído Adicional**: Interferências eletromagnéticas impactam diretamente a amplitude.

### 7.2 Relação Sinal-Ruído (SNR)

A SNR em AM é menor comparada a outras modulações, como FM, devido à sensibilidade à variação de amplitude.

### 7.3 Técnicas de Mitigação

- **Filtragem**: Uso de filtros para remover ruídos fora da banda de interesse.
- **Limitadores**: Não são eficazes em AM, pois cortariam a amplitude útil do sinal.

## 8. Comparação com Outras Técnicas de Modulação

### 8.1 Modulação em Frequência (FM)

- **Vantagem**: Maior imunidade ao ruído.
- **Desvantagem**: Maior complexidade e largura de banda necessária.

### 8.2 Modulação em Fase (PM)

- **Similar ao FM**, mas modula a fase da portadora.

### 8.3 Modulação por Deslocamento de Amplitude (ASK)

- **Digital**: Níveis discretos de amplitude representam dados binários.

### 8.4 Modulação em Quadratura de Amplitude (QAM)

- **Combina AM e PM**: Modula amplitude e fase simultaneamente para aumentar a eficiência espectral.

## 9. Aplicações Avançadas

### 9.1 DSB-SC (Double Sideband Suppressed Carrier)

- **Características**: Portadora suprimida, apenas bandas laterais transmitidas.
- **Vantagem**: Maior eficiência de potência.

### 9.2 SSB (Single Sideband)

- **Características**: Transmite apenas uma banda lateral.
- **Vantagem**: Redução de largura de banda e potência necessária.

### 9.3 VSB (Vestigial Sideband)

- **Características**: Transmite uma banda lateral completa e parte da outra.
- **Aplicação**: Transmissão de sinais de TV analógica.

## 10. Exemplos Práticos e Problemas Resolvidos

### 10.1 Exemplo 1: Cálculo do Índice de Modulação

**Dados**:

- \( A_c = 10 \, V \)
- \( A_m = 5 \, V \)

**Cálculo**:

$$
m = \frac{A_m}{A_c} = \frac{5}{10} = 0.5
$$

### 10.2 Exemplo 2: Potência em AM

**Dados**:

- \( A_c = 10 \, V \)
- \( m = 1 \)
- \( R = 50 \, \Omega \)

**Potência da Portadora**:

$$
P_c = \frac{A_c^2}{2R} = \frac{10^2}{2 \times 50} = 1 \, W
$$

**Potência Total**:

$$
P_t = P_c \left( 1 + \frac{m^2}{2} \right) = 1 \left( 1 + \frac{1}{2} \right) = 1.5 \, W
$$

### 10.3 Problema Resolvido: Largura de Banda

**Questão**: Qual a largura de banda necessária para transmitir um sinal de áudio com frequências até \( 5 \, kHz \) usando AM?

**Resposta**:

$$
BW = 2 f_m^{\text{máx}} = 2 \times 5 \, kHz = 10 \, kHz
$$

## 11. Diagramas e Ilustrações Detalhadas

### 11.1 Forma de Onda no Domínio do Tempo

![Forma de Onda AM no Tempo](am-time-domain.png)

### 11.2 Esquema de Circuito de Modulador AM

![Circuito de Modulador AM](am-modulator-circuit.png)

### 11.3 Esquema de Circuito de Demodulador AM

![Circuito de Demodulador AM](am-demodulator-circuit.png)

## 12. Normas e Regulamentações

### 12.1 Alocação de Frequências

- **Órgãos Reguladores**: ANATEL (Brasil), FCC (EUA), ITU (Internacional).
- **Bandas Designadas**: Ondas médias (530 kHz a 1710 kHz), ondas curtas, etc.

### 12.2 Limitações Legais

- **Potência Máxima**: Regulamentada para evitar interferência.
- **Espectro**: Uso eficiente e compartilhado requer conformidade com normas.

## Referências

1. **Haykin, S.** "Communication Systems", 5th Edition, Wiley, 2009.
2. **Proakis, J.G., Salehi, M.** "Fundamentals of Communication Systems", Prentice Hall, 2005.
3. **Lathi, B.P.** "Modern Digital and Analog Communication Systems", Oxford University Press, 2010.

