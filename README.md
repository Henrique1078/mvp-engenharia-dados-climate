# 🌍 Global Climate Change Data Analysis (2020-2025)

## 📌 Visão Geral
Este projeto é um MVP (Minimum Viable Product) desenvolvido como requisito para a pós-graduação em Ciência de Dados da PUC-Rio (Módulo: Engenharia de Dados).

O objetivo é construir um pipeline de dados completo (Coleta, Modelagem, Carga e Análise) em ambiente Cloud para investigar indicadores climáticos globais.

## 🎯 Objetivo do Projeto

### O Problema
As mudanças climáticas representam um dos maiores desafios globais, mas a análise isolada de métricas nem sempre revela a gravidade do impacto local. O problema que este projeto visa resolver é a **fragmentação da visão sobre a vulnerabilidade climática global**, integrando dados de temperatura, emissões, nível do mar e índices de risco.

### Perguntas de Negócio
O projeto busca responder às seguintes questões principais:

1.  **Tendência Temporal:** Qual é a tendência de variação da Temperatura Média global e por continente ao longo do período (2020-2025)?
2.  **Correlação Crítica:** Existe correlação entre o volume de Emissões de CO₂ de um país e o seu Aumento do Nível do Mar ou Temperatura?
3.  **Análise de Vulnerabilidade:** Quais são os Top 5 países com o maior *Climate Risk Index* e como seus indicadores se comportam comparados à média global?
4.  **Impacto Regional:** Qual continente apresenta a maior média de Emissões de CO₂ e isso se reflete em temperaturas mais altas?

## 📊 Dados
**Fonte:** Kaggle - Global Climate Change Data (2020–2025)
**Formato:** CSV
**Descrição:** Dados contendo temperatura média, emissões de CO2, aumento do nível do mar e índice de risco climático por país e ano.

## 🛠️ Tecnologias Utilizadas
* **Linguagem:** Python (PySpark & Pandas)
* **Plataforma:** Databricks Community Edition
* **Armazenamento:** DBFS (Databricks File System)
* **Versionamento:** Git & GitHub

## 📚 Catálogo de Dados (Data Dictionary)

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





---
*Desenvolvido por Henrique.*
