# NFeRecepcaoEvento

!!! Quote ""
    `Função`: Serviço destinado à recepção de mensagem de Evento da NF-e.<br>
    `Processo`: síncrono.<br>
    `Método`: nfeRecepcaoEvento
<br>


O Método NFE_RecepcaoEvento pode receber um objeto que possua até 20 eventos e atende qualquer um dos tipos de eventos listados abaixo:

- `210210`: Ciência da Operação.
- `210200`: Confirmação da Operação.
- `110110`: Carta de Correção.
- `110111`: Cancelamento.
- `210220`: Desconhecimento da Operação.
- `210240`: Operação Não Realizada.
- `110140`: EPEC (Evento Prévio de Emissão em Contingência).
<br><br>

??? Quote "Interface de Entrada"
    | Chave      | Tipo     | Descrição                |
    | ---------- | -------- | ------------------------ |
    | `cOrgao`   |  Number  | Código do órgão de recepção do Evento, conforme Tabela do IBGE ou: 91=Ambiente Nacional. Informar o código da UF para este evento.                |
    | `tpAmb`    |  Number  | Identificação do Ambiente: 1- Produção; 2- Homologação; |
    | `CNPJ`     |  String  | CNPJ do autor do evento |
    | `CPF`      |  String  | CPF do autor do evento |
    | `chNFe`    |  String  | Chave de Acesso da NF-e à qual o evento será vinculado |
    | `dhEvento`    |  String  | Data e hora do evento no formato AAAA-MM-DD-Thh:m m:ssTZD (UTC – Universal Coordinated Time) |
    | `tpEvento`    |  String  | Código do evento (de acordo com tabelas do item 3.1) |
    | `nSeqEvento`  |  Number  | Sequencial do evento para o mesmo tipo de evento. |
    | `verEvento`   |  String  | Versão do grupo de detalhe do evento. |
    | `descEvento`   |  String  | Informar a descrição do evento. |
    | `xCorrecao`   |  String  | Correção a ser considerada, texto livre. A correção mais recente substitui as anteriores. |
    | `xCondUso`   |  String  | Condições de uso da Carta de Correção, informar a literal : “A Carta de Correção é disciplinada pelo § 1º-A do art. 7º do Convênio S/N, de 15 de dezembro de 1970 e pode ser utilizada para regularização de erro ocorrido na emissão de documento fiscal, desde que o erro não esteja relacionado com: I - as variáveis que determinam o valor do imposto tais como: base de cálculo, alíquota, diferença de preço, quantidade, valor da operação ou da prestação; II - a correção de dados cadastrais que implique mudança do remetente ou do destinatário; III - a data de emissão ou de saída.” (texto com acentuação) ou “A Carta de Correcao e disciplinada pelo paragrafo 1o-A do art. 7o do Convenio S/N, de 15 de dezembro de 1970 e pode ser utilizada para regularizacao de erro ocorrido na emissao de documento fiscal, desde que o erro nao esteja relacionado com: I - as variaveis que determinam o valor do imposto tais como: base de calculo, aliquota, diferenca de preco, quantidade, valor da operacao ou da prestacao; II - a correcao de dados cadastrais que implique mudanca do remetente ou do destinatario; III - a data de emissao ou de saida.” (texto sem acentuação) |
    | `nProt`   |  String  | Informar o número do Protocolo de Autorização da NFe. |
    | `xJust`   |  String  | Informar a justificativa. |
    | `cOrgaoAutor`   |  Number  | Código do Órgão do Autor do Evento.Nota: Informar o código da UF do Emitente para este evento. |
    | `tpAutor`   |  String  | Informar "1=Empresa Emitente/Pessoa Física" para este evento.(NT 2018.004) Nota: 1=Empresa Emitente; 2=Empresa Destinatária; 3=Empresa; 5=Fisco; 6=RFB; 9=Outros Órgãos. |
    | `verAplic`   |  String  | VVersão do aplicativo do Autor do Evento. |
    | `dhEmi`   |  String  | Data e hora no formato UTC (Universal Coordinated Time): "AAAA-MM-DDThh:m m:ss TZD" |
    | `tpNF`   |  Number  | 0- Entrada 1- Saída |
    | `IE`   |  String  | Inscrição Estadual |
    | `UF`   |  String  | Sigla da UF do destinatário. Informar “EX” no caso de operação com o exterior. |
    | `vNF`   |  String  | Valor total da NF-e. |
    | `vICMS`   |  String  | Valor total do ICMS. |
    | `vST`   |  String  | Valor total do ICMS Substituição Tributária. |

