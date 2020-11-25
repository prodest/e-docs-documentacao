# Sincronização do Banco de Dados x Projeto Database

O projeto **Database**, que é um projeto do tipo SQL Server Database Project, possibilita que consigamos manter uma representação da estrutura corrente do banco de dados (Esquema/Schema) dentro do nosso projeto. Este projeto permite que consigamos acompanhar o histórico de alterações do esquema, além possibilitar voltar o esquema do banco para qualquer estado anterior.
Projetos do tipo **SQL Server Database Project** nos permitem fazer uma comparação entre duas fontes de esquemas de bancos.

![Solution Explorer Bar](../../Recursos/Ferramentas/imagem1.png)

Uma vez selecionadas as duas fontes, basta solicitar que ambas sejam comparadas que o Visual Studio vai apresentar na tela uma lista com todas as difereças entre os esquemas selecionados. No exemplo abaixo, fica evidenciado adição de uma coluna **campoAdicional** na tabela **Agente**.

![Schema Compare](../../Recursos/Ferramentas/imagem2.png)

![File Diff](../../Recursos/Ferramentas/imagem3.png)

A partir deste ponto, basta que selecionar quais alterações deverão ser aplicadas. O Visual Studio permite que apliquemos as alterações de forma direta, simplesmente executando o update através do **botão update** ou gerando um **script** para posterior execução.

![File Diff](../../Recursos/Ferramentas/imagem4.png)

Por fim, vale ressaltar que a ferramenta apenas sincroniza os esquemas selecionados para comparação. Todas as alterações feitas em banco precisam ser refletidas nas entities e suas relações adicionadas ao context.