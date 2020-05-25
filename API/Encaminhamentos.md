**[Integração via API](Guideline.md) - Encaminhamentos**

O Encaminhamento é a forma de Documentos tramitarem sem estarem entranhados a um processo, de forma avulsa.

**Ações disponíveis:**
- [Encmainhar](#encaminhar)
- [Consultar](#consultar)

### Encaminhar
Um Encaminhamento pode ser inserido sem referenciar um Encaminhamento Anterior, neste caso ele será o raiz.

Um Encaminhamento pode ser inserido referenciando um Encaminhamento Anterior, conforme descrito abaixo:
- Complementar, quando remetente deseja complementar com alguma informação o Encaminhamento que foi feito anteriormente
- Responder, quando o destinatário deseja responder ao rementente do Encaminhamento Anterior
- Reencaminhar, quando o destinatário deseja encaminhar o Encaminhamento Anterior para um outro destinatário

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Encaminhamentos/Encaminhamentos_Post).

O Access Token obtido através da **Autenticação de Usuário** no Acesso Cidadão utilizando o scope 'api-sigades-encaminhamento' é requerido no cabeçalho das requisições aos endpoints de Encaminhar usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Consultar
Após um Encaminhamento ser inserido ele poderá ser consultado.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Encaminhamentos/Encaminhamentos_Get).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-consultar' ou 'api-sigades-encaminhamento' é requerido no cabeçalho das requisições aos endpoints de Consulta usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)