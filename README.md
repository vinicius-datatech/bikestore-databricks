# 🚲 Bike Store — Pipeline de Dados na Nuvem

![Databricks](https://img.shields.io/badge/Databricks-Azure-red?logo=databricks)
![Microsoft Azure](https://img.shields.io/badge/Microsoft-Azure-0078D4?logo=microsoftazure)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-PySpark-E25A1C?logo=apachespark)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-Data%20Lakehouse-blue)
![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github)

> **MVP — Construção de um Pipeline de Dados na Nuvem**  
> Projeto desenvolvido na **Pós-Graduação em Ciência de Dados & Analytics — PUC-Rio**, utilizando **Azure Databricks** e **Azure Data Lake Storage**.

## 📌 Sobre o projeto

Este repositório apresenta a implementação de um **MVP de Engenharia de Dados**, construído a partir da proposta acadêmica de desenvolver, do início ao fim, um pipeline funcional de dados em nuvem.

O projeto foi estruturado seguindo a lógica de um **Lakehouse** e da **Arquitetura Medalhão**, organizando o fluxo de dados em camadas:

**Dados brutos → Bronze → Silver → Gold → análise/consumo**

A documentação do MVP estabelece como etapas centrais: definição do objetivo, busca e coleta dos dados, modelagem, carga/ETL e análise da qualidade e dos resultados. O documento também solicita que o repositório público contenha o código e evidências visuais das etapas executadas na plataforma de nuvem.

## 🎯 Objetivo

Construir um pipeline de dados em nuvem capaz de:

- disponibilizar os dados em um ambiente centralizado;
- organizar os dados segundo uma arquitetura em camadas;
- executar processos de ingestão e transformação;
- aplicar validações de qualidade;
- disponibilizar dados tratados para consumo analítico;
- automatizar a execução do fluxo por meio de **Jobs e Pipelines do Databricks**;
- produzir estruturas Gold direcionadas ao consumo e à análise.

## 🧩 Contexto do MVP

O projeto utiliza um conjunto de dados relacionado a uma operação de **Bike Store**, contendo entidades como:

- Brands;
- Categories;
- Customers;
- Order Items;
- Orders;
- Products;
- Staffs;
- Stocks;
- Stores.

A organização do projeto no Databricks evidencia a separação das etapas de processamento em diretórios específicos para **Bronze**, **Silver** e **Gold**, além de uma área complementar para pedidos.

---

# 🏗️ Arquitetura da solução

A solução combina **Microsoft Azure**, **Azure Data Lake Storage**, **Azure Databricks**, **Delta Lake**, **Unity Catalog** e **Jobs/Pipelines**.

```text
                    ┌──────────────────────────────┐
                    │        Dados de origem       │
                    │      Bike Store / CSVs       │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │      Azure Data Lake         │
                    │        Storage Gen2          │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │            BRONZE            │
                    │       Dados brutos/raw       │
                    │  brands, categories, etc.    │
                    └──────────────┬───────────────┘
                                   │
                         Validação Bronze
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │            SILVER            │
                    │ Dados tratados/padronizados │
                    │ products, orders, customers  │
                    └──────────────┬───────────────┘
                                   │
                         Validação Silver
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │             GOLD             │
                    │       Dados para consumo     │
                    │  Sales NY / Orders Pending   │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │       Análise / Consumo      │
                    │     SQL / Databricks / BI    │
                    └──────────────────────────────┘
```

## 🥉 Bronze — dados brutos

A camada Bronze representa a entrada dos dados no Lakehouse, preservando os dados próximos ao estado original.

No MVP foram estruturados notebooks para:

- validação da camada Bronze;
- Brands;
- Categories;
- Customers;
- Order Items;
- Orders;
- Products;
- Staffs;
- Stocks;
- Stores;
- criação das tabelas Bronze.

### Evidência no Databricks

<img width="959" height="537" alt="Projeto Bike - Camada Bronze" src="https://github.com/user-attachments/assets/65daae80-30a7-4aff-9a63-f64f3bac61a9" />


---

## 🥈 Silver — dados tratados

A camada Silver concentra os processos de transformação, limpeza e padronização necessários para disponibilizar dados mais confiáveis para as etapas posteriores.

No projeto foram estruturados notebooks para:

- validação da camada Silver;
- transformação de Products;
- transformação de Orders;
- transformação de Customers.

### Evidência no Databricks

![Camada Silver](docs/images/projeto-bike-camada-silver.png)

---

## 🥇 Gold — dados para consumo

A camada Gold reúne estruturas direcionadas ao consumo analítico.

No MVP foram implementadas estruturas relacionadas a:

- **Sales NY** — estrutura analítica relacionada às vendas da operação de Nova York;
- **Orders Pending** — estrutura destinada à análise de pedidos pendentes.

### Evidência no Databricks

![Camada Gold](docs/images/projeto-bike-camada-gold.png)

---

# ☁️ Azure Data Lake

O armazenamento em nuvem foi organizado no **Azure Data Lake**, com separação entre áreas de origem e destino e diretórios associados às camadas do pipeline.

A estrutura visual registrada no projeto contempla:

- área de armazenamento;
- container;
- pasta raiz;
- pastas de origem;
- pastas de destino;
- Bronze;
- Silver;
- Gold;
- arquivos e estruturas Delta.

### Centro de armazenamento

![Azure Data Lake — Centro de armazenamento](docs/images/azure-datalake-centro-de-armazenamento.png)

### Container

![Azure Data Lake — Container](docs/images/azure-datalake-conteiner.png)

### Arquitetura Medalhão

![Azure Data Lake — Arquitetura Medalhão](docs/images/azure-datalake-conteiner-arquitetura-medalion.png)

### Estrutura de pastas

![Azure Data Lake — Pastas de origem e destino](docs/images/azure-datalake-pastas-destino-e-origem.png)

---

# 🔄 Pipeline de ETL

O pipeline foi organizado para executar o processamento de forma encadeada, respeitando as dependências entre as camadas.

A execução registrada no Databricks apresenta o seguinte fluxo:

```text
Bronze
  ├── brands
  ├── categories
  ├── customers
  ├── order_items
  ├── orders
  ├── products
  ├── staffs
  ├── stocks
  └── stores
          │
          ▼
    validate_bronze
          │
          ▼
Silver
  ├── Silver products
  ├── Silver orders
  └── Silver customers
          │
          ▼
    validate_silver
          │
          ▼
Gold
  ├── Gold Sales NY
  └── Gold orders pending
```

### Grafo de execução

![Jobs e Pipeline — Gráfico](docs/images/jobs-e-pipeline-grafico.png)

### Linha do tempo

![Jobs e Pipeline — Linha do tempo](docs/images/jobs-e-pipeline-linha-do-tempo.png)

### Lista de tarefas

![Jobs e Pipeline — Lista](docs/images/jobs-e-pipeline-lista.png)

---

# 🧪 Qualidade de Dados

A proposta do MVP determina que a análise seja precedida por uma verificação da qualidade dos dados.

Foram consideradas dimensões como:

| Dimensão | Objetivo |
|---|---|
| **Completude** | Verificar valores nulos ou vazios |
| **Consistência** | Verificar padrões e formatos esperados |
| **Unicidade** | Identificar duplicidades indevidas |
| **Acurácia** | Avaliar se os valores fazem sentido no contexto |
| **Outliers** | Identificar valores extremos que possam distorcer análises |

O projeto possui notebooks específicos de validação para as camadas **Bronze** e **Silver**, evidenciados no fluxo de execução do Job.

---

# 📚 Modelagem e Catálogo de Dados

O projeto adota a lógica da **Arquitetura Medalhão**, na qual cada camada representa um estágio de refinamento dos dados:

- **Bronze:** dados brutos;
- **Silver:** dados limpos e padronizados;
- **Gold:** dados modelados e preparados para consumo.

A documentação do MVP também destaca a importância de um catálogo de dados contendo informações sobre tabelas, campos, tipos de dados, domínio dos valores e linhagem.

No ambiente Databricks, a estrutura de tabelas pode ser acompanhada por meio do **Unity Catalog**.

### Unity Catalog

![Unity Catalog — Tabelas](docs/images/unity-catalog-tabelas.png)

---

# 🗂️ Estrutura do projeto no Databricks

A organização observada no Workspace do projeto é:

```text
Projeto Bikes/
│
├── 01.bronze/
│   ├── 00.validate_bronze
│   ├── 01.brands
│   ├── 02.categories
│   ├── 03.customers
│   ├── 04.order_items
│   ├── 05.orders
│   ├── 06.products
│   ├── 07.staffs
│   ├── 08.stocks
│   ├── 09.stores
│   └── 10.Create tables bronze
│
├── 02.silver/
│   └── 00.Prod/
│       ├── 00.validate_silver
│       ├── 01.Silver products Prod
│       ├── 02.Silver orders Prod
│       └── 03.Silver customers Prod
│
├── 03.gold/
│   └── Prod/
│       ├── 01.Gold Sales NY Prod
│       └── 02.Gold orders pending Prod
│
└── 05.orders/
```

### Workspace

![Databricks Workspace — Projeto Bikes](docs/images/projeto-bike-workspace.png)

---

# 📊 Evidências das camadas no Azure Data Lake

## Bronze

![Azure Data Lake — Bronze](docs/images/azure-datalake-pasta-bronze.png)

![Azure Data Lake — Bronze / Brands](docs/images/azure-datalake-pasta-bronze-brands-exemplo.png)

![Azure Data Lake — Bronze / Delta Log](docs/images/azure-datalake-pasta-bronze-delta-log.png)

## Silver

![Azure Data Lake — Silver](docs/images/azure-datalake-pasta-silver.png)

![Azure Data Lake — Silver / Customer](docs/images/azure-datalake-pasta-silver-customer-exemplo.png)

![Azure Data Lake — Silver / Delta Log](docs/images/azure-datalake-pasta-silver-delta-log.png)

## Gold

![Azure Data Lake — Gold](docs/images/azure-datalake-pasta-gold.png)

![Azure Data Lake — Gold / Sales NY](docs/images/azure-datalake-pasta-gold-sales-ny-exemplo.png)

![Azure Data Lake — Gold / Delta Log](docs/images/azure-datalake-pasta-gold-delta-log.png)

---

# 🔍 Evidências complementares do armazenamento

### Pasta raiz

![Azure Data Lake — Pasta raiz](docs/images/azure-datalake-conteiner-pasta-raiz.png)

### Pastas de origem

![Azure Data Lake — Pastas de origem](docs/images/azure-datalake-pastas-origem.png)

### Container

![Azure Data Lake — Container](docs/images/azure-datalake-conteiner.png)

### Volumes / Resource de origem

![Databricks Volumes — Resource de origem](docs/images/projeto-bike-volumes-resource-origem.png)

---

# 🛠️ Tecnologias utilizadas

| Tecnologia | Utilização |
|---|---|
| **Microsoft Azure** | Infraestrutura de nuvem |
| **Azure Data Lake Storage** | Armazenamento dos dados |
| **Azure Databricks** | Desenvolvimento e execução do pipeline |
| **Apache Spark / PySpark** | Processamento dos dados |
| **Delta Lake** | Armazenamento e processamento das tabelas em formato Delta |
| **Unity Catalog** | Organização e governança/catalogação |
| **Jobs & Pipelines** | Orquestração e execução das etapas |
| **GitHub** | Versionamento e disponibilização do projeto |

---

# ▶️ Como reproduzir o projeto

## Pré-requisitos

Para reproduzir o MVP, recomenda-se possuir:

1. Acesso a um ambiente **Azure Databricks**;
2. Acesso ao **Azure Data Lake Storage**;
3. Permissões necessárias para leitura e escrita no armazenamento;
4. Acesso aos notebooks e scripts deste repositório;
5. Dados de origem utilizados pelo projeto;
6. Configuração das estruturas de catálogo/armazenamento necessárias no ambiente.

> ⚠️ **Observação:** credenciais, chaves, tokens, secrets e informações sensíveis não devem ser versionados no GitHub.

## Fluxo recomendado

```text
1. Configurar o ambiente Azure
2. Configurar o Data Lake
3. Disponibilizar os dados de origem
4. Executar a camada Bronze
5. Validar Bronze
6. Executar a camada Silver
7. Validar Silver
8. Executar a camada Gold
9. Executar as análises
10. Orquestrar o fluxo pelo Job
```

---

# 📈 Resultados e entregáveis

O MVP demonstra, de forma integrada, os principais componentes de um pipeline de Engenharia de Dados em nuvem:

- ingestão de dados;
- armazenamento em Data Lake;
- arquitetura Medalhão;
- processamento por camadas;
- transformação e padronização;
- validação de qualidade;
- tabelas Delta;
- catálogo de dados;
- orquestração por Jobs/Pipelines;
- disponibilização de dados para consumo analítico.

O resultado é um fluxo de dados estruturado **da origem ao consumo**, permitindo acompanhar a evolução dos dados desde a camada bruta até as estruturas Gold.

---

# 🎓 Contexto acadêmico

**Curso:** Pós-Graduação em Ciência de Dados & Analytics  
**Instituição:** PUC-Rio  
**Atividade:** MVP — Construção de um Pipeline de Dados na Nuvem  
**Área:** Engenharia de Dados  
**Ambiente:** Microsoft Azure / Azure Databricks / Azure Data Lake

O documento orientador do MVP estabelece como requisitos a disponibilização do código em repositório público do GitHub e a apresentação de evidências das etapas realizadas na plataforma de nuvem.

---

# 📖 Referências

- Documentação oficial do **Azure Databricks**
- Documentação oficial do **Microsoft Azure**
- Documentação do **Azure Data Lake Storage**
- Documentação do **Apache Spark**
- Documentação do **Delta Lake**
- Documentação do **Unity Catalog**
- Materiais didáticos da **Pós-Graduação em Ciência de Dados & Analytics — PUC-Rio**

---

# 👤 Autor

**Vinícius Araújo Moraes**

🎓 Pós-Graduação em Ciência de Dados & Analytics — PUC-Rio  
📊 Data Analytics | Data Engineering | BI  
☁️ Azure | Databricks | Data Lake | Spark | SQL | Python

🔗 **Repositório:**  
https://github.com/vinicius-datatech/bikestore-databricks

---

## 📌 Observação sobre os dados

Este repositório tem finalidade **acadêmica e de portfólio**. A disponibilização dos dados utilizados não é necessária para a entrega do MVP, conforme as especificações da atividade acadêmica.

---

### ⭐ Projeto acadêmico de Engenharia de Dados em nuvem

**Da ingestão ao consumo: dados organizados, transformados, validados e preparados para análise.**
