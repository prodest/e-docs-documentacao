**[Integração via API](Guideline.md) - Documentos**

A documentação para os métodos de Documentos pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Documentos).

O procedimento padrão para registrar documentos no E-Docs consistem em:
- **[1 - Autenticação no E-Docs:](#autenticacao-no-e-docs)**
  - Autenticar para uso do E-Docs por método Bearer;
- **[2 - Envio de Arquivo para E-Docs:](#envio-de-arquivo-para-e-docs)**
  - a - Enviar para o E-docs o tamanho do arquivo a ser enviado, recebendo o endereço para onde deve ser enviado o arquivo físico;
  - b - Enviar o arquivo para o caminho acima (esse envio não será realizado através de end-point E-Docs) recebendo um objeto JSON com informações para as etapas posteriores;
- **[3 - Registro do documento e captura](#registro-do-documento-e-captura)**
  - **[Se for arquivo nato-digital e com Assinatura Eletrônica E-Docs:](#se-for-arquivo-nato-digital-e-com-assinatura-digital-e-docs)**
    - a - O documento deverá passar pela Fase de Assinatura, onde o Capturador (o cidadão ou servidor responsável pelo registro) informará o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informações de metadados e quais serão os assinantes para o mesmo;
    - b - Todos os assinantes devem assinar ou recusar assinatura;
    - c - Após o último assinante se manifestar, o documento será enviado para captura, sendo retornado um identificador do evento dessa captura;
  - **[Se for arquivo nato digital e com apenas a Assinatura Eletrônica E-Docs do Capturador:](#se-for-arquivo-nato-digital-e-com-apenas-a-assinatura-digital-e-Docs-do-capturador)**
    - a - O Capturador (o cidadão ou servidor responsável pelo registro) informará o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informações de metadados;
    - b - O documento será assinado pelo capturador e posteriormente o documento será enviado para captura, sendo retornado um identificador do evento dessa captura;
  - **[Para todos os outros casos:](#para-todos-os-outros-casos)**
    - a - O Capturador (o cidadão ou servidor responsável pelo registro) informará o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informações de metadados;
    - b - O documento será enviado para captura, sendo retornado um identificador do evento dessa captura;
- **[4 - Captura do documento:](#captura-do-documento)**
  - a - O E-Docs irá colocar o documento na fila de captura, em um objeto de evento, com o identificador recebido na etapa anterior;
  - b - Uma vez o evento seja executado, o objeto de evento será complementado com a informação do identificador do documento capturado;
- **[5 - Documento capturado:](#documento-capturado)**
  - O documento já pode ser utilizado em processos, encaminhamentos, consultas, etc.

### Autenticação no E-Docs

A autenticação será através do padrão **Bearer Token**, utilizando o Access Token obtido através da **Autenticação de Usuário** no Acesso Cidadão. 

- Para as requisições aos endpoints de Fase de Assinatura e Captura será requerido o scope 'api-sigades-documento' no cabeçalho;
- Para as requisições de consulta, será requerido o scope 'api-sigades-consultar' (ou a anterior) no cabeçalho. 

[Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5).

### Envio de Arquivo para E-Docs
A API do E-Docs aceita apenas arquivos texto, de extensão PDF.

O primeiro endpoint a ser utilizado é o [pegar-url-envio](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-get_v2_documentos_upload_arquivo_pegar_url_envio__tamanhoArquivo_) onde deve ser enviado exato do tamanho do arquivo a ser enviado, recebendo ao final uma url que será utilizada para o envio do arquivo físico.

De posse desse endereço, deve-se realizar uma requisição POST direto para a nuvem do E-Docs, conforme exemplos de código abaixo.

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

Agora o método para realizar a requisição POST (essa etapa deve ser realizada imediatamente após a execução da etapa anterior, pois a janela de envio se fecha em poucos segundos):
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
        Name = "file", //nome do parâmetro do arquivo, não alterar
        FileName = data.File.Split('\\')[^1] //na prática esse nome aqui não será utilizado
    };

    //adiviona os parâmetros retornados pelo JSON no content
    using var content = new MultipartFormDataContent
    {
        streamContent
    };
    data.Body.ToList().ForEach(parametro =>
    {
        content.Add(new StringContent(paramstro.Value), parametro.Key);
    });

    //faz a requisição
    using var response = await client.PostAsync(url, content);

    //se tudo der certo vai retornar true
    return response.IsSuccessStatusCode;
}
```

Esse arquivo irá para uma área temporária aguardando os próximos passos de registro dos metadados do Documento. Caso não seja realizado esse próximo passo, esse arquivo será excluído do servidor, por falta de vínculo com um Documento registrado no E-Docs.

### Registro do documento e captura

Nesse passo você deverá dar continuidade aos passos anteriores de upload do arquivo a ser registrado.

Ao fim desse passo você terá posse do identificador do evento de captura que foi enfileirado.

Há diferentes tipos de etapas, de acordo com o tipo de documento enviado:

### Se for arquivo nato-digital e com assinatura digital E-Docs

Arquivo nato-digital é um arquivo originado a partir de um documento digital, tal como suítes de escritório, e exportado para PDF.

Nesse caso, haverá multiplos assinantes, ou há um assinante, mas este não é o capturador, portanto as assinaturas serão realizadas em um momento posterior, através de endpoints específicos. 

Em caso de o documento em fase de assinatura ter sido criado por um cidadão, todos os assinantes devem ser cidadãos.

Portanto, o primeiro endpoint é o de envio do nome do arquivo criado na nuvem constante no JSON retornado na etapa anterior, tal qual das informações do Documento, conforme descrito [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_auto_assinado_servidor) ou [aqui se for um cidadão](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_auto_assinado_cidadao).

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md)

Registrado o documento em fase de assinatura, o retorno será um identificador de documento em fase de assinatura.

Nesse momento, em posse desse identificador, os usuários assinantes devem - autenticados com seus respectivos Access Tokens - realizar a assinatura conforme descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-get_v2_documentos_fase_assinatura_assinar__IdDocumentoFaseAssinatura_).

Com a última manifestação de assinante realizada o documento é capturado e o retorno do endpoint de assinatura retorna capturado como true e idCapturaEvento retorna o identificador do evento de captura que foi enfileirado.

### Se for arquivo nato digital e com apenas a assinatura digital E-Docs do Capturador

Arquivo nato-digital é um arquivo originado a partir de um documento digital, tal como suítes de escritório, e exportado para PDF.

Nesse caso, haverá apenas um assinante, e este é o próprio capturador, portanto a assinatura serão realizada automaticamente.

Assim, o endpoint recebrá o nome do arquivo criado na nuvem constante no JSON retornado na etapa anterior, tal qual as informações do Documento, conforme descrito [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_fase_assinatura_enviar_servidor) ou [aqui se for um cidadão](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_fase_assinatura_enviar_cidadao).

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md)

Registrado o documento, o E-Docs automaticamente irá acrescentar o Capturador como assinante, já realizando também essa etapa.

Por fim é realizada a captura e retorna-se o identificador do evento de captura que foi enfileirado.

### Para todos os outros casos

Aqui se engloba os tipos de arquivo:
- Arquivo nato-digital, que é um arquivo originado a partir de um documento digital, tal como suítes de escritório, e exportado para PDF.
  - Se o arquivo nato-digital é apenas uma cópia, sem nenhum assinatura;
  - Se o arquivo nato-digital foi previamente assinado por uma assinatura digital padrão ICP-Brasil.
- Arquivo digitalizado, que é um arquivo originado a partir de um documento físico em papel, digitalizado por foto ou dispositivo digitalizador de documentos tal qual scanner, no formato PDF.

Assim, será enviado o nome do arquivo criado na nuvem constante no JSON retornado na etapa anterior, tal qual as informações do Documento, para o endpoint mais adequado:

- Nato-digital ICP-Brasil, [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_icp_brasil_servidor) ou [aqui se for um cidadão](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_icp_brasil_cidadao)
- Nato-digital cópia, [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_copia_servidor) ou [aqui se for um cidadão](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_nato_digital_copia_cidadao)
- Digitalizado, [aqui se for um servidor](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_digitalizado_servidor) ou [aqui se for um cidadão](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_capturar_digitalizado_cidadao)

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md).

Por fim é realizada a captura e retorna-se o identificador do evento de captura que foi enfileirado.

### Captura do Documento

A captura do Documento é a forma de institucionalizá-lo e fazer com que ele possa ser utilizado dentro do E-Docs.

Na etapa anterior, o Documento foi categorizado quando à sua Natureza, Valor Legal e Gênero

Natureza:
- Nato-digital;
- Digitalizado

Valor Legal:
- Original;
- Cópia Autenticada Administrativamente;
- Cópia Simples

Gênero:
- Textual (único aceito pela API);
- Áudio;
- Vídeo

Como explicitado na etapa anterior, ao enviar o documento para captura, ele é encapsulado em um evento, que fica enfileirado aguardando o seu momento para ser executado.

Com a posse do identificador você pode consultar se o evento já foi executado, retornando o identificador do documento que foi capturado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Documento capturado

Após um Documento ser capturado ele poderá ser consultado, validado, entre outros.

Destacamos entre os demais end points:
- Pode usar: se o usuário tem permissão para usar esse documento em processos, encaminhamentos, etc. [Clique aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-get_v2_documentos__idDocumento__pode_usar).
- Validação de Assinatura Digital: Para validar se esse arquivo é um arquivo capturado no E-Docs. Ele não valida a veracidade do conteúdo, apenas o armazenamento no E-Docs. [Clique aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Documentos-post_v2_documentos_assinatura_digital_valida).

Para os demais endpoints, consultar a documentação completa [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Documentos).

### Informações necessárias para preenchimento

Para buscar o patriarcas, órgãos, setores, grupos de trabalho e comissões, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

Para buscar o planos ativos e classes ativas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-ClassificacaoDocumental).

Para buscar os fundamentos legais cabíveis a você, utilize [esse endpoint](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).

Para buscar informações do usuário logado, tal qual assinaturas, papeis, caixas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).
