**Integração via API - Guideline**

O Sistema E-Docs faz integração com os seguintes sistemas:
-[Acesso Cidadão](https://acessocidadao.es.gov.br)
O Acesso Cidadão é utilizado para tratar as autenticações e autorizações dos usuários.

O Acesso Cidadão possui sua API publicada em [aqui](https://sistemas.es.gov.br/prodest/acessocidadao.webapi/swagger).

-[Organograma](https://organograma.es.gov.br)
O Organograma é utilizado para consultar os Órgãos e Setores nele cadastrados.
Atualmente o Organograma possui uma integração com o sistema de Recursos Humanos do Governo do Estado do Espírito Santo, onde toda alteração referente a órgão e setor realizada lá é refletida no Orgranograma.

O Organograma possui sua API publicada em [aqui](https://api.organograma.es.gov.br).

**Step by step:**
- Adicionar um sistema no Acesso Cidadão
-   Adicionar um App com o fluxo Hybrid, as propriedades destes App serão necessárias para configurar a autenticação dos usuários.
- ...