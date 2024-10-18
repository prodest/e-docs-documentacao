**[Mudanças na API do E-Docs](Guideline.md)**

Recentemente, o E-Docs passou por uma migração de infraestrutura, o que impactou diretamente a forma de integração via API.
Devido a uma mudança no padrão do serviço MinIO, a URL de envio de arquivos foi modificada.

A partir de 02/12/2024, não aceitaremos mais requisições via API para o E-Docs utilizando a infraestrutura antiga.

Para continuar a integração com o E-Docs, siga as instruções abaixo:

Se você está utilizando a API do E-Docs V1, ela será descontinuada e você deve migrar imediatamente para a V2.

Se você está utilizando a API do E-Docs V2, ela continuará ativa, porém com algumas alterações:

- A URL para solicitação de envio de documentos foi alterada para `/v2/documentos/upload-arquivo/gerar-url-upload/{tamanhoArquivo}`
- Essa nova URL possui um novo requisito, que é enviar o arquivo SEMPRE como último passo, conforme as [instruções atualizadas](Documento.md).

Caso você tenha dúvidas sobre a migração, entre em contato com o time de desenvolvimento o quanto antes.
