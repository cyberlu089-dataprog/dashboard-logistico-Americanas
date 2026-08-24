# dashboard-logistico-Americanas
Dashboard desenvolvido para o acompanhamento de logística e fretes das Lojas Americanas(2018 e 2019). Inclui modelagem Star Schema, análise de faturamento, distribuição geográfica por UF, perfil de frota e relatórios de custos de veículos via DAX avançado (TREATAS).  

"""# Dashboard de Logística e Fretes — Lojas Americanas

Este repositório contém o modelo de dados e o painel analítico no Power BI desenvolvido para o acompanhamento estratégico de entregas, faturamento de fretes, inteligência de frota e custos operacionais das Lojas Americanas.

---

## 📌 Visão Geral do Dashboard

O dashboard foi projetado para fornecer visibilidade completa da operação logística, agrupando indicadores-chave de desempenho (KPIs) e distribuições por tipo de veículo, geografia e linha do tempo.

### 📊 KPIs Principais
* **Entregas:** 80.501
* **Faturamento Frete:** R$ 201,319 Mi
* **Clientes Atendidos:** 1.000

### 📈 Análises Visuais
* **Entregas por Tipo de Veículo:** Gráfico de barras horizontais destacando a alocação por categoria de transporte (Toco, Truck, Carreta, VUC e 3/4).
* **Frete por Tipo de Veículo:** Gráfico de colunas detalhando a receita por frota (ex: Toco liderando com 26 Mil).
* **Fretes por UF:** Gráfico de rosca apresentando a participação por estado (SP: 32,42%, RJ: 24,54%, MG: 22,56%, ES: 20,48%).
* **Evolução Temporal:** Gráfico de área demonstrando o comportamento mensal dos fretes entre 2018 e 2019.

---

## 🏗️ Arquitetura e Modelo de Dados

O modelo adota uma estrutura em estrela (*Star Schema*) adaptada, integrando tabelas dimensão e fato para permitir filtros cruzados eficientes entre geografia, veículos e custos.

### Tabelas do Modelo

| Tabela | Tipo | Descrição |
| :--- | :--- | :--- |
| `dCliente1` | Dimensão | Cadastro de clientes com `ID Cliente`, `Cidade` e `UF`. |
| `dVeiculo2` | Dimensão | Cadastro da frota contendo `ID Veiculo`, `Placa`, `Marca`, `Tipo Veiculo` e `Baú`. |
| `fFrete3` | Fato | Registros de viagens contendo `Data`, `ID Cliente`, `ID Veiculo`, `Placa`, `Peso (KG)`, `Valor da Mercadoria` e `Valor do Frete Liquido`. |
| `fKmRodado4` | Fato | Registro de rodagem e custos contendo `ID Veiculo`, `Mês`, `Km percorridos`, `Gasto com Combustível`, `Manut.` e `Custos Fixos`. |

---

## 📐 Medidas DAX Utilizadas

Para contornar o relacionamento indireto entre os custos da frota e a localização geográfica dos clientes, foram desenvolvidas medidas DAX avançadas utilizando a função `TREATAS`:

```dax
// Cálculo da soma direta de todos os custos associados aos veículos
Custo Total = 
SUM(fKmRodado4[Gasto com Combustível]) +
SUM(fKmRodado4[Manut.]) +
SUM(fKmRodado4[Custos Fixos])
