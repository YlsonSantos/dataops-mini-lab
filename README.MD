# DataOps Mini Lab - Pipeline de Pedidos 

Este repositório contém a primeira versão de um pipeline de dados funcional, desenvolvido como parte do aprendizado de práticas de **DataOps**. O objetivo principal é realizar a ingestão de dados brutos (CSV) para uma base analítica local utilizando **DuckDB**.

## 📋 Cenário
Uma empresa recebe diariamente arquivos CSV com dados de pedidos. O pipeline processa esses arquivos, realiza a tipagem dos dados e persiste em uma camada de warehouse para consultas rápidas e agregações de status.

## 🛠️ Tecnologias Utilizadas
* **Python 3.11+**
* **Pandas**: Para manipulação e leitura dos dados brutos.
* **DuckDB**: Banco de dados OLAP in-process para armazenamento e consultas SQL.
* **Git**: Versionamento de código.

## Estrutura do Projeto
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
