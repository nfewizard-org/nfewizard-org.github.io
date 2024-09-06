# Inicializar Ambiente

Repositório do projeto [NFeWizard-io](https://github.com/nfewizard-org/nfewizard-io).

!!! Warning ""
    `ATENÇÃO`: Após a inicialização do ambiente você será capaz de utilizar a biblioteca para se comunicar com os webservices da SEFAZ.
    É importante que os &nbsp;objetos (dados) fornecidos aos métodos da biblioteca estejam na mesma ordem dos exemplos, uma vez que os XML serão gerados na mesma ordem e &nbsp;validados pelo webservice.
<br>

Para mais informações sobre opções de configuração consulte a sessão [`Configuração de Ambiente`](configuracaoDeAmbiente.md).
<br><br>

!!! Quote "Instalação"
    npm install nfewizard-io<br>
    yarn add nfewizard-io

```typescript title="NFE_LoadEnvironment" linenums="1"
import NFeWizard from 'nfewizard-io';

const nfewizard = new NFeWizard();

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
```