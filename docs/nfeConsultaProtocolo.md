# NFeConsulta Protocolo

!!! Quote ""
    `Função`: Serviço destinado ao atendimento de solicitações de consulta da situação atual da NF-e na Base de Dados do Portal da Secretaria de Fazenda &nbsp;Estadual.<br>
    `Processo`: síncrono.<br>
    `Método`: nfeConsulta
<br>

??? Quote "Interface de Entrada"
    | Chave                    | Tipo | Descrição  |
    |--------------------------|-----------|-----------|
    | `chNFe`             | String | Chave de acesso da NFe |


```typescript title="NFE_ConsultaStatusServico" linenums="1"
await nfeWizard.NFE_ConsultaProtocolo('99999999999999999999999999999999999999999999');
```
<br>

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo     | Descrição                |
    | ---------- | -------- | ------------------------ |
    | `tpAmb`      | Number  | Identificação do Ambiente: 1- Produção; 2- Homologação.               |
    | `verAplic`     |  String  | Versão do Aplicativo que recebeu a Consulta. |
    | `cStat`      |  String  | Código do status da resposta para o Lote. |
    | `xMotivo`      |  String  | Descrição literal do status da resposta. |
    | `cUF`    |  String  | Código da UF que atendeu a solicitação. |
    | `dhRecbto`   |  String  | Preenchido com a data e hora do processamento (informado também no caso de rejeição). Formato: “AAAA-MM-DDThh:m m:ssTZD” (UTC –Universal Coordinated Time). |
    | `chNFe`    |  String  | Chave de Acesso da NF-e consultada. |
    | `nProt`    |  String  | Número do protocolo de autorização. |
    | `digVal`    |  String  | Valor do digest (hash) da assinatura digital do documento fiscal. |
    | `xml`    |  String  | Retorno original da SEFAZ (XML) convertido para String. |

```json
{
  "tpAmb": "2",
  "verAplic": "SP_NFE_PL009_V4",
  "cStat": "100",
  "xMotivo": "Autorizado o uso da NF-e",
  "cUF": "35",
  "dhRecbto": "2024-07-16T17:21:44-03:00",
  "chNFe": "99999999999999999999999999999999999999999999",
  "protNFe": {
    "infProt": {
      "tpAmb": "2",
      "verAplic": "SP_NFE_PL009_V4",
      "chNFe": "99999999999999999999999999999999999999999999",
      "dhRecbto": "2024-07-14T09:57:08-03:00",
      "nProt": "999999999999999",
      "digVal": "",
      "cStat": "100",
      "xMotivo": "Autorizado o uso da NF-e"
    }
  },
  "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?> <soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"> <soap:Body> <nfeResultMsg xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeConsultaProtocolo4\"> <retConsSitNFe versao=\"4.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"> <tpAmb>1</tpAmb> <verAplic>SP_NFE_PL009_V4</verAplic> <cStat>100</cStat> <xMotivo>Autorizado o uso da NF-e</xMotivo> <cUF>35</cUF> <dhRecbto>2024-07-11T21:51:46-03:00</dhRecbto> <chNFe>99999999999999999999999999999999999999999999</chNFe> <protNFe versao=\"4.00\"> <infProt> <tpAmb>1</tpAmb> <verAplic>SP_NFE_PL009_V4</verAplic> <chNFe>99999999999999999999999999999999999999999999</chNFe> <dhRecbto>2024-02-06T15:36:49-03:00</dhRecbto> <nProt></nProt> <digVal></digVal> <cStat>100</cStat> <xMotivo>Autorizado o uso da NF-e</xMotivo> </infProt> </protNFe> </retConsSitNFe> </nfeResultMsg> </soap:Body> </soap:Envelope>"
}
```


<br>
Para mais informações sobre o processo consulte [`Web Service – NfeConsultaProtocolo`](http://moc.sped.fazenda.pr.gov.br/NFeConsultaProtocolo.html).
<br><br>