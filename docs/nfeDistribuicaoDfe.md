# NFeDistribuicaoDFe

!!! Quote ""
    `Função`: Serviço para consultar o cadastro de contribuintes do ICMS da unidade federada.<br>
    `Processo`: síncrono.<br>
    `Método`: nfeDistDFeInteresse
<br>

O Método NFE_DistribuicaoDFe pode receber um objeto que atenda qualquer um dos tipos de distribuição, sendo eles:

- `ultNSU`: Consulta a partir do último NSU recebido.
- `NSU`: Consulta NSU específico.
- `chNFe`: Consulta por chave de acesso específica.
<br><br>

??? Quote "Interface de Entrada"
    | Chave      | Tipo   | Descrição                                         |
    | ---------- | ------ | ------------------------------------------------- |
    | `cUFAutor` | Number | Código da UF do Autor                             |
    | `CNPJ`     | String | CNPJ do interessado no DF-e                       |
    | `ultNSU`   | String | Último Número Sequencial Único recebido pelo ator |
    | `NSU`      | String | Número Sequencial Único                           |
    | `chNFe`    | String | Chave de acesso específica                        |

#### `NFE_DistribuicaoDFe`


```typescript title="NFE_DistribuicaoDFe" linenums="1"
import { ConsultaNFe } from '@Protocols';

const distribuicao: ConsultaNFe = {
    cUFAutor: 35,
    CNPJ: '99999999999999',
    // Apenas um dos objetos abaixo deve ser informado
    distNSU: {
        ultNSU: '000000000000000',
    },
    consNSU: {
        NSU: '000000000000000',
    },
    consChNFe: {
        chNFe: '99999999999999999999999999999999999999999999',
    }
}

await nfewizard.NFE_DistribuicaoDFe(distribuicao);
```
<br>
Também é possível utilizar o método especifico para cada tipo de distribuição:
<br><br>

___

#### `NFE_DistribuicaoDFePorUltNSU`


```typescript title="NFE_DistribuicaoDFePorUltNSU" linenums="1"
import { DFePorUltimoNSU } from '@Protocols';

const ultimoNSU: DFePorUltimoNSU = {
    cUFAutor: 35,
    CNPJ: '99999999999999',
    distNSU: {
        ultNSU: '000000000000001'
    },
}

await nfewizard.NFE_DistribuicaoDFePorUltNSU(ultimoNSU);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação.                                                                                                     |
    | `verAplic` | String | Versão do Aplicativo que recebeu a Consulta.                                                                                                                |
    | `cStat`    | String | Código do status da resposta para o Lote.                                                                                                                   |
    | `xMotivo`  | String | Descrição literal do status da resposta.                                                                                                                    |
    | `dhResp` | String | Data e hora da mensagem de Resposta. Formato:  “AAAA-MMDDThh:m m:ssTZD” (UTC – Universal Coordinated) |
    | `docZip`    | Array | Informação resumida ou documento fiscal eletrônico de interesse da ou empresa. O conteúdo desta tag estará compactado no padrão gZip. O tipo do campo é base64Binary.                                                                                                                         |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String.                                                                                                     |

```json
{
  "retDistDFeInt": {
    "tpAmb": "1",
    "verAplic": "1.7.1",
    "cStat": "138",
    "xMotivo": "Documento(s) localizado(s)",
    "dhResp": "2024-07-16T17:58:27-03:00",
    "ultNSU": "000000000006026",
    "maxNSU": "000000000006068",
    "loteDistDFeInt": {
      "docZip": [
        "H4sIAAAAAAAEAIWS3W...",
        "H4sIAAAAAAAEAIVSXW...",
        "H4sIAAAAAAAEAIWSbW...",
        "H4sIAAAAAAAEAIWSy2...",
        "H4sIAAAAAAAEAKVYaX..."
      ]
    }
  },
  "xml": "<?xml version= \"1.0\" encoding= \"utf-8\"?> <soap:Envelope xmlns:soap= \"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi= \"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd= \"http://www.w3.org/2001/XMLSchema\"> <soap:Body> <nfeDistDFeInteresseResponse xmlns= \"http://www.portalfiscal.inf.br/nfe/wsdl/NFeDistribuicaoDFe\"> <nfeDistDFeInteresseResult> <retDistDFeInt xmlns:xsd= \"http://www.w3.org/2001/XMLSchema\" xmlns:xsi= \"http://www.w3.org/2001/XMLSchema-instance\" versao= \"1.01\" xmlns= \"http://www.portalfiscal.inf.br/nfe\"> <tpAmb>1</tpAmb> <verAplic>1.7.1</verAplic> <cStat>138</cStat> <xMotivo>Documento(s) localizado(s)</xMotivo> <dhResp>2024-07-16T17:58:27-03:00</dhResp> <ultNSU>000000000006026</ultNSU> <maxNSU>000000000006068</maxNSU> <loteDistDFeInt> <docZip NSU= \"000000000005977\" schema= \"resNFe_v1.01.xsd\"> H4sIAAAAAAAEAIWS3W...</docZip> <docZip NSU= \"000000000005978\" schema= \"resNFe_v1.01.xsd\"> H4sIAAAAAAAEAIVSXW...</docZip> <docZip NSU= \"000000000005979\" schema= \"resNFe_v1.01.xsd\"> H4sIAAAAAAAEAIWSbW...</docZip> <docZip NSU= \"000000000005980\" schema= \"resNFe_v1.01.xsd\"> H4sIAAAAAAAEAIWSy2...</docZip> <docZip NSU= \"000000000005981\" schema= \"procEventoNFe_v1.00.xsd\"> H4sIAAAAAAAEAKVYaX...</docZip> </loteDistDFeInt> </retDistDFeInt> </nfeDistDFeInteresseResult> </nfeDistDFeInteresseResponse> </soap:Body> </soap:Envelope>"
}
```

<br>
___

#### `NFE_DistribuicaoDFePorNSU`

```typescript title="NFE_DistribuicaoDFePorNSU" linenums="1"
import { DFePorNSU } from '@Protocols';

