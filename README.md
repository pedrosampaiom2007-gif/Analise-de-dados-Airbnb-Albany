# Quanto custa uma noite no Rio? Diagnóstico de preços do Airbnb

> 🚧 *Projeto em andamento.*

Projeto de **tratamento e análise de dados com Python e pandas** que simula uma demanda real de trabalho: a Maré Hospedagens (empresa fictícia) quer saber **onde, quanto e quando cobrar** pelas diárias no Rio de Janeiro antes de expandir sua carteira de imóveis.

Projeto de conclusão da trilha de Python para Data Science da Alura.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pedrosampaiom2007-gif/Analise-de-dados-Airbnb-Rio/blob/main/notebooks/analise_precos_airbnb_rio.ipynb)

## 📌 A demanda

| Documento | Conteúdo |
| --- | --- |
| [01 · Demanda](docs/01_demanda.md) | Chamado DADOS-042 e o e-mail original do solicitante |
| [02 · Ata do kickoff](docs/02_ata_kickoff.md) | Perguntas de negócio, definições, premissas e riscos |
| [03 · Especificação técnica](docs/03_especificacao_tecnica.md) | Fontes, regras de qualidade (R1 a R12), entregáveis e critérios de aceite |
| [Dicionário de dados](docs/dicionario_de_dados.md) | Colunas da fonte e da base tratada |

**Perguntas de negócio:**
1. Quais bairros têm as diárias mais altas e mais baixas?
2. Quanto custa cada tipo de acomodação em cada bairro?
3. Superhosts cobram mais e são mais bem avaliados?
4. Quais comodidades estão ligadas a diárias maiores?
5. Quanto o preço e a ocupação mudam no Carnaval e no Réveillon?
6. Quanto custa a diária mediana em dólar?

## 📊 Resultados

> *(preencher: principais números e 2 ou 3 gráficos. Relatório completo em [reports/relatorio_executivo.md](reports/relatorio_executivo.md))*

## 🛠️ Ferramentas

Python · pandas · NumPy · Matplotlib · Seaborn · Requests (API do Banco Central) · SQLAlchemy/SQLite · Google Colab

## 📁 Estrutura

```
├── docs/                   # demanda, ata do kickoff, especificação técnica e dicionário de dados
├── notebooks/              # notebook de tratamento e análise
├── data/
│   ├── raw/                # dados brutos do Inside Airbnb (não versionados)
│   └── processed/          # base tratada (CSV e SQLite)
├── reports/
│   ├── relatorio_executivo.md
│   └── figures/            # gráficos do relatório
└── requirements.txt
```

## ▶️ Como executar

- **No Colab:** clique no botão "Open in Colab" acima e cole os links dos arquivos do Inside Airbnb na seção 1 do notebook.
- **Localmente:**
  ```bash
  pip install -r requirements.txt
  jupyter notebook notebooks/analise_precos_airbnb_rio.ipynb
  ```

## 📚 Fonte dos dados

[Inside Airbnb](https://insideairbnb.com/), Rio de Janeiro, licença [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Cotação do dólar: [API SGS do Banco Central](https://dadosabertos.bcb.gov.br/).
