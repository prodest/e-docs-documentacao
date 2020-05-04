**Credenciamento de Acesso a Documentos**

Para decidir quem [Pode Ver](PodeVer.md) e [PodeUsar](PodeUsar.md) um documento, são analisadas algumas características do documento, sendo as duas principais o nível de acesso e os credenciamentos gerados. 

Abaixo, os tipos de credenciamento implementados no E-Docs

## Credenciamento Organizacional

Credencia os órgãos por onde o documento passar, para permitir o acesso aos servidores do órgão aos documentos organizacionais. Considera-se que um documento passou pelo órgão quando é:  

- capturado por um papel do órgão
- assinado por um papel do órgão
- recebido via encaminhamento ou processo por um órgão ou papel, grupo ou setor dele
- entranhado a um processo sob custódia do órgão ou papel, grupo ou setor dele
- entranhado a uma autuação feita no órgão ou setor dele
- entranhado a um despacho feito no/para órgão ou papel, grupo ou setor dele
- um termo de ato processual gerado sob custódia do órgão ou papel, grupo ou setor dele

## Credenciamento Setorial

Credencia os setores por onde o documento passar, para permitir o acesso aos servidores do setor aos documentos setoriais. Considera-se que o documento passou pelo setor quando é:

- capturado por um papel do setor
- assinado por um papel do setor
- recebido via encaminhamento ou processo por um setor ou papel/grupo dele
- entranhado a um processo sob custódia do setor ou papel/grupo dele
- entranhado a uma autuação feita no setor
- entranhado a um despacho feito no/para setor ou papel/grupo dele
- um termo de ato processual gerado sob custódia do setor ou papel/grupo dele

## Credenciamento Padrão

Credencia os agentes por onde o documento passar, para permitir o acesso aos documentos sigilosos. Também é usado para saber quem "recebeu" um documento, seja via encaminhamento ou processo. Considera-se que o documento passou pelo agente quando é:

- capturado por um papel ou cidadão, credenciando o capturador
- recebido via encaminhamento ou processo, credenciando os destinatários
- entranhado a um processo, credenciando o local onde estava o processo
- entranhado a uma autuação, credenciando o local da autuação
- entranhado a um despacho, credenciando o local onde estava e o local para onde está indo o processo
- um termo de ato processual, credenciando o local onde estava o processo

## Credenciamento Leitura

Credencia um papel ou cidadão para ter acesso a determinado documento em um determinado nível. Caso haja alteração no nível de acesso do documento, novo credenciamento leitura se faz necessário para o novo nível de acesso do documento, caso não exista. O credenciamento leitura pode ser feito das seguintes formas:

- através de solicitação para alguém que tenha acesso ao documento, caso ele não seja classificado
- através de solicitação para algum credenciador de documentos classificados em determinado nível de acesso
- através de um auto-credenciamento por parte de um auditor, para realização de suas atividades
- através de uma solicitação de acesso à peças de processo devidamente aprovada

