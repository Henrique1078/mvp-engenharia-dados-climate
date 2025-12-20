# Global Climate Change Data Analysis (2020-2025)

## Visão Geral
Este projeto é um MVP (Minimum Viable Product) desenvolvido como requisito para a pós-graduação em Ciência de Dados da PUC-Rio (Módulo: Engenharia de Dados).

O objetivo é construir um pipeline de dados completo (Coleta, Modelagem, Carga e Análise) em ambiente Cloud para investigar indicadores climáticos globais.

## Objetivo do Projeto

### O Problema
As mudanças climáticas representam um dos maiores desafios globais, mas a análise isolada de métricas nem sempre revela a gravidade do impacto local. O problema que este projeto visa resolver é a **fragmentação da visão sobre a vulnerabilidade climática global**, integrando dados de temperatura, emissões, nível do mar e índices de risco.

### Perguntas de Negócio
O projeto busca responder às seguintes questões principais:

1.  **Tendência Temporal:** Qual é a tendência de variação da Temperatura Média global e por continente ao longo do período (2020-2025)?
2.  **Correlação Crítica:** Existe correlação entre o volume de Emissões de CO₂ de um país e o seu Aumento do Nível do Mar ou Temperatura?
3.  **Análise de Vulnerabilidade:** Quais são os Top 5 países com o maior *Climate Risk Index* e como seus indicadores se comportam comparados à média global?
4.  **Impacto Regional:** Qual continente apresenta a maior média de Emissões de CO₂ e isso se reflete em temperaturas mais altas?

## Dados
**Fonte:** Kaggle - Global Climate Change Data (2020–2025)
**Formato:** CSV
**Descrição:** Dados contendo temperatura média, emissões de CO2, aumento do nível do mar e índice de risco climático por país e ano.

**Disponível em:** https://www.kaggle.com/datasets/shahzadi786/global-climate-change-data-20202025?resource=download

## Tecnologias Utilizadas
* **Linguagem:** Python (PySpark & Pandas)
* **Plataforma:** Databricks Community Edition
* **Armazenamento:** DBFS (Databricks File System)
* **Versionamento:** Git & GitHub

## Catálogo de Dados (Data Dictionary)

A tabela final na camada Prata (`silver_climate_data`) possui 1.200 registros e o seguinte esquema:

| Coluna | Tipo | Descrição | Domínio / Range (Min-Max) |
| :--- | :--- | :--- | :--- |
| **year** | `integer` | Ano de registro da métrica. | 2020 a 2025 |
| **continent** | `string` | Continente onde o país está localizado. | Africa, Asia, Europe, North America, Oceania, South America |
| **country** | `string` | Nome do país analisado. | Texto livre (ex: Argentina a USA) |
| **avg_temperature_celsius** | `double` | Temperatura média anual em graus Celsius. | 10.0°C a 35.0°C |
| **co2_emissions_mt** | `double` | Emissão anual de CO₂ em milhões de toneladas. | 103.32 Mt a 999.55 Mt |
| **sea_level_rise_mm** | `double` | Aumento estimado do nível do mar em milímetros. | 1.0 mm a 5.0 mm |
| **climate_risk_index** | `integer` | Índice de vulnerabilidade climática (quanto maior, maior o risco). | 20 a 90 |


### Tabela de Tendência Temporal: Temperatura Média por Ano e Continente (Pergunta 1)

Esta tabela agrega a temperatura média por ano e continente, derivada da camada Silver.

| Coluna               | Tipo      | Descrição                                                  | Domínio / Range (Min-Max)       |
|----------------------|-----------|------------------------------------------------------------|---------------------------------|
| **Ano**              | `integer` | Ano da agregação temporal.                                 | 2020 a 2025                     |
| **Continente**       | `string`  | Nome do continente analisado.                              | Africa, Asia, Europe, North America, Oceania, South America |
| **Temp. Média (°C)** | `double`  | Temperatura média anual agregada para o continente no ano específico. | 19.06°C a 26.70°C               |


