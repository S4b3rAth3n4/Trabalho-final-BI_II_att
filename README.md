# Análise de Preços de GPUs

## Descrição do Projeto

Este projeto tem como objetivo desenvolver um dashboard de Business Intelligence para análise do mercado de placas de vídeo (GPUs), utilizando dados de produtos, fabricantes, preços e características técnicas.

Através do Power BI, o projeto busca identificar padrões de preços, evolução tecnológica dos modelos e comportamento dos fabricantes, permitindo uma análise estratégica do mercado de GPUs.

O dashboard foi desenvolvido com foco em três principais análises: visão executiva do mercado, análise de tendências e comparação técnica/custo-benefício dos produtos.

---

# Problema de Negócio

O mercado de GPUs apresenta constantes mudanças relacionadas a preço, evolução tecnológica e lançamento de novos modelos. Essas variações dificultam a análise sobre quais fabricantes possuem maior presença, como os preços evoluem e quais produtos apresentam melhor posicionamento no mercado.

O projeto busca responder perguntas como:

* Como os preços das GPUs variam ao longo do tempo?
* Quais fabricantes possuem maior participação no mercado?
* Como as características técnicas das placas evoluíram?
* Quais modelos apresentam melhor relação entre preço e especificações?

---

# Dataset

**Nome do Dataset:** All_GPUs

**Fonte:** Kaggle

Link:
https://www.kaggle.com/datasets/minhnhatvuong/all-gpus

O dataset contém informações sobre placas de vídeo, fabricantes, características técnicas e dados relacionados a preços e produtos.

Licença do dataset:
Não identificada.

---

# Modelo de Dados

O projeto utiliza um modelo dimensional organizado pelas seguintes tabelas:

## Tab_Fato

Contém informações principais relacionadas aos registros analisados:

* Tipo_Usuario_Alvo
* Chave do produto
* Chave do fabricante
* Chave de data
* Quantidade vendida
* Valor da venda
* Status do pedido (em validação)

---

## Dim_GPU / Produto

Contém informações técnicas das placas de vídeo:

* Architecture_ID
* Release_Price
* Memory
* Core_Speed
* Boost_Clock
* Max_Power
* ROPs
* Shader

---

## Dim_Fabricante

Responsável pelas informações das marcas:

* Manufacturer

---

## Dim_Calendário

Tabela utilizada para análises temporais:

* Data
* Ano
* Mês
* Trimestre

---

## Dim_Financeiro

Informações financeiras:

* Custo
* Estoque
* MSRP

*(Campos em validação)*

---

## Dim_Process

Informações sobre processo de fabricação:

* Nó de fabricação do chip

*(Campo de baixa prioridade/em validação)*

---

# Dashboard

O dashboard foi dividido em três páginas principais:

## 1. Visão Executiva do Mercado de GPUs

Apresenta uma visão geral do mercado através dos principais indicadores:

* Preço médio das GPUs;
* Total de modelos analisados;
* Distribuição de GPUs por fabricante;
* Evolução dos lançamentos.

---

## 2. Análise de Mercado e Tendências

Permite comparar fabricantes e observar padrões do mercado:

* Preço médio por fabricante;
* Evolução dos preços;
* Consumo energético;
* Comparação entre modelos.

---

## 3. Análise Técnica e Custo-Benefício das GPUs

Realiza uma análise detalhada dos produtos:

* Ranking de GPUs por preço;
* Comparação de especificações técnicas;
* Análise de memória;
* Relação entre preço e características.

---

# Principais KPIs

Os principais indicadores utilizados no projeto são:

* Preço Médio das GPUs;
* Total de Modelos de GPUs na Base;
* Distribuição de GPUs por Fabricante;
* Evolução dos lançamentos;
* Preço Médio por Fabricante;
* Consumo Médio de Energia;
* Ranking das GPUs por preço;
* Análise de memória das GPUs.

---

# Tecnologias Utilizadas

* Power BI Desktop
* Power BI Project (.pbip)
* GitHub

---

# Como abrir o projeto

1. Baixar ou clonar este repositório.
2. Abrir o arquivo `.pbip` utilizando o Power BI Desktop.
3. Caso necessário, atualizar as conexões dos dados.
4. Executar o dashboard.

---

# Autores

* Bernardo
* Bruno

Disciplina:
Business Intelligence II
