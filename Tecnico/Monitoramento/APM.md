**APM**

Para monitoramento do desempenho da aplicação, utilizamos o APM Elastic Search.

Há uma instância só para dados de monitoramento, e eles estão guardados por 7 dias para consultas e comparações.

Atualmente, usamos a seguinte configuração:

```
  "Logging": {
    "IncludeScopes": false,
    "LogLevel": {
      "Default": "Warning",
      "Elastic.Apm": "Warning"
    }
  },
  "ElasticApm": {
    "ServerUrls": "host:porta",
    "TransactionSampleRate": 1.0
  },
```

Com ela, todos os requests são salvos para monitoramento e análise, sendo possível, dentro do período de 7 dias, avaliar qualquer requisição ou transação* feita dentro do E-Docs, em qualquer um de seus módulos.

Por padrão, o APM para .NET Core monitora todas as requisições realizadas ao MVC, criando a chamada TRANSACTION.

Caso seja necessário destacar, dentro de uma TRANSACTION, algum trecho específico, é possível criar um SPAN a partir de uma TRANSACTION existente.

Também é possível CRIAR uma nova TRANSACTION independente de um request para monitorar pontos específicos do sistema, ou mesmo para códigos internos executados a partir do Hangfire ou outra ferramenta de mensagem como o Redis.

A documentação completa do APM pode ser consultada diretamente no [site da Elastic](https://www.elastic.co/guide/en/apm/agent/dotnet/1.x/intro.html)