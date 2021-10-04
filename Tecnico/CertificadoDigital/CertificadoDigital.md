**Como gerar um certificado pfx para o E-Docs**

**Instale o openssl**  

*https://www.openssl.org/*


**Solicita��o de Assinatura de Certificado**  

Primeiramente, precisaremos gerar um arquivo de *Solicita��o de Assinatura de Certificado*. Este arquivo cont�m uma mensagem codificada (RSA) e cont�m os seguintes dados: Common Name (CN), Organization (O) , Organization Unit (OU), City (L), State (S), Country (C), Email Address e chave p�blica.

`openssl req -newkey rsa:2048 -keyout privatekey.key -out mycsr.csr`

O openssl solicitar� que o usu�rio crie uma senha (PEM Passphase). Tamb�m ser�o solicitados alguns dados que comp�em o Distinguished Name (DN), al�m de uma outra senha (Challenge Password).

![20210708Certificado](../../Recursos/CertificadoDigital/figura1.png)

Ao final deste passo, ser� criado um arquivo contendo a *Solicita��o de Assinatura de Certificado* (.csr) e um arquivo contendo a *chave privada* (.key) que faz par com a chave p�blica contida no arquivo csr.

![20210708Certificado](../../Recursos/CertificadoDigital/figura2.png)

O arquivo csr ser� solicitado como entrada por algum formul�rio da aplica��o do emissor para que um certificado no formato p7b seja gerado.

![20210708Certificado](../../Recursos/CertificadoDigital/figura3.png)
![20210708Certificado](../../Recursos/CertificadoDigital/figura4.png)

O E-Docs trabalha com certificados no formato pfx, ent�o precisamos converter o certificado de p7b para pfx. Essa convers�o � feita em dois passos, onde o primeiro passo consiste em gerar um arquivo .cer a partir do p7b.

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

A partir deste ponto ser� necess�rio baixar o certificado da Autoridade Certificadora (CA), que no nosso exemplo foi a *Serpro*. Este certificado pode ser encontrado no site da serpro sob o seguinte endere�o: �https://certificados.serpro.gov.br/serproacf/certificate-chain�. 

![20210708Certificado](../../Recursos/CertificadoDigital/figura5.png)

A figura abaixo mostra o caminho da certifica��o p7b do edocs (esquerda) e o caminho da certifica��o da Serpro (direita).

![20210708Certificado](../../Recursos/CertificadoDigital/figura6.png)

Para converter o certificado do formato .cer para um certificado no formato .pfx, basta executar o seguinte comando:

`openssl pkcs12 -export -in certificate.cer -inkey privatekey.key -out certificate.pfx -certfile cacert.cer`

No processo de convers�o ser� solicitado que se informe o PEM Passphrase, que foi definido no primeiro passo deste guia. Por fim, ser� solicitado que seja criada uma senha de exporta��o (Export Password). 

![20210708Certificado](../../Recursos/CertificadoDigital/figura7.png)

Entre os artefatos gerados neste guia, para efeito de assinatura digital de documentos, o E-docs precisa apenas do certificado pfx e sua senha de exporta��o.