const nsu: DFePorNSU = {
    cUFAutor: 35,
    CNPJ: '99999999999999',
    consNSU: {
        NSU: '000000000000000'
    },
}

await nfewizard.NFE_DistribuicaoDFePorNSU(nsu);
```

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
  "retDistDFeInt": {
    "tpAmb": "1",
    "verAplic": "1.7.1",
    "cStat": "138",
    "xMotivo": "Documento localizado",
    "dhResp": "2024-07-16T17:43:35-03:00",
    "loteDistDFeInt": {
      "docZip": "H4sIAAAAAAAEANU6a5..."
    }
  },
  "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?> <soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"> <soap:Body> <nfeDistDFeInteresseResponse xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeDistribuicaoDFe\"> <nfeDistDFeInteresseResult> <retDistDFeInt xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" versao=\"1.01\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"> <tpAmb>2</tpAmb> <verAplic>1.7.1</verAplic> <cStat>138</cStat> <xMotivo>Documento localizado</xMotivo> <dhResp>2024-07-11T21:57:05-03:00</dhResp> <loteDistDFeInt> <docZip NSU=\"000000000000040\" schema=\"procNFe_v4.00.xsd\"> </docZip> </loteDistDFeInt> </retDistDFeInt> </nfeDistDFeInteresseResult> </nfeDistDFeInteresseResponse> </soap:Body> </soap:Envelope>",
}
```

<br>
___

#### `NFE_DistribuicaoDFePorChave`

```typescript title="NFE_DistribuicaoDFePorChave" linenums="1"
import { DFePorChaveNFe } from '@Protocols';

const chave: DFePorChaveNFe = {
    cUFAutor: 35,
    CNPJ: '99999999999999',
    consChNFe: {
         chNFe: '99999999999999999999999999999999999999999999'
    },
}

await nfewizard.NFE_DistribuicaoDFePorChave(chave);
```

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
  "retDistDFeInt": {
    "tpAmb": "1",
    "verAplic": "1.7.1",
    "cStat": "138",
    "xMotivo": "Documento localizado",
    "dhResp": "2024-07-16T17:43:35-03:00",
    "loteDistDFeInt": {
      "docZip": "H4sIAAAAAAAEANU6a5..."
    }
  },
  "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?> <soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"> <soap:Body> <nfeDistDFeInteresseResponse xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeDistribuicaoDFe\"> <nfeDistDFeInteresseResult> <retDistDFeInt xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" versao=\"1.01\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"> <tpAmb>2</tpAmb> <verAplic>1.7.1</verAplic> <cStat>138</cStat> <xMotivo>Documento localizado</xMotivo> <dhResp>2024-07-11T21:57:05-03:00</dhResp> <loteDistDFeInt> <docZip NSU=\"000000000000040\" schema=\"procNFe_v4.00.xsd\"> </docZip> </loteDistDFeInt> </retDistDFeInt> </nfeDistDFeInteresseResult> </nfeDistDFeInteresseResponse> </soap:Body> </soap:Envelope>",
}
```

<br>


<br>
Para mais informações sobre o processo consulte [`Web Service – NfeDistribuicaoDFe`](http://moc.sped.fazenda.pr.gov.br/NFeDistribuicaoDFe.html).
<br><br>