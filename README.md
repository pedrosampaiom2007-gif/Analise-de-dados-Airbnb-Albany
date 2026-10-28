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
- Base tratada salva em CSV e em um arquivo SQLite.

## Resultados

A base tinha 48.247 anúncios. Depois do tratamento ficaram 36.178 para a análise.

**1. Bairros mais caros e mais baratos.** O Leblon é o bairro mais caro, com média de R$ 716 por noite, seguido de São Conrado e Ipanema. O mais barato é o Encantado (R$ 180), quase 4 vezes menos.

![Bairros mais caros](imagens/p1_bairros_mais_caros.png)
![Bairros mais baratos](imagens/p1_bairros_mais_baratos.png)

**2. Tipo de acomodação.** O apartamento inteiro é sempre o tipo mais caro: R$ 738 no Leblon e R$ 700 em Ipanema. Nesses bairros, o quarto privativo custa menos de 60% do apartamento inteiro.

**3. Superhosts.** Não cobram mais (R$ 462 contra R$ 466), mas são mais bem avaliados: nota média de 4,89 contra 4,75.

**4. Comodidades.** Wi-Fi (92% dos anúncios) e cozinha (91%) são as mais comuns. Anúncios com piscina custam em média 18% a mais (R$ 528 contra R$ 448).

**5. Novos anfitriões.** A entrada de anfitriões cresceu muito a partir de 2022: foram 655 em 2021 e 4.256 em 2025. O ano de entrada foi estimado pela primeira avaliação, porque a data de cadastro veio vazia nesta extração.

![Anfitriões por ano](imagens/p5_anfitrioes_por_ano.png)

**6. Diária em dólar.** A diária média é de R$ 463,98, o que equivale a US$ 87,05 (dólar a R$ 5,33).

### Limitações
- O preço analisado é o anunciado, não o valor pago pelo hóspede.
- Os dados são de uma única extração (22/09/2026).
- A diferença de preço da piscina pode ter relação com outros fatores, como o bairro e o tamanho do imóvel.

## Ferramentas

Python, pandas, NumPy, Matplotlib, Seaborn, Requests e Google Colab.

## Fonte dos dados

[Inside Airbnb](https://insideairbnb.com/get-the-data/), Rio de Janeiro, licença [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
