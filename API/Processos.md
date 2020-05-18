**Integração via API - Processos**

Autuação e tramitação de Processos Administrativos seguindo a formalidade da legislação vigente.

O Processo possui um custodiante que pode ser:
- Uma Organiação (Órgão), neste caso o responsável pela organização poderá realizar os atos processuais, podendo delegar tais competências.
- Uma Unidade (setor), neste caso o responsável pela unidade poderá realizar os atos processuais, podendo delegar tais competências.
- Um Grupo, neste caso todos os membros do Grupo poderão realizar os atos processuais.
- Um Papel (servidor púbico ocupando um cargo ou função), neste caso somente o detentor do Papel poderá realizar os atos processuais.

**Ações disponíveis:**
- [Autuar](#Autuar)
- [Despachar](#Despachar)
- [Entranhar Documentos](#Entranhar Documentos)
- [Desentranhar Documentos](#desentranhar-documentos)
- [Encerrar](#Encerrar)
- [Consultar](#Consultar)

##**Autuar**
Um Processo Administrativo passa a existir no momento de sua autuação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Autuar).

No momento da autuação poderá ser informados quais documentos já serão entranhados ao processo.

Todo Processo é autuado na Unidade onde o Papel que fez a autuação está lotado.

**#Despachar**
O Despacho é usado para movimentar o Processo Administrativo, fazendo com que o Processo mude de custodiante.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Despachar).

No momento do despacho poderá ser informados quais documentos serão entranhados ao processo.

**Entranhar Documento**
Através desse método é possível entranhar um Documento ao Processo sem que ele sofra uma movimentação.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Entranhar).

##**Desentranhar Documentos**
Através desse método é possível desentranhar um Documento que tenha sido entranhado anteriormente ao Processo. Este ato não movimenta o Processo.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Desentranhar).

[**Encerrar**]
Após concluidos os tramites do Processo e tendo ele atingido o seu objetivo, encerra-se o Processo.

O Encerramento fará com que o processo seja movimentado para a Unidade que esteja vinculado ao atual custodiante.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Processos/Processos_Encerrar).

