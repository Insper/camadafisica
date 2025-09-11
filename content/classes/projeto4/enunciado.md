# Enunciado do Projeto

Você deverá implementar um mecanismo de **verificação de integridade da transmissão** (*checksum*).  
Isso deve ser feito utilizando **CRC-16**.

Em aula, seu professor explicou como funciona esse algoritmo.  
Você **não precisará implementá-lo do zero**, apenas utilizar alguma biblioteca que o contenha.  
Caso queira relembrar o funcionamento, poderá pesquisar em material de apoio ou consultar uma ferramenta de IA.

---

## Requisitos

1. Transmitir, em algum campo do *header*, **2 bytes** contendo o CRC-16 do respectivo *payload* (apenas o *payload*) sendo transmitido.  
   Todos os pacotes deverão conter o CRC do *payload*.  

2. Caso o lado receptor (server) detecte uma incoerência entre o CRC enviado e o CRC calculado após o recebimento,  
   este deverá retornar uma mensagem (pacote) informando o erro de CRC e solicitando o reenvio do pacote.  
   Se estiver tudo correto, a resposta deverá indicar ausência de erros e a transmissão seguirá normalmente.  

3. Além do CRC, tanto o cliente quanto o servidor deverão gerar um arquivo `.txt` com **log da transmissão**.  
   Em ambos os lados, uma nova linha deverá ser criada no arquivo sempre que um pacote for enviado ou recebido.  

---

## Estrutura do Log

Cada linha do log deverá conter:

- Instante do envio ou recebimento  
- Tipo de operação (*envio* ou *recebimento*)  
- Tipo de mensagem (de acordo com o protocolo: dados, OK, erro)  
- Tamanho total em bytes  
- Pacote enviado (se for pacote do tipo *dados*)  
- Total de pacotes (se for pacote do tipo *dados*)  
- CRC do *payload* (se for pacote do tipo *dados*)  

Você pode formatar o arquivo como preferir.  
Abaixo, um exemplo de log gerado pelo cliente:

```bash
29/09/2020 13:34:23.089  / envio / 3 / 128 / 1 / 23/ F23F  
29/09/2020 13:34:23.230  / receb / 4 / 14  
29/09/2020 13:34:23.569  / envio / 3 / 128 / 2 / 23/ FE3A  
29/09/2020 13:34:23.885  / receb / 4 / 14  
29/09/2020 13:34:24.029  / envio / 3 / 128 / 3 / 23/1802  
29/09/2020 13:34:24.230  / receb / 4 / 14  
```

### Legenda do exemplo:

- Tipo de pacote dados: número 3
- Pacote de resposta OK: número 4
- Pacotes com até 128 bytes

---

## Condições de Teste

Durante o desenvolvimento, implemente **erros propositais** (*hard coded*) para gerar arquivos de log nas seguintes situações:

- Transmissão sem nenhuma intercorrência  
- Transmissão com erro na ordem dos pacotes enviados pelo cliente  
- Transmissão com erro de CRC  
- Transmissão com interrupção física (fios retirados e reconectados) seguida de reinício da transmissão  

Seu professor irá solicitar transmissões simulando essas condições.

---

## Durante a Apresentação

Durante a correção, seu professor poderá:
- Fazer perguntas sobre o funcionamento do protocolo
- Testar o sistema diante de falhas, como desligamento e religamento de jumpers
- Analisar o comportamento do sistema para verificar a detecção e correção dos erros

---

## Avaliação

As notas **C** a **A+** serão atribuídas com base em:

- Robustez da implementação
- Precisão na detecção e correção de erros
- Funcionalidades implementadas
- Velocidade da transmissão

---

## Prazo de Entrega

- **Data limite:** 18/09/2025