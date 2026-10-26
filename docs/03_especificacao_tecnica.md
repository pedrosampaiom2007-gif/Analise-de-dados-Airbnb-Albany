# 03 · Especificação técnica

> **Simulação.** Empresa e datas fictícias.

**Chamado:** DADOS-042 · **Baseado em:** [demanda](01_demanda.md) e [ata do kickoff](02_ata_kickoff.md)

## 1. Fontes de dados

| Fonte | Arquivo | Uso | Acesso |
| --- | --- | --- | --- |
| Inside Airbnb, Rio de Janeiro | `listings.csv.gz` | Anúncios: preço, bairro, tipo, anfitrião, comodidades, avaliações | [insideairbnb.com/get-the-data](https://insideairbnb.com/get-the-data/) (CC BY 4.0) |
| Inside Airbnb, Rio de Janeiro | `calendar.csv.gz` | Disponibilidade e preço por dia nos próximos 365 dias | mesmo link |
| Banco Central (SGS) | API, série 1 | Cotação do dólar comercial | `https://api.bcb.gov.br/dados/serie/bcdata.sgs.1/dados/ultimos/1?formato=json` |

As colunas usadas estão no [dicionário de dados](dicionario_de_dados.md).

## 2. Regras de tratamento (qualidade de dados)

A base tratada **só é aprovada** se cumprir todas as regras:

| # | Regra | Colunas |
| --- | --- | --- |
| R1 | Preço convertido de texto (`"$1,234.00"`) para `float` | `price` |
| R2 | Percentuais convertidos de texto (`"95%"`) para `float` entre 0 e 1 | `host_response_rate`, `host_acceptance_rate` |
| R3 | Colunas `t`/`f` convertidas para `0`/`1` com dicionário de mapeamento | `host_is_superhost`, `instant_bookable`, `host_identity_verified` |
| R4 | Datas convertidas para `datetime` | `host_since`, `first_review`, `last_review` |
| R5 | Sem linhas duplicadas e sem `id` repetido | `id` |
| R6 | Anúncios **sem preço** removidos | `price` |
| R7 | Nulos nas notas de avaliação **tratados e justificados** (remover, preencher ou manter, com explicação) | `review_scores_*` |
| R8 | Outliers de preço identificados pelo **método IQR**, com decisão documentada (remover ou limitar) | `price` |
| R9 | Comodidades transformadas de string para lista (regex + `str.split`) | `amenities` |
| R10 | Número de banheiros extraído do texto (`"1.5 baths"` vira `1.5`) | `bathrooms_text` |
| R11 | Coluna nova `anos_como_anfitriao`, calculada a partir de `host_since` | nova |
| R12 | **Log de tratamento**: linhas antes e depois de cada etapa | todas |

## 3. Entregáveis

| # | Entregável | Local |
| --- | --- | --- |
| E1 | Notebook comentado, com cada decisão explicada em markdown | `notebooks/analise_precos_airbnb_rio.ipynb` |
| E2 | Base tratada em CSV | `data/processed/listings_tratado.csv` |
| E3 | Base em SQLite (tabela `listings`) com 3 consultas SQL de exemplo no notebook | `data/processed/airbnb_rio.db` |
| E4 | Log de tratamento | no relatório executivo |
| E5 | Dicionário de dados da base tratada | `docs/dicionario_de_dados.md` |
| E6 | Relatório executivo com P1 a P6 e de 3 a 5 gráficos | `reports/relatorio_executivo.md` e `reports/figures/` |

## 4. Padrões do time

- **Dados brutos não vão para o repositório** (já estão no `.gitignore`); a fonte e a data da extração ficam documentadas.
- Nomes de variáveis e colunas novas em `snake_case`, em português.
- Toda célula de código começa com um comentário dizendo o que faz.
- Nada de `inplace=True` em cadeia (`df['col'].fillna(..., inplace=True)`): gera aviso no pandas 2 e deixa de funcionar no 3.
- Gráficos com título, rótulos nos eixos e fonte dos dados.
- Entrega via **Pull Request** para a branch `main`, preenchendo o [template de PR](../.github/pull_request_template.md).

## 5. Critérios de aceite (Definition of Done)

- [ ] O notebook roda do início ao fim sem erro (*Runtime > Run all* no Colab).
- [ ] As regras R1 a R12 foram aplicadas e são verificáveis com `info()` e `isna().sum()` no fim do tratamento.
- [ ] Cada pergunta P1 a P6 tem **resposta numérica** e **um gráfico ou tabela**.
- [ ] Toda remoção de dados tem justificativa e aparece no log.
- [ ] O relatório executivo dá para entender **sem abrir o notebook**.
- [ ] As limitações (preço anunciado, extração única etc.) estão descritas no relatório.
