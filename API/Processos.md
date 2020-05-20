**[Integração via API](Guideline.md) - Processos**

Autuação e tramitação de Processos Administrativos seguindo a formalidade da legislação vigente.

O Processo possui um custodiante que pode ser:
- Uma Organiação (Órgão), neste caso o responsável pela organização poderá realizar os atos processuais, podendo delegar tais competências.
- Uma Unidade (setor), neste caso o responsável pela unidade poderá realizar os atos processuais, podendo delegar tais competências.
- Um Grupo, neste caso todos os membros do Grupo poderão realizar os atos processuais.
- Um Papel (servidor púbico ocupando um cargo ou função), neste caso somente o detentor do Papel poderá realizar os atos processuais.

Para realizar os Atos Autuar, Despachar, Entranhar Documentos, Desentranhar Documentos e Encerrar é necesário que o usuário possua pelo menos um papel no Acesso Cidadão, e este papel deve possuir uma lotação.
Usuários que são servidores do Governo do Estado do Espírito Santo já possuem seus papeis atibuídos através da integração com o sistema SIARHES, bem como sua lotação.
Caso seja necessário atribuir um papel a um terceiro, o administrador do sistema que está se integrando poderá fazer isso diretamente no Acesso Cidadão, neste caso também é necessário informar a lotação do papel do terceiro.

**Ações disponíveis:**
- [Autuar](#autuar)
- [Despachar](#despachar)
- [Entranhar Documentos](#entranhar-documentos)
- [Desentranhar Documentos](#desentranhar-documentos)
- [Encerrar](#encerrar)
- [Consultar](#consultar)

### Autuar
Um Processo Administrativo passa a existir no momento de sua autuação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Autuar).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-processo' é requerido no cabeçalho das requisições ao endpoint de Autuação usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

No momento da autuação poderá ser informados quais documentos já serão entranhados ao processo.

Todo Processo é autuado na Unidade onde o Papel que fez a autuação está lotado.

### Despachar
O Despacho é usado para movimentar o Processo Administrativo, fazendo com que o Processo mude de custodiante.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Despachar).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-processo' é requerido no cabeçalho das requisições ao endpoint de Despacho usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

No momento do despacho poderá ser informados quais documentos serão entranhados ao processo.

### Entranhar Documento
Através desse método é possível entranhar um Documento ao Processo sem que ele sofra uma movimentação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Entranhar).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-processo' é requerido no cabeçalho das requisições ao endpoint de Entranhamento de Documento usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Desentranhar Documentos
Através desse método é possível desentranhar um Documento que tenha sido entranhado anteriormente ao Processo. Este ato não movimenta o Processo.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Desentranhar).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-processo' é requerido no cabeçalho das requisições ao endpoint de Desentranhamento de Documento usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Encerrar
Após concluidos os tramites do Processo e tendo ele atingido o seu objetivo, encerra-se o Processo.

O Encerramento fará com que o processo seja movimentado para a Unidade que esteja vinculado ao atual custodiante.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Encerrar).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-processo' é requerido no cabeçalho das requisições ao endpoint de Encerramento usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)

### Consultar
Os Processos poderão ser consultados.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Get).

O Access Token obtido através da autenticação no Acesso Cidadão utilizando o scope 'api-sigades-consultar' ou 'api-sigades-processo' é requerido no cabeçalho das requisições aos endpoints de Consulta usando o padrão Bearer Token. [Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5)