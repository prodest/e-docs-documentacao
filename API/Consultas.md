**[Integração via API](Guideline.md) - Informações Complementares para Preenchimento de Processos, Documentos e Encaminhamentos**

Segue abaixo classes de informações que serão necessários consultar para preencher adequadamente os cadastros de Processos, Documentos e Encaminhamento.

Será necessário autenticação com Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-consultar' no cabeçalho das requisições aos endpoints usando o padrão Bearer Token. 

[Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)


**Ações disponíveis:**
- [Agentes](#agentes)
- [Classificação Documental](#classificacao-documental)
- [Fundamentos Legais](#fundamentos-legais)
- [Usuário](#usuario)
- [Restrição de Acesso](#restricao-acesso)

### Agentes

Patriarcas, órgãos, setores, grupos de trabalho e comissões serão utilizados em cadastros de Documentos, Encaminhamentos e Processos.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

### Classificação Documental

Planos ativos e classes serão utilizados em cadastros de Documentos e Processos, de acordo com a Organização.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-ClassificacaoDocumental).

### Fundamentos Legais

Fundamentos legais serão utilizados em cadastros de Documentos e Processos, de acordo com a Organização.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).

### Usuário

Através desses endpoints é possível buscar informações inerentes ao usuário logado pelo AccessToken, tal como as formas de assinar, os papéis, utilizações dos papéis, permissões de autuação e locais de autuação, tal qual visualizar as caixas de processo e encaminhamento.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).

### Restrição de Acesso

As limitações de acesso ao conteúdo a um Documento, de acordo com legislação.

Acesse o guia específico desse tema [aqui](RestricaoAcesso.md).