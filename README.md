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

# 🎯 Objetivo de Negócio 

Desenvolver uma solução de Engenharia de Dados em nuvem capaz de integrar, processar, transformar e disponibilizar informações provenientes da operação de uma rede de lojas de bicicletas, permitindo identificar e analisar o desempenho comercial das unidades por meio do volume de vendas realizadas.

A solução deverá possibilitar a identificação das lojas com maior representatividade nas vendas, fornecendo subsídios para a avaliação do desempenho comercial, a comparação entre unidades e a identificação de oportunidades de melhoria na gestão das operações.

Por meio da implementação de um pipeline estruturado em arquitetura Medalhão (Bronze, Silver e Gold), busca-se transformar dados operacionais brutos em informações organizadas, consistentes e preparadas para consumo analítico, apoiando a tomada de decisões orientadas por dados (Data-Driven Decision Making).

### Pergunta de Negócio Principal

Quais lojas apresentam o maior volume de vendas de bicicletas e como se caracteriza o desempenho comercial de cada unidade, considerando a quantidade de produtos comercializados e os valores das transações realizadas?

## 🧩 Contexto do MVP

Construir um pipeline de dados em nuvem capaz de:

- disponibilizar os dados em um ambiente centralizado;
- organizar os dados segundo uma arquitetura em camadas;
- executar processos de ingestão e transformação;
- aplicar validações de qualidade;
- disponibilizar dados tratados para consumo analítico;
- automatizar a execução do fluxo por meio de **Jobs e Pipelines do Databricks**;
- produzir estruturas Gold direcionadas ao consumo e à análise.

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

#  🧪🎲 Coleta de Dados (Fonte de Dados)

O conjunto de dados utilizado no projeto foi obtido por meio da plataforma Kaggle, a partir do repositório público Bike Store Sample Database.

**Fonte:** Kaggle — Bike Store Sample Database

**Link:** https://www.kaggle.com/datasets/dillonmyrick/bike-store-sample-database/data

O conjunto de dados disponibiliza arquivos no formato CSV, contendo informações relacionadas à operação comercial de uma rede de lojas de bicicletas.

Os dados contemplam diferentes entidades do negócio, incluindo lojas, clientes, produtos, marcas, categorias, funcionários, estoques, pedidos e itens de pedidos.

A utilização de arquivos CSV possibilitou a ingestão dos dados para o Azure Data Lake Storage Gen2, que foi utilizado como camada centralizada de armazenamento da solução.

Posteriormente, os arquivos foram processados pelo Azure Databricks, utilizando Apache Spark/PySpark e Delta Lake, seguindo as etapas de ingestão, transformação, validação e disponibilização dos dados para consumo analítico.

---

# 📚 Modelagem e Catálogo de Dados

Catálogo de dados — tabelas de origem

Abaixo está a primeira versão do catálogo, considerando as nove entidades do dataset.

| Tabela      | Descrição funcional           | Finalidade                                      |
|-------------|-------------------------------|-------------------------------------------------|
| brands      | Cadastro de marcas            | Identificar as marcas comercializadas          |
| categories  | Cadastro de categorias        | Classificar os produtos                        |
| customers   | Cadastro de clientes          | Identificar os consumidores                    |
| order_items | Itens associados aos pedidos  | Quantificar produtos e valores vendidos        |
| orders      | Cadastro de pedidos           | Registrar as transações comerciais             |
| products    | Cadastro de produtos          | Identificar bicicletas e demais produtos       |
| staffs      | Cadastro de funcionários      | Identificar responsáveis pelas operações       |
| stocks      | Posição de estoque            | Consultar disponibilidade por loja e produto   |
| stores      | Cadastro das lojas            | Identificar as unidades comerciais             |


O projeto adota a lógica da **Arquitetura Medalhão**, na qual cada camada representa um estágio de refinamento dos dados:

- **Bronze:** dados brutos;
- **Silver:** dados limpos e padronizados;
- **Gold:** dados modelados e preparados para consumo.

A documentação do MVP também destaca a importância de um catálogo de dados contendo informações sobre tabelas, campos, tipos de dados, domínio dos valores e linhagem.

