# NFeGerarDanfe

!!! Quote ""
    `Função`: Método destinado à gerar DANFE com base num objeto do tipo NFe | NFeDanfe.<br>
    `Processo`: assíncrono.
<br>

!!! Quote "Interface de Entrada"
    A interface de geração da DANFE é muito extensa.
    Para consulta-la verifique a documentação em [`DANFE e Código de Barras - 2.8.1. Formulário A-4 em Modo Retrato`](http://moc.sped.fazenda.pr.gov.br/DanfeCodigoBarras.html).

#### `Gerar Danfe`

Você pode gerar a DANFE com o mesmo objeto com o qual transmitiu a NFe, porém existem algumas regras:

- **DANFE HOMOLOGAÇÃO**: Caso a propriedade NFe.infNFe.ide.tpAmb = 2 (Homologação) será adicionada ao rodapé da DANFE a tarja `AMBIENTE DE HOMOLOGAÇÃO - NF-E SEM VALOR FISCAL`.
- **DANFE PRODUÇÃO**: Caso a propriedade NFe.infNFe.ide.tpAmb = 1 (Produção) e exista a propriedade protNFe a DANFE será gerada de forma completa.
- **DANFE PRODUÇÃO SEM protNFe**: Caso a propriedade NFe.infNFe.ide.tpAmb = 1 (Produção) e não exista a propriedade protNFe a DANFE será gerada com a tarja `NF-E NÃO ENVIADA PARA SEFAZ` sobre o código de barras.
<br>
<br>

Exemplo de geração da DANFE:
<br><br>
<!-- porém caso não exista a protNFe a DANFE será gerada com a tarja `NF-E NÃO ENVIADA PARA SEFAZ`. : -->

```typescript title="NFE_GerarDanfe" linenums="1"
import { NFeDanfe, NFe } from '@Protocols';

const autorizacao: NFe | NFeDanfe = {
    indSinc: 0,
    idLote: 1,
    NFe: [
        {
            infNFe: {
                ide: {
                    cUF: 35,
                    cNF: '99999999',
                    natOp: "VENDA DE MERCADORIA",
                    mod: 55,
                    serie: '1',
                    nNF: 999999999,
                    dhEmi: "2024-07-08T00:00:00-03:00",
                    tpNF: 1,
                    idDest: 1,
                    cMunFG: 9999999,
                    tpImp: 1,
                    tpEmis: 1,
                    cDV: 0,
                    tpAmb: 2,
                    finNFe: 1,
                    indFinal: 1,
                    indPres: 9,
                    indIntermed: 0,
                    procEmi: 0,
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
                    IE: "999999999999"
                },
                det: [
                    {
                        prod: {
                            cProd: "99999999",
                            cEAN: "9999999999999",
                            xProd: "QUEIJO MUSSARELA ",
                            NCM: "99999999",
                            EXTIPI: "00",
                            CFOP: 5102,
                            uCom: "KG",
                            qCom: 24.93,
                            vUnCom: "33.9",
                            vProd: "845.13",
                            cEANTrib: "9999999999999",
                            uTrib: "KG",
                            qTrib: 24.93,
                            vUnTrib: "33.9",
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
                    modFrete: 0,
                    vol: [
                        {
                            qVol: 1,
                            esp: "CAIXA(S)",
                            marca: "MARCA",
                            pesoL: "24.930",
                            pesoB: "24.930"
                        }
                    ]
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

await nfewizard.NFE_GerarDanfe({
    chave: '99999999999999999999999999999999999999999999',
    data: {
        NFe: autorizacao.NFe
    },
    outputPath: 'src/assets/DANFE.pdf'
})
```
<br>

`Retorno`:

!!! Quote "Interface de Retorno"
    O arquivo será gerado com nome e caminho definidos na propriedade ***outputPath***.<br>
    Ex: outputPath: 'src/assets/DANFE.pdf'

<br>

___

#### `Gerar Danfe com retorno do método NFEAutorizacao`

```typescript title="NFE_GerarDanfe" linenums="1"
import { NFeDanfe } from '@Protocols';

// Transmite NFe
const autorizacao: NFeDanfe = {
    // Segue o mesmo padrão do exemplo anterior
    indSinc: 0,
    idLote: 1,
    NFe: [...],
};

const retorno = await nfewizard.NFE_Autorizacao(autorizacao);

// Gera DANFE da NFe transmitida
const chave = retorno[0].protNFe.infProt.chNFe;
await nfewizard.NFE_GerarDanfe({
    chave,
    data: retorno[0],
    outputPath: 'src/assets/DANFE.pdf'
})
```
<br>

`Retorno`:

!!! Quote "Interface de Retorno"
    O arquivo será gerado com nome e caminho definidos na propriedade ***outputPath***.<br>
    Ex: outputPath: 'src/assets/DANFE.pdf'

<br>

___

#### `Gerar Danfe com multiplas NFe`

!!! Warning "Atenção"
    `ATENÇÃO`: O método `NFE_GerarDanfe` aceita um parâmetro data que pode ser um objeto contendo NFe (do tipo LayoutNFe ou um array de objetos LayoutNFe[]) e protNFe (do tipo protNFe). No entanto, se o parâmetro data.NFe for um array, o método gerará a DANFE apenas para o primeiro item do array.<br>

Se você precisa gerar a DANFE para cada nota fiscal presente em um array, deve chamar o método `NFE_GerarDanfe` dentro de um loop, passando cada item do array individualmente:

```typescript title="NFE_GerarDanfe" linenums="1"
import { NFeDanfe } from '@Protocols';

/**
 * Exemplo com NFe não transmitida
*/
const autorizacao: NFeDanfe = {
    indSinc: 0,
    idLote: 1,
    NFe: [...],
};

if (autorizacao.NFe instanceof Array) {
    autorizacao.NFe.forEach(async (NFe: LayoutNFe) => {
        await nfewizard.NFE_GerarDanfe({
            chave: '99999999999999999999999999999999999999999999',
            data: {
                NFe,
            },
            outputPath: `src/assets/DANFE-${chave}.pdf`
        })
    });
}


/**
 * Exemplo com NFe já transmitida
*/

const retorno = await nfewizard.NFE_Autorizacao(autorizacao);

retorno.forEach(async (NFe) => {
    const chave = NFe.protNFe.infProt.chNFe;
    await nfewizard.NFE_GerarDanfe({
        chave: chave,
        data: NFe,
        outputPath: `src/assets/DANFE-${chave}.pdf`
    })
});
```

Isso garantirá que uma DANFE será gerada para cada nota fiscal no array.

___
<br><br>

#### Observações

!!! Warning "Atenção"
    `ATENÇÃO`: O método `NFE_GerarDanfe` atualmente gera documentos apenas no formado `RETRATO`.<br>
    
<br><br>