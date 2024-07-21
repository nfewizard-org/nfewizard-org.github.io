# Uso Indevido

!!! Warning "Uso Indevido"
    `ATENÇÃO`: O contribuinte que estiver utilizando indevidamente os sistemas poderá sofrer as penalidades definidas na legislação de cada UF.
<br>

Para mais informações sobre o uso indevido consulte os documentos abaixo:<br> 
[`Manual de Orientação ao Contribuinte da Nota Fiscal Eletrônica - 4.3.8`](http://moc.sped.fazenda.pr.gov.br/).<br>
[`Notas Técnicas - Nota Técnica 2014.002 - v.1.21 - Publicada em 27/06/2024`](https://www.nfe.fazenda.gov.br/portal/listaConteudo.aspx?tipoConteudo=04BIflQt1aY=).<br>
`Obs: Podem haver versões mais atualizadas para as notas técnicas aqui informadas.`
<br><br>

## Regras de Uso Indevido - NT 2014.002 - Versões 1.21 – Junho de 2024

#### 3.11.4. Recomendações Para Evitar o Uso Indevido
A análise do comportamento atual das aplicações das empresas (“aplicação cliente”) permite
identificar algumas situações de “uso indevido” nos ambientes autorizadores.
Como exemplo maior do mau uso do ambiente, ressalta-se a falta de controle de algumas
aplicações que entram em “loop”, consumindo recursos de forma indevida, sobrecarregando
principalmente o canal de comunicação com a Internet.
Para este Web Service serão mantidos controles para identificar as situações de uso indevido
de sucessivas tentativas de busca de registros já disponibilizados anteriormente, quando utilizada a tag:
distNSU.
As novas tentativas serão rejeitadas com o erro “656–Rejeição: Consumo Indevido”.
#### 3.11.4.1 - O uso indevido relativo ao Web Service NFeDistribuicaoDFe na consulta com tag:distNSU é baseado nos critérios descritos abaixo:
##### 1) Não há mais documentos a distribuir e usuário continua consultando:
Se não existir mais documentos a serem retornados (cStat=137) o usuário deve aguardar uma hora
para realizar nova consulta. A realização de novas consultas em 1h, após receber a mensagem
cStat137, gerará o uso indevido, retornando cStat=656. Nesse caso, o CNPJ é bloqueado por 1 hora,
sendo impedido de realizar novas consultas nesse intervalo. Decorrido o intervalo de tempo, o
desbloqueio será automático.
O campo xMotivo traz a seguinte descrição para ajudar o usuário a entender o que está causando o
uso indevido: “Rejeicao: Consumo Indevido. Deve ser aguardado 1 hora para efetuar nova solicitação caso
não existam mais documentos a serem pesquisados. Tente apos 1 hora”
##### 2) Usuário não está consultando os NSU de forma sequencial:

O usuário deve sempre realizar a consulta baseada no ultNsu retornado na consulta anterior, ou
seja, deve usar os valores do ultNSU retornados pelo serviço nas chamadas subsequentes. O valor
do ultNSU corresponde ao ponto de onde a leitura dos blocos de documentos deve continuar.
Quando ultNSU for igual ao valor do maxNSU retornado pelo serviço, quer dizer que não existem
mais documentos para serem recuperados. Neste caso, para não haver bloqueio por uso indevido,
deve-se aguardar 1 hora para realização de novas consultas.
Se consultar fora da sequência, será bloqueado. Decorrido o intervalo de tempo, o desbloqueio será
automático.

O campo xMotivo traz a seguinte mensagem: “Rejeicao: Consumo Indevido. Deve ser utilizado o ultNSU
nas solicitacoes subsequentes. Tente apos 1 hora”

`Atenção`: Se diversas aplicações do mesmo ator (emitente ou destinatário ou transportador na NF-e
ou indicado no campo autxml) da NF-e efetuarem consultas por NSU para o mesmo CNPJ (14 dígitos
– informado na requisição xml), essas devem seguir a
mesma sequência de numeração ordenada e de forma ascendente. Caso contrário, enquadrar-seão na categoria de uso indevido.

`Observação`: A partir da data informada na versão 1.14 desta Nota Técnica, o número da última
consulta realizada para o CNPJ de 14 dígitos informado na requisição passou a ser retornado no XML
da rejeição 656 (consumo indevido), caso a consulta tenha sido efetuada com a tag “distNSU”. Assim,
caso o usuário não conheça o número do ultNSU, pode realizar a consulta a partir deste número.

#### 3.11.4.2 - O uso indevido relativo ao Web Service NFeDistribuicaoDFe nas consultas com tag: consChNFe e tag: consNSU:
As consultas por chave de acesso e por NSU foram construídas para permitirem ao usuário buscar
pontualmente alguma NF-e e de um período retroativo máximo de 90 (noventa) dias. Se o usuário
necessitar fazer download de todas as NF-es de no máximo 90 dias de um CNPJ ator interessado,
deve usar a consulta “distNSU”.

##### 1) Consultada uma quantidade de NF-e ou NSU superior ao limite permitido por hora:
Será permitido um número limitado de consultas por chave de acesso ou NSU em um período de
1hora. Se o usuário continuar consultando após atingir o limite de consultas por chave de acesso ou
NSU em 1h, retornará a mensagem 656 – Consumo indevido – ultrapassou o limite de 20 consultas
por hora. Nesse caso, o CNPJ é bloqueado por 1 hora, sendo impedido de realizar novas consultas
nesse intervalo. Decorrido o intervalo de tempo, o desbloqueio será automático.
Observação: Em quaisquer dos três tipos de consulta, quando o usuário receber a mensagem 656
– consumo indevido, deve aguardar 1hora. Se retomar a consulta antes de completar 1 (uma) hora,
o tempo é zerado e a contagem reiniciará até completar 1hora.
