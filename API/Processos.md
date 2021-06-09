**[Integra��o via API](Guideline.md) - Processos**

A documenta��o para os m�todos de Processos pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Processos).

Autua��o e tramita��o de Processos Administrativos seguindo a formalidade da legisla��o vigente.

O Processo possui um custodiante que pode ser:
- Uma Organiza��o (�rg�o), neste caso o respons�vel pela organiza��o poder� realizar os atos processuais, podendo delegar tais compet�ncias.
- Uma Unidade (setor), neste caso o respons�vel pela unidade poder� realizar os atos processuais, podendo delegar tais compet�ncias.
- Um Grupo, neste caso todos os membros do Grupo poder�o realizar os atos processuais.
- Um Papel (servidor p�blico ocupando um cargo ou fun��o), neste caso somente o detentor do Papel poder� realizar os atos processuais.

Para realizar os Atos Autuar, Despachar, Avocar, Entranhar Documentos, Desentranhar Documentos, Entranhar Encaminhamentos, Editar, Encerrar e Reabrir � neces�rio que o usu�rio possua pelo menos um papel no Acesso Cidad�o, e este papel deve possuir uma lota��o.
Usu�rios que s�o servidores do Governo do Estado do Esp�rito Santo j� possuem seus papeis atribu�dos atrav�s da integra��o com o sistema SIARHES, bem como sua lota��o.
Caso seja necess�rio atribuir um papel a um terceiro, o administrador do sistema que est� se integrando poder� fazer isso diretamente no Acesso Cidad�o, neste caso tamb�m � necess�rio informar a lota��o do papel do terceiro.

**A��es dispon�veis:**
- [Autuar](#autuar)
- [Despachar](#despachar)
- [Avocar](#avocar)
- [Entranhar Documentos](#entranhar-documentos)
- [Desentranhar Documentos](#desentranhar-documentos)
- [Entranhar Encaminhamentos](#entranhar-encaminhamento)
- [Editar](#editar)
- [Encerrar](#encerrar)
- [Reabrir](#reabrir)
- [Consultar](#consultar)

### Autentica��o no E-Docs

A autentica��o ser� atrav�s do padr�o **Bearer Token**, utilizando o Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o. 

- Para as requisi��es aos endpoints de Atos Processuais ser� requerido o scope 'api-sigades-processo' no cabe�alho;
- Para as requisi��es de consulta, ser� requerido o scope 'api-sigades-consultar' (ou a anterior) no cabe�alho. 

[Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5).

### Autuar
Um Processo Administrativo passa a existir no momento de sua autua��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_autuar).

No momento da autua��o poder� ser informados quais documentos j� ser�o entranhados ao processo.

Todo Processo � autuado na Unidade onde o Papel que fez a autua��o est� lotado.

Esse endpoint envia o ato de autua��o para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do processo que foi autuado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Despachar
O Despacho � usado para movimentar o Processo Administrativo, fazendo com que o Processo mude de custodiante.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_despachar).

No momento do despacho poder� ser informados quais documentos ser�o entranhados ao processo.

Esse endpoint envia o ato de despacho para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Avocar
O ato de avocar um processo � usado para movimentar o Processo Administrativo de volta a quem o despachou previamente, fazendo com que o Processo retorne ao custodiante. � importante frisar que s� se pode avocar processos para si quando um processo despachado n�o sofreu outro ato processual pelo destinat�rio.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_avocar).

Esse endpoint envia o ato de avocamento para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Entranhar Documento
Atrav�s desse m�todo � poss�vel entranhar um Documento ao Processo sem que ele sofra uma movimenta��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_entranhar_documentos).

Esse endpoint envia o ato de entranhamento para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Desentranhar Documentos
Atrav�s desse m�todo � poss�vel desentranhar um Documento que tenha sido entranhado anteriormente ao Processo. Este ato n�o movimenta o Processo.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_desentranhar).

Importante observar que o desentranhamento n�o anula o ato que entranhou o documento, e tamb�m n�o ir� apagar completamente o hist�rico de que aquele documento foi entranhado e posteriormente desentranhado do processo, por motivos de seguran�a.

Esse endpoint envia o ato de desentranhamento para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Entranhar Encaminhamento
Atrav�s desse m�todo � poss�vel entranhar um Encaminhamento e os Documentos associados ao mesmo a um Processo sem que ele sofra uma movimenta��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_entranhar_encaminhamento).

Esse endpoint envia o ato de entranhamento para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Editar
Atrav�s desse m�todo � poss�vel editar algumas informa��es de um Processo sem que ele sofra uma movimenta��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_editar).

Esse endpoint envia o ato de edi��o para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Encerrar
Ap�s concluidos os tr�mites do Processo e tendo ele atingido o seu objetivo, encerra-se o Processo.

O Encerramento far� com que o processo seja movimentado para a Unidade que esteja vinculado ao atual custodiante.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_encerrar).

Esse endpoint envia o ato de encerramento para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Reabrir
Atrav�s desse m�todo � poss�vel reabrir um Processo previamente encerrado.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_reabrir).

Esse endpoint envia o ato de reabertura para a fila de execu��es de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador voc� pode consultar se o evento j� foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Consultar
Uma vez que os eventos tenham sido executados, os Processos e seus atos poder�o ser consultados.

A documenta��o completa pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Processos).

### Informa��es complementares para preenchimento

Abaixo as informa��es b�sicas necess�rias para o preenchimento de cadastros de Documentos:

Para buscar patriarcas, �rg�os, setores, grupos de trabalho e comiss�es, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

Para buscar planos ativos e classes ativas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-ClassificacaoDocumental).

Para buscar informa��es do usu�rio logado, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).

Clique [aqui](Consultas.md) para maiores informa��es.