### Tabela de Correlações Críticas: Coeficientes de Pearson entre Métricas Climáticas (Pergunta 2)

Esta tabela apresenta os coeficientes de correlação de Pearson entre métricas climáticas, calculados a partir da camada Silver.

| Coluna                              | Tipo      | Descrição                                                  | Domínio / Range (Min-Max)       |
|-------------------------------------|-----------|------------------------------------------------------------|---------------------------------|
| **Par de Métricas**                 | `string`  | Descrição do par de variáveis correlacionadas (ex: CO₂ vs Temperatura). | Texto descritivo (pares específicos de métricas climáticas) |
| **Coeficiente de Correlação (Pearson)** | `double` | Valor do coeficiente de correlação linear.                | -1.0 a 1.0                      |
| **Interpretação Estatística**       | `string`  | Classificação qualitativa da correlação.                   | Texto categórico (ex: Inexistente/Nula) |


### Tabela de Análise de Vulnerabilidade: Top 5 Países por Climate Risk Index (Pergunta 3)

Esta tabela lista os Top 5 países por índice de risco, com comparações à média global, derivada da camada Silver.

| Coluna                     | Tipo      | Descrição                                                  | Domínio / Range (Min-Max)       |
|----------------------------|-----------|------------------------------------------------------------|---------------------------------|
| **País**                   | `string`  | Nome do país ranqueado.                                    | Texto livre (ex: Italy, Indonesia) |
| **Risco Médio (Index)**    | `double`  | Média do índice de risco climático para o país.            | 57.81 a 63.49                   |
| **Temp. País (°C)**        | `double`  | Temperatura média anual do país.                            | 20.94°C a 22.53°C               |
| **Diferença da Global**    | `double`  | Diferença entre a temperatura do país e a média global (22.42°C). | -1.47°C a +0.12°C               |
| **Nível do Mar (mm)**      | `double`  | Aumento médio do nível do mar para o país.                 | 2.74 mm a 3.41 mm               |
| **Status Nível do Mar**    | `string`  | Classificação em relação à média global (3.03 mm).          | Texto categórico (ex: Abaixo da Média, Acima da Média) |


### Tabela de Impacto Regional: Ranking de Continentes por Emissões de CO₂ e Temperatura (Pergunta 4)

Esta tabela ranqueia continentes por emissões médias de CO₂ e compara com temperaturas, agregada da camada Silver.

| Coluna                        | Tipo      | Descrição                                                  | Domínio / Range (Min-Max)       |
|-------------------------------|-----------|------------------------------------------------------------|---------------------------------|
| **Ranking**                   | `string`  | Posição no ranking de emissões (ex: 1º).                   | Texto ordinal (1º a 6º)         |
| **Continente**                | `string`  | Nome do continente ranqueado.                              | Africa, Asia, Europe, North America, Oceania, South America |
| **Média Emissões CO₂ (Mt)**   | `double`  | Média anual de emissões de CO₂ para o continente.          | 530.62 Mt a 583.90 Mt           |
| **Média Temperatura (°C)**    | `double`  | Temperatura média anual para o continente.                 | 21.86°C a 22.82°C               |



## 5. Solução do Problema e Análises

### Pergunta 1: Tendência Temporal
**Questão:** Qual é a tendência de variação da Temperatura Média global e por continente ao longo do período (2020-2025)?

**Resultado Técnico:**
A tabela abaixo apresenta a média de temperatura agrupada por ano e continente:

| Ano | Continente | Temp. Média (°C) |
| :--- | :--- | :--- |
| 2020 | Africa | 21.53 |
| 2021 | Africa | 20.73 |
| 2022 | Africa | 22.30 |
| 2023 | Africa | 22.42 |
| 2024 | Africa | 22.23 |
| 2025 | Africa | 23.04 |
| 2020 | Asia | 26.70 |
| 2021 | Asia | 21.57 |
| 2022 | Asia | 21.47 |
| 2023 | Asia | 21.38 |
| 2024 | Asia | 21.97 |
| 2025 | Asia | 21.62 |
| 2020 | Europe | 22.49 |
| 2021 | Europe | 23.04 |
| 2022 | Europe | 21.72 |
| 2023 | Europe | 22.01 |
| 2024 | Europe | 19.06 |
| 2025 | Europe | 21.64 |
| 2020 | North America | 24.11 |
| 2021 | North America | 21.30 |
| 2022 | North America | 21.45 |
| 2023 | North America | 21.37 |
| 2024 | North America | 23.07 |
| 2025 | North America | 23.68 |
| 2020 | Oceania | 21.51 |
| 2021 | Oceania | 23.13 |
| 2022 | Oceania | 23.02 |
| 2023 | Oceania | 24.80 |
| 2024 | Oceania | 22.07 |
| 2025 | Oceania | 21.12 |
| 2020 | South America | 24.37 |
| 2021 | South America | 22.90 |
| 2022 | South America | 20.37 |
| 2023 | South America | 23.21 |
| 2024 | South America | 22.63 |
| 2025 | South America | 21.81 |

**Discussão e Análise Aprofundada:**
A análise da série temporal de 5 anos (2020-2025) revela um cenário climático complexo, onde a variabilidade regional supera uma tendência global uniforme. Ao contrário de um aquecimento linear simples, os dados mostram ciclos de volatilidade intensa:

1.  **A "Anomalia de 2020" na Ásia e Américas:**
    * O ano de 2020 registrou temperaturas médias atipicamente altas na **Ásia (26.7°C)**, **América do Norte (24.1°C)** e **América do Sul (24.4°C)**.
    * Imediatamente após este pico, houve uma "correção térmica" em 2021, com quedas bruscas superiores a 5°C na Ásia, indicando possíveis eventos climáticos extremos isolados no início da década ou mudanças drásticas em padrões de emissões/atmosféricos.

2.  **A Estabilidade Africana vs. Volatilidade Europeia:**
    * A **África** é o único continente que apresenta uma tendência de aquecimento mais consistente no pós-2021, saindo de 20.7°C para 23.0°C em 2025.
    * Em contraste, a **Europa** demonstra alta oscilação, com um mergulho significativo de temperatura em 2024 (19.0°C), o menor registro de todo o dataset, antes de voltar a subir em 2025. Isso sugere uma maior suscetibilidade a frentes frias ou alterações nas correntes de ar do Atlântico Norte.

3.  **O "Pico Isolado" da Oceania:**
    * Enquanto o resto do mundo parecia se estabilizar em 2023, a **Oceania** divergiu, registrando seu recorde de calor (24.8°C). Esse comportamento assíncrono reforça a importância de analisar dados climáticos localmente, pois fenômenos como *El Niño/La Niña* afetam hemisférios de formas opostas.

**Conclusão da Questão 1:**
Não observamos um aquecimento uniforme. O período é marcado por **extremos agudos** (2020 muito quente, 2024 frio na Europa) e desconexão entre os hemisférios. Para estratégias de mitigação, isso indica que médias globais podem mascarar crises locais severas.

### Pergunta 2: Correlação Crítica
**Questão:** Existe correlação estatística direta entre o volume anual de Emissões de CO₂ de um país e seus indicadores de Temperatura ou Aumento do Nível do Mar?

**Resultado Técnico:**
O cálculo da Correlação de Pearson resultou nos seguintes coeficientes:

| Par de Métricas | Coeficiente de Correlação (Pearson) | Interpretação Estatística |
| :--- | :--- | :--- |
| **CO₂ vs Temperatura** | -0.0294 | Correlação Inexistente/Nula |
| **CO₂ vs Nível do Mar** | -0.0254 | Correlação Inexistente/Nula |

> *Nota: O coeficiente de Pearson varia de -1 a 1. Valores próximos de 0 indicam ausência de correlação linear.*

**Discussão e Análise:**
Os resultados indicam uma **ausência de correlação linear direta** (valores próximos de zero) entre as emissões anuais de um país e seus efeitos climáticos imediatos no mesmo ano.

