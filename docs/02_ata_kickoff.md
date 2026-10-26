# 02 · Ata da reunião de kickoff

> **Simulação.** Empresa e datas fictícias.

| Campo | Valor |
| --- | --- |
| **Chamado** | DADOS-042 |
| **Data** | 26/10/2026, 30 min |
| **Participantes** | Diretoria de Expansão (solicitante), Coordenação de Dados, Analista de Dados |

## 1. Objetivo da reunião

Transformar o e-mail da [demanda](01_demanda.md) em perguntas que os dados conseguem responder, e alinhar definições antes de começar.

## 2. Perguntas de negócio acordadas

| # | Pergunta | Para quê |
| --- | --- | --- |
| P1 | Quais são os **10 bairros mais caros e os 10 mais baratos** (preço mediano por noite)? | Escolher onde captar imóveis |
| P2 | Qual é o preço mediano por **tipo de quarto** em cada bairro? | Tabela de preços por perfil de imóvel |
| P3 | **Superhosts** cobram mais? Têm avaliações melhores? | Decidir se vale investir no programa de Superhost |
| P4 | Quais **comodidades** estão ligadas a diárias maiores? | Orientar a captação (piscina, vista para o mar, ar-condicionado...) |
| P5 | Quanto o preço e a ocupação variam **por mês**, principalmente no **Carnaval e no Réveillon**? | Tabela de preços sazonal |
| P6 | Qual é a diária mediana **em dólar**? | Campanha do Marketing para estrangeiros |

## 3. Definições

| Termo | Definição combinada |
| --- | --- |
| **Preço** | Diária **anunciada** (coluna `price`), em R$. Não é o valor efetivamente pago pelo hóspede. |
| **Bairro** | Coluna `neighbourhood_cleansed`. |
| **Ranking de bairros (P1)** | Só entram bairros com **pelo menos 30 anúncios**, para não distorcer com poucos casos. |
| **Medida de preço** | **Mediana**, não média: preços extremos puxam a média para cima. |
| **Réveillon** | 28/12 a 02/01. |
| **Carnaval** | Sábado até Quarta-feira de Cinzas. Em 2027: 06/02 a 10/02. |
| **Ocupação** | Proporção de dias **indisponíveis** no `calendar` (a base não diz se o dia foi reservado ou bloqueado pelo anfitrião). |
| **Dólar** | Cotação do dólar comercial (venda) do Banco Central, série SGS 1, no dia da análise. |

## 4. Premissas

- A base é a **extração mais recente** do Inside Airbnb para o Rio de Janeiro. A data da extração deve constar no relatório.
- Anúncios **sem preço** não entram nas análises de preço.
- Outliers de preço devem ser tratados com critério estatístico (IQR) e a decisão deve ser **documentada**.

## 5. Riscos levantados

| Risco | Impacto | Combinado |
| --- | --- | --- |
| Preço anunciado ≠ preço praticado | Valores podem estar acima do real | Deixar claro nas limitações do relatório |
| Coluna de preço do `calendar` pode vir vazia em algumas extrações | P5 fica sem preço por data | Responder P5 só com ocupação e avisar o solicitante |
| Anúncios com preços absurdos (ex.: R$ 50 mil por noite) | Distorcem rankings | Tratamento de outliers (regra R8) |
| Base é uma "foto" de um único momento | Não mostra tendência ao longo dos anos | Registrar como limitação |

## 6. Fora do escopo

- Modelo de previsão de preço (possível próxima demanda).
- Dashboard interativo.
- Outras cidades.

## 7. Encaminhamentos

| Ação | Responsável | Prazo |
| --- | --- | --- |
| Escrever a especificação técnica | Analista de Dados | 26/10 |
| Checkpoint: revisar o tratamento dos dados | Coordenação de Dados | 30/10 |
| Entregar notebook, base tratada e relatório via PR | Analista de Dados | 06/11 |
| Agendar apresentação para a Diretoria | Coordenação de Dados | após a aprovação do PR |
