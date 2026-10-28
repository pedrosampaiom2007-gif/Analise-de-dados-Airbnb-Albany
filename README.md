# Análise de preços do Airbnb no Rio de Janeiro

Projeto de tratamento e análise de dados com Python e pandas, desenvolvido como conclusão da trilha de Python para Data Science da Alura.

O objetivo foi pegar uma base pública real, com dados sujos, deixá-la confiável e usá-la para responder perguntas sobre os preços das hospedagens no Rio de Janeiro.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pedrosampaiom2007-gif/Analise-de-dados-Airbnb-Rio/blob/main/notebooks/analise_precos_airbnb_rio.ipynb)

## Perguntas

1. Quais são os bairros mais caros e os mais baratos?
2. Quanto custa cada tipo de acomodação nos bairros com mais anúncios?
3. Superhosts cobram mais e são mais bem avaliados?
4. Quais são as comodidades mais comuns? Ter piscina deixa a diária mais cara?
5. Quantos anfitriões entraram no Airbnb a cada ano?
6. Quanto custa a diária média em dólar?

## O que foi feito

### 1. Coleta e entendimento da base
- Leitura do arquivo `listings` do Inside Airbnb, carregando apenas as 29 colunas necessárias.
- Tradução dos nomes das colunas para o português.
- Verificação do tamanho da base, dos tipos de cada coluna e da quantidade de valores nulos.

### 2. Tratamento
- **Duplicadas:** verificação de linhas repetidas e do mesmo imóvel cadastrado mais de uma vez (mesmo anfitrião, nome e localização).
- **Preço:** conversão de texto (`$1,234.00`) para número, removendo o símbolo e o separador de milhar.
- **Taxas do anfitrião:** conversão de texto (`95%`) para número entre 0 e 1.
- **Colunas de sim/não:** os valores `t` e `f` foram convertidos para verdadeiro e falso com um dicionário de mapeamento.
- **Datas:** conversão das colunas de data para o tipo datetime.
- **Anúncios sem avaliação:** removidos, pois não têm notas para as análises de avaliação.
- **Banheiros:** extração do número de banheiros a partir do texto (`1.5 baths` vira `1.5`; `Half-bath` vira `0.5`) com expressões regulares.

### 3. Outliers
- Identificação dos preços fora do padrão pelo método do intervalo interquartil (IQR).
- Remoção desses anúncios, porque preços extremos distorcem a média e não representam a hospedagem típica.

### 4. Transformações
- **Comodidades:** conversão do texto para lista e uso do `explode` para contar cada comodidade separadamente.
- **Piscina:** criação de uma coluna indicando se o anúncio tem piscina, desconsiderando termos parecidos que não são piscina (mesa de sinuca, vista da piscina e a marca Whirlpool).
- **Ano de entrada:** criação de uma coluna com o ano em que o anfitrião entrou no Airbnb.

### 5. Análises
- Preço médio por bairro, considerando apenas bairros com pelo menos 30 anúncios.
- Tabela dinâmica com o preço médio por tipo de acomodação nos 10 bairros com mais anúncios.
- Comparação de preço e nota entre Superhosts e demais anfitriões.
- Ranking das comodidades mais comuns e comparação de preço entre anúncios com e sem piscina.
- Quantidade de anfitriões que entraram na plataforma por ano.
- Conversão da diária média para dólar com a cotação obtida na API do Banco Central.

### 6. Exportação
- Base tratada salva em CSV e em um banco SQLite, com uma consulta SQL de exemplo.

## Resultados

Em atualização.

## Ferramentas

Python, pandas, NumPy, Matplotlib, Seaborn, Requests, SQLAlchemy, SQLite e Google Colab.

## Fonte dos dados

[Inside Airbnb](https://insideairbnb.com/get-the-data/), Rio de Janeiro, licença [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
