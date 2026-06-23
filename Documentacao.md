# 📊 Dashboard de Análise do Mercado de GPUs

Este repositório contém a estrutura de modelação de dados e o relatório em Power BI para análise de mercado, especificações técnicas, preços e receitas estimadas de GPUs (Unidades de Processamento Gráfico).

## 🗂️ Estrutura do Projeto

* `model.bim`: Definição do Modelo Semântico (tabular) com tabelas, relacionamentos e medidas DAX desenvolvidas.
* `report.json`: Estrutura de layout, configurações visuais e páginas do relatório Power BI.

---

## 📐 Modelo de Dados (Esquema em Estrela)

O projeto segue as melhores práticas de modelação em **Star Schema** (Esquema em Estrela), separando os factos de negócio das suas respetivas dimensões para otimizar a performance dos cálculos DAX.

### 📈 Tabela de Factos
* **`tab_fato`**: Contém os dados transacionais e técnicos de cada GPU. Inclui colunas como `Direct_X`, `Memory_Bandwidth`, `Shader`, `TMUs`, `Texture_Rate`, `release_price` e `release_date`.

### 🧭 Tabelas de Dimensão
* **`dim_GPU/pruduto`**: Detalhes do produto (Arquitetura, Fabricante, Tipo de Memória, Nome do Modelo).
* **`dim_fabricante`**: Cadastro de Fabricantes/Brands do ecossistema.
* **`dim_process`**: Informações sobre a litografia e tecnologia do processo de fabrico (ex: nanómetros).
* **`dim_financeiro`**: Segmentações de preço de lançamento.
* **`dim_calendario`**: Tabela de tempo gerada por DAX (`CALENDAR`) com hierarquias de Ano, Mês, Nome do Mês, Trimestre e AnoMes para suporte a análises temporais (Time Intelligence).

---

## 🧮 Métricas e Medidas DAX

Todas as medidas de negócio foram centralizadas numa tabela dedicada chamada **`Medidas`**. Abaixo estão descritas as principais fórmulas implementadas:

### 🔹 Métricas Básicas
* **Total de GPUs**: 
    ```dax
    Total de GPUs = COUNTROWS(tab_fato)
    ```
* **Preço Médio**:
    ```dax
    Preco Medio = AVERAGE(tab_fato[release_price])
    ```
* **Receita Total Estimada**:
    ```dax
    Receita Total Estimada = SUM(tab_fato[release_price])
    ```
* **Qtd Fabricantes**:
    ```dax
    Qtd Fabricantes = DISTINCTCOUNT(tab_fato[Manufacturer_ID])
    ```
* **Memória Média (MB)**:
    ```dax
    Memoria Media MB = AVERAGE(tab_fato[Memory])
    ```

### 📅 Análises Temporais (Time Intelligence)
* **Receita YTD (Year-to-Date)**: Acumulado de receita do ano corrente.
    ```dax
    Receita YTD = TOTALYTD(SUM(tab_fato[release_price]), dim_calendario[Date])
    ```
* **Receita MTD (Month-to-Date)**: Acumulado de receita do mês corrente.
    ```dax
    Receita MTD = TOTALMTD(SUM(tab_fato[release_price]), dim_calendario[Date])
    ```
* **Lançamentos Ano Anterior**: Quantidade de GPUs lançadas no mesmo período do ano anterior.
    ```dax
    Lancamentos Ano Anterior = CALCULATE(COUNTROWS(tab_fato), SAMEPERIODLASTYEAR(dim_calendario[Date]))
    ```

### 🔍 Inteligência de Mercado Avançada
* **Menor Preço Componente Equivalente**: Identifica o menor preço entre GPUs com o mesmo tipo e capacidade de memória (removendo filtros de fabricante para permitir comparações competitivas).
    ```dax
    Menor Preco Componente Equivalente = 
    CALCULATE(
        MIN(tab_fato[release_price]),
        ALLEXCEPT(tab_fato, tab_fato[Memory_Type_ID], tab_fato[Memory])
    )
    ```
* **Preço Médio Período Recente**: Média de preço das GPUs lançadas nos últimos 24 meses face à data mais recente da base.
    ```dax
    Preco Medio Periodo Recente = 
    CALCULATE(
        AVERAGE(tab_fato[release_price]),
        FILTER(
            ALL(dim_calendario),
            dim_calendario[Date] > EDATE(MAX(tab_fato[release_date]), -24)
        )
    )
    ```
* **Preço Médio Período Histórico**: Média de preço das GPUs lançadas antes dos últimos 24 meses.
    ```dax
    Preco Medio Periodo Historico = 
    CALCULATE(
        AVERAGE(tab_fato[release_price]),
        FILTER(
            ALL(dim_calendario),
            dim_calendario[Date] <= EDATE(MAX(tab_fato[release_date]), -24)
        )
    )
    ```
* **Variação Percentual Preço**: Compara a evolução do preço médio entre o período histórico e o recente.
    ```dax
    Variacao Percentual Preco = 
    VAR PrecoRecente = [Preco Medio Periodo Recente]
    VAR PrecoHistorico = [Preco Medio Periodo Historico]
    RETURN
        DIVIDE(PrecoRecente - PrecoHistorico, PrecoHistorico, BLANK())
    ```

---

## 🎨 Design e Funcionalidades do Relatório

O relatório foi desenvolvido utilizando o tema nativo moderno **CY24SU08** e foca-se na experiência do utilizador:
* **Alinhamento Vertical Topo**: Configuração de layout limpa para dashboards analíticos.
* **Interações Avançadas**: Filtros cruzados (*drill-through*) nativos ativos para exploração detalhada de especificações.
* **Dicas de Ferramenta Avançadas (*Enhanced Tooltips*)**: Configuração de contexto para apresentar métricas rápidas ao passar o rato sobre os gráficos.

## 🛠️ Como Utilizar este Repositório

1.  **Power BI Desktop / Developer Mode**: Podes utilizar estas definições JSON/BIM em conjunto com o Power BI Project (`.pbip`) ou ferramentas externas como o **Tabular Editor** e o **VS Code**.
2.  **Atualização de Dados**: O modelo está preparado para o carregamento em modo *Import*. Certifica-se de que mapeias a origem da tabela `tab_fato` com as credenciais corretas para o processamento.