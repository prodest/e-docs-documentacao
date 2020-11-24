# Solution Visual Studio

A solution do E-Docs no Visual Studio chama-se **ClassificacaoDocumental.sln** (um resquício do passado). Abaixo listamos os projetos agrupados pelo seu tipo:



### E-Docs Front-End

**Web** - contém tudo relacionado à interface (cshtml, css, js, imagens, etc). Também contém os Controllers MVC que fazem a rota das requisições.

**Presentation** - contém as classes Service, que chamam o back-end e preparam os dados para a interface, bem como as ViewModels que carregam os dados.

***Web.Configuration*** - projeto satélite que abriga classes de configuração usadas no Startup.cs do projeto Web.



### **E-Docs Back-End**

**Business** - contém toda a lógica de negócio do E-Docs, armazenadas nas classes Core. A modelagem de objetos de negócio é agnóstica, em classes com sufixo Model.

**Infrastructure** - fornece os alicerces do sistema. Armazena a modelagem ORM, implementa repositórios para acesso às diferentes fontes de dados (banco de dados, Elastic Search) e encapsula integrações com outros sistemas (Acesso Cidadão, Organograma, Notificações, etc)

***Cache*** - projeto satélite que possui a implementação do HierarchicalCache, uma classe que abstrai o uso de cache local (com MemoryCache) e de cache distribuído (Redis).

***Dependency*** - projeto satélite que possui toda a configuração de injeção de dependências do sistema.

***Monitoring*** - projeto satélite que possui lógica de coleta de informações de uso de memória e data de start dos servidores do E-Docs.



### **E-Docs API**

**Web.Api** - contém os endpoints de integração do E-Docs para outros sistemas



### **Processamento**

**BackgroundJobs** - implementa o servidor de processamento de tarefas do sistema, usando Hangfire. Executa tarefas imediatamente em segundo (indexar processo, credenciar documentos), e também tarefas agendadas em horário pre-determinado.

**ProcessJobs** - implementa o servidor de enfileiramento de eventos do sistema. Todas as principais funções do E-Docs (captura, encaminhamento, atos processuais) são processadas aqui.



### **Projetos Suporte**

**DocumentModels** - implementa o servidor de modelos de documentos do sistema. Recebe dados em formato json e retorna um documento em HTML, com formação e imagens auto-contidas, pronto para ser convertido em PDF.



### **Utilitários**

**Database** - projeto de apoio que contém todos os scripts de criação de elementos de banco de dados (tabelas, FK's, indices). Útil para uma eventual criação de uma base do zero. A cada mudança no banco, os arquivos referentes sofrem alteração se necessário. Importante: este projeto NÃO armazena os eventuais scripts incrementais da versão.



#### **Testes**

Tests

UnitTestBusiness

XUnit.TestInfrastructure