Esta descoberta levanta pontos cruciais para a modelagem climática:
1.  **Latência do Sistema Climático:** O aquecimento global e o degelo não são reações instantâneas às emissões do ano corrente. O CO₂ possui um efeito cumulativo na atmosfera, e seus impactos na temperatura e no nível do mar podem levar décadas para se manifestarem plenamente (*Climate Lag*).
2.  **Limitação do Recorte Temporal:** Uma janela de análise de apenas 5 anos (2020-2025) é insuficiente para capturar tendências macroclimáticas de causa e efeito, provando que análises de curto prazo podem mascarar a gravidade do problema.
3.  **Complexidade das Variáveis:** A temperatura de um país é influenciada por fatores geográficos, correntes marítimas e estações do ano muito mais fortemente do que pelo volume de CO₂ emitido localmente naquele ano específico.

**Conclusão da Questão 2:**
Não é possível prever o aumento de temperatura ou do nível do mar de um país baseando-se apenas em suas emissões do ano atual. O impacto é sistêmico, global e de longo prazo, não local e imediato.

### Pergunta 3: Análise de Vulnerabilidade
**Questão:** Quais são os Top 5 países com o maior *Climate Risk Index* e como seus indicadores se comportam comparados à média global?

**Resultado Técnico:**
A tabela abaixo compara os indicadores dos 5 países mais vulneráveis com as médias globais (Global Temp: 22.42°C | Global Sea Rise: 3.03mm).

| País | Risco Médio (Index) | Temp. País (°C) | Diferença da Global | Nível do Mar (mm) | Status Nível do Mar |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Italy** | 63.49 | 20.94°C | -1.47°C | 2.94 | Abaixo da Média |
| **Indonesia** | 60.43 | 21.82°C | -0.60°C | **3.41** | **Acima da Média** |
| **Germany** | 59.26 | 22.53°C | +0.12°C | 2.87 | Abaixo da Média |
| **Pakistan** | 58.64 | 22.01°C | -0.40°C | 2.74 | Abaixo da Média |
| **Egypt** | 57.81 | 22.37°C | -0.05°C | **3.09** | **Acima da Média** |

**Discussão e Análise:**
A análise revela o **"Paradoxo da Vulnerabilidade"**: Estar no topo do ranking de risco não significa necessariamente ter as maiores temperaturas médias absolutas.

