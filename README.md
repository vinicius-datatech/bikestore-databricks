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

### Evidência no Databricks - Camada Bronze

<img width="959" height="537" alt="Projeto Bike - Camada Bronze" src="https://github.com/user-attachments/assets/65daae80-30a7-4aff-9a63-f64f3bac61a9" />

---

## 🥈 Silver — dados tratados

A camada Silver concentra os processos de transformação, limpeza e padronização necessários para disponibilizar dados mais confiáveis para as etapas posteriores.

No projeto foram estruturados notebooks para:

- validação da camada Silver;
- transformação de Products;
- transformação de Orders;
- transformação de Customers.

### Evidência no Databricks - Camada Silver

<img width="959" height="539" alt="Projeto Bike - Camada Silver" src="https://github.com/user-attachments/assets/436fc9d9-89c5-472e-9a40-045a8a09610c" />

---

## 🥇 Gold — dados para consumo

A camada Gold reúne estruturas direcionadas ao consumo analítico.

No MVP foram implementadas estruturas relacionadas a:

- **Sales NY** — estrutura analítica relacionada às vendas da operação de Nova York;
- **Orders Pending** — estrutura destinada à análise de pedidos pendentes.

### Evidência no Databricks - Camada Gold

<img width="959" height="539" alt="Projeto Bike - Camada Gold" src="https://github.com/user-attachments/assets/3de8e3e1-79a1-418c-b459-bfc15f77fd81" />

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

### Centro de armazenamento - Azure Data Lake

<img width="958" height="539" alt="Azure - Datalake - Centro de Armazenamento" src="https://github.com/user-attachments/assets/9cbae36b-fa7a-415f-9961-77dc2dcc8c10" />

### Container

<img width="959" height="539" alt="Azure - Datalake - Conteiner" src="https://github.com/user-attachments/assets/f9fb06d1-1bb0-4cc2-8fa3-ef104cd15ad6" />

### Arquitetura Medalhão (Medallion Architecture)

<img width="959" height="539" alt="Azure - Datalake - Conteiner - Arquitetura Medalion" src="https://github.com/user-attachments/assets/df70386d-ebbe-4a41-b179-0e2095a7a5d4" />

### Estrutura de pastas

<img width="959" height="539" alt="Azure - Datalake - Pastas Destino e Origem" src="https://github.com/user-attachments/assets/1ce1c0ec-09d9-491e-99bc-b06779da2b0f" />

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

<img width="959" height="539" alt="Jobs e Pipeline - Gráfico" src="https://github.com/user-attachments/assets/07bf731e-43a9-40b0-aa2a-0bc005f4346c" />

### Linha do tempo

<img width="959" height="539" alt="Jobs e Pipeline - Linha do Tempo" src="https://github.com/user-attachments/assets/75459e6a-b21e-4753-9c1b-d30d26c577cb" />

### Lista

<img width="959" height="539" alt="Jobs e Pipeline - Lista" src="https://github.com/user-attachments/assets/9fb32ba9-5ebb-4834-a4db-095ac7e6e8a2" />

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

<img width="959" height="539" alt="Unity Catalog - Tabelas" src="https://github.com/user-attachments/assets/336ff206-b9e6-4da2-ab87-97f21bc7496c" />

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
    └── Prod/
        ├── 01.Gold Sales NY Prod
        └── 02.Gold orders pending Prod


```

### Workspace

<img width="959" height="539" alt="Projeto Bike - Workspace" src="https://github.com/user-attachments/assets/62baa76c-fda9-4e60-95bb-7e5e8b0e039c" />

---

# 📊 Evidências das camadas no Azure Data Lake

## Bronze

<img width="959" height="539" alt="Azure - Datalake - Pasta Bronze" src="https://github.com/user-attachments/assets/e64d97eb-c3d4-43a7-9449-219feeeaae26" />

<img width="959" height="539" alt="Azure - Datalake - Pasta Bronze - Brands (Exemplo)" src="https://github.com/user-attachments/assets/e21d65a9-8f83-4f5f-949e-14dd8f196a0c" />

<img width="959" height="538" alt="Azure - Datalake - Pasta Bronze - Delta Log" src="https://github.com/user-attachments/assets/35a78c3f-7fe9-4406-ae5e-0ddc4a29f79b" />

## Silver

<img width="959" height="539" alt="Azure - Datalake - Pasta Silver" src="https://github.com/user-attachments/assets/c060c199-4c7e-49c4-9ccc-f00e58054074" />

<img width="959" height="539" alt="Azure - Datalake - Pasta Silver - Customer (Exemplo)" src="https://github.com/user-attachments/assets/b9beb641-9700-4bd2-9a65-042cf3c1ff39" />

<img width="959" height="539" alt="Azure - Datalake - Pasta Silver - Delta Log" src="https://github.com/user-attachments/assets/1ffc7670-5649-4fd7-a721-284e34e218ea" />

## Gold

<img width="959" height="539" alt="Azure - Datalake - Pasta Gold" src="https://github.com/user-attachments/assets/b76d6007-b610-40ba-ac6c-b3ab111346a1" />

<img width="959" height="539" alt="Azure - Datalake - Pasta Gold - Sales NY (Exemplo)" src="https://github.com/user-attachments/assets/185c8abe-86ed-4c91-a631-6187a6e74c4f" />

<img width="959" height="539" alt="Azure - Datalake - Pasta Gold - Delta Log" src="https://github.com/user-attachments/assets/968e8229-6f16-49ed-970c-cdf479fc943d" />

---

# 🔍 Evidências complementares do armazenamento

### Pasta raiz

<img width="959" height="539" alt="Azure - Datalake - Conteiner - Pasta Raiz" src="https://github.com/user-attachments/assets/78ed3a4d-33d6-40cb-9213-b3db86c8adf5" />

### Pastas de origem

<img width="959" height="539" alt="Azure - Datalake - Pastas Origem" src="https://github.com/user-attachments/assets/27557490-720b-47a1-aa60-17fcbfc994f9" />

### Container

<img width="959" height="539" alt="Azure - Datalake - Conteiner" src="https://github.com/user-attachments/assets/569c1971-0cba-4682-97b9-74fbbb753765" />

### Volumes / Resource de origem

<img width="959" height="539" alt="Projeto Bike - Volumes - Resource Origem" src="https://github.com/user-attachments/assets/f37be5dc-d6bb-4d56-9396-ecdea8d162ac" />

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

**Vinícius Araújo Moraes da Silva**

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
