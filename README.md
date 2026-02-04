# dio-lab-microsoft-platform
# Azure Serverless Rent Car 🚗☁️

Este projeto é uma **Azure Function** desenvolvida em .NET 8 (Isolated Worker) responsável por processar solicitações de aluguel de carros de forma assíncrona e escalável. A função é acionada por mensagens em uma fila do **Azure Service Bus** e persiste os dados em um banco de dados **Azure SQL**.

## 📋 Funcionalidades

- **Processamento Assíncrono:** Recebe mensagens da fila `fila-locacao-auto` via *Service Bus Trigger*.
- **Validação de Dados:** Desserializa o payload JSON e valida a estrutura da solicitação de aluguel.
- **Persistência:** Conecta-se a um Banco de Dados SQL e insere os registros na tabela de locações.
- **Tratamento de Erros:** Envia mensagens mal formatadas para a *Dead Letter Queue* para análise posterior.

## 🚀 Tecnologias Utilizadas

* **C# / .NET 8.0**
* **Azure Functions** (Worker Process Isolado)
* **Azure Service Bus** (Mensageria)
* **Azure SQL Database** (Armazenamento Relacional)
* **ADO.NET** (`Microsoft.Data.SqlClient`) para conexão direta e eficiente com o banco.

## 🏗️ Arquitetura da Solução

O fluxo de dados segue o seguinte padrão:
1.  Uma aplicação externa (Front-end ou API) envia um JSON para a fila no Service Bus.
2.  A **Azure Function** detecta a nova mensagem e inicia o processamento.
3.  Os dados são gravados na tabela `Locacao` do banco de dados SQL.

## ⚙️ Configuração Local

Para rodar este projeto localmente, você precisará configurar o arquivo `local.settings.json` na raiz do projeto com as suas strings de conexão:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated",
    "ServiceBusConnection": "SUA_CONNECTION_STRING_DO_SERVICE_BUS",
    "SqlConnectionString": "SUA_CONNECTION_STRING_DO_SQL_SERVER"
  }
}