1.  **Vulnerabilidade Europeia:** A presença da **Itália (#1)** e **Alemanha (#3)** no topo, mesmo com temperaturas médias próximas ou abaixo da global, indica que o risco climático em países desenvolvidos pode estar atrelado à **variabilidade extrema** (ondas de calor agudas ou inundações repentinas) e não apenas ao "calor constante". Isso desafia a noção de que apenas países tropicais estão em perigo.
2.  **O Fator Oceânico:** **Indonésia** e **Egito** apresentam aumento do nível do mar acima da média global (3.41mm e 3.09mm, respectivamente). Para a Indonésia (arquipélago) e Egito (Delta do Nilo), milímetros a mais representam riscos existenciais de erosão costeira e salinização, justificando seus altos índices de risco (acima de 57).
3.  **Média vs. Extremo:** O fato de a maioria desses países ter uma temperatura média *menor* que a global reforça que o *Climate Risk Index* é uma métrica complexa. Ele captura a **sensibilidade** do país a desvios, provando que um aumento pequeno em uma região temperada pode ser mais devastador economicamente do que o calor constante em uma região já adaptada.

**Conclusão da Questão 3:**
A vulnerabilidade climática é democrática e atinge tanto economias centrais (Europa) quanto emergentes (Ásia/África). O risco é impulsionado mais pela geografia (nível do mar na Indonésia/Egito) e exposição a eventos extremos do que apenas pela média termométrica.

### Pergunta 4: Impacto Regional
**Questão:** Qual continente apresenta a maior média de Emissões de CO₂ e isso se reflete em temperaturas mais altas?

**Resultado Técnico:**
A tabela abaixo classifica os continentes por volume médio de emissões e suas respectivas temperaturas médias.

| Ranking | Continente | Média Emissões CO₂ (Mt) | Média Temperatura (°C) |
| :--- | :--- | :--- | :--- |
| **1º** | **Asia** | **583.90** | 22.52 |
| **2º** | **North America** | 583.64 | 22.58 |
| **3º** | **Africa** | 553.54 | 21.99 |
| **4º** | **South America** | 550.75 | **22.82 (Mais Quente)** |
| **5º** | **Europe** | 541.30 | 21.86 (Mais Frio) |
| **6º** | **Oceania** | 530.62 | 22.71 |

**Discussão e Análise:**
A análise regional expõe uma **assimetria entre poluição e aquecimento local**:

1.  **Os Grandes Emissores:** Ásia e América do Norte lideram o ranking de emissões, praticamente empatados (~583 Mt). Isso reflete a intensa atividade industrial e econômica dessas regiões no Hemisfério Norte.
2.  **A Vítima Geográfica:** A América do Sul aparece apenas em 4º lugar nas emissões, mas registra a **maior temperatura média global (22.82°C)**. Similarmente, a Oceania é o continente que menos emite (530 Mt), mas é o segundo mais quente (22.71°C).
3.  **O Fator Latitude:** A Europa, mesmo emitindo volumes próximos aos da América do Sul e África, mantém a menor média de temperatura (21.86°C), protegida por sua latitude mais alta.

**Conclusão da Questão 4:**
Ser o maior poluidor (Ásia/América do Norte) não significa ser o local mais quente. O Hemisfério Sul (América do Sul/Oceania) sofre com temperaturas mais altas devido a fatores geográficos e oceânicos, independentemente de emitirem menos CO₂ que seus vizinhos do Norte.

---

### Conclusão Geral do Projeto
Este MVP demonstrou que a vulnerabilidade climática é um fenômeno **sistêmico e não-linear**. Através do pipeline de dados construído, refutamos a hipótese de que "países que mais poluem sofrem mais aquecimento imediato".

**Principais Descobertas:**
1.  **Ausência de Correlação Local Imediata:** Emissões de CO₂ não geram aquecimento instantâneo no mesmo ano/local (Correlação de Pearson ~0). O problema é acumulativo.
2.  **O Paradoxo da Riqueza e Risco:** Países desenvolvidos (Itália, Alemanha) lideram o índice de risco climático, provando que infraestrutura complexa pode ser mais sensível a eventos extremos do que se imaginava.
3.  **Assimetria Hemisférica:** O Hemisfério Norte emite mais (indústria), mas o Hemisfério Sul registra médias de temperatura superiores (geografia).

O projeto atingiu seu objetivo de desfragmentar a visão climática, provando que a análise de dados é fundamental para desmistificar o senso comum sobre as mudanças climáticas.

## 6. Autoavaliação

### Atingimento dos Objetivos
O projeto atingiu 100% dos objetivos propostos. Foi possível construir um pipeline completo no Databricks, desde a ingestão de dados brutos até a geração de insights analíticos. As 4 perguntas de negócio foram respondidas com dados concretos, revelando que a vulnerabilidade climática não segue uma correlação linear simples com as emissões locais.

### Dificuldades Encontradas
O principal desafio foi o tratamento da qualidade dos dados na camada Prata, especificamente a normalização dos nomes das colunas e a garantia de tipagem correta para permitir cálculos estatísticos (como a correlação de Pearson) sem erros de execução no Spark. A adaptação à sintaxe do PySpark para agregações complexas também exigiu uma curva de aprendizado.

### Próximos Passos
Para evoluir este MVP em um portfólio de produção, os próximos passos seriam:
1.  **Automação:** Orquestrar os notebooks via Databricks Workflows ou Airflow para execução diária.
2.  **Enriquecimento:** Cruzar estes dados com indicadores econômicos (PIB) para calcular a "eficiência de carbono" de cada país.
3.  **Dashboard:** Conectar o Power BI diretamente à tabela `silver_climate_data` para visualização interativa externa.


---
*Desenvolvido por Henrique.*