No ambiente Databricks, a estrutura de tabelas pode ser acompanhada por meio do **Unity Catalog**.

### Unity Catalog

<img width="959" height="539" alt="Unity Catalog - Tabelas" src="https://github.com/user-attachments/assets/336ff206-b9e6-4da2-ab87-97f21bc7496c" />

---

# 🧪 Qualidade de Dados e Validação do Pipeline

A qualidade dos dados foi considerada uma etapa fundamental na implementação da solução, buscando assegurar a integridade do fluxo de processamento entre as diferentes camadas da Arquitetura Medalhão.

Para essa finalidade, foram desenvolvidos dois notebooks específicos de validação:

**1. 00.validate_bronze**

Responsável por atuar como ponto de controle após a ingestão dos dados na camada Bronze. Sua finalidade é verificar a conclusão da etapa de processamento e validar as condições necessárias para permitir a continuidade do pipeline em direção à camada Silver.

**2. 00.validate_silver**

Responsável por atuar como ponto de controle após as transformações realizadas na camada Silver. Sua finalidade é verificar a conclusão dessa etapa e permitir que o processamento avance para a construção das estruturas analíticas da camada Gold.

Os dois notebooks estão integrados à orquestração do Job no Azure Databricks, estabelecendo dependências entre as etapas de processamento.

Dessa forma, o fluxo de execução segue a sequência:

- Ingestão e processamento dos dados na camada Bronze;
- Execução da validação Bronze;
- Transformação e padronização na camada Silver;
- Execução da validação Silver;
- Construção das estruturas analíticas na camada Gold.

Essa organização contribui para a rastreabilidade das execuções, o controle das dependências e a identificação de eventuais falhas durante o processamento.

Além disso, a implementação está alinhada às principais dimensões de qualidade de dados:

| Dimensão | Objetivo |
|---|---|
| Completude | Identificar campos sem preenchimento ou valores ausentes |
| Consistência | Verificar a coerência dos dados e dos padrões utilizados |
| Unicidade | Identificar registros duplicados indevidamente |
| Acurácia | Avaliar a adequação dos valores ao contexto de negócio |
| Integridade | Verificar a consistência dos relacionamentos entre entidades |

**Resultado esperado:** estabelecer pontos de controle entre as camadas do pipeline, contribuindo para a confiabilidade do processamento e a disponibilização dos dados para consumo analítico.

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

<img width="1364" height="765" alt="Projeto Bike - Workspace-editado" src="https://github.com/user-attachments/assets/ce9640f3-fc9b-4c91-aa65-46680351a26d" />

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

# 📊 Análise da Solução Implementada

A solução desenvolvida teve como propósito estruturar um ambiente de Engenharia de Dados em nuvem capaz de transformar informações operacionais de uma rede de lojas de bicicletas em estruturas organizadas e preparadas para análise.

A implementação da arquitetura Lakehouse, utilizando Azure Data Lake Storage Gen2 e Azure Databricks, permitiu centralizar os arquivos de origem e estabelecer um fluxo estruturado de processamento.

A adoção da Arquitetura Medalhão possibilitou organizar o tratamento dos dados em diferentes níveis de refinamento.

Na camada Bronze, os dados foram ingeridos e organizados em estruturas Delta, preservando sua característica de dados de origem.

Na camada Silver, foram implementados processos de transformação e padronização das entidades Products, Orders e Customers, preparando essas informações para utilização nas etapas analíticas.

Na camada Gold, foram disponibilizadas duas estruturas direcionadas ao consumo: Sales NY e Orders Pending.

A estrutura Sales NY representa a etapa mais diretamente relacionada ao objetivo de negócio, pois disponibiliza informações comerciais associadas às vendas da operação de Nova York.

Já a estrutura Orders Pending amplia a possibilidade de análise operacional, permitindo acompanhar pedidos que ainda não foram concluídos.

### 💬 Discussão da Solução

A implementação demonstra como a Engenharia de Dados pode contribuir para organizar informações provenientes de diferentes entidades de um sistema transacional, transformando-as em estruturas adequadas para análises de negócio.

