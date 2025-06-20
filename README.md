# Crossfit
DOCUMENTATION IN THE   NOTION: https://bolder-ice-30c.notion.site/Projeto-An-lise-de-Alunos-de-Crossfit-20a4a17cfd55804496c7ef3e34bd8f48?source=copy_link

<img src="https://github.com/dunaoki/Imagens/blob/main/cross.png" alt="Banner" width="800"/>


# 📊 Projeto: Análise de Alunos de Crossfit

### 🔎 Visão Geral

Este projeto foi desenvolvido com o objetivo de analisar o comportamento de alunos em uma academia de Crossfit, utilizando ferramentas de **BI (Business Intelligence)** para extrair insights relevantes sobre **frequência, cancelamentos, planos contratados, perda de peso** e o impacto financeiro geral.

---

### 🛠️ Ferramentas e Tecnologias Utilizadas

- **Power BI** – Visualização interativa de dados
- **Power Query** – Processo de ETL (extração, transformação e carregamento)
- **DAX (Data Analysis Expressions)** – Criação de medidas e cálculos dinâmicos
- **CSV** – Fonte de dados original

---

### 🔄 Processo de ETL com Power Query

**1. Extração dos dados:**

[Importação de um arquivo `.csv` contendo informações dos alunos, planos e status (ativo ou cancelado).](https://www.notion.so/Importa-o-de-um-arquivo-csv-contendo-informa-es-dos-alunos-planos-e-status-ativo-ou-cancelado-20a4a17cfd5580c08f40cf5a59d7bcf1?pvs=21)

**2. Transformação:**

- Normalização dos nomes das colunas.
- Conversão de tipos de dados (por exemplo, frequência como número inteiro, status como texto categórico).

[Criação de colunas calculadas, como **"Perda de Peso Total"** e **"Plano por Ano"**.](https://www.notion.so/Cria-o-de-colunas-calculadas-como-Perda-de-Peso-Total-e-Plano-por-Ano-20b4a17cfd5580ecb741f774467e4861?pvs=21)

[Criação de tabela Dcalendario e relacionando tabelas.](https://www.notion.so/Cria-o-de-tabela-Dcalendario-e-relacionando-tabelas-20b4a17cfd558044b1c3ff1ba0c38ce5?pvs=21)

**3. Limpeza:**

- Filtragem de registros nulos.
- Padronização de status ("cancelado" vs "ativo").
- Junção de tabelas com lookup para detalhamento dos planos e valores.

---

### 📐 Métricas Criadas com DAX

- **Total de Alunos:**
    
    ```markdown
    DAX
    TotalAlunos = DISTINCTCOUNT(dados_academia_crossfit[nome])
    
    ```
    
- **DimCalendario:**
    
    ```markdown
    DAX
    **DCalendario** = CALENDAR(MIN(dados_academia_crossfit[Data Inicial]), MAX(dados_academia_crossfit[Data Final]))
    
    Ano = YEAR(**DCalendario[Date])
    Mes = MOUNTH(DCalendario[Date])**
    ```
    
- **Contagem Frequencia por Status:**
    
    ```markdown
    DAX
    FrequenciaComStatus = 
    IF ( SELECTEDVALUE(dados_academia_crossfit[Status]) = " cancelado", "cancelado",
    FORMAT (SUM(dados_academia_crossfit[Frequencia Semanal]), "#,##0"))
    ```
    
- **Contagem por Plano e Ano:**
    
    ```markdown
    DAX
    Perda de Peso =
    IF(ISBLANK([peso atual]),0,
    [Peso inicial] - [peso atual])
    
    ```
    

---

### 📈 Visualizações Criadas

- **Cartões de KPI:**
    - Total de alunos ativos/cancelados
    - Soma de receita gerada
- **Tabela de Dados:**
    - Nome dos alunos, frequência, status e perda de peso
    - Análise Temporal do mês anterior

```markdown
# calculando o faturamento do mês anterior
Last Mes = 
CALCULATE([valor],
DATEADD(dcalendario[date],-1,MONTH))
```

```markdown
# comparando o faturamento atual com o mês anterior
Last Mes delta= [valor] - [last Mes]
```
- **Gráfico de Linhas:**
    - Evolução de planos contratados por ano (Mensal, Semestral, Anual)
    - - tem um tooltip de análise do mesmo mês do ano anterior
    
    ![Captura de Tela 2025-06-20 às 16.51.58.png](attachment:bbf17f4d-a432-436f-8f72-4de0ab0529cd:Captura_de_Tela_2025-06-20_as_16.51.58.png)
    

```markdown
#calculando o valor do mesmo mês do ano anterior 
MoM= 
CALCULATE([valor] ,SAMEPERIODLASTYEAR(dcalendario[date]))
```

```markdown
#calculando a diferença de valor do mês atual com do mesmo mês do ano anterior
MoM delta = [valor] - [MoM]
```
- **Gráfico de Barras Horizontais:**
    - Comparativo entre planos com base no status de matrícula

---

### 🔍 Insights Gerados

- Alunos com planos **mensais** representam a maior parte dos contratos ativos.
- A perda de peso tende a ser maior entre alunos com **frequência mais alta**.
- O número de **cancelamentos aumentou em 2025**, sugerindo a necessidade de estratégias de retenção.
- Planos **anuais** demonstraram maior queda de adesão, o que pode indicar uma preferência por opções mais flexíveis.

---

### 💡 Considerações e Ações Sugeridas

- Investir em programas de fidelização para reter alunos com planos anuais.

[Ofertas](https://www.notion.so/Ofertas-20a4a17cfd5580779d20e3f17f28ce1b?pvs=21)

- Oferecer benefícios progressivos para alunos com maior frequência.
- Criar planos personalizados baseados na evolução de peso e metas dos alunos.
- Realizar entrevistas com alunos cancelados para entender motivos e reduzir churn.

---

### 💼 Habilidades Demonstradas

- ✅ Manipulação e limpeza de dados com Power Query
- ✅ Modelagem de dados eficiente
- ✅ Criação de KPIs e cálculos complexos com DAX
- ✅ Storytelling com dados usando visualizações estratégicas
- ✅ Aplicação de lógica de negócios em contextos reais
