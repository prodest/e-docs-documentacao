**[Integra��o via API](Guideline.md) - Documentos**

A documenta��o para os m�todos de Documentos pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Documentos).

O procedimento padr�o para registrar documentos no E-Docs consistem em:
- **[1 - Autentica��o no E-Docs:](#autenticacao-no-e-docs)**
  - Autenticar para uso do E-Docs por m�todo Bearer;
- **[2 - Envio de Arquivo para E-Docs:](#envio-de-arquivo-para-e-docs)**
  - a - Enviar para o E-docs o tamanho do arquivo a ser enviado, recebendo o endere�o para onde deve ser enviado o arquivo f�sico;
  - b - Enviar o arquivo para o caminho acima (esse envio n�o ser� realizado atrav�s de end-point E-Docs) recebendo um objeto JSON com informa��es para as etapas posteriores;
- **[3 - Registro do documento e captura](#registro-do-documento-e-captura)**
  - **[Se for arquivo nato-digital e com assinatura digital E-Docs:](#se-for-arquivo-nato-digital-e-com-assinatura-digital-e-docs)**
    - a - O documento dever� passar pela Fase de Assinatura, onde o Capturador (o cidad�o ou servidor respons�vel pelo registro) informar� o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informa��es de metadados e quais ser�o os assinantes para o mesmo;
    - b - Todos os assinantes devem assinar ou recusar assinatura;
    - c - Ap�s o �ltimo assinante se manifestar, o documento ser� enviado para captura, sendo retornado um identificador do evento dessa captura;
  - **[Se for arquivo nato digital e com apenas a assinatura digital E-Docs do Capturador:](#se-for-arquivo-nato-digital-e-com-apenas-a-assinatura-digital-e-Docs-do-capturador)**
    - a - O Capturador (o cidad�o ou servidor respons�vel pelo registro) informar� o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informa��es de metadados;
    - b - O documento ser� assinado pelo capturador e posteriormente o documento ser� enviado para captura, sendo retornado um identificador do evento dessa captura;
  - **[Para todos os outros casos:](#para-todos-os-outros-casos)**
    - a - O Capturador (o cidad�o ou servidor respons�vel pelo registro) informar� o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informa��es de metadados;
    - b - O documento ser� enviado para captura, sendo retornado um identificador do evento dessa captura;
- **[4 - Captura do documento:](#captura-do-documento)**
  - a - O E-Docs ir� colocar o documento na fila de captura, em um objeto de evento, com o identificador recebido na etapa anterior;
  - b - Uma vez o evento seja executado, o objeto de evento ser� complementado com a informa��o do identificador do documento capturado;
- **[5 - Documento capturado:](#documento-capturado)**
  - O documento j� pode ser utilizado em processos, encaminhamentos, consultas, etc.

### Autentica��o no E-Docs

A autentica��o ser� atrav�s do padr�o **Bearer Token**, utilizando o Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o. 

- Para as requisi��es aos endpoints de Fase de Assinatura e Captura ser� requerido o scope 'api-sigades-documento' no cabe�alho;
- Para as requisi��es de consulta, ser� requerido o scope 'api-sigades-documento' (ou a anterior) no cabe�alho. 

[Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5).

### Envio de Arquivo para E-Docs
A API do E-Docs aceita apenas arquivos texto, de extens�o PDF.

O primeiro endpoint a ser utilizado � o [pegar-url-envio](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-get_v2_documentos_upload_arquivo_pegar_url_envio__tamanhoArquivo_) onde deve ser enviado exato do tamanho do arquivo a ser enviado, recebendo ao final uma url que ser� utilizada para o envio do arquivo f�sico.

De posse desse endere�o, deve-se realizar uma requisi��o POST direto para a nuvem do E-Docs, conforme exemplos de c�digo abaixo.

Primeiro criar um modelo que vai conter o JSON recebido no endpoint anterior e o caminho completo do arquivo no servidor local:
```c#
class UploadDataJsonModel
{
    public UploadDataJsonModel(string caminhoCompletoArquivoLocal, DocumentoArquivoApiModel json)
    {
        Url = json.Url;
        File = caminhoCompletoArquivoLocal;
        Body = json.Body;
    }

    [JsonProperty("file")]
    public string File { get; set; }
    [JsonProperty("url")]
    public string Url { get; set; }
    [JsonProperty("body")]
    public IDictionary<string, string> Body { get; set; }
}
```

Agora o m�todo para realizar a requisi��o POST (essa etapa deve ser realizada imediatamente ap�s a execu��o da etapa anterior, pois a janela de envio se fecha em poucos segundos):
```c#
public async Task<bool> UploadFileToUrl(string url, UploadDataJsonModel data) {
    //cria o cliente do request
    using var client = new HttpClient();
    client.DefaultRequestHeaders.Add("Accept", "application/json");

    //cria o content com o arquivo
    var arquivo = File.ReadAllBytes(data.File).ToArray();
    using MemoryStream memoryStream = new MemoryStream(arquivo);
    using StreamContent streamContent = new StreamContent(memoryStream);
    streamContent.Headers.ContentType = MediaTypeHeaderValue.Parse("application/octet-stream");
    streamContent.Headers.ContentDisposition = new ContentDispositionHeaderValue("form-data")
    {
        Name = "file", //nome do par�metro do arquivo, n�o alterar
        FileName = data.File.Split('\\')[^1] //na pr�tica esse nome aqui n�o ser� utilizado
    };

    //adiviona os par�metros retornados pelo JSON no content
    using var content = new MultipartFormDataContent
    {
        streamContent
    };
    data.Body.ToList().ForEach(parametro =>
    {
        content.Add(new StringContent(paramstro.Value), parametro.Key);
    });

    //faz a requisi��o
    using var response = await client.PostAsync(url, content);

    //se tudo der certo vai retornar true
    return response.IsSuccessStatusCode;
}
```

Esse arquivo ir� para uma �rea tempor�ria aguardando os pr�ximos passos de registro dos metadados do Documento. Caso n�o seja realizado esse pr�ximo passo, esse arquivo ser� exclu�do do servidor, por falta de v�nculo com um Documento registrado no E-Docs.

### Registro do documento e captura

Nesse passo voc� dever� dar continuidade aos passos anteriores de upload do arquivo a ser registrado.

Ao fim desse passo voc� ter� posse do identificador do evento de captura que foi enfileirado.

H� diferentes tipos de etapas, de acordo com o tipo de documento enviado:

### Se for arquivo nato-digital e com assinatura digital E-Docs

Arquivo nato-digital � um arquivo originado a partir de um documento digital, tal como su�tes de escrit�rio, e exportado para PDF.

Nesse caso, haver� multiplos assinantes, ou h� um assinante, mas este n�o � o capturador, portanto as assinaturas ser�o realizadas em um momento posterior, atrav�s de endpoints espec�ficos.

Portanto, o primeiro endpoint � o de envio do nome do arquivo criado na nuvem constante no JSON retornado na etapa anterior, tal qual das informa��es do Documento, conforme descrito [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_auto_assinado_servidor) ou [aqui se for um cidad�o](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_auto_assinado_cidadao).

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md)

Registrado o documento em fase de assinatura, o retorno ser� um identificador de documento em fase de assinatura.

Nesse momento, em posse desse identificador, os usu�rios assinantes devem - autenticados com seus respectivos Access Tokens - realizar a assinatura conforme descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-get_v2_documentos_fase_assinatura_assinar__IdDocumentoFaseAssinatura_).

Com a �ltima manifesta��o de assinante realizada o documento � capturado e o retorno do endpoint de assinatura retorna capturado como true e idCapturaEvento retorna o identificador do evento de captura que foi enfileirado.

### Se for arquivo nato digital e com apenas a assinatura digital E-Docs do Capturador

Arquivo nato-digital � um arquivo originado a partir de um documento digital, tal como su�tes de escrit�rio, e exportado para PDF.

Nesse caso, haver� apenas um assinante, e este � o pr�prio capturador, portanto a assinatura ser�o realizada automaticamente.

Assim, o endpoint recebr� o nome do arquivo criado na nuvem constante no JSON retornado na etapa anterior, tal qual as informa��es do Documento, conforme descrito [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_fase_assinatura_enviar_servidor) ou [aqui se for um cidad�o](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_fase_assinatura_enviar_cidadao).

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md)

Registrado o documento, o E-Docs automaticamente ir� acrescentar o Capturador como assinante, j� realizando tamb�m essa etapa.

Por fim � realizada a captura e retorna-se o identificador do evento de captura que foi enfileirado.

### Para todos os outros casos

Aqui se engloba os tipos de arquivo:
- Arquivo nato-digital, que � um arquivo originado a partir de um documento digital, tal como su�tes de escrit�rio, e exportado para PDF.
  - Se o arquivo nato-digital � apenas uma c�pia, sem nenhum assinatura;
  - Se o arquivo nato-digital foi previamente assinado por uma assinatura digital padr�o ICP-Brasil.
- Arquivo digitalizado, que � um arquivo originado a partir de um documento f�sico em papel, digitalizado por foto ou dispositivo digitalizador de documentos tal qual scanner, no formato PDF.

Assim, ser� enviado o nome do arquivo criado na nuvem constante no JSON retornado na etapa anterior, tal qual as informa��es do Documento, para o endpoint mais adequado:

- Nato-digital ICP-Brasil, [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_icp_brasil_servidor) ou [aqui se for um cidad�o](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_icp_brasil_cidadao)
- Nato-digital c�pia, [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_copia_servidor) ou [aqui se for um cidad�o](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_copia_cidadao)
- Digitalizado, [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_digitalizado_servidor) ou [aqui se for um cidad�o](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_digitalizado_cidadao)

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md).

Por fim � realizada a captura e retorna-se o identificador do evento de captura que foi enfileirado.

### Captura do Documento

A captura do Documento � a forma de institucionaliz�-lo e fazer com que ele possa ser utilizado dentro do E-Docs.

Na etapa anterior, o Documento foi categorizado quando � sua Natureza, Valor Legal e G�nero

Natureza:
- Nato-digital;
- Digitalizado

Valor Legal:
- Original;
- C�pia Autenticada Administrativamente;
- C�pia Simples

G�nero:
- Textual (�nico aceito pela API);
- �udio;
- V�deo

Como explicitado na etapa anterior, ao enviar o documento para captura, ele � encapsulado em um evento, que fica enfileirado aguardando o seu momento para ser executado.

Com a posse do identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do documento que foi capturado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Documento capturado

Ap�s um Documento ser capturado ele poder� ser consultado, validado, entre outros.

Destacamos entre os demais end points:
- Pode usar: se o usu�rio tem permiss�o para usar esse documento em processos, encaminhamentos, etc. [Clique aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-get_v2_documentos__idDocumento__pode_usar).
- Valida��o de Assinatura Digital: Para validar se esse arquivo � um arquivo capturado no E-Docs. Ele n�o valida a veracidade do conte�do, apenas o armazenamento no E-Docs. [Clique aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_assinatura_digital_valida).

Para os demais endpoints, consultar a documenta��o completa [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Documentos).

### Informa��es necess�rias para preenchimento

Para buscar o patriarcas, �rg�os, setores, grupos de trabalho e comiss�es, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

Para buscar o planos ativos e classes ativas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-ClassificacaoDocumental).

Para buscar os fundamentos legais cab�veis a voc�, utilize [esse endpoint](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).

Para buscar informa��es a um usu�rio logado, tal qual assinaturas, papeis, caixas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).