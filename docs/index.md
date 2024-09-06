# Home

Repositório do projeto [NFeWizard-io](https://github.com/nfewizard-org/nfewizard-io).
<div style="height: 200px; display: flex; justify-content: center; align-items: center; width: 200px;">
  <img src="assets/logo.jpg" />
</div>

## Sobre

NFeWizard-io é uma biblioteca Node.js projetada para simplificar a interação com os webservices da SEFAZ, proporcionando uma solução robusta para automação de processos relacionados à Nota Fiscal Eletrônica (NF-e). A biblioteca oferece métodos abrangentes para diversas operações fiscais, incluindo:

- **Autorização (Emissão de NFe)**: Submissão de notas fiscais eletrônicas para autorização.
- **Distribuição DFe**: Consulta e Download de DF-e (Documentos fiscais eletrônicos), facilitando o acesso a documentos fiscais eletrônicos.
- **Consulta de Protocolo**: Verificação da situação atual da NF-e na Base de Dados do Portal da Secretaria de Fazenda Estadual.
- **Inutilização de NFe**: Processo de inutilização de números de NF-e que não serão utilizados, assegurando a conformidade fiscal.
- **Consulta de Status do Serviço**: Monitoramento do status dos serviços da SEFAZ, garantindo a disponibilidade dos webservices.
- **Recepção de Eventos**: Tratamento de diversos eventos relacionados à NFe, incluindo:
    - Cancelamento de NFe
    - Carta de Correção
    - Ciência da Operação
    - Confirmação da Operação
    - Desconhecimento da Operação
    - EPEC (Evento Prévio de Emissão em Contingência)
    - Operação Não Realizada
- **Geração de DANFE**: Criação do Documento Auxiliar da Nota Fiscal Eletrônica (DANFE), um resumo impresso da NFe.

<br>
!!! Quote "Instalação"
    npm install nfewizard-io<br>
    yarn add nfewizard-io

## Exemplo de Utilização

```typescript
import NFeWizard from 'nfewizard-io';

// Instanciar
const nfewizard = new NFeWizard();

// Inicializar
await nfewizard.NFE_LoadEnvironment({
    config: {
        dfe: {
            baixarXMLDistribuicao: true,
            pathXMLDistribuicao: "tmp/DistribuicaoDFe",
            armazenarXMLAutorizacao: true,
            pathXMLAutorizacao: "tmp/Autorizacao",
            armazenarXMLRetorno: true,
            pathXMLRetorno: "tmp/RequestLogs",
            armazenarXMLConsulta: true,
            pathXMLConsulta: "tmp/RequestLogs",
            armazenarXMLConsultaComTagSoap: false,
            armazenarRetornoEmJSON: true,
            pathRetornoEmJSON: "tmp/DistribuicaoDFe",

            pathCertificado: "certificado.pfx",
            senhaCertificado: "123456",
            UF: "SP",
            CPFCNPJ: "99999999999999",
        },
        nfe: {
            ambiente: 2,
            versaoDF: "4.00",
            idCSC: 1,
            tokenCSC: '99999999-9999-9999-9999-999999999999'
        },
        email: {
            host: 'smtp.example.com',
            port: 587,
            secure: false,
            auth: {
                user: 'seu-email@example.com',
                pass: 'sua-senha'
            },
            emailParams: {
                from: '"Seu Nome" <seu-email@example.com>',
                to: 'destinatario@example.com',
            }
        },
        lib: {
            connection: {
                timeout: 30000,
            },
        }
    }
});

// Exemplo de Utilização
const chaveNFe: DFePorChaveNFe = {
    cUFAutor: 35,
    CNPJ: '99999999999999',
    consChNFe: {
        chNFe: '00000000000000000000000000000000000000000000'
    },
}

await nfewizard.NFE_DistribuicaoDFePorChave(chaveNFe);
```

<!-- ## Documentação

- [Inicializar ambiente](./src/config/CONFIG.md): Parametros de inicialização da lib
- [Exemplos de Uso](./src/exemplos/): Exemplo de utilização da lib
- [XMLs de Exemplo](./src/exemplos/): Exemplos de XML de consulta e retorno -->

## Observações
!!! Warning "Observações"
    `Certificado`: Implementado apenas em certificados A1.<br>
    `NodeJs`: Testado com versões 16 ou superiores.<br>
    `UF`: Testado apenas para São Paulo. Por favor, abra uma issue caso encontre problemas com outros estados.<br>


## Contribua para Nossa Biblioteca Open Source

Primeiramente, obrigado por considerar contribuir para nossa biblioteca! Nosso projeto é de código aberto e gratuito para uso, mas manter e desenvolver novas funcionalidades requer tempo e esforço. Se você achar nosso trabalho útil e quiser apoiar nosso desenvolvimento, considere fazer uma doação.

## Por que doar?

- **Suporte Contínuo**: Sua doação ajuda a manter o projeto ativo e em constante evolução.
- **Novos Recursos**: Com seu apoio, podemos adicionar novos recursos e melhorias.
- **Manutenção e Correções**: Garantimos que bugs sejam corrigidos rapidamente e que o código esteja sempre atualizado.
- **Reconhecimento**: Apoiadores são reconhecidos em nossa documentação e página do projeto.
- **Fraldas**: Meu primeiro filho nasceu no inicio desse ano, fraldas são caras! 🍼🚼

## Como doar?

Você pode contribuir através das seguintes plataformas:

- [GitHub Sponsors](https://github.com/sponsors/Maurelima)
- **Pix**: Se preferir doar via Pix, utilize a seguinte chave:

    ```
    Chave Pix: 944ce2f2-e90f-400a-a388-bb1fe6719e02
    Nome: Marco Lima
    ```

Agradecemos imensamente seu apoio!

## Outras formas de contribuir

Se você não puder doar financeiramente, existem outras maneiras valiosas de contribuir:

- **Reportar Bugs**: Envie relatórios de bugs e problemas que encontrar.
- **Submeter PRs**: Contribua com código, documentação ou testes.
- **Espalhe a Palavra**: Compartilhe nosso projeto com amigos e colegas.

## Agradecimentos

Agradecemos imensamente seu apoio e contribuição. Juntos, podemos construir e manter uma ferramenta incrível para todos!

**Muito obrigado!**


## Devs

| [<img src="https://avatars.githubusercontent.com/u/59918400?s=400&u=3554ebcf0f75263637516867945ebd371e68da71&v=4" width="75px;"/>](https://github.com/Maurelima) |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|                                                            [Marco Lima](https://github.com/Maurelima)                                                            |

