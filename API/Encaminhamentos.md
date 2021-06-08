**[Integra��o via API](Guideline.md) - Encaminhamentos**

A documenta��o para os m�todos de Encaminhamentos pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Encaminhamentos).

As a��es poss�veis para encaminhamento s�o:
- **[1 - Novo Encaminhamento:](#novo-encaminhamento)**
  - Autenticar para uso do E-Docs por m�todo Bearer;
- **[2 - Reencaminhamento:](#reencaminhamento)**
  - Enviar para o E-docs o tamanho do arquivo a ser enviado, recebendo o endere�o para onde deve ser enviado o arquivo f�sico;
- **[3 - Responder](#responder)**
- O documento dever� passar pela Fase de Assinatura, onde o Capturador (o cidad�o ou servidor respons�vel pelo registro) informar� o nome do arquivo criado na nuvem constante no JSON recebido na etapa anterior e todas as informa��es de metadados e quais ser�o os assinantes para o mesmo;
- **[4 - Complementar:](#complementar)**
  - O E-Docs ir� colocar o documento na fila de captura, em um objeto de evento, com o identificador recebido na etapa anterior;
- **[5 - Consultas:](#consultas)**
  - O documento j� pode ser utilizado em processos, encaminhamentos, consultas, etc.

### Autentica��o no E-Docs

A autentica��o ser� atrav�s do padr�o **Bearer Token**, utilizando o Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o. 

- Para as requisi��es aos endpoints de a��es de encaminhamento ser� requerido o scope 'api-sigades-encaminhamento' no cabe�alho;
- Para as requisi��es de consulta, ser� requerido o scope 'api-sigades-consultar' (ou a anterior) no cabe�alho. 

[Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5).

### Novo Encaminhamento

Um encaminhamento original, sem que haja um v�nculo com encaminhamento anterior.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documenta��o](Documentos.md).

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_novo);

O retorno do endpoint ser� o identificador do evento de encaminhamento que foi enfileirado.

### Reencaminhamento

Um encaminhamento de um encaminhamento recebido.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documenta��o](Documentos.md).

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_reencaminhar);

O retorno do endpoint ser� o identificador do evento de encaminhamento que foi enfileirado.

### Responder

Um encaminhamento de resposta ao remetente de um encaminhamento.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documenta��o](Documentos.md).

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_responder);

O retorno do endpoint ser� o identificador do evento de encaminhamento que foi enfileirado.

### Complementar

Complementar um encaminhamento enviado com novas informa��es, se ele ainda n�o foi reencaminhado ou respondido pelo destinat�rio.

Se houver documentos associados deve-se seguir previamente o passo de capturar esse documento, conforme [a documenta��o](Documentos.md).

Para maiores informa��es sobre restri��o de acesso [clique aqui](RestricaoAcesso.md).

Uma vez definidos os metadados do encaminhamento, utilizar esse endpoint [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Encaminhamentos-post_v2_encaminhamento_complementar);

O retorno do endpoint ser� o identificador do evento de encaminhamento que foi enfileirado.

### Consultas

Como explicitado na etapa anterior, ao enviar o encaminhamento, ele � encapsulado em um evento, que fica enfileirado aguardando o seu momento para ser executado.

Com a posse do identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do encaminhamento que foi enviado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

Ap�s um Encamihamento ser registrado ele poder� ser consultado, respondido, etc.

Para os endpoints de consulta, consultar a documenta��o completa [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Encaminhamentos).

### Informa��es necess�rias para preenchimento

Para buscar o patriarcas, �rg�os, setores, grupos de trabalho e comiss�es, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

Para buscar os fundamentos legais cab�veis a voc�, utilize [esse endpoint](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).

Para buscar informa��es do usu�rio logado, tal qual assinaturas, papeis, caixas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).