Um dos principais benefícios da solução é a organização dos dados em camadas, permitindo separar a ingestão, o tratamento e a disponibilização analítica.

Outro aspecto relevante é a utilização do Azure Databricks para processamento distribuído, combinada ao armazenamento Delta Lake e à organização dos dados por meio do Unity Catalog.

A implementação do Job com dependências entre as etapas Bronze, Silver e Gold também representa um avanço importante, pois permite estruturar a execução do pipeline de maneira orquestrada e acompanhar o processamento desde a origem até a disponibilização das estruturas analíticas.

Do ponto de vista do negócio, a estrutura Gold Sales NY oferece uma base para investigar o desempenho comercial da operação de Nova York. Entretanto, para responder integralmente à pergunta sobre quais lojas apresentam o maior volume de vendas, é necessário que a análise contemple todas as unidades comerciais, permitindo uma comparação entre elas.

Portanto, o projeto estabelece uma infraestrutura funcional para o processamento e a disponibilização dos dados, criando condições para a evolução de análises comerciais mais abrangentes.

### 📈 Oportunidades de Evolução

Como possibilidades de evolução da solução, destacam-se:

- Ampliar a estrutura analítica Gold para contemplar todas as lojas;
- Desenvolver indicadores de quantidade de bicicletas vendidas por unidade;
- Calcular o faturamento total por loja;
- Comparar o desempenho comercial entre períodos;
- Identificar produtos, marcas e categorias com maior volume de vendas;
- Disponibilizar os indicadores em dashboards no Power BI.

Essas evoluções permitiriam ampliar a utilização dos dados para apoiar decisões estratégicas e operacionais.

### 📈 Resultados e entregáveis

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

# 🙂  Autoavaliação

O desenvolvimento deste MVP representou uma experiência importante para consolidar os conhecimentos adquiridos na Pós-Graduação em Ciência de Dados & Analytics da PUC-Rio, especialmente no campo da Engenharia de Dados e da computação em nuvem.

Durante a realização do projeto, tive a oportunidade de trabalhar com tecnologias e conceitos fundamentais para a construção de pipelines modernos de dados, utilizando Microsoft Azure, Azure Data Lake Storage Gen2, Azure Databricks, Apache Spark, PySpark, Delta Lake e Unity Catalog.

Um dos principais aprendizados foi compreender, na prática, como estruturar uma arquitetura Lakehouse utilizando o conceito de Arquitetura Medalhão, organizando os dados em camadas Bronze, Silver e Gold.

Também considero relevante a implementação dos processos de ingestão e transformação, a criação de tabelas Delta, a configuração das estruturas de armazenamento e a organização dos processos de execução por meio de Jobs com dependências entre as etapas.

Outro aprendizado importante foi a compreensão da necessidade de estabelecer mecanismos de validação e controle do pipeline, contribuindo para a rastreabilidade e a confiabilidade do processamento.

Considero que um dos pontos fortes do trabalho foi a construção da infraestrutura de dados em nuvem e a integração dos diferentes componentes da solução, desde o armazenamento no Azure Data Lake até a disponibilização das estruturas analíticas no Databricks.

Como oportunidade de evolução, identifico a necessidade de aprofundar as análises de negócio, ampliar as estruturas Gold para contemplar todas as lojas e desenvolver indicadores que permitam avaliar o desempenho comercial da rede de maneira mais abrangente.

De maneira geral, avalio que o projeto atingiu um resultado significativo dentro da proposta acadêmica, proporcionando uma experiência prática de desenvolvimento de uma solução de Engenharia de Dados em nuvem.

Mais do que implementar ferramentas isoladamente, o trabalho permitiu compreender a importância da integração entre infraestrutura, processamento, modelagem, qualidade e disponibilização dos dados.

**Concluo que o MVP contribuiu significativamente para o desenvolvimento das minhas competências em Engenharia de Dados, fortalecendo minha capacidade de projetar, implementar e documentar soluções orientadas a dados em ambientes de nuvem.**

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
