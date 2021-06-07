## Restrição de Acesso

Para visualizar o modelo, acesse [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#model-RestricaoAcessoApiEntry).

Para maiores informações, clique [aqui](../Documentos/AcessoLimitado.md).

Há os seguintes níveis de acesso para documentos disponíveis pela API:
- [Público](#publico)
- [Organizacional](#organizacional)
- [Sigiloso](#sigiloso)
- [Classificado](#classificado)

### Público

O documento é visualizável por qualquer pessoa.

Basta enviar o modelo com transparenciaAtiva como true, e nulo no restante.

### Organizacional

O documento é visualizável por qualquer pessoa lotada nos Órgãos por onde o documento transitou.

Basta enviar o modelo com transparenciaAtiva como false, e nulo no restante.

### Sigiloso

O documento é visualizável somente por pessoas diretamente credenciadas a ele.

Basta enviar o modelo com transparenciaAtiva como false, a lista de identificadores de fundamentos legais adequados e classificação de informação como nulo.

### Classificado

O documento é visualizável somente por pessoas previamente credenciadas para visualizar documentos com essa classificação.

Basta enviar o modelo com transparenciaAtiva como false, a lista de identificadores de fundamentos legais adequados e as informações de classificação de informação.

### Informações necessárias

Para buscar o seu patriarca, utilize [esse endpoint](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Agente-get_v2_agente_patriarcas).

Para buscar os fundamentos legais cabíveis a você, utilize [esse endpoint](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-FundamentosLegais-get_v2_fundamentos_legais__idPatriarca_).