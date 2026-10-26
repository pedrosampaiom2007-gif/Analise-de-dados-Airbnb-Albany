# Dicionário de dados

## 1. Fonte: `listings.csv.gz` (colunas usadas)

Resumo das colunas carregadas no notebook. O dicionário oficial completo está na página de download do [Inside Airbnb](https://insideairbnb.com/get-the-data/).

| Coluna | Formato na fonte | Descrição | Tratamento previsto |
| --- | --- | --- | --- |
| `id` | número | Identificador do anúncio | R5 |
| `name` | texto | Título do anúncio | — |
| `host_id` | número | Identificador do anfitrião | — |
| `host_since` | texto (data) | Data em que o anfitrião entrou no Airbnb | R4, R11 |
| `host_response_rate` | texto (`"95%"`) | Taxa de resposta do anfitrião | R2 |
| `host_acceptance_rate` | texto (`"80%"`) | Taxa de aceitação de reservas | R2 |
| `host_is_superhost` | `t`/`f` | Se o anfitrião é Superhost | R3 |
| `host_identity_verified` | `t`/`f` | Se a identidade do anfitrião foi verificada | R3 |
| `host_listings_count` | número | Quantos anúncios o anfitrião tem | — |
| `neighbourhood_cleansed` | texto | Bairro do anúncio | — |
| `latitude`, `longitude` | número | Localização aproximada do imóvel | — |
| `property_type` | texto | Tipo de propriedade (apartamento, casa, loft...) | — |
| `room_type` | texto | Tipo de acomodação: casa/apto inteiro, quarto privativo, quarto compartilhado, quarto de hotel | dummies |
| `accommodates` | número | Quantidade máxima de hóspedes | — |
| `bathrooms_text` | texto (`"1.5 baths"`) | Banheiros, em texto | R10 |
| `bedrooms` | número | Quartos | — |
| `beds` | número | Camas | — |
| `amenities` | texto (`'["Wifi", "TV"]'`) | Comodidades, como lista guardada em texto | R9 |
| `price` | texto (`"$1,234.00"`) | Diária anunciada, em moeda local (R$) | R1, R6, R8 |
| `minimum_nights` | número | Mínimo de noites por reserva | — |
| `availability_365` | número | Dias disponíveis nos próximos 365 dias | — |
| `number_of_reviews` | número | Total de avaliações | — |
| `first_review`, `last_review` | texto (data) | Datas da primeira e da última avaliação | R4 |
| `review_scores_rating` | número | Nota geral (0 a 5) | R7 |
| `review_scores_location` | número | Nota da localização | R7 |
| `review_scores_value` | número | Nota do custo-benefício | R7 |
| `instant_bookable` | `t`/`f` | Se aceita reserva imediata | R3 |

## 2. Fonte: `calendar.csv.gz`

| Coluna | Formato na fonte | Descrição |
| --- | --- | --- |
| `listing_id` | número | Identificador do anúncio (liga com `id` do listings) |
| `date` | texto (data) | Dia |
| `available` | `t`/`f` | Se o dia está disponível para reserva |
| `price` | texto | Preço do dia (pode vir vazio em algumas extrações) |
| `minimum_nights`, `maximum_nights` | número | Regras de estadia naquele dia |

## 3. Base tratada: `data/processed/listings_tratado.csv`

> *(preencher ao final do tratamento: entregável E5)*

| Coluna | Tipo | Descrição |
| --- | --- | --- |
| `id` | int64 | Identificador do anúncio |
| `price` | float64 | Diária anunciada em R$ |
| `anos_como_anfitriao` | float64 | Anos desde `host_since` até a data da extração |
| | | |
