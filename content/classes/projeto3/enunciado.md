# Projeto 3: Datagrama

## Objetivo

Implementar um sistema de comunicação baseado em datagramas, demonstrando os conceitos fundamentais de comunicação em pacotes e protocolos de rede.

## Descrição

Neste projeto, você irá desenvolver um programa que:

1. Implementa a estrutura de um datagrama
2. Realiza a fragmentação e reassemblagem de pacotes
3. Implementa um protocolo de comunicação baseado em datagramas
4. Demonstra o funcionamento do sistema de comunicação

## Requisitos

- Python 3.x
- Biblioteca socket (opcional)
- Conhecimentos sobre protocolos de rede
- Entendimento sobre fragmentação de pacotes

## Entregáveis

1. Código fonte do programa implementado
2. Relatório técnico contendo:
   - Descrição da implementação do datagrama
   - Análise do protocolo de comunicação
   - Resultados dos testes realizados
   - Discussão sobre possíveis melhorias

## Avaliação

O projeto será avaliado considerando:

- Corretude da implementação
- Qualidade do código e documentação
- Relatório técnico
- Apresentação oral

## Datas

- Entrega: [Data a ser definida]
- Apresentação: [Data a ser definida]

## Recursos Adicionais

- [Link para documentação sobre datagramas]
- [Link para tutoriais sobre protocolos de rede]
- [Link para exemplos de código]

## Detalhes Técnicos

### Estrutura do Datagrama

O datagrama deve conter:

1. **Cabeçalho**
   - Identificador do pacote
   - Tamanho total
   - Flags de controle
   - Offset de fragmentação

2. **Dados**
   - Payload do pacote
   - Padding se necessário

### Funcionalidades

Você deve implementar:

1. **Fragmentação**
   - Divisão de pacotes grandes
   - Geração de fragmentos
   - Controle de sequência

2. **Reassemblagem**
   - Ordenação de fragmentos
   - Verificação de integridade
   - Tratamento de perdas

3. **Protocolo**
   - Controle de fluxo
   - Retransmissão
   - Timeout

### Conceitos de Avaliação

#### Conceito C
- Implementar estrutura básica do datagrama
- Realizar fragmentação simples

#### Conceito B
- Implementar reassemblagem
- Adicionar controle de sequência

#### Conceito B+
- Implementar protocolo completo
- Adicionar retransmissão

#### Conceito A+
- Implementar todas as funcionalidades
- Otimizar performance
- Documentar limitações

