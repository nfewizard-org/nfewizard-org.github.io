# NFeInutilizacao

!!! Quote ""
    `Função`: Serviço destinado ao atendimento de solicitações de inutilização de numeração.<br>
    `Processo`: síncrono.<br>
    `Método`: nfeInutilizacaoNF
<br>

??? Quote "Interface de Entrada"
    | Chave      | Tipo     | Descrição                |
    | ---------- | -------- | ------------------------ |
    | `cUF`      | Number  | Código da UF do solicitante               |
    | `CNPJ`     |  String  | CNPJ do emitente |
    | `ano`      |  String  | Ano de inutilização da numeração |
    | `mod`      |  String  | Modelo do documento (55 ou 65) |
    | `serie`    |  String  | Série da NF-e |
    | `nNFIni`   |  String  | Número da NF-e inicial a ser inutilizada |
    | `nNFFin`   |  String  | Número da NF-e final a ser inutilizada |
    | `xJust`    |  String  | nformar a justificativa do pedido de inutilização |


```typescript title="NFE_Inutilizacao" linenums="1"
import { InutilizacaoData } from '@Protocols';

const inutilizacao: InutilizacaoData = {
    cUF: 35,
    CNPJ: '99999999999999',
    ano: '24',
    mod: '55',
    serie: '1',
    nNFIni: '112',
    nNFFin: '112',
    xJust: 'Teste de homologação',
}

await nfeWizard.NFE_Inutilizacao(inutilizacao)
```
<br>


`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação.                                                                                                     |
    | `verAplic` | String | Versão do Aplicativo que recebeu a Consulta.                                                                                                                |
    | `cStat`    | String | Código do status da resposta para o Lote.                                                                                                                   |
    | `xMotivo`  | String | Descrição literal do status da resposta.                                                                                                                    |
    | `dhResp` | String | Data e hora da mensagem de Resposta. Formato:  “AAAA-MMDDThh:m m:ssTZD” (UTC – Universal Coordinated) |
    | `docZip`    | String | Informação resumida ou documento fiscal eletrônico de interesse da ou empresa. O conteúdo desta tag estará compactado no padrão gZip. O tipo do campo é base64Binary.                                                                                                                         |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String.                                                                                                     |

```json
{
  "tpAmb": "2",
  "verAplic": "SP_NFE_PL009_V4",
  "cStat": "102",
  "xMotivo": "Inutilização de número homologado",
  "cUF": "35",
  "ano": "24",
  "CNPJ": "99999999999999",
  "mod": "55",
  "serie": "1",
  "nNFIni": "999",
  "nNFFin": "999",
  "dhRecbto": "2024-07-16T18:14:13-03:00",
  "nProt": "999999999999999",
  "xml": "<?xml version= \"1.0\" encoding= \"utf-8\"?> <soap:Envelope xmlns:soap= \"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi= \"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd= \"http://www.w3.org/2001/XMLSchema\"> <soap:Body> <nfeResultMsg xmlns= \"http://www.portalfiscal.inf.br/nfe/wsdl/NFeInutilizacao4\"> <retInutNFe versao= \"4.00\" xmlns= \"http://www.portalfiscal.inf.br/nfe\"> <infInut> <tpAmb>2</tpAmb> <verAplic>SP_NFE_PL009_V4</verAplic> <cStat>102</cStat> <xMotivo>Inutilização de número homologado</xMotivo> <cUF>35</cUF> <ano>24</ano> <CNPJ>99999999999999</CNPJ> <mod>55</mod> <serie>1</serie> <nNFIni>999</nNFIni> <nNFFin>999</nNFFin> <dhRecbto>2024-07-16T18:14:13-03:00</dhRecbto> <nProt>999999999999999</nProt> </infInut> </retInutNFe> </nfeResultMsg> </soap:Body> </soap:Envelope>"
}
```


<br>
Para mais informações sobre o processo consulte [`Web Service – NfeInutilizacao`](http://moc.sped.fazenda.pr.gov.br/NFeInutilizacao.html).
<br><br>