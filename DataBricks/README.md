<h1> Curso DIO: Microsoft AI for Tech - Azure Databricks </h1>

<p align="left">
  <img src="https://img.shields.io/static/v1?label=&message=Azure&color=blue&style=for-the-badge&logo=microsoftazure"/>
  <img src="https://img.shields.io/static/v1?label=&message=MS-SQL&color=blue&style=for-the-badge&logo=mssql"/>
  <img src="https://img.shields.io/static/v1?label=&message=dataBricks&color=blue&style=for-the-badge&logo=databricks"/>
  <img src="https://img.shields.io/static/v1?label=&message=datafactory&color=blue&style=for-the-badge&logo=datafactory"/>
  <img src="http://img.shields.io/static/v1?label=STATUS&message=CONCLUIDO&color=GREEN&style=for-the-badge"/>
</p>


📚 Arquitetura de Dados End-to-End no Microsoft Azure utilizando Azure Data Fabric e Azure DataBricks

Este repositório contém a documentação e os artefatos necessários para implementar uma solução completa de engenharia de dados utilizando os serviços da plataforma Microsoft Azure. 

🎯 Objetivo 

Criar um pipeline de dados desde a extração de dados de um banco SQL até a transformação e armazenamento em diferentes camadas (bronze, prata e ouro), usando os seguintes componentes: 

    Azure SQL Database
    Azure Data Lake Storage Gen2
    Azure Data Factory
    Azure Databricks


     
🧩 Arquitetura Geral 
 
 
[Fonte de Dados] → [Azure SQL DB]
        ↓
[Azure Data Factory] → [Data Lake (Staging / Bronze)]
        ↓
[Azure Databricks] → Transformações (Bronze → Prata → Ouro)
 
 
 
🛠️ Passo a Passo da Implementação 
1. Criar Conta no Azure 

    Acesse https://azure.microsoft.com   e crie uma conta gratuita ou use sua assinatura corporativa.
    Após login, acesse o portal do Azure: https://portal.azure.com 
     

2. Criar Banco de Dados SQL 

    No portal do Azure, clique em Criar um recurso .
    Procure por Banco de Dados SQL .
    Preencha as informações:
        Nome do banco de dados
        Grupo de recursos
        Servidor (crie um novo ou selecione existente)
        Configure firewall para permitir acesso ao IP atual
         
    Após criar, importe seus dados ou conecte fontes externas.
     

    💡 Use scripts SQL ou ferramentas como SSMS ou Azure Data Studio para popular seu banco. 
     

3. Criar Projeto no Azure DevOps 

    Acesse https://dev.azure.com . 
    Crie uma nova organização (se necessário).
    Crie um novo projeto:
        Nome do projeto
        Visibilidade pública ou privada
         
    Dentro do projeto:
        Crie um repositório Git (ou vincule um repositório do GitHub)
        Adicione este README e outros arquivos do projeto
         
     

4. Criar Azure Data Lake Storage Gen2 

    No portal do Azure, clique em Criar um recurso .
    Procure por Conta de Armazenamento .
    Escolha Armazenamento v2 (finalidade geral v2) .
    Ative a opção Hierarchical namespace  para ativar o Data Lake Gen2.
    Após criar, acesse a conta de armazenamento:
        Navegue até Contêineres de blob 
        Crie os seguintes contêineres:
            staging (dados temporários)
            bronze (dados brutos)
            prata (dados limpos)
            ouro (dados agregados)
             
         
     

5. Criar Instância do Azure Data Factory 

    No portal do Azure, clique em Criar um recurso .
    Procure por Data Factory .
    Selecione Data Factory  e preencha:
        Nome exclusivo
        Grupo de recursos
        Localização
         
    Após criado, abra o Data Factory no portal.
    Habilite o Git  para versionamento (opcional mas recomendado).
     

