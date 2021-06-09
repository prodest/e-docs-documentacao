**[Integra��o via API](Guideline.md) - Informa��es Complementares para Preenchimento de Processos, Documentos e Encaminhamentos**

Segue abaixo classes de informa��es que ser�o necess�rios consultar para preencher adequadamente os cadastros de Processos, Documentos e Encaminhamento.

Ser� necess�rio autentica��o com Access Token obtido atrav�s da autentica��o no Acesso Cidad�o utilizando o scope 'api-sigades-consultar' no cabe�alho das requisi��es aos endpoints usando o padr�o Bearer Token. 

[Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)


**A��es dispon�veis:**
- [Agentes](#agentes)
- [Classifica��o Documental](#classificacao-documental)
- [Fundamentos Legais](#fundamentos-legais)
- [Usu�rio](#usuario)
- [Restri��o de Acesso](#restricao-acesso)

### Agentes

Patriarcas, �rg�os, setores, grupos de trabalho e comiss�es ser�o utilizados em cadastros de Documentos, Encaminhamentos e Processos.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

### Classifica��o Documental

Planos ativos e classes ser�o utilizados em cadastros de Documentos e Processos, de acordo com a Organiza��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-ClassificacaoDocumental).

### Fundamentos Legais

Fundamentos legais ser�o utilizados em cadastros de Documentos e Processos, de acordo com a Organiza��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).

### Usu�rio

Atrav�s desses endpoints � poss�vel buscar informa��es inerentes ao usu�rio logado pelo AccessToken, tal como as formas de assinar, os pap�is, utiliza��es dos pap�is, permiss�es de autua��o e locais de autua��o, tal qual visualizar as caixas de processo e encaminhamento.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).

### Restri��o de Acesso

As limita��es de acesso ao conte�do a um Documento, de acordo com legisla��o.

Acesse o guia espec�fico desse tema [aqui](RestricaoAcesso.md).