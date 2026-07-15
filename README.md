# 📊 Incentivos Argentina — Dashboard Power BI

Dashboard em **Power BI** para acompanhamento e gestão de **incentivos comerciais** (Sell In, Forecast, Quiebres/Rupturas e Pagamento de Incentivos) da operação na **Argentina**, com visões consolidadas (Overview / KAM) e visões de campo (Field / EVV / Promotor).

---

## 🧾 Sumário

- [Visão geral](#-visão-geral)
- [Páginas do relatório](#-páginas-do-relatório)
- [Modelo de dados](#-modelo-de-dados)
- [Principais métricas (DAX)](#-principais-métricas-dax)
- [Filtros e segmentações](#-filtros-e-segmentações)
- [Como usar](#-como-usar)
- [Requisitos](#-requisitos)
- [Estrutura do repositório](#-estrutura-do-repositório)
- [Roadmap / próximos passos](#-roadmap--próximos-passos)

---

## 🔎 Visão geral

O arquivo `Incentivos_Argentina.pbix` consolida os dados de vendas, forecast e apuração de incentivos por canal, agente/KAM e promotor de campo (EVV), permitindo:

- Acompanhar a **evolução de Sell In vs Forecast** por período (`AnoMes`);
- Medir o **percentual de atingimento** de vendas e a ocorrência de **quiebres** (rupturas de estoque/atendimento);
- Calcular o **valor de pagamento de incentivos** por canal, agente comercial, KAM, brand e promotor;
- Dar visibilidade separada para o time **corporativo/KAM** (visão gerencial) e para o time de **campo/EVV** (execução e adherência do promotor em ponto de venda).

---

## 🗂 Páginas do relatório

| # | Página | Objetivo |
|---|--------|----------|
| 1 | **Overview** | Visão executiva geral: cards de Sell In, Forecast acumulado, % de variação Sell In vs Forecast, gráfico combinado (linha + coluna) de Sell In vs Forecast por mês, gráfico 100% empilhado de participação por Brand, e pivot table detalhada por Sales Office / Brand / Agente. Contém slicers de período, agente (KAM), EVV, sales office e brand. |
| 2 | **KAM Incentivos** | Pivot table detalhada por Sales Office, Brand e Agente com as métricas de vendas, atingimento, quiebres e o **valor de pagamento de incentivo** (por pessoa/brand, por canal e total), voltada ao acompanhamento do KAM. |
| 3 | **Field Overview** | Visão de campo: tabelas com o desempenho por Agente/Canal/Brand e uma pivot table específica de **EVV** (Execução em Ponto de Venda / Visita), trazendo Forecast, Sell In, % de atingimento e valor de pagamento por EVV. |
| 4 | **Field Incentivos** | Apuração final do incentivo do time de campo: Forecast, Sell In, % atingimento, e o detalhamento do pagamento (**Valor Pago EVV**, **Valor Pago EVV Adherência**, **Valor Pago EVV Execução** e **Pago Total**) por Canal, EVV, Promotor e Brand. |

> As páginas navegam entre si através de botões de ação (*action buttons*) e possuem *bookmarks* configurados (ex.: filtro "Sem Promotor") para tratar cenários sem promotor cadastrado.

---

## 🧮 Modelo de dados

Tabelas identificadas no modelo (via consultas dos visuais):

| Tabela | Papel no modelo |
|--------|------------------|
| `dCalendar` | Dimensão de calendário / período (`AnoMes`) |
| `dKAM` | Dimensão de KAM / estrutura comercial (Agente, Sales Office) |
| `dEVV/Promotor` | Dimensão de campo: EVV e Promotor |
| `de-para Prod` | Tabela de de-para de produtos, usada para mapear o **Brand de Incentivos** (`P-BRAND INCENTIVOS`) |
| `fForecast` | Fato de Forecast (previsão de vendas) |
| `_Medidas` | Tabela dedicada às **medidas DAX** (measure table) |

**Principais colunas utilizadas nos visuais:**

- `AnoMes` — período (ano/mês)
- `Canal` — canal de venda
- `EVV` — identificador de execução/visita em campo
- `Promotor` — promotor responsável
- `O-Agent` — agente comercial
- `O-Sales Office (Sold-to)` — filial/escritório de venda (sold-to)
- `P-BRAND INCENTIVOS` — marca (brand) elegível a incentivo
- `Cum Forecast` — forecast acumulado

---

## 📐 Principais métricas (DAX)

Medidas centrais (tabela `_Medidas`) utilizadas nos visuais do relatório:

**Vendas, Forecast e Atingimento**
- `Sales Ajustado` / `Sales Ajustado EVV`
- `Forecast Ajustado` / `Forecast EVV`
- `% Sales`
- `% VAR SellIn vs Forecast`
- `Quiebres Ajustado`
- `% Sales + Quiebres` / `% Sales + Quiebres EVV`
- `% Range Result SI` / `% Range Result SI EVV`
- `% Alcance Canal`

**Execução e adherência de campo (EVV)**
- `Ejecución`
- `Resultado Adherencia EVV`

**Pagamento de incentivos**
- `Valor Pago (Pessoa x P-BRAND)`
- `Valor Pago Canal`
- `Valor Pago Total`
- `Valor Pago EVV`
- `Valor Pago EVV Adherencia`
- `Valor Pago EVV Execucao`
- `Pago Total`

> As fórmulas DAX completas ficam armazenadas no modelo de dados compactado do `.pbix` e podem ser revisadas diretamente no Power BI Desktop (guia *Modelagem → Medidas*).

---

## 🎛 Filtros e segmentações

Slicers disponíveis por página:

- **Overview:** Período (`AnoMes`), Agente (`O-Agent`), EVV, Sales Office, Brand (`P-BRAND INCENTIVOS`)
- **Field Overview (campo):** Canal, EVV, Promotor, Brand, Período (`AnoMes`)

---

## 📁 Estrutura do repositório

```
.
├── Incentivos_Argentina.pbix   # Arquivo principal do dashboard
└── README.md                   # Este documento
```

---

## 🗺 Roadmap / próximos passos

- [ ] Documentar o dicionário de dados completo (todas as colunas das dimensões)
- [ ] Adicionar prints/screenshots das páginas no README
- [ ] Publicar o relatório no Power BI Service com atualização automática agendada
- [ ] Criar changelog de versões do `.pbix`

---

## 📄 Licença

Uso interno / corporativo. Ajuste esta seção conforme a política de dados e confidencialidade da sua organização (este dashboard contém informações comerciais sensíveis de incentivos).
