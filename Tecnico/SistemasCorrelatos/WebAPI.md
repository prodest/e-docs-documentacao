# **API v2**

Os códigos de status das respostas HTTP indicam se uma requisição HTTP foi corretamente concluída. As respostas são agrupadas em cinco classes:

- Respostas de informação (100-199)
- **Respostas de sucesso (200-299)**
- Redirecionamentos (300-399)
- **Erros do cliente (400-499)**
- **Erros do servidor (500-599)**

200 OK
- Recurso encontrado, mas lista vazia
- Recurso encontrado, mas com lista

## **Documentos com Assinatura Eletrônica E-Docs**

Documentos que já serão capturados com a assinatura eletrônica E-Docs.

Esses endpoints devem ser utilizados quando:
- Somente o capturador será o assinante.

### **Consultas**

As consultas aos documentos com assinatura eletrônica E-Docs que foram capturados deverão ser realizadas nos endpoints de consultas de documentos.

### **Inserções**

`POST /v2/documento-assinatura/cidadaos`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- FundamentosLegais - Lista de guids

`POST /v2/documento-assinatura/servidores`

Atributos
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- Identificador do Papel do Capturador - guid
- Identificador da Classe - guid
- Fundamentos Legais - Lista de guids

## **Documento em Fase Assinatura**

Documentos que ficarão na fase de assinatura até a assinatura do último assinante indicado. Após a assinatura de todos os assinantes indicados este documento será capturado como um documento com assinatura eletrônica E-Docs.

Esses endpoints devem ser utilizados quando:
- O capturador não for o assinante; ou
- O documento for assinado por mais de um assinante.

### **Consultas**
`POST /v2/documentos-fase-assinatura/search`

### **Inserções**

`POST /v2/documentos-fase-assinatura/cidadaos`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- FundamentosLegais - Lista de Guids

`POST /v2/documentos-fase-assinatura/servidores`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- Fundamentos Legais - Lista de guids
- Identificador do Papel do Capturador - guid
- Identificador da Classe - guid

### **Ações**

`POST /v2/documentos-fase-assinatura/{idDocumentoFaseAssinatura}/assinatura`
Não possui atributos a serem informados

`POST /v2/documentos-fase-assinatura/{idDocumentoFaseAssinatura}/bloqueio`
Não possui atributos a serem informados

`POST /v2/documentos-fase-assinatura/{idDocumentoFaseAssinatura}/recusa`

Atributos:
- Justificativa

### **Exclusões**
`DELETE /v2/documento-fase-assinatura/{idDocumentoFaseAssinatura}`


## **Documento**

### **Inserções**

`POST /v2/documentos/textuais/digitalizados/servidores`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- Fundamentos Legais - Lista de guids
- Identificador do Papel do Capturador - guid
- Documento de origem


`POST /v2/documentos/textuais/digitalizados/cidadaos`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- Fundamentos Legais - Lista de guids


`POST /v2/documentos/textuais/nato-digitais/copias`

Atributos:
- Conteúdo - Matriz de bytes


`POST /v2/documentos/textuais/nato-digitais/icps-brasil`

Atributos:
- Conteúdo - Matriz de bytes


`POST /v2/documentos/audios`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- Fundamentos Legais - Lista de guids


`POST /v2/documentos/videos`

Atributos:
- Conteúdo - Matriz de bytes
- Nome - Alfanumérico
- Público - Boleano
- Fundamentos Legais - Lista de guids


**Consultas**

`POST /v2/documentos/search`

**Único Elemento**

`GET ​/v2​/documento​/{protocolo}`

**Lista de Elementos**

`GET ​/v2​/documentos​/{id}​/assinantes`

`GET ​/v2​/documentos​/{id}​/fundamentos-legais`

`GET ​/v2​/documentos​/{id}​/temp-content-url`

`GET ​/v2​/documentos​/{id}​/encaminhamentos`

`GET ​/v2​/documentos​/{id}​/processos`

**Edições**

`PUT /v2/documentos/{idDocumento}/fundamentos-legais`

## **Processo**

### **Inserções**

`POST /v2/processos/autuacao`

`POST /v2/processos/{idProcesso}/despacho`

`POST /v2/processos/{idProcesso}/desentranhamento`

`POST /v2/processos/{idProcesso}/entranhamento`

`POST /v2/processos/{idProcesso}/avocamento`

`POST /v2/processos/{idProcesso}/encerramento`

`POST /v2/processos/{idProcesso}/reabertura`

`POST /v2/processos/{idProcesso}/edicao`

### **Consultas**

`POST /v2/processos/search`

`POST /v2/processos/{idProcesso}/documentos/search`

`POST /v2/processos/{idProcesso}/atos/search`

### **Encaminhamento**

### **Inserções**

`POST /v2/encaminhamentos`

`POST /v2/encaminhamentos/{idEncaminhamento}/encaminhamento`

### **Consultas**

`POST /v2/encaminhamentos/search`

`POST /v2/encaminhamentos/{idEncaminhamento}/documentos/search`

`POST /v2/encaminhamentos/{idEncaminhamento}/anteriores/search`

`POST /v2/encaminhamentos/{idEncaminhamento}/posteriores/search`

`POST /v2/encaminhamentos/{idEncaminhamento}/entranhamentos/search`