**[Integração via API](Guideline.md) - Processos**

A documentação para os métodos de Processos pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Processos).

Autuação e tramitação de Processos Administrativos seguindo a formalidade da legislação vigente.

O Processo possui um custodiante que pode ser:
- Uma Organização (Órgão), neste caso o responsável pela organização poderá realizar os atos processuais, podendo delegar tais competências.
- Uma Unidade (setor), neste caso o responsável pela unidade poderá realizar os atos processuais, podendo delegar tais competências.
- Um Grupo, neste caso todos os membros do Grupo poderão realizar os atos processuais.
- Um Papel (servidor público ocupando um cargo ou função), neste caso somente o detentor do Papel poderá realizar os atos processuais.

Para realizar os Atos Autuar, Despachar, Avocar, Entranhar Documentos, Desentranhar Documentos, Entranhar Encaminhamentos, Editar, Encerrar e Reabrir é necesário que o usuário possua pelo menos um papel no Acesso Cidadão, e este papel deve possuir uma lotação.
Usuários que são servidores do Governo do Estado do Espírito Santo já possuem seus papeis atribuídos através da integração com o sistema SIARHES, bem como sua lotação.
Caso seja necessário atribuir um papel a um terceiro, o administrador do sistema que está se integrando poderá fazer isso diretamente no Acesso Cidadão, neste caso também é necessário informar a lotação do papel do terceiro.

**Ações disponíveis:**
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

### Autenticação no E-Docs

A autenticação será através do padrão **Bearer Token**, utilizando o Access Token obtido através da **Autenticação de Usuário** no Acesso Cidadão. 

- Para as requisições aos endpoints de Atos Processuais será requerido o scope 'api-sigades-processo' no cabeçalho;
- Para as requisições de consulta, será requerido o scope 'api-sigades-consultar' (ou a anterior) no cabeçalho. 

[Especificação de uso do Bearer Token](https://tools.ietf.org/html/rfc6750#page-5).

### Autuar
Um Processo Administrativo passa a existir no momento de sua autuação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_autuar).

No momento da autuação poderá ser informados quais documentos já serão entranhados ao processo.

Todo Processo é autuado na Unidade onde o Papel que fez a autuação está lotado.

Esse endpoint envia o ato de autuação para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do processo que foi autuado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Despachar
O Despacho é usado para movimentar o Processo Administrativo, fazendo com que o Processo mude de custodiante.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_despachar).

No momento do despacho poderá ser informados quais documentos serão entranhados ao processo.

Esse endpoint envia o ato de despacho para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Avocar
O ato de avocar um processo é usado para movimentar o Processo Administrativo de volta a quem o despachou previamente, fazendo com que o Processo retorne ao custodiante. É importante frisar que só se pode avocar processos para si quando um processo despachado não sofreu outro ato processual pelo destinatário.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_avocar).

Esse endpoint envia o ato de avocamento para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Entranhar Documento
Através desse método é possível entranhar um Documento ao Processo sem que ele sofra uma movimentação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_entranhar_documentos).

Esse endpoint envia o ato de entranhamento para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Desentranhar Documentos
Através desse método é possível desentranhar um Documento que tenha sido entranhado anteriormente ao Processo. Este ato não movimenta o Processo.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_desentranhar).

Importante observar que o desentranhamento não anula o ato que entranhou o documento, e também não irá apagar completamente o histórico de que aquele documento foi entranhado e posteriormente desentranhado do processo, por motivos de segurança.

Esse endpoint envia o ato de desentranhamento para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Entranhar Encaminhamento
Através desse método é possível entranhar um Encaminhamento e os Documentos associados ao mesmo a um Processo sem que ele sofra uma movimentação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_entranhar_encaminhamento).

Esse endpoint envia o ato de entranhamento para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Editar
Através desse método é possível editar algumas informações de um Processo sem que ele sofra uma movimentação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_editar).

Esse endpoint envia o ato de edição para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Encerrar
Após concluidos os trâmites do Processo e tendo ele atingido o seu objetivo, encerra-se o Processo.

O Encerramento fará com que o processo seja movimentado para a Unidade que esteja vinculado ao atual custodiante.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_encerrar).

Esse endpoint envia o ato de encerramento para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Reabrir
Através desse método é possível reabrir um Processo previamente encerrado.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Processos-post_v2_processos_reabrir).

Esse endpoint envia o ato de reabertura para a fila de execuções de eventos do E-Docs, retornando o identificador do evento de ato que foi enfileirado.

Com a posse desse identificador você pode consultar se o evento já foi executado, retornando o identificador do ato que foi realizado, conforme o end point descrito [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-Eventos-get_v2_eventos__idEvento_).

### Consultar
Uma vez que os eventos tenham sido executados, os Processos e seus atos poderão ser consultados.

A documentação completa pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Processos).

### Informações complementares para preenchimento

Abaixo as informações básicas necessárias para o preenchimento de cadastros de Documentos:

Para buscar patriarcas, órgãos, setores, grupos de trabalho e comissões, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Agente).

Para buscar planos ativos e classes ativas, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-ClassificacaoDocumental).

Para buscar informações do usuário logado, utilize [esses endpoints](https://api.e-docs.es.gov.br/swagger/index.html?urls.primaryName=V2.0#operations-tag-Usuario).

Clique [aqui](Consultas.md) para maiores informações.