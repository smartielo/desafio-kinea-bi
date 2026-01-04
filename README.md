# Desafio Técnico de BI & Dados - Análise de Fundos CVM

Este repositório contém a solução "End-to-End" para o desafio de Business Intelligence e Data Science, focado na modelagem preditiva de captação líquida (`Net Flow`) de fundos de ações brasileiros.

## Objetivo de Negócio
Identificar quais fatores (Drivers) impulsionam a entrada ou saída de dinheiro em fundos de investimento e criar um modelo preditivo capaz de antecipar quais fundos terão maior captação no curto prazo (21 dias).

## Resultados Chave (Highlights)
* **Modelo Final:** Random Forest Regressor.
* **Performance:** $R^2$ de **34.6%** em dados de teste Out-of-Time (OOT).
* **Impacto de Negócio:** O modelo demonstrou **monotonicidade perfeita** na ordenação dos fundos.
    * Os fundos classificados no **Top 10% (Decil 9)** pelo modelo tiveram, na realidade, a maior captação média.
    * Os fundos classificados no **Bottom 10% (Decil 0)** tiveram captação negativa (resgates).

## Estrutura do Pipeline

```text
desafio-kinea-bi/
├── data/
│   ├── raw/          # Dados brutos da CVM
│   └── processed/    # Dados limpos e features calculadas (CSV)
├── notebooks/
│   ├── 01_download_dados.ipynb      # Extração: 24 meses de histórico CVM
│   ├── 02_limpeza_dados.ipynb       # ETL: Tratamento da Resolução 175 e filtros
│   ├── 03_feature_engineering.ipynb # Features: Retorno, Volatilidade e Target
│   ├── 04_modelagem_basica.ipynb    # Baseline: Regressão Linear (Falha: R² Negativo)
│   └── 05_modelagem_avancada.ipynb  # Final: Random Forest + Validação de Decis
└── README.md         # Documentação
```

## Como Executar
## 1. Pré-requisitos
Certifique-se de ter Python 3.10+ instalado. Recomenda-se o uso de ambiente virtual

```bash
# Clone o repositório
git clone [https://github.com/smartielo/desafio-kinea-bi.git](https://github.com/smartielo/desafio-kinea-bi.git)
cd desafio-kinea-bi

# Crie e ative o ambiente virtual
python -m venv venv
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Instale as dependências
pip install pandas numpy requests jupyter matplotlib seaborn scikit-learn
```
***

## 2. O Fluxo de Trabalho
O pipeline foi dividido em notebooks numerados para garantir reprodutibilidade linear:

- Extração (01_download_dados.ipynb):

  * Baixa os informes diários dos últimos 24 meses do Portal de Dados Abertos da CVM.

  * Output: Arquivos .csv e .zip em data/raw.

- Limpeza e Consolidação (02_limpeza_dados.ipynb):

  * Filtra fundos da classe "Ações", trata mudanças de layout (Resolução 175) e consolida em um arquivo otimizado.

  * Output: data/processed/base_acoes_consolidada.csv.

- Engenharia de Features (03_feature_engineering.ipynb):

  * Calcula janelas móveis (21, 63, 126 dias) para Retorno e Risco. Cria o Target (Soma do fluxo futuro em T+21).

  * Output: data/processed/base_modelagem.csv.

- Modelagem (04 e 05):

  * Separação Temporal (Out-of-Time): Últimos 90 dias reservados para teste.

  * Comparativo: Regressão Linear vs Random Forest.

*** 
## Análise de Resultados
- Por que Random Forest?\
A Regressão Linear apresentou $R^2$ negativo (-0.01), indicando que a relação entre Retorno/Risco e Captação não é linear. A Random Forest capturou a complexidade do mercado, atingindo $R^2$ de 0.34. 
- Validação por Decis (Ranking). 
Dividindo as previsões do modelo em 10 grupos (decis):
  * 1. O modelo ordenou perfeitamente os fundos do pior para o melhor.
  * 2. Isso valida o uso da ferramenta para seleção e recomendação de fundos baseada em probabilidade de captação.

***

## Tecnologias Utilizadas

- Python: Linguagem principal.
- Pandas: Manipulação de dados e séries temporais.
- Requests: Automação de downloads.
- Scikit-Learn: Modelagem preditiva.

***

Projeto desenvolvido para fins de avaliação técnica.

***

