# Decisões de Modelagem

O projeto utiliza um modelo dimensional desenvolvido no Power BI.

A estrutura foi organizada separando informações em tabelas de fatos e dimensões, facilitando análises, filtros e criação de indicadores.

## Tabela Fato

A tabela fato concentra informações principais utilizadas nas análises.

Campos principais:

- Produto
- Fabricante
- Data
- Valores analisados


## Dimensão Produto/GPU

Contém características técnicas das placas:

- Arquitetura
- Memória
- Clock
- Consumo energético
- Preço


## Dimensão Fabricante

Armazena informações das marcas analisadas.


## Dimensão Calendário

Utilizada para análises temporais:

- Ano
- Mês
- Trimestre

Essa modelagem permite análises de preço, evolução tecnológica e comparação entre fabricantes.
