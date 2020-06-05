**Processo Administrativo**

Processo administrativo é a sequência de atividades da Administração, interligadas entre si, que visa a alcançar determinado efeito final previsto em lei. Trata-se do modo como a Administração Pública toma suas decisões, seja por iniciativa de um particular, seja por iniciativa própria.

No Brasil, a Lei que trata das diretrizes gerais do procedimento administrativo é a Lei n.º 9.784 de 1999, a qual se aplica a todos entes da Administração Pública direta e indireta federais. Além disso, o STJ tem reconhecido a aplicação desta lei federal para entes estaduais e municipais que ainda não aprovaram leis próprias.


Um processo é identificado no E-Docs pelo seu **Protocolo**, uma sequencia de letras e números única no formato AAAA-XXXXX, onde os 4 caracteres antes do traço constituem o Ano de sua autuação, e os cinco caracteres após o traço são uma combinação aleatória em **Base 30** (algarismos e/ou letras consoantes - vogais são excluídas. Como existem 10 algarismos e 20 consoantes, temos 30 caracteres distintos à disposição, por isso o nome). Exemplo: 2020-F4X3T


Compõem os **Metadados** de um processo suas informações básicas:
* Resumo - o título do processo
* Classe - a classificação documental do processo. Usada para categorização e definição de prazos de guarda e descarte.
* Interessados - pessoas físicas ou jurídicas que tenham interesse direto no teor do processo, ou que possam ser afetados por decisões tomadas durante seu curso.

A **Tramitação** de um Processo pode ser feita entre Agentes dos tipos Órgão, Unidade, Grupo e Servidor. Entende-se por **Custódia** a posse de um processo por um agente em determinado momento. Apenas o agente que possui a custódia do processo tem a prerrogativa de realizar vários atos processuais, como entranhar novas peças, despachar para outros agentes, encerrar o processo, entre outros. Os processos sob sua custódia podem ser consultados na **Caixa de Entrada de Processos**, em uma das caixas onde você tem acesso.

Tanto os metadados de um processo quanto as informações a respeito de sua tramitação são **Públicos**, e acessíveis a qualquer usuário logado no sistema E-Docs. Já o teor dos documentos que compõem o processo podem ter diferentes níveis de acesso, que determinam quem pode os ler.


Processos são organizados em **Atos Processuais**. Os atos são as realizações de procedimentos praticados no andamento do processo. Basicamente, tudo que se pode fazer em um processo é através de um Ato. Os Atos existentes no E-Docs são:

* **Autuação** - o início de um processo, informando os metadados.
* **Edição** - alteração dos metadados inseridos na autuação.
* **Despacho** - o envio do processo para outro Agente, de forma que o processo siga seu curso.
* **Entranhamento** - a inclusão de documentos no processo. Nesta inclusão, o documento passa a ser chamado **Peça Processual**, e recebe um número Sequencial único e incremental dentro do Processo, de forma a identifica-lo dentro do mesmo.
* **Desentranhamento** - a retirada lógica de peças do processo, seja por inclusão equivocada, seja por expiração de sua validade.
* **Avocamento** - puxa de volta um processo já despachado por um Agente, desde que quem tenha sua custódia ainda não tenha feito nenhum outro ato.
* **Encerramento** - determina o fim da tramitação do processo. Até este momento, o processo é dito como *Em Andamento*, podendo tramitar onde for necessário. Ao ser encerrado, o processo fica na área de processos encerrados do setor onde ocorreu o encerramento.
* **Reabertura** - a reabertura volta o processo para Em Andamento, permitindo sua tramitação novamente.
* **Ajuste de Custódia** - ato especial, de acesso restrito, usado para mover processos presos em caixas inativas para um novo destino, de forma que o processo possa voltar a ser tramitado.

Todo ato processual gera um documento especial, chamado **Termo**, contendo as informações do ato realizado em si. O termo é capturado automaticamente ao se executar o ato; ele é nato-digital, tem valor original, e é assinado eletronicamente pelo usuário responsável pela ação. Os Termos de Autuação e Edição contém apenas metadados, e portanto são sempre públicos. Já os termos dos demais atos possuem informações adicionais, oriundas de campos obrigatórios ao se realizar o ato, e o conteúdo destas informações pode ou não requerer sigilo. Por padrão, se nenhum fundamento legal for informado, os demais termos possuem nível de acesso Organizacional.
