**[Integração via API](Guideline.md) - Documentos**

**Ações disponíveis:**
- [Capturar](#capturar)
  - Capturar Documentos Cópia, Nato-digital ou digitalizado
  - Capturar Documentos que possuem Assinatura Digital
  - Capturar Documentos fazendo a Assinatura Eletrônica do E-Docs
  - Capturar um Documento para ser Assinado Eletronicamente via E-Docs
  - Assinar um Documento que está em fase de assinatura
  - Recusar um Documento que está em fase de assinatura
  - Bloquear um Documento que está em fase de assinatura
  - Desbloquear um Documento que está em fase de assinatura
- [Consultar](#consultar)

### Capturar
A captura do Documento é a forma de institucionalizá-lo e fazer com que ele possa ser utilizado dentro do E-Docs.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Documentos/Documentos_Post).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-documento' é requerido no cabeçalho das requisições aos endpoints de Captura usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

Para melhor entendimento, o Documento pode ser categorizado quando à sua Natureza, Valor Legal e Gênoro

Natureza:
- Nato-digital
- Digitalizado

Valor Legal:
- Original. 
- Cópia Autenticada Administrativamente
- Cópia Simples

Gênoro:
- Textual
- Áudio
- Vídeo

### Consultar
Após um Documento ser capturado ele poderá ser consultado.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Documentos/Documentos_Get).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-consultar' ou 'api-sigades-documento' é requerido no cabeçalho das requisições aos endpoints de Consulta usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)