6. Criar Instância do Azure Databricks 

    No portal do Azure, clique em Criar um recurso .
    Procure por Azure Databricks .
    Escolha Workspace .
    Preencha:
        Região
        Plano de preço (Standard ou Premium)
        Vincule ao grupo de recursos
         
    Após criar, acesse o workspace do Databricks:
        Crie clusters (SingleNode ou Standard)
        Configure notebooks e bibliotecas conforme necessário
         
     

7. Conectar Linked Services no Azure Data Factory 

No Azure Data Factory: 
a. Conectar Azure SQL Database 

    Abra o Data Factory Studio.
    Em Gerenciar > Linked Services , adicione:
        Tipo: Azure SQL Database 
        Preencha:
            Método de autenticação
            Credenciais (usando segredos do Key Vault é recomendado)
            Teste a conexão
             
         
     

b. Conectar Azure Data Lake Storage Gen2 

    Em Linked Services , adicione:
        Tipo: Azure Blob Storage  ou Azure Data Lake Storage Gen2 
        Forneça a chave de acesso ou use Managed Identity
        Teste a conexão
         
     

8. Elaborar Pipeline para Extração de Tabelas no SQL e Gravar como Parquet no Data Lake 

    No Data Factory, crie um novo pipeline.
    Adicione uma atividade Copy Data :
        Fonte: Tabela SQL (selecionada ou dinâmica)
        Destino: Data Lake Storage (contêiner staging)
        Formato: Parquet 
         
    Configure mapeamentos e configurações adicionais conforme necessário.
    Execute/teste o pipeline e valide os dados no contêiner staging.
     

9. Conectar Data Lake no Azure Databricks 

    No Azure Databricks, acesse o workspace.
    Crie um notebook Python ou Scala.
    Configure o acesso ao Data Lake:
     

 

    Leitura de dados:
     
df = spark.read.parquet("abfss://bronze@<storage-account>.dfs.core.windows.net/tabela")
 
 
 
10. Criar Notebooks para Transformação (Bronze, Prata e Ouro) 
Notebook 1: Bronze → Prata 

    Leitura de dados do contêiner bronze
    Limpeza, validação, tratamento de nulos
    Salvamento no contêiner prata como Parquet
     

Notebook 2: Prata → Ouro 

    Agregações, joins, modelagem dimensional
    Salvamento no contêiner ouro como Parquet ou Delta Lake
     

📁 Estrutura Recomendada do Repositório 
 
repo/
│
├── README.md                   # Este arquivo
├── pipelines/                  # JSONs dos pipelines do Data Factory
├── notebooks/                  # Notebooks exportados do Databricks
├── sql-scripts/                # Scripts de criação e inserção no SQL
├── templates/                  # Templates ARM ou Bicep (opcional)
├── devops-pipelines/           # YAML do Azure Pipelines
└── docs/                       # Documentação adicional
 
 
 
🔐 Boas Práticas de Segurança 

    Utilize Managed Identities  entre serviços.
    Armazene segredos no Azure Key Vault .
    Controle de acesso via RBAC  nos recursos do Azure.
    Versione apenas código e configurações não sensíveis.
     

🔄 CI/CD com Azure DevOps 

Você pode configurar pipelines de CI/CD para: 

    Automatizar deploy de pipelines do Data Factory
    Publicar notebooks no Databricks
    Validar integridade dos dados
     

Verifique a pasta devops-pipelines/ para exemplos de pipelines YAML. 
🧪 Validação Final 

    Execute o pipeline completo no Azure Data Factory.
    Confirme que os dados foram salvos corretamente no Data Lake.
    Valide as transformações no Databricks.
    Consulte os dados finais no contêiner ouro.
     

📞 Suporte 

Para dúvidas ou contribuições, abra uma issue ou envie um pull request. 

    ✅ Desenvolvido por Maurício André de Almeida como trabalho no curso de Microsoft AI for Tech - Azure Databricks na DIO.ME
    📅 Última atualização: Abril de 2025 


# Autor

[<img loading="lazy" src="https://avatars.githubusercontent.com/u/195226841?v=4" width=115><br><sub> Mauricio Andre de Almeida</sub>](https://github.com/mauricioaalmeida) 
