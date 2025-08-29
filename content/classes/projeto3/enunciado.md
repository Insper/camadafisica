# Enunciado do Projeto 03

Nesse projeto, sua aplicação que exerce o papel de **client** deverá realizar **download de arquivos** vindos da
aplicação **server**. Esses arquivos deverão ser fragmentados e enviados através de "pacotes" (*datagramas*). Deverá
existir **handshake** e **confirmação de recebimento** de cada pacote, como explicado a seguir!

## Datagrama

Você pode definir como será seu datagrama, mas aconselhamos a reservar uma boa quantidade de bytes (10 ou 12 bytes) para o head, a fim de ter espaço suficiente para uma boa comunicação entre as partes. O tamanho do head deve ser fixo. O payload pode ter tamanho variável durante a transmissão, mas **nunca poderá ser maior que 100 Bytes**. Além disso sugerimos um EOP de sua libre escolha com 3 ou 4 bytes.

> Não importa o tipo de mensagem, sempre será enviada através de um datagrama como definido acima, tanto de *client* para *server* como no sentido oposto.

## Handshake

Antes do envio da mensagem, o **client** deve enviar uma mensagem para verificar se o **server** está "vivo" e indagar quais arquivos estão disponíveis.

O **server** deve responder com os nomes dos arquivos disponíveis, e esses nomes deverão aparecer no terminal do cliente caso contrario um Timeout de 3 segundos se não houver resposta.




## Escolha de 2 ou mais arquivos.

O client então solicita um dos arquivos. O server deve responder algo como: “arquivo x escolhido, deseja adicionar outro arquivo?”
O cliente deverá então escolher um segundo arquivo.
O server deve responder com “arquivo x e y escolhidos, deseja adicionar outro arquivo?”
Se o client responder que sim, o server fornece a lista disponível, o cliente escolhe outro arquivo, e o server vai
registrando as escolhas. Se o cliente responder que não, o server deve responder algo como: “entendido. Vou iniciar
a transmissão simultânea dos arquivos escolhidos”

## Transmissão

A transmissão deve ser necessariamente feita da seguinte maneira:

Toda vez que o server enviar um pacote de um dos arquivos, o cliente deve responder confirmando o recebimento, e só então o server envia o próximo. Todas essas confirmações devem estar sendo printadas no terminal. Descreva tudo que esteja ocorrendo através de prints.

Os pacotes devem ser alternados, ou seja, um pacote de cada arquivo, sendo que os dois ou mais arquivos sejam transmitidos simultaneamente enquanto a transmissão não termina. À medida que arquivos sejam enviados completamente, apenas os pacotes dos arquivos ainda em transmissão são enviados, obviamente.

## Fim

Os arquivos devem ser salvos no computador do cliente e não podem estar "corrompidos".
Um print com o resumo da transmissão deve aparecer, mostrando tamanho dos arquivos recebidos, número de pacotes de cada arquivo.


## Critérios de Entrega

Fique atento à data de entrega.

### Conceito C (nota 5)
- Uma transmissão de sucesso de 2 arquivos simultâneos escolhidos pelo usuário.

### Conceito B (nota 7,5)
- Transmissão de sucesso mais a funcionalidade em que o usuário client poderá apartar uma tecla para pausar
o processo, uma outra tecla para reiniciar o processo e outra para abortar a transmissão.

### Conceito A (nota 9)
- Uma simulação em que se os fios entre os Arduinos (qualquer um deles ou ambos) forem desconectados e conectados novamente, a transmissão retorna e termina com sucesso!

### Conceito A+ (nota 10)
- Todas as funcionalidades com prints caprichados de todo o processo no lado cliente e também server!


> Dica! Lembre-se sempre que server e client podem conversar autonomamente através de mensagens no head. Cada byte em cada posição do head pode significar algo! Além disso, o time out pode ser usado para tomada de decisões caso algo esperado não ocorra... Criem seu próprio protocolo de download baseado em datagramas!