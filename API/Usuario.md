**[Integra��o via API](Guideline.md) - Processos**

Autua��o e tramita��o de Processos Administrativos seguindo a formalidade da legisla��o vigente.

O Processo possui um custodiante que pode ser:
- Uma Organia��o (�rg�o), neste caso o respons�vel pela organiza��o poder� realizar os atos processuais, podendo delegar tais compet�ncias.
- Uma Unidade (setor), neste caso o respons�vel pela unidade poder� realizar os atos processuais, podendo delegar tais compet�ncias.
- Um Grupo, neste caso todos os membros do Grupo poder�o realizar os atos processuais.
- Um Papel (servidor p�bico ocupando um cargo ou fun��o), neste caso somente o detentor do Papel poder� realizar os atos processuais.

Para realizar os Atos Autuar, Despachar, Entranhar Documentos, Desentranhar Documentos e Encerrar � neces�rio que o usu�rio possua pelo menos um papel no Acesso Cidad�o, e este papel deve possuir uma lota��o.
Usu�rios que s�o servidores do Governo do Estado do Esp�rito Santo j� possuem seus papeis atibu�dos atrav�s da integra��o com o sistema SIARHES, bem como sua lota��o.
Caso seja necess�rio atribuir um papel a um terceiro, o administrador do sistema que est� se integrando poder� fazer isso diretamente no Acesso Cidad�o, neste caso tamb�m � necess�rio informar a lota��o do papel do terceiro.

**A��es dispon�veis:**
- [Autuar](#autuar)
- [Despachar](#despachar)
- [Entranhar Documentos](#entranhar-documentos)
- [Desentranhar Documentos](#desentranhar-documentos)
- [Encerrar](#encerrar)
- [Consultar](#consultar)

### Autuar
Um Processo Administrativo passa a existir no momento de sua autua��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Autuar).

O Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o utilizando o scope 'api-sigades-processo' � requerido no cabe�alho das requisi��es ao endpoint de Autua��o usando o padr�o Bearer Token. [Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

No momento da autua��o poder� ser informados quais documentos j� ser�o entranhados ao processo.

Todo Processo � autuado na Unidade onde o Papel que fez a autua��o est� lotado.

### Despachar
O Despacho � usado para movimentar o Processo Administrativo, fazendo com que o Processo mude de custodiante.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Despachar).

O Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o utilizando o scope 'api-sigades-processo' � requerido no cabe�alho das requisi��es ao endpoint de Despacho usando o padr�o Bearer Token. [Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

No momento do despacho poder� ser informados quais documentos ser�o entranhados ao processo.

### Entranhar Documento
Atrav�s desse m�todo � poss�vel entranhar um Documento ao Processo sem que ele sofra uma movimenta��o.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Entranhar).

O Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o utilizando o scope 'api-sigades-processo' � requerido no cabe�alho das requisi��es ao endpoint de Entranhamento de Documento usando o padr�o Bearer Token. [Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Desentranhar Documentos
Atrav�s desse m�todo � poss�vel desentranhar um Documento que tenha sido entranhado anteriormente ao Processo. Este ato n�o movimenta o Processo.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Desentranhar).

O Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o utilizando o scope 'api-sigades-processo' � requerido no cabe�alho das requisi��es ao endpoint de Desentranhamento de Documento usando o padr�o Bearer Token. [Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Encerrar
Ap�s concluidos os tramites do Processo e tendo ele atingido o seu objetivo, encerra-se o Processo.

O Encerramento far� com que o processo seja movimentado para a Unidade que esteja vinculado ao atual custodiante.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Encerrar).

O Access Token obtido atrav�s da **Autentica��o de Usu�rio** no Acesso Cidad�o utilizando o scope 'api-sigades-processo' � requerido no cabe�alho das requisi��es ao endpoint de Encerramento usando o padr�o Bearer Token. [Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Consultar
Os Processos poder�o ser consultados.

A documenta��o deste m�todo pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Get).

O Access Token obtido atrav�s da autentica��o no Acesso Cidad�o utilizando o scope 'api-sigades-consultar' ou 'api-sigades-processo' � requerido no cabe�alho das requisi��es aos endpoints de Consulta usando o padr�o Bearer Token. [Especifica��o de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)