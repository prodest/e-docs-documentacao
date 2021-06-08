**[Integração via API](Guideline.md) - Encaminhamentos**

A documentação para os métodos de Encaminhamentos pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Encaminhamentos).

As ações possíveis para encaminhamento são:
- **[1 - Novo Encaminhamento:](#novo-encaminhamento)**
  - Autenticar para uso do E-Docs por método Bearer;
- **[2 - Reencaminhamento:](#reencaminhamento)**
  - Enviar para o E-docs o tamanho do arquivo a ser enviado, recebendo o endereço para onde deve ser enviado o arquivo físico;
- **[3 - Responder](#responder)**
- O documento deverá passar pela Fase de Assinatura, onde o Capturador (o cidadão ou servidor responsável pelo registro) informará o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informações de metadados e quais serão os assinantes para o mesmo;
- **[4 - Complementar:](#complementar)**
  - O E-Docs irá colocar o documento na fila de captura, em um objeto de evento, com o identificador recebido na etapa anterior;
- **[5 - Consultas:](#consultas)**
  - O documento já pode ser utilizado em processos, encaminhamentos, consultas, etc.

### Autenticação no E-Docs

A autenticação será através do padrão **Bearer Token**, utilizando o Access Token obtido através da **Autenticação de Usuário** no Acesso Cidadão. 

- Para as requisições aos endpoints de ações de encaminhamento será requerido o scope 'api-sigades-encaminhamento' no cabeçalho;
- Para as requisições de consulta, será requerido o scope 'api-sigades-consultar' (ou a anterior) no cabeçalho. 

[Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5).

### Novo Encaminhamento

Um encaminhamento original, sem que haja um vínculo com encaminhamento anterior.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documentação](Documentos.md).

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_novo);

O retorno do endpoint será o identificador do evento de encaminhamento que foi enfileirado.

### Reencaminhamento

Um encaminhamento de um encaminhamento recebido.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documentação](Documentos.md).

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_reencaminhar);

O retorno do endpoint será o identificador do evento de encaminhamento que foi enfileirado.

### Responder

Um encaminhamento de resposta ao remetente de um encaminhamento.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documentação](Documentos.md).

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_responder);

O retorno do endpoint será o identificador do evento de encaminhamento que foi enfileirado.

### Complementar

Complementar um encaminhamento enviado com novas informações, se ele ainda não foi reencaminhado ou respondido pelo destinatário.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documentação](Documentos.md).

Para maiores informações sobre restrição de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_complementar);

O retorno do endpoint será o identificador do evento de encaminhamento que foi enfileirado.

### Consultas

Como explicitado na etapa anterior, ao enviar o encaminhamento, ele é encapsulado em um evento, que fica enfileirado aguardando o seu momento para ser executado.

Com a posse do identificador você pode consultar se o evento já foi executado, retornando o identificador do encaminhamento que foi enviado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

Após um Encamihamento ser registrado ele poderá ser consultado, respondido, etc.

Para os endpoints de consulta, consultar a documentação completa [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Encaminhamentos).

### Informações necessárias para preenchimento

Para buscar o patriarcas, órgãos, setores, grupos de trabalho e comissões, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

Para buscar os fundamentos legais cabíveis a você, utilize [esse endpoint](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).

Para buscar informações do usuário logado, tal qual assinaturas, papeis, caixas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).