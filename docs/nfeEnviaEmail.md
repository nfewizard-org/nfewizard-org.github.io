# NFeEnviaEmail

!!! Quote ""
    `Função`: Método destinado ao envio de e-mails.<br>
    `Processo`: síncrono.<br>
<br>

```typescript title="NFE_EnviaEmail" linenums="1"
const nfeWizard = new NFeWizard();

const messageExample = `
<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Envio de NF-e e DANFE</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }

        .container {
            width: 100%;
            max-width: 600px;
            margin: 0 auto;
            background-color: #ffffff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .header {
            background-color: #007BFF;
            color: #ffffff;
            padding: 10px 20px;
            text-align: center;
        }

        .content {
            margin: 20px 0;
        }

        .content h1 {
            color: #333333;
            font-size: 24px;
        }

        .content p {
            color: #555555;
            font-size: 16px;
            line-height: 1.5;
        }

        .footer {
            background-color: #007BFF;
            color: #ffffff;
            padding: 10px 20px;
            text-align: center;
        }

        .footer p {
            margin: 0;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="header">
            <h2>Envio de NF-e e DANFE</h2>
        </div>
        <div class="content">
            <h1>Prezado Cliente,</h1>
            <p>
                Estamos enviando em anexo a Nota Fiscal Eletrônica (NF-e) e o Documento Auxiliar da Nota Fiscal
                Eletrônica (DANFE) referente à sua compra.
            </p>
            <p>
                Por favor, verifique os documentos anexos:
            </p>
            <ul>
                <li>DANFE.pdf</li>
                <li>35240706319316000127550011452380351650831257.json</li>
                <li>35240706319316000127550011452380351650831257.xml</li>
            </ul>
            <p>
                Caso tenha alguma dúvida ou necessite de mais informações, não hesite em nos contatar.
            </p>
            <p>
                Agradecemos pela sua preferência.
            </p>
        </div>
        <div class="footer">
            <p>
                Atenciosamente,<br>
                Equipe de Atendimento ao Cliente
            </p>
        </div>
    </div>
</body>
</html>
`;

nfeWizard.NFE_EnviaEmail({
    messageExample,
    subject: 'Envio de DANFE e NF-e',
    attachments: [
        {
            filename: 'DANFE.pdf',
            path: './tmp/Autorizacao/DANFE-99999999999999999999999999999999999999999999.pdf'
        },
        {
            filename: '99999999999999999999999999999999999999999999.xml',
            path: './tmp/Autorizacao/99999999999999999999999999999999999999999999.xml'
        },
    ]
});
```
<br>

`Retorno`:

!!! Quote "Interface de Retorno"
    E-mail enviado com sucesso.

<br><br>