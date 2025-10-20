# Projeto 7 – Equalizador de Áudio Multibanda

## Objetivo

**`Após a resolução dos exercícios propostos`**, você deverá construir um equalizador de áudio capaz de atuar em **12 bandas de frequências** (ou mais, se desejar).

## Funcionalidades Requeridas

- O usuário deve poder configurar o filtro para atenuar ou amplificar cada uma das frequências em diferentes níveis
- Interface com o usuário pode ser CLI ou GUI
- A atenuação e amplificação de cada faixa deve estar entre **-10dB a +10dB**
- Utilizar as frequências especificadas na figura fornecida
- Obter a função de transferência discreta dos filtros usando o código `filtro_peak_EQ` disponibilizado via BB (código-base: [filtro_peak_EQ.ipynb](filtro_peaking_EQ.ipynb))
- Manter um áudio curto gravado para testes
- Plotar o **Diagrama de Bode do filtro completo**
- Desenvolver método para obter uma função de transferência equivalente a todas as funções individuais de cada banda

## Arquitetura Recomendada
![alt text](image-6.png)

### Fluxo da Aplicação

1. **Configuração inicial**: usuário define amplificação/atenuação de cada banda
2. **Processamento**: código obtém as funções de transferência coerentes com a configuração
3. **Aplicação dos filtros**: aplicar os filtros um a um ao sinal
4. **Reprodução**: executar o sinal resultante após o sinal original para comparação

## Especificações Técnicas

| Parâmetro          | Valor / Faixa                     |
|--------------------|-----------------------------------|
| Bandas de frequência | 31 Hz, 63 Hz, 125 Hz, 250 Hz, 500 Hz, 1 kHz, 2 kHz, 4 kHz, 8 kHz, 16 kHz, 20 kHz (ajuste conforme necessário) |
| Ganho por banda     | –10 dB ➔ +10 dB (passo 1 dB)      |
| Tipo de filtro      | **Peaking EQ** (código-base: [filtro_peak_EQ.ipynb](filtro_peaking_EQ.ipynb)) |
| Ordem do filtro     | 2ª ordem (bi-quad) por banda      |
| Taxa de amostragem  | 44,1 kHz (ou igual ao do arquivo de teste) |
| Formato do áudio    | `.wav`, 16 bits, mono ou estéreo (tratar ambos os canais) |


## Rubrica

| Nota | Requisitos |
|------|------------|
| **C** | Filtros implementados e atuando no sinal |
| **B** | Interface com usuário bem construída, execução dos áudios |
| **A** | Diagrama de Bode do filtro completo |
| **C+, B+, A+** | Atribuídas mediante contexto geral, capricho e resolução dos exercícios |