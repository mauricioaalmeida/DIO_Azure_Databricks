<h1> DESAFIO DE PROJETO: Criando Processos de Redundância de Arquivos na Azure </h1>

<p align="left">
  <img src="https://img.shields.io/static/v1?label=&message=Azure&color=blue&style=for-the-badge&logo=microsoftazure"/>
  <img src="https://img.shields.io/static/v1?label=&message=MS-SQL&color=blue&style=for-the-badge&logo=mssql"/>
  <img src="https://img.shields.io/static/v1?label=&message=dataBricks&color=blue&style=for-the-badge&logo=databricks"/>
  <img src="https://img.shields.io/static/v1?label=&message=datafactory&color=blue&style=for-the-badge&logo=datafactory"/>
  <img src="http://img.shields.io/static/v1?label=STATUS&message=CONCLUIDO&color=GREEN&style=for-the-badge"/>
</p>


Este Projeto foi realizado por Maurício André de Almeida como trabalho no curso de Microsoft AI for Tech - Azure Databricks na DIO.ME

- Para este trabalho, Criei os seguintes LinkedServices no DataFactory:
  - Azure Blob Storage (para o armazenamento no estilo Medalion: Bronze/Prata/Ouro de arquivos)
  - Azure SQL Database (Banco de dados de teste: AdventureWorks)
  - 
![LinkedServices](LinkedServices.jpg)

- Criei um Pipeline para copiar uma tabela do BD e gravar no armazenamento bronze como um arquivo do tipo Parquet

![Pipeline](Pipeline.jpg)

- Executei o Pipeline e o arquivo Parquet foi criado no Blob Storage:

![ParquetFile](ParquetFile.jpg)

# Autor

[<img loading="lazy" src="https://avatars.githubusercontent.com/u/195226841?v=4" width=115><br><sub> Mauricio Andre de Almeida</sub>](https://github.com/mauricioaalmeida) 

