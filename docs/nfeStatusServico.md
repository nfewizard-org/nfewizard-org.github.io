# NFeStatus Servico

!!! Quote ""
    `Função`: Serviço destinado à consulta do status do serviço prestado pelo Portal da Secretaria de Fazenda Estadual.<br>
    `Processo`: síncrono.<br>
    `Método`: nfeStatusServico
<br>

```typescript title="NFE_ConsultaStatusServico" linenums="1"
await nfewizard.NFE_ConsultaStatusServico();
```
<br>

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo     | Descrição                |
    | ---------- | -------- | ------------------------ |
    | `tpAmb`      | Number  | Identificação do Ambiente: 1- Produção; 2- Homologação               |
    | `verAplic`     |  String  | Versão do Aplicativo que recebeu a Consulta. |
    | `cStat`      |  String  | Código do status da resposta para o Lote |
    | `xMotivo`      |  String  | Descrição literal do status da resposta |
    | `cUF`    |  String  | Código da UF que atendeu a solicitação |
    | `dhRecbto`   |  String  | Preenchido com a data e hora do processamento (informado também no caso de rejeição). Formato: “AAAA-MM-DDThh:m m:ssTZD” (UTC –Universal Coordinated Time). |
    | `tMed`   |  String  | Tempo médio de resposta do serviço (em segundos) dos últimos 5 minutos (item 5.7). |
    | `dhRetorno`    |  String  | Preenchido com a data e hora previstas para o retorno do Web Service, no formato “AAAA-MM-DDThh:m m:ss” |
    | `xml`    |  String  | Retorno original da SEFAZ (XML) convertido para String |

```json
{
  "tpAmb": "2",
  "verAplic": "SP_NFE_PL009_V4",
  "cStat": "107",
  "xMotivo": "Serviço em Operação",
  "cUF": "35",
  "dhRecbto": "2024-07-16T16:59:59-03:00",
  "tMed": "1",
  "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeResultMsg xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeStatusServico4\"><retConsStatServ versao=\"4.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><tpAmb>2</tpAmb><verAplic>SP_NFE_PL009_V4</verAplic><cStat>107</cStat><xMotivo>Serviço em Operação</xMotivo><cUF>35</cUF><dhRecbto>2024-07-16T16:59:59-03:00</dhRecbto><tMed>1</tMed></retConsStatServ></nfeResultMsg></soap:Body></soap:Envelope>"
}
```

<br>
Para mais informações sobre o processo consulte [`Web Service – NfeStatusServico`](http://moc.sped.fazenda.pr.gov.br/NFeStatusServico.html).
<br><br>