#### `NFE_RecepcaoEvento`

```typescript title="NFE_RecepcaoEvento" linenums="1"
import { EventoNFe } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const evento: EventoNFe = {
    idLote: 1,
    evento: [
        // O método aceita até 20 eventos por lote
        {
            cOrgao: 91,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210210',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Ciencia da Operacao',
            }
        },
        {
            tpAmb: 2,
            cOrgao: 91,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210200',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Confirmacao da Operacao',
            }
        },
        {
            cOrgao: 35,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '110110',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Carta de Correção',
                xCorrecao: 'Teste de homologação',
                xCondUso: 'A Carta de Correcao e disciplinada pelo paragrafo 1o-A do art. 7o do Convenio S/N, de 15 de dezembro de 1970 e pode ser utilizada para regularizacao de erro ocorrido na emissao de documento fiscal, desde que o erro nao esteja relacionado com: I - as variaveis que determinam o valor do imposto tais como: base de calculo, aliquota, diferenca de preco, quantidade, valor da operacao ou da prestacao; II - a correcao de dados cadastrais que implique mudanca do remetente ou do destinatario; III - a data de emissao ou de saida.',
            }
        },
        {
            tpAmb: 2,
            cOrgao: 35,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '110111',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Cancelamento',
                nProt: '999999999999999',
                xJust: 'Cancelamento homologacao',
            }
        },
        {
            cOrgao: 91,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210220',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Desconhecimento da Operacao',
            }
        },
        {
            cOrgao: 91,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210240',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Operacao nao Realizada',
                xJust: 'Teste Operacao nao Realizada em homologação'
            }
        },
        {
            tpAmb: 2,
            cOrgao: 91,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '110140',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'EPEC',
                cOrgaoAutor: 35,
                tpAutor: 1,
                verAplic: '1.00',
                dhEmi: '2024-07-10T09:38:55-03:00',
                tpNF: 1,
                IE: '999999999999',
                dest: {
                    UF: 'SP',
                    CNPJ: '99999999999999',
                    IE: '999999999999',
                    vNF: '999.99',
                    vICMS: '999.99',
                    vST: '999.99',
                }
            }
        }

    ]
}

await nfewizard.NFE_RecepcaoEvento(evento);
```
<br>
Também é possível utilizar o método especifico para cada tipo de evento:
<br><br>

---

<!-- #### `NFE_CienciaDaOperacao` -->
#### <code style="color: blue;">NFE_CienciaDaOperacao</code>



