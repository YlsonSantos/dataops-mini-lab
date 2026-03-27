# DataOps Mini Lab - Pipeline de pedidos 

Este repositório contém a primeira versão de um pipeline de dados funcional, desenvolvido como parte do aprendizado de práticas de **DataOps**. O objetivo principal é realizar a ingestão de dados brutos (CSV) para uma base analítica local utilizando **DuckDB**.

## Cenário
Uma empresa recebe diariamente arquivos CSV com dados de pedidos. O pipeline processa esses arquivos, realiza a tipagem dos dados e persiste em uma camada de warehouse para consultas rápidas e agregações de status.

## Tecnologias utilizadas
* **Python 3.11+**
* **Pandas**: Para manipulação e leitura dos dados brutos.
* **DuckDB**: Banco de dados OLAP in-process para armazenamento e consultas SQL.
* **Git**: Versionamento de código.

## Estrutura do projeto
```text
dataops-mini-lab/
├── data/
│   ├── raw/                # Dados brutos recebidos (CSV)
│   └── curated/            # (Futuro) Dados limpos e transformados
├── ingestion/
│   └── load_orders.py      # Script principal de ETL
├── warehouse/
│   └── local.duckdb        # Base de dados local (gerada na execução)
├── .gitignore              # Arquivos ignorados pelo Git (.venv, .duckdb)
└── README.md
```

## 1. Clone o repositório:

```bash
git clone [https://github.com/YlsonSantos/dataops-mini-lab.git](https://github.com/YlsonSantos/dataops-mini-lab.git)
cd dataops-mini-lab
```

## 2. Crie e ative o ambiente virtual:

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
```

## 3. Instale as dependências:

```Bash
pip install pandas duckdb
```

## 4. Execute o pipeline:

```Bash
python ingestion/load_orders.py
```
---
## Reflexão final

**1. Onde está o dado bruto neste projeto?**
O dado bruto está localizado no arquivo CSV em `data/raw/orders_2026_03_23.csv`. Em um pipeline de dados real, esta pasta representa a "Landing Zone" ou camada "Bronze", onde os dados chegam em seu estado original.

**2. Qual é o papel do script Python no fluxo?**
O script Python (`load_orders.py`) atua como o **Orquestrador do Pipeline**. Ele é responsável por:
* Validar a existência do arquivo de entrada.
* Ler e carregar os dados brutos na memória usando o Pandas.
* Estabelecer a conexão com o banco de dados DuckDB.
* Executar os comandos SQL de transformação (tipagem de dados) e carga.
* Gerar o relatório final de agregação para validação.

**3. O que aconteceria se uma coluna do CSV mudasse de nome?**
O pipeline quebraria com um erro de execução. Como o script utiliza comandos SQL (`CAST(coluna AS TIPO)`), o DuckDB não encontraria o nome da coluna antiga referenciada no código. Isso demonstra a necessidade de implementarmos **Contratos de Dados** no futuro para garantir a resiliência do pipeline.

**4. Por que o primeiro commit no Git é importante?**
O primeiro commit estabelece a **Baseline** (linha de base) do projeto. Ele garante que temos uma versão funcional e estável registrada, permitindo que, caso as próximas evoluções apresentem bugs, possamos realizar um **Rollback** (retorno) para este estado conhecido e seguro.

**5. O pipeline funciona, mas ele já pode ser considerado confiável para produção?**
Ainda não. Embora seja funcional, para ser "Production-Ready" (pronto para produção) sob a ótica de DataOps, ele precisaria de:
* **Testes de Qualidade:** Validar se há valores nulos ou valores de venda negativos.
* **Logging e Monitoramento:** Registrar erros de forma automática.
* **Agendamento:** Uma forma de rodar o script sem intervenção manual.
* **Tratamento de Erros:** Mensagens mais amigáveis e recuperação de falhas se o arquivo CSV vier corrompido.
