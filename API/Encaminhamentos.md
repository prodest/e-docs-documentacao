**Integração via API - Encaminhamentos**

O Encaminhamento é a forma de Documentos tramitarem sem estarem entranhados a um processo, de forma avulsa.

**Ações disponíveis:**
- [Encmainhar](#encaminhar)
- Inserir um novo Encaminhamento
- [Consultar](#consultar)
- Consultar os Encaminhamentos

## Encaminhar
Um Encaminhamento pode ser inserido sem referenciar um Encaminhamento Anterior, neste caso ele será o raiz.

Um Encaminhamento pode ser inserido referenciando um Encaminhamento Anterior, conforme descrito abaixo:
- Complementar, quando remetente deseja complementar com alguma informação o Encaminhamento que foi feito anteriormente
- Responder, quando o destinatário deseja responder ao rementente do Encaminhamento Anterior
- Reencaminhar, quando o destinatário deseja encaminhar o Encaminhamento Anterior para um outro destinatário

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Encaminhamentos/Encaminhamentos_Post).

### Consultar
Após um Encaminhamento ser inserido ele poderá ser consultado.

A documentação deste método pode ser vista [aqui](https://api.e-docs.es.gov.br/swagger/index.html#/Encaminhamentos/Encaminhamentos_Get).