```typescript title="NFE_CienciaDaOperacao" linenums="1"
import { CienciaDaOperacao } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const cienciaDaOperacao: CienciaDaOperacao = {
    idLote: 1,
    evento: [
        {
            cOrgao: 91,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210210',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Ciencia da Operacao',
            }
        }
    ]
}

await nfewizard.NFE_CienciaDaOperacao(cienciaDaOperacao);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `idLote`    | Number | Identificador de controle do Lote de envio do Evento. |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação. |
    | `verAplic` | String | Versão da aplicação que processou o evento. |
    | `cOrgao` | Number | Órgão de recepção do Evento, idem a mensagem de entrada. |
    | `cStat`    | Number | Código do status da resposta. |
    | `xMotivo`  | String | Descrição do status da resposta. |
    | `chNFe` | String | Chave de Acesso da NF-e à qual o evento foi vinculado |
    | `tpEvento`    | String | 	Código do evento. |
    | `xEvento`    | String | 	Descrição do evento. |
    | `nSeqEvento`    | Number | 	Sequencial do evento para o mesmo tipo de evento. |
    | `CNPJDest`    | Number | 	 CNPJ do destinatário da NF-e. |
    | `dhRegEvento`    | String | 	Data e hora do registro do evento no formato AAAAMMDDThh:m m:ssTZD (UTC – Universal Coordinated Time).Se o evento for rejeitado informar a data e hora de recebimento do evento. |
    | `nProt`      | Number | Número do Protocolo do Evento. |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String. |

```json
[
  {
    "idLote": "1",
    "tpAmb": "2",
    "verAplic": "AN_1.8.4",
    "cOrgao": "91",
    "cStat": "128",
    "xMotivo": "Lote de evento processado",
    "retEvento": {
      "infEvento": {
        "tpAmb": "2",
        "verAplic": "AN_1.8.4",
        "cOrgao": "91",
        "cStat": "135",
        "xMotivo": "Evento registrado e vinculado a NF-e",
        "chNFe": "99999999999999999999999999999999999999999999",
        "tpEvento": "210210",
        "xEvento": "Ciencia da Operacao",
        "nSeqEvento": "1",
        "CNPJDest": "99999999999999",
        "dhRegEvento": "2024-07-17T15:32:48-03:00",
        "nProt": "999999999999999"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeRecepcaoEventoNFResult xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeRecepcaoEvento4\"><retEnvEvento versao=\"1.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><idLote>1</idLote><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>128</cStat><xMotivo>Lote de evento processado</xMotivo><retEvento versao=\"1.00\"><infEvento><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>573</cStat><xMotivo>Rejeicao: Duplicidade de evento</xMotivo><chNFe>99999999999999999999999999999999999999999999</chNFe><tpEvento>210210</tpEvento><xEvento>Ciencia da Operacao</xEvento><nSeqEvento>1</nSeqEvento><dhRegEvento>2024-07-17T15:32:48-03:00</dhRegEvento></infEvento></retEvento></retEnvEvento></nfeRecepcaoEventoNFResult></soap:Body></soap:Envelope>"
  }
]
```

<br>

---

#### `NFE_ConfirmacaoDaOperacao`

```typescript title="NFE_ConfirmacaoDaOperacao" linenums="1"
import { ConfirmacaoDaOperacao } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const confirmacaoDaOperacao: ConfirmacaoDaOperacao = {
    idLote: 1,
    evento: [
        {
            tpAmb: 2,
            cOrgao: 91,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210200',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Confirmacao da Operacao',
            }
        }
    ]
}

await nfewizard.NFE_ConfirmacaoDaOperacao(confirmacaoDaOperacao);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `idLote`    | Number | Identificador de controle do Lote de envio do Evento. |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação. |
    | `verAplic` | String | Versão da aplicação que processou o evento. |
    | `cOrgao` | Number | Órgão de recepção do Evento, idem a mensagem de entrada. |
    | `cStat`    | Number | Código do status da resposta. |
    | `xMotivo`  | String | Descrição do status da resposta. |
    | `chNFe` | String | Chave de Acesso da NF-e à qual o evento foi vinculado |
    | `tpEvento`    | String | 	Código do evento. |
    | `xEvento`    | String | 	Descrição do evento. |
    | `nSeqEvento`    | Number | 	Sequencial do evento para o mesmo tipo de evento. |
    | `CNPJDest`    | Number | 	 CNPJ do destinatário da NF-e. |
    | `dhRegEvento`    | String | 	Data e hora do registro do evento no formato AAAAMMDDThh:m m:ssTZD (UTC – Universal Coordinated Time).Se o evento for rejeitado informar a data e hora de recebimento do evento. |
    | `nProt`      | Number | Número do Protocolo do Evento. |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String. |

```json
[
  {
    "idLote": "1",
    "tpAmb": "2",
    "verAplic": "AN_1.8.4",
    "cOrgao": "91",
    "cStat": "128",
    "xMotivo": "Lote de evento processado",
    "retEvento": {
      "infEvento": {
        "tpAmb": "2",
        "verAplic": "AN_1.8.4",
        "cOrgao": "91",
        "cStat": "135",
        "xMotivo": "Evento registrado e vinculado a NF-e",
        "chNFe": "99999999999999999999999999999999999999999999",
        "tpEvento": "210200",
        "xEvento": "Confirmacao da Operacao",
        "nSeqEvento": "1",
        "CNPJDest": "99999999999999",
        "dhRegEvento": "2024-07-17T15:48:45-03:00",
        "nProt": "999999999999999"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeRecepcaoEventoNFResult xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeRecepcaoEvento4\"><retEnvEvento versao=\"1.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><idLote>1</idLote><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>128</cStat><xMotivo>Lote de evento processado</xMotivo><retEvento versao=\"1.00\"><infEvento Id=\"ID999999999999999\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>136</cStat><xMotivo>Evento registrado, mas nao vinculado a NF-e</xMotivo><chNFe>99999999999999999999999999999999999999999999</chNFe><tpEvento>210200</tpEvento><xEvento>Confirmacao da Operacao</xEvento><nSeqEvento>1</nSeqEvento><CNPJDest>99999999999999</CNPJDest><dhRegEvento>2024-07-17T15:48:45-03:00</dhRegEvento><nProt>999999999999999</nProt></infEvento></retEvento></retEnvEvento></nfeRecepcaoEventoNFResult></soap:Body></soap:Envelope>"
  }
]
```

<br>

---

#### `NFE_CartaDeCorrecao`

```typescript title="NFE_CartaDeCorrecao" linenums="1"
import { CartaDeCorrecao } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const cartaDeCorrecao: CartaDeCorrecao = {
    idLote: 1,
    evento: [
        {
            cOrgao: 35,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '110110',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Carta de Correção',
                xCorrecao: 'Teste de homologação',
                xCondUso: 'A Carta de Correcao e disciplinada pelo paragrafo 1o-A do art. 7o do Convenio S/N, de 15 de dezembro de 1970 e pode ser utilizada para regularizacao de erro ocorrido na emissao de documento fiscal, desde que o erro nao esteja relacionado com: I - as variaveis que determinam o valor do imposto tais como: base de calculo, aliquota, diferenca de preco, quantidade, valor da operacao ou da prestacao; II - a correcao de dados cadastrais que implique mudanca do remetente ou do destinatario; III - a data de emissao ou de saida.',
            }
        }
    ]
}

await nfewizard.NFE_CartaDeCorrecao(cartaDeCorrecao);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `idLote`    | Number | Identificador de controle do Lote de envio do Evento. |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação. |
    | `verAplic` | String | Versão da aplicação que processou o evento. |
    | `cOrgao` | Number | Órgão de recepção do Evento, idem a mensagem de entrada. |
    | `cStat`    | Number | Código do status da resposta. |
    | `xMotivo`  | String | Descrição do status da resposta. |
    | `chNFe` | String | Chave de Acesso da NF-e à qual o evento foi vinculado |
    | `tpEvento`    | String | 	Código do evento. |
    | `xEvento`    | String | 	Descrição do evento. |
    | `nSeqEvento`    | Number | 	Sequencial do evento para o mesmo tipo de evento. |
    | `CNPJDest`    | Number | 	 CNPJ do destinatário da NF-e. |
    | `dhRegEvento`    | String | 	Data e hora do registro do evento no formato AAAAMMDDThh:m m:ssTZD (UTC – Universal Coordinated Time).Se o evento for rejeitado informar a data e hora de recebimento do evento. |
    | `nProt`      | Number | Número do Protocolo do Evento. |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String. |

```json
[
  {
    "idLote": "1",
    "tpAmb": "2",
    "verAplic": "SP_EVENTOS_PL_100",
    "cOrgao": "35",
    "cStat": "128",
    "xMotivo": "Lote de Evento Processado",
    "retEvento": {
      "infEvento": {
        "tpAmb": "2",
        "verAplic": "SP_EVENTOS_PL_100",
        "cOrgao": "35",
        "cStat": "135",
        "xMotivo": "Evento registrado e vinculado a NF-e",
        "chNFe": "99999999999999999999999999999999999999999999",
        "tpEvento": "110110",
        "xEvento": "Carta de Correção registrada",
        "nSeqEvento": "1",
        "CNPJDest": "99999999999999",
        "dhRegEvento": "2024-07-17T15:58:10-03:00",
        "nProt": "999999999999999"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeResultMsg xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeRecepcaoEvento4\"><retEnvEvento versao=\"1.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><idLote>1</idLote><tpAmb>2</tpAmb><verAplic>SP_EVENTOS_PL_100</verAplic><cOrgao>35</cOrgao><cStat>128</cStat><xMotivo>Lote de Evento Processado</xMotivo><retEvento versao=\"1.00\"><infEvento><tpAmb>2</tpAmb><verAplic>SP_EVENTOS_PL_100</verAplic><cOrgao>35</cOrgao><cStat>135</cStat><xMotivo>Evento registrado e vinculado a NF-e</xMotivo><chNFe>99999999999999999999999999999999999999999999</chNFe><tpEvento>110110</tpEvento><xEvento>Carta de Correção registrada</xEvento><nSeqEvento>1</nSeqEvento><CNPJDest>99999999999999</CNPJDest><dhRegEvento>2024-07-17T15:58:10-03:00</dhRegEvento><nProt>999999999999999</nProt></infEvento></retEvento></retEnvEvento></nfeResultMsg></soap:Body></soap:Envelope>"
  }
]
```

<br>

---

#### `NFE_Cancelamento`

```typescript title="NFE_Cancelamento" linenums="1"
import { Cancelamento } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const cancelamento: Cancelamento = {
    idLote: 1,
    evento: [
        {
            tpAmb: 2,
            cOrgao: 35,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '110111',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Cancelamento',
                nProt: '999999999999999',
                xJust: 'Cancelamento homologacao',
            }
        }
    ]
}

await nfewizard.NFE_Cancelamento(cancelamento);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `idLote`    | Number | Identificador de controle do Lote de envio do Evento. |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação. |
    | `verAplic` | String | Versão da aplicação que processou o evento. |
    | `cOrgao` | Number | Órgão de recepção do Evento, idem a mensagem de entrada. |
    | `cStat`    | Number | Código do status da resposta. |
    | `xMotivo`  | String | Descrição do status da resposta. |
    | `chNFe` | String | Chave de Acesso da NF-e à qual o evento foi vinculado |
    | `tpEvento`    | String | 	Código do evento. |
    | `xEvento`    | String | 	Descrição do evento. |
    | `nSeqEvento`    | Number | 	Sequencial do evento para o mesmo tipo de evento. |
    | `CNPJDest`    | Number | 	 CNPJ do destinatário da NF-e. |
    | `dhRegEvento`    | String | 	Data e hora do registro do evento no formato AAAAMMDDThh:m m:ssTZD (UTC – Universal Coordinated Time).Se o evento for rejeitado informar a data e hora de recebimento do evento. |
    | `nProt`      | Number | Número do Protocolo do Evento. |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String. |

```json
[
  {
    "idLote": "1",
    "tpAmb": "2",
    "verAplic": "SP_EVENTOS_PL_100",
    "cOrgao": "35",
    "cStat": "128",
    "xMotivo": "Lote de Evento Processado",
    "retEvento": {
      "infEvento": {
        "tpAmb": "2",
        "verAplic": "SP_EVENTOS_PL_100",
        "cOrgao": "35",
        "cStat": "135",
        "xMotivo": "Evento registrado e vinculado a NF-e",
        "chNFe": "99999999999999999999999999999999999999999999",
        "tpEvento": "110111",
        "xEvento": "Cancelamento registrado",
        "nSeqEvento": "1",
        "CNPJDest": "99999999999999",
        "dhRegEvento": "2024-07-17T17:37:52-03:00",
        "nProt": "999999999999999"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeResultMsg xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeRecepcaoEvento4\"><retEnvEvento versao=\"1.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><idLote>1</idLote><tpAmb>2</tpAmb><verAplic>SP_EVENTOS_PL_100</verAplic><cOrgao>35</cOrgao><cStat>128</cStat><xMotivo>Lote de Evento Processado</xMotivo><retEvento versao=\"1.00\"><infEvento><tpAmb>2</tpAmb><verAplic>SP_EVENTOS_PL_100</verAplic><cOrgao>35</cOrgao><cStat>135</cStat><xMotivo>Evento registrado e vinculado a NF-e</xMotivo><chNFe>99999999999999999999999999999999999999999999</chNFe><tpEvento>110111</tpEvento><xEvento>Cancelamento registrado</xEvento><nSeqEvento>1</nSeqEvento><CNPJDest>99999999999999</CNPJDest><dhRegEvento>2024-07-17T17:37:52-03:00</dhRegEvento><nProt>999999999999999</nProt></infEvento></retEvento></retEnvEvento></nfeResultMsg></soap:Body></soap:Envelope>"
  }
]
```

<br>

---

#### `NFE_DesconhecimentoDaOperacao`

```typescript title="NFE_DesconhecimentoDaOperacao" linenums="1"
import { DesconhecimentoDaOperacao } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const desconhecimentoDaOperacao: DesconhecimentoDaOperacao = {
    idLote: 1,
    evento: [
        {
            cOrgao: 91,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210220',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Desconhecimento da Operacao',
            }
        }
    ]
}

await nfewizard.NFE_DesconhecimentoDaOperacao(desconhecimentoDaOperacao);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `idLote`    | Number | Identificador de controle do Lote de envio do Evento. |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação. |
    | `verAplic` | String | Versão da aplicação que processou o evento. |
    | `cOrgao` | Number | Órgão de recepção do Evento, idem a mensagem de entrada. |
    | `cStat`    | Number | Código do status da resposta. |
    | `xMotivo`  | String | Descrição do status da resposta. |
    | `chNFe` | String | Chave de Acesso da NF-e à qual o evento foi vinculado |
    | `tpEvento`    | String | 	Código do evento. |
    | `xEvento`    | String | 	Descrição do evento. |
    | `nSeqEvento`    | Number | 	Sequencial do evento para o mesmo tipo de evento. |
    | `CNPJDest`    | Number | 	 CNPJ do destinatário da NF-e. |
    | `dhRegEvento`    | String | 	Data e hora do registro do evento no formato AAAAMMDDThh:m m:ssTZD (UTC – Universal Coordinated Time).Se o evento for rejeitado informar a data e hora de recebimento do evento. |
    | `nProt`      | Number | Número do Protocolo do Evento. |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String. |

```json
[
  {
    "idLote": "1",
    "tpAmb": "2",
    "verAplic": "AN_1.8.4",
    "cOrgao": "91",
    "cStat": "128",
    "xMotivo": "Lote de evento processado",
    "retEvento": {
      "infEvento": {
        "tpAmb": "2",
        "verAplic": "AN_1.8.4",
        "cOrgao": "91",
        "cStat": "135",
        "xMotivo": "Evento registrado e vinculado a NF-e",
        "chNFe": "99999999999999999999999999999999999999999999",
        "tpEvento": "210220",
        "xEvento": "Desconhecimento da Operacao",
        "nSeqEvento": "1",
        "CNPJDest": "99999999999999",
        "dhRegEvento": "2024-07-17T17:23:39-03:00",
        "nProt": "999999999999999"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeRecepcaoEventoNFResult xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeRecepcaoEvento4\"><retEnvEvento versao=\"1.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><idLote>1</idLote><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>128</cStat><xMotivo>Lote de evento processado</xMotivo><retEvento versao=\"1.00\"><infEvento Id=\"ID891240002367854\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>135</cStat><xMotivo>Evento registrado e vinculado a NF-e</xMotivo><chNFe>99999999999999999999999999999999999999999999</chNFe><tpEvento>210220</tpEvento><xEvento>Desconhecimento da Operacao</xEvento><nSeqEvento>1</nSeqEvento><CNPJDest>99999999999999</CNPJDest><dhRegEvento>2024-07-17T17:23:39-03:00</dhRegEvento><nProt>891240002367854</nProt></infEvento></retEvento></retEnvEvento></nfeRecepcaoEventoNFResult></soap:Body></soap:Envelope>"
  }
]
```

<br>

---

#### `NFE_OperacaoNaoRealizada`

```typescript title="NFE_OperacaoNaoRealizada" linenums="1"
import { OperacaoNaoRealizada } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const operacaoNaoRealizada: OperacaoNaoRealizada = {
    idLote: 1,
    evento: [
        {
            cOrgao: 91,
            tpAmb: 2,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '210240',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'Operacao nao Realizada',
                xJust: 'Teste Operacao nao Realizada em homologação'
            }
        }
    ]
}

await nfewizard.NFE_OperacaoNaoRealizada(operacaoNaoRealizada);
```

`Retorno`:

??? Quote "Interface de Retorno"
    | Chave      | Tipo   | Descrição                                                                                                                                                   |
    | ---------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `idLote`    | Number | Identificador de controle do Lote de envio do Evento. |
    | `tpAmb`    | Number | Identificação do Ambiente: 1- Produção; 2- Homologação. |
    | `verAplic` | String | Versão da aplicação que processou o evento. |
    | `cOrgao` | Number | Órgão de recepção do Evento, idem a mensagem de entrada. |
    | `cStat`    | Number | Código do status da resposta. |
    | `xMotivo`  | String | Descrição do status da resposta. |
    | `chNFe` | String | Chave de Acesso da NF-e à qual o evento foi vinculado |
    | `tpEvento`    | String | 	Código do evento. |
    | `xEvento`    | String | 	Descrição do evento. |
    | `nSeqEvento`    | Number | 	Sequencial do evento para o mesmo tipo de evento. |
    | `CNPJDest`    | Number | 	 CNPJ do destinatário da NF-e. |
    | `dhRegEvento`    | String | 	Data e hora do registro do evento no formato AAAAMMDDThh:m m:ssTZD (UTC – Universal Coordinated Time).Se o evento for rejeitado informar a data e hora de recebimento do evento. |
    | `nProt`      | Number | Número do Protocolo do Evento. |
    | `xml`      | String | Retorno original da SEFAZ (XML) convertido para String. |

```json
[
  {
    "idLote": "1",
    "tpAmb": "2",
    "verAplic": "AN_1.8.4",
    "cOrgao": "91",
    "cStat": "128",
    "xMotivo": "Lote de evento processado",
    "retEvento": {
      "infEvento": {
        "tpAmb": "2",
        "verAplic": "AN_1.8.4",
        "cOrgao": "91",
        "cStat": "135",
        "xMotivo": "Evento registrado e vinculado a NF-e",
        "chNFe": "99999999999999999999999999999999999999999999",
        "tpEvento": "210240",
        "xEvento": "Operacao nao Realizada",
        "nSeqEvento": "1",
        "CNPJDest": "99999999999999",
        "dhRegEvento": "2024-07-17T17:35:55-03:00",
        "nProt": "999999999999999"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><soap:Envelope xmlns:soap=\"http://www.w3.org/2003/05/soap-envelope\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\"><soap:Body><nfeRecepcaoEventoNFResult xmlns=\"http://www.portalfiscal.inf.br/nfe/wsdl/NFeRecepcaoEvento4\"><retEnvEvento versao=\"1.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><idLote>1</idLote><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>128</cStat><xMotivo>Lote de evento processado</xMotivo><retEvento versao=\"1.00\"><infEvento Id=\"ID999999999999999\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><tpAmb>2</tpAmb><verAplic>AN_1.8.4</verAplic><cOrgao>91</cOrgao><cStat>135</cStat><xMotivo>Evento registrado e vinculado a NF-e</xMotivo><chNFe>99999999999999999999999999999999999999999999</chNFe><tpEvento>210240</tpEvento><xEvento>Operacao nao Realizada</xEvento><nSeqEvento>1</nSeqEvento><CNPJDest>99999999999999</CNPJDest><dhRegEvento>2024-07-17T17:35:55-03:00</dhRegEvento><nProt>999999999999999</nProt></infEvento></retEvento></retEnvEvento></nfeRecepcaoEventoNFResult></soap:Body></soap:Envelope>"
  }
]
```

<br>

---

#### `NFE_EventoPrevioDeEmissaoEmContingencia`

```typescript title="NFE_EventoPrevioDeEmissaoEmContingencia" linenums="1"
import { EPEC } from '@Protocols';

const timeZone = Intl.DateTimeFormat().resolvedOptions().timeZone;
const epec: EPEC = {
    idLote: 1,
    evento: [
        {
            tpAmb: 2,
            cOrgao: 91,
            CNPJ: '99999999999999',
            chNFe: '99999999999999999999999999999999999999999999',
            dhEvento: format(new Date(), "yyyy-MM-dd'T'HH:mm:ssXXX", { timeZone }),
            tpEvento: '110140',
            nSeqEvento: 1,
            verEvento: '1.00',
            detEvento: {
                descEvento: 'EPEC',
                cOrgaoAutor: 35,
                tpAutor: 1,
                verAplic: '1.00',
                dhEmi: '2024-07-10T09:38:55-03:00',
                tpNF: 1,
                IE: '999999999999',
                dest: {
                    UF: 'SP',
                    CNPJ: '88888888888888',
                    IE: '888888888888',
                    vNF: '999.99',
                    vICMS: '999.99',
                    vST: '999.99',
                }
            }
        }
    ]
}

await nfewizard.NFE_EventoPrevioDeEmissaoEmContingencia(epec);
```
<br>
`Retorno`:


<br>
Para mais informações sobre o processo consulte [`Web Service – NFeRecepcaoEvento – Parte Geral`](http://moc.sped.fazenda.pr.gov.br/RecepcaoEventoGeral.html).
<br><br>