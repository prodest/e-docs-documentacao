**Integração via API - Guideline**

Os métodos disponíveis para utilização via api podem ser consultados [aqui](https://api.e-docs.es.gov.br/swagger).

O ambiente de Treinamento deve ser utilizado para os testes.
[E-Docs Web - Treinamento](https://treinamento.e-docs.es.gov.br)
[E-Docs Api - Treinamento](https://api.treinamento.e-docs.es.gov.br/)

O Sistema E-Docs faz integração com os seguintes sistemas:

- [Acesso Cidadão](https://acessocidadao.es.gov.br)

O Acesso Cidadão é utilizado para tratar as autenticações e autorizações dos usuários.

O Acesso Cidadão possui sua API publicada em [aqui](https://sistemas.es.gov.br/prodest/acessocidadao.webapi/swagger).

- [Organograma](https://organograma.es.gov.br)

O Organograma é utilizado para consultar os Órgãos e Setores nele cadastrados.
Atualmente o Organograma possui uma integração com o sistema de Recursos Humanos do Governo do Estado do Espírito Santo, onde toda alteração referente a órgão e setor realizada lá é refletida no Orgranograma.

O Organograma possui sua API publicada em [aqui](https://api.organograma.es.gov.br).



Antes de utilizar a API do E-Docs ou do Organograma, você deve [solicitar acesso](SolicitarAcesso.md) para sua aplicação.




**Primeiros passos:**
- Adicionar um sistema no Acesso Cidadão
  - Adicionar um App com o fluxo Hybrid, as propriedades destes App serão necessárias para configurar a autenticação dos usuários para que ele possa realizar as operações no E-Docs.
  - Adicionar um App com o fluxo ClientCredentials, as propriedades destes App serão necessárias para que o sistema faça consultas em outros sistemas, por exemplo o organograma.
  - Pode ser que seja necessário utilizar métodos que estão disponibilizados via [Api](https://sistemas.es.gov.br/prodest/acessocidadao.webapi/swagger) do Acesso Cidadão.
- Caso seja necessário obter informações do Organograma será necessário acrescentar o scope api-organograma ao App de fluxo ClientCredentials que foi criado no Acesso Cidadão.


**Principais ações do E-Docs**
- [Documentos](Documentos.md)
  - Capturar
- [Encaminhamentos](Encaminhamentos.md)
  - Adicionar
- [Processos](Processos.md)
  - Autuar
  - Despachar
  - Entranhar Documentos
  - Desentranhar Documentos
  - Encerrar