# Quanto custa uma noite no Rio? Análise de preços do Airbnb

Peguei os dados públicos dos anúncios do Airbnb no Rio de Janeiro, tratei a base e analisei **onde, quanto e quando** as diárias são mais caras.

Projeto de conclusão da trilha de Python para Data Science da Alura.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pedrosampaiom2007-gif/Analise-de-dados-Airbnb-Rio/blob/main/notebooks/analise_precos_airbnb_rio.ipynb)

## ❓ Perguntas

1. Quais são os bairros mais caros e os mais baratos?
2. Quanto custa cada tipo de acomodação em cada bairro?
3. Superhosts cobram mais e são mais bem avaliados?
4. Quais comodidades estão ligadas a diárias maiores?
5. Quanto o preço e a ocupação mudam no Carnaval e no Réveillon?
6. Quanto custa a diária mediana em dólar?

## 🧹 O que foi feito

- **Coleta:** leitura dos arquivos do Inside Airbnb direto da URL e cotação do dólar pela API do Banco Central.
- **Limpeza:** preços e percentuais em texto convertidos para número, colunas `t`/`f` para 0/1, datas, duplicadas e nulos.
- **Outliers:** identificação pelo método IQR e tratamento dos preços fora da curva.
- **Transformações:** comodidades em lista (regex + `explode`), tempo de cada anfitrião na plataforma.
- **Análise:** agrupamentos, tabelas dinâmicas e gráficos para responder às perguntas.
- **Exportação:** base tratada em CSV e SQLite, com consultas SQL.

## 📊 Resultados

> *(preencher: principais números e 2 ou 3 gráficos)*

## 🛠️ Ferramentas

Python · pandas · NumPy · Matplotlib · Seaborn · Requests · SQLAlchemy/SQLite · Google Colab

## 📚 Fonte dos dados

[Inside Airbnb](https://insideairbnb.com/), Rio de Janeiro, licença [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
