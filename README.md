# Desafio Técnico de BI & Dados - Análise de Fundos CVM

Este repositório contém a solução para o desafio técnico de Business Intelligence (Investimentos), focado na análise de drivers de captação líquida de fundos de ações utilizando dados públicos da CVM.

***

## 🎯 Objetivo
Investigar e modelar o fluxo de captação (`Net Flow`) de fundos de ações brasileiros, identificando quais fatores (Retorno, Volatilidade, Tamanho, etc.) melhor explicam a entrada ou saída de capital no curto prazo ($T+1$ a $T+21$).

***

## 🗂 Estrutura do Projeto

```text
desafio-kinea-bi/
├── data/
│   ├── raw/          # Dados brutos baixados diretamente da CVM (ignorados no git)
│   └── processed/    # Dados limpos e consolidados em Parquet
├── notebooks/
│   ├── 01_download_dados.ipynb    # ETL: Extração automatizada da CVM
│   ├── 02_limpeza_dados.ipynb     # ETL: Filtragem (Ações) e Tratamento (Res. 175)
│   └── 03_feature_engineering.ipynb # Criação de Variáveis (Retorno, Volatilidade)
├── README.md         # Documentação do projeto
└── requirements.txt  # Bibliotecas necessárias
```
## 🚀 Como Executar
## 1. Pré-requisitos
Certifique-se de ter Python 3.10+ instalado. Recomenda-se o uso de ambiente virtual

```bash
# Clone o repositório
git clone [https://github.com/SEU_USUARIO/desafio-kinea-bi.git](https://github.com/SEU_USUARIO/desafio-kinea-bi.git)
cd desafio-kinea-bi

# Crie e ative o ambiente virtual
python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Instale as dependências
pip install pandas numpy requests jupyter matplotlib seaborn scikit-learn pyarrow fastparquet
```

## 2. Pipeline de Dados (ETL)
O pipeline foi dividido em notebooks para garantir reprodutibilidade e clareza:

Extração: Execute notebooks/01_download_dados.ipynb.

O que faz: Baixa os informes diários dos últimos 24 meses do Portal de Dados Abertos da CVM.

Output: Arquivos .csv e .zip em data/raw.

Limpeza e Consolidação: Execute notebooks/02_limpeza_dados.ipynb.

O que faz: Filtra fundos da classe "Ações", trata mudanças de layout (Resolução 175) e consolida em um arquivo otimizado.

Output: data/processed/base_acoes_consolidada.parquet.

***

## 🛠 Tecnologias Utilizadas
- Python: Linguagem principal.
- Pandas: Manipulação de dados e séries temporais.
- Requests: Automação de downloads.
- Parquet: Formato de armazenamento colunar para alta performance.

***

Projeto desenvolvido para fins de avaliação técnica.

***

