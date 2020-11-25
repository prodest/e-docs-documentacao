Uma das etapas da **validação** da **assinatura digital** consiste em validar online a **cadeia do certificado**. Entretanto, por questões de boas práticas segurança, foi decidido que o servidor que terá acesso à internet deverá ficar num ambiente em que as requisições https aceitas são únicamente de saída (outbound).

O projeto encarregado de fazer esta validação avaliará se o certificado foi **revogado**, se a **cadeia de confiabilidade** é válida e se a raiz do certificado é **ICP-Brasil**. 

![endpoint](../../Recursos/Infraestrutura/endpoint.png)

O endpoint aceita como parâmetro de entrada o certificado da cada assinatura digital e retorna uma mensagem de erro em caso alguma validação falhe.