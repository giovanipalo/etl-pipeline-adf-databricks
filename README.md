# Pipeline de ETL com Azure Data Factory e Databricks

Este projeto implementa um pipeline de ETL (Extract, Transform, Load) utilizando Azure Data Factory para orquestração e Azure Databricks para transformação dos dados. Os dados são coletados de uma fonte web pública, processados em camadas (bronze, silver, gold) e preparados para visualização analítica.

## Estrutura do Projeto

etl-pipeline-adf-databricks/
├── adf/
│ ├── datasets/ # Definições de datasets (entrada e saída)
│ ├── linkedServices/ # Conexões com fontes e destinos (Web, ADLS, etc.)
│ ├── pipelines/ # Pipelines do ADF para orquestração do ETL
│ ├── triggers/ # (Vazio) Reservado para gatilhos agendados
│ ├── publish_config.json # Configuração de publicação do ADF
│ └── etl-prod-eastus-adf.json # Metadados da instância do Data Factory
│
├── databricks/
│ └── notebooks/
│ ├── silver_layer.dbc # Notebook Databricks: bronze → silver
│ └── gold_layer.dbc # Notebook Databricks: silver → gold


## Tecnologias Utilizadas

- **Azure Data Factory** – orquestração dos fluxos de dados  
- **Azure Databricks** – transformação e tratamento dos dados  
- **Azure Data Lake Storage Gen2** – armazenamento dos dados em camadas  
- *(Opcional)* **Power BI** – visualização analítica dos dados

## Como Utilizar

### 1. Importar Notebooks no Databricks

Para importar os arquivos `.dbc`:

1. Acesse seu workspace no Azure Databricks
2. Vá em **Workspace** > clique com o botão direito > **Import**
3. Escolha **DBC Archive**, selecione o arquivo `.dbc` localizado em `/databricks/notebooks/`

### 2. Importar Artefatos do ADF

Você pode importar os componentes do ADF de duas formas:

#### a) Via Portal do Azure (Importação Manual)

1. Acesse o Azure Data Factory Studio
2. Clique em **Autor** > botão de **Importar JSON**
3. Importe os arquivos de `/adf/pipelines/`, `/datasets/`, `/linkedServices/`, etc.

#### b) Conectar o ADF ao repositório GitHub

1. Configure o controle de versão no ADF com este repositório
2. O ADF reconhecerá automaticamente os arquivos organizados em `/adf/`

## Observações

- O arquivo `etl-prod-eastus-adf.json` contém metadados da instância do ADF e é mantido apenas por completude.
- A pasta `triggers/` está vazia, mas incluída para futuras extensões (como agendamentos).
- Este repositório **não contém credenciais** ou dados sensíveis.
