# NFCeAutorizacao

!!! Quote ""
    `Função`: Serviço destinado à recepção de mensagens de lote de NF-e.<br>
    `Processo`: assíncrono/síncrono.<br>
    `Método`: nfeAutorizacaoLote
<br>

O Método NFCE_Autorizacao pode receber um array que possua até 50 NF-e, seguindo definição do [`Leiaute da NF-e`](http://moc.sped.fazenda.pr.gov.br/Leiaute.html).
<br>

!!! Quote "Interface de Entrada"
    A interface de entrada da NF-e é muito extensa.
    Para consulta-la verifique a documentação em [`Leiaute da NF-e`](http://moc.sped.fazenda.pr.gov.br/Leiaute.html).

#### `NFCE_Autorizacao`

```typescript title="NFCE_Autorizacao" linenums="1"
import { NFe } from '@Protocols';

const autorizacao: NFe = {
    indSinc: 1,
    idLote: 1,
    NFe: [
        {
            infNFe: {
                ide: {
                    cUF: 35,
                    cNF: '99999999',
                    natOp: "VENDA DE MERCADORIA",
                    mod: 65,
                    serie: '1',
                    nNF: 999999999,
                    dhEmi: "2024-09-02T12:28:02-03:00",
                    tpNF: 1,
                    idDest: 1,
                    cMunFG: 9999999,
                    tpImp: 4,
                    tpEmis: 1,
                    cDV: 0,
                    tpAmb: 2,
                    finNFe: 1,
                    indFinal: 1,
                    indPres: 1,
                    indIntermed: 0,
                    procEmi: 0,
                    verProc: '0.1.0',
                    // Utilize os campos abaixo em caso de contingência
                    // dhCont: '2024-09-01T13:54:03-03:00',
                    // xJust: 'Testes de emissão NFCe'
                },
                emit: {
                    CNPJCPF: '99999999999999',
                    xNome: "NOME EMITENTE",
                    xFant: "NOME FANT EMITENTE",
                    enderEmit: {
                        xLgr: "RUA X",
                        nro: '12x',
                        xBairro: "BAIRRO",
                        cMun: 9999999,
                        xMun: "MUNICIPIO",
                        UF: "SP",
                        CEP: '99999999',
                        cPais: 9999,
                        xPais: "BRASIL",
                        fone: "99999999999",
                    },
                    IE: "999999999999",
                    CRT: 3
                },
                dest: {
                    CNPJCPF: '99999999999999',
                    xNome: "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                    enderDest: {
                        xLgr: "RUA Y",
                        nro: "9999",
                        xBairro: "BAIRRO",
                        cMun: 9999999,
                        xMun: "MUNICIPIO",
                        UF: "SP",
                        CEP: '99999999',
                        cPais: 9999,
                        xPais: "BRASIL",
                        fone: "99999999999"
                    },
                    indIEDest: 1,
                },
                det: [
                    {
                        prod: {
                            cProd: "99999999",
                            cEAN: "9999999999999",
                            xProd: "NOTA FISCAL EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
                            NCM: "99999999",
                            EXTIPI: "00",
                            CFOP: 5102,
                            uCom: "UN",
                            qCom: 1,
                            vUnCom: "845.13",
                            vProd: "845.13",
                            cEANTrib: "9999999999999",
                            uTrib: "UN",
                            qTrib: 1,
                            vUnTrib: "845.13",
                            indTot: 1,
                        },
                        imposto: {
                            ICMS: {
                                ICMS00: {
                                    orig: 0,
                                    CST: "00",
                                    modBC: 3,
                                    vBC: "845.13",
                                    pICMS: "12.00",
                                    vICMS: "101.42"
                                }
                            },
                            PIS: {
                                PISNT: {
                                    CST: "06",
                                }
                            },
                            COFINS: {
                                COFINSNT: {
                                    CST: "06",
                                }
                            }
                        },
                    },
                ],
                total: {
                    ICMSTot: {
                        vBC: "845.13",
                        vICMS: "101.42",
                        vICMSDeson: "0.00",
                        vFCP: "0.00",
                        vBCST: "0.00",
                        vST: "0.00",
                        vFCPST: "0.00",
                        vFCPSTRet: "0.00",
                        vProd: "845.13",
                        vFrete: "0.00",
                        vSeg: "0.00",
                        vDesc: "0.00",
                        vII: "0.00",
                        vIPI: "0.00",
                        vIPIDevol: "0.00",
                        vPIS: "0.00",
                        vCOFINS: "0.00",
                        vOutro: "0.00",
                        vNF: "845.13",
                    }
                },
                transp: {
                    modFrete: 9,
                },
                pag: {
                    detPag: [
                        {
                            indPag: 1,
                            tPag: 99,
                            xPag: "Outros",
                            vPag: "845.13"
                        }
                    ]
                },
            },
        },
    ],
};

await nfeWizard.NFCE_Autorizacao(autorizacao);
```
<br>

`Retorno`:

!!! Quote "Interface de Retorno"
    A interface de retorno da NF-e é muito extensa.
    Para consulta-la verifique a documentação em [`Leiaute da NF-e`](http://moc.sped.fazenda.pr.gov.br/NFeAutorizacao.html).

```json
[
  {
    "NFe": {
      "infNFe": {
        "ide": {
          "cUF": "35",
          "cNF": "99999999",
          "natOp": "VENDA DE MERCADORIA",
          "mod": "55",
          "serie": "1",
          "nNF": "999999999",
          "dhEmi": "2024-07-08T00:00:00-03:00",
          "tpNF": "1",
          "idDest": "1",
          "cMunFG": "9999999",
          "tpImp": "1",
          "tpEmis": "1",
          "cDV": "9",
          "tpAmb": "2",
          "finNFe": "1",
          "indFinal": "1",
          "indPres": "9",
          "indIntermed": "0",
          "procEmi": "0",
          "verProc": "1.0.0.0"
        },
        "emit": {
          "CNPJ": "99999999999999",
          "xNome": "NOME DO EMITENTE",
          "xFant": "NOME FANTASIA DO EMITENTE",
          "enderEmit": {
            "xLgr": "DESCRIÇÃO LOGRADOURO EMITENTE",
            "nro": "9999",
            "xBairro": "BAIRRO EMITENTE",
            "cMun": "9999999",
            "xMun": "MUNICIPIO",
            "UF": "SP",
            "CEP": "99999999",
            "cPais": "1058",
            "xPais": "BRASIL",
            "fone": "99999999999"
          },
          "IE": "999999999999",
          "CRT": "3"
        },
        "dest": {
          "CNPJ": "99999999999999",
          "xNome": "NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL",
          "enderDest": {
            "xLgr": "DESCRIÇÃO LOGRADOURO DESTINATÁRIO",
            "nro": "9999",
            "xBairro": "BAIRRO DESTINATÁRIO",
            "cMun": "9999999",
            "xMun": "MUNICIPIO",
            "UF": "SP",
            "CEP": "99999999",
            "cPais": "1058",
            "xPais": "BRASIL",
            "fone": "99999999999"
          },
          "indIEDest": "1",
          "IE": "999999999999"
        },
        "det": {
          "prod": {
            "cProd": "99999999",
            "cEAN": "9999999999999",
            "xProd": "QUEIJO MUSSARELA",
            "NCM": "04061010",
            "EXTIPI": "00",
            "CFOP": "5102",
            "uCom": "UN",
            "qCom": "24.93",
            "vUnCom": "845.13",
            "vProd": "845.13",
            "cEANTrib": "9999999999999",
            "uTrib": "UN",
            "qTrib": "1",
            "vUnTrib": "845.13",
            "indTot": "1"
          },
          "imposto": {
            "ICMS": {
              "ICMS00": {
                "orig": "0",
                "CST": "00",
                "modBC": "3",
                "vBC": "845.13",
                "pICMS": "12.00",
                "vICMS": "101.42"
              }
            },
            "PIS": {
              "PISNT": {
                "CST": "06"
              }
            },
            "COFINS": {
              "COFINSNT": {
                "CST": "06"
              }
            }
          }
        },
        "total": {
          "ICMSTot": {
            "vBC": "845.13",
            "vICMS": "101.42",
            "vICMSDeson": "0.00",
            "vFCP": "0.00",
            "vBCST": "0.00",
            "vST": "0.00",
            "vFCPST": "0.00",
            "vFCPSTRet": "0.00",
            "vProd": "845.13",
            "vFrete": "0.00",
            "vSeg": "0.00",
            "vDesc": "0.00",
            "vII": "0.00",
            "vIPI": "0.00",
            "vIPIDevol": "0.00",
            "vPIS": "0.00",
            "vCOFINS": "0.00",
            "vOutro": "0.00",
            "vNF": "845.13"
          }
        },
        "transp": {
          "modFrete": "9",
        },
        "pag": {
            "detPag": {
                "indPag": "1",
                "tPag": "99",
                "xPag": "Outros",
                "vPag": "845.13"
            }
        }
      },
      "infNFeSupl": {
            "qrCode": "https://www.homologacao.nfce.fazenda.sp.gov.br/qrcode?p=...",
            "urlChave": "https://www.homologacao.nfce.fazenda.sp.gov.br/consulta"
        },
      "Signature": {
        "SignedInfo": {
          "CanonicalizationMethod": {},
          "SignatureMethod": {},
          "Reference": {
            "Transforms": {
              "Transform": [
                {},
                {}
              ]
            },
            "DigestMethod": {},
            "DigestValue": "qV+ghmu..."
          }
        },
        "SignatureValue": "UwxIHUqkll0CN1...",
        "KeyInfo": {
          "X509Data": {
            "X509Certificate": "MIIIHjCCBgagA..."
          }
        }
      }
    },
    "protNFe": {
      "infProt": {
        "tpAmb": "2",
        "verAplic": "SP_NFE_PL009_V4",
        "chNFe": "99999999999999999999999999999999999999999999",
        "dhRecbto": "2024-07-17T15:56:46-03:00",
        "nProt": "999999999999999",
        "digVal": "qV+ghmu...",
        "cStat": "100",
        "xMotivo": "Autorizado o uso da NF-e"
      }
    },
    "xml": "<?xml version=\"1.0\" encoding=\"UTF-8\"?><nfeProc versao=\"4.00\" xmlns=\"http://www.portalfiscal.inf.br/nfe\"><NFe xmlns=\"http://www.portalfiscal.inf.br/nfe\"><infNFe versao=\"4.00\" Id=\"NFe99999999999999999999999999999999999999999999\"><ide><cUF>35</cUF><cNF>99999999</cNF><natOp>VENDA DE MERCADORIA</natOp><mod>55</mod><serie>1</serie><nNF>999999999</nNF><dhEmi>2024-07-08T00:00:00-03:00</dhEmi><tpNF>1</tpNF><idDest>1</idDest><cMunFG>9999999</cMunFG><tpImp>1</tpImp><tpEmis>1</tpEmis><cDV>9</cDV><tpAmb>2</tpAmb><finNFe>1</finNFe><indFinal>1</indFinal><indPres>9</indPres><indIntermed>0</indIntermed><procEmi>0</procEmi><verProc>1.0.0.0</verProc></ide><emit><CNPJ>99999999999999</CNPJ><xNome>NOME DO EMITENTE</xNome><xFant>NOME FANTASIA DO EMITENTE</xFant><enderEmit><xLgr>DESCRIÇÃO LOGRADOURO EMITENTE EMITENTE</xLgr><nro>9999</nro><xBairro>BAIRRO EMITENTE</xBairro><cMun>9999999</cMun><xMun>MUNICIPIO</xMun><UF>SP</UF><CEP>99999999</CEP><cPais>1058</cPais><xPais>BRASIL</xPais><fone>99999999999</fone></enderEmit><IE>999999999999</IE><CRT>3</CRT></emit><dest><CNPJ>99999999999999</CNPJ><xNome>NF-E EMITIDA EM AMBIENTE DE HOMOLOGACAO - SEM VALOR FISCAL</xNome><enderDest><xLgr>DESCRIÇÃO LOGRADOURO DESTINATÁRIO</xLgr><nro>9999</nro><xBairro>BAIRRO DESTINATARIO</xBairro><cMun>9999999</cMun><xMun>MUNICIPIO</xMun><UF>SP</UF><CEP>99999999</CEP><cPais>1058</cPais><xPais>BRASIL</xPais><fone>99999999999</fone></enderDest><indIEDest>1</indIEDest><IE>999999999999</IE></dest><det nItem=\"1\"><prod><cProd>99999999</cProd><cEAN>9999999999999</cEAN><xProd>QUEIJO MUSSARELA 4,0 KG (6 X 4)</xProd><NCM>04061010</NCM><EXTIPI>00</EXTIPI><CFOP>5102</CFOP><uCom>KG</uCom><qCom>24.93</qCom><vUnCom>33.9</vUnCom><vProd>845.13</vProd><cEANTrib>9999999999999</cEANTrib><uTrib>KG</uTrib><qTrib>24.93</qTrib><vUnTrib>33.9</vUnTrib><indTot>1</indTot></prod><imposto><ICMS><ICMS00><orig>0</orig><CST>00</CST><modBC>3</modBC><vBC>845.13</vBC><pICMS>12.00</pICMS><vICMS>101.42</vICMS></ICMS00></ICMS><PIS><PISNT><CST>06</CST></PISNT></PIS><COFINS><COFINSNT><CST>06</CST></COFINSNT></COFINS></imposto></det><total><ICMSTot><vBC>845.13</vBC><vICMS>101.42</vICMS><vICMSDeson>0.00</vICMSDeson><vFCP>0.00</vFCP><vBCST>0.00</vBCST><vST>0.00</vST><vFCPST>0.00</vFCPST><vFCPSTRet>0.00</vFCPSTRet><vProd>845.13</vProd><vFrete>0.00</vFrete><vSeg>0.00</vSeg><vDesc>0.00</vDesc><vII>0.00</vII><vIPI>0.00</vIPI><vIPIDevol>0.00</vIPIDevol><vPIS>0.00</vPIS><vCOFINS>0.00</vCOFINS><vOutro>0.00</vOutro><vNF>845.13</vNF></ICMSTot></total><transp><modFrete>0</modFrete><vol><qVol>1</qVol><esp>CAIXA(S)</esp><marca>MARCA</marca><pesoL>24.930</pesoL><pesoB>24.930</pesoB></vol></transp><pag><detPag><indPag>1</indPag><tPag>99</tPag><xPag>Outros</xPag><vPag>845.13</vPag></detPag></pag></infNFe><Signature xmlns=\"http://www.w3.org/2000/09/xmldsig#\"><SignedInfo><CanonicalizationMethod Algorithm=\"http://www.w3.org/TR/2001/REC-xml-c14n-20010315\"/><SignatureMethod Algorithm=\"http://www.w3.org/2000/09/xmldsig#rsa-sha1\"/><Reference URI=\"#NFe99999999999999999999999999999999999999999999\"><Transforms><Transform Algorithm=\"http://www.w3.org/2000/09/xmldsig#enveloped-signature\"/><Transform Algorithm=\"http://www.w3.org/TR/2001/REC-xml-c14n-20010315\"/></Transforms><DigestMethod Algorithm=\"http://www.w3.org/2000/09/xmldsig#sha1\"/><DigestValue>qV+ghmu...</DigestValue></Reference></SignedInfo><SignatureValue>UwxIHUqkll0CN1...</SignatureValue><KeyInfo><X509Data><X509Certificate>MIIIHjCCBgagA...</X509Certificate></X509Data></KeyInfo></Signature></NFe><protNFe versao=\"4.00\"><infProt><tpAmb>2</tpAmb><verAplic>SP_NFE_PL009_V4</verAplic><chNFe>99999999999999999999999999999999999999999999</chNFe><dhRecbto>2024-07-17T15:56:46-03:00</dhRecbto><nProt>999999999999999</nProt><digVal>qV+ghmu...</digVal><cStat>100</cStat><xMotivo>Autorizado o uso da NF-e</xMotivo></infProt></protNFe></nfeProc>"
  }
]
```

<br>
Para mais informações sobre o processo consulte [`Web Service – NfeAutorizacao`](http://moc.sped.fazenda.pr.gov.br/NFeAutorizacao.html).
<br><br>

#### Observações

!!! Warning "Atenção"
    `ATENÇÃO`: O método `NFCE_Autorizacao` deve ser utilizado apenas para NFe modelo 65 (NFC-e), devendo ser usado o método `NFE_Autorizacao` para o modelo 55.<br>
    
<br><br>