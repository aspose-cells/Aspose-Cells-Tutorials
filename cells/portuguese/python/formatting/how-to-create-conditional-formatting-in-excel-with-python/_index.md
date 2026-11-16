---
category: general
date: 2026-11-16
description: Crie formatação condicional no Excel usando Python. Aprenda a adicionar
  um intervalo de formatação condicional, destacar datas e criar uma pasta de trabalho
  programaticamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: pt
lastmod: 2026-11-16
og_description: Crie formatação condicional no Excel com Python. Este tutorial mostra
  como adicionar um intervalo de formatação condicional, destacar datas e gerar uma
  pasta de trabalho.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Crie formatação condicional no Excel com Python – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Como criar formatação condicional no Excel com Python
url: /pt/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar formatação condicional no Excel com Python

Se você precisa **criar formatação condicional** em um arquivo Excel enquanto trabalha em Python, este guia mostra exatamente como fazer isso. Você aprenderá a **criar excel workbook python**‑style, definir um intervalo de formatação e destacar datas sem sair do IDE.

A formatação condicional permite sinalizar visualmente células que atendem a critérios específicos — perfeito para dashboards, relatórios ou planilhas de validação de dados. Ao final deste tutorial você terá uma planilha totalmente funcional que colore células datadas como “Ontem” em rosa, enquanto o restante do intervalo permanece verde.

## O que você vai conseguir

* Construir uma nova planilha do zero.  
* Adicionar uma coleção de formatação‑condicional para um bloco de células específico.  
* Aplicar uma regra **TIME_PERIOD** que destaca datas (o cenário “como destacar datas”).  
* Salvar o arquivo como uma planilha XLSX pronta para processamento posterior.

**Pré‑requisitos**  
* Python 3.8+  
* Pacote Python `aspose-cells` (`pip install aspose-cells`)  
* Familiaridade básica com o módulo `datetime` do Python  

---

## Como criar formatação condicional em Python

O primeiro passo é configurar a planilha e a aba que receberá as regras de formatação.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Por que isso importa** – `Workbook` é o ponto de entrada para todas as operações do Excel. Criar a planilha programaticamente substitui a etapa manual “Arquivo → Novo”, permitindo pipelines de relatórios automatizados.

---

## Preparando a coleção de formatação‑condicional – adicionar intervalo de formatação condicional

Em seguida definimos o bloco de células que receberá a regra. Neste exemplo o intervalo é **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explicação** – `conditional_formattings.add` registra uma nova coleção vinculada à string de endereço. A primeira condição (`conds[0]`) funciona como um estilo “padrão”; a regra posterior o substituirá quando seus critérios forem atendidos.

---

## Adicionando uma condição TIME_PERIOD – como destacar datas

Agora adicionamos a lógica que identifica datas de “Ontem” e as pinta de rosa.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Por que usar TIME_PERIOD?** – Aspose.Cells fornece enumerações internas como `YESTERDAY`, `TODAY` e `LAST_WEEK`. Elas avaliam o valor de data da célula em relação à data atual do sistema, eliminando a necessidade de fórmulas personalizadas.

---

## Populando dados de exemplo – demonstrar a regra

Para ver a formatação em ação inserimos uma data que corresponde à regra e outra que não corresponde.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Observação sobre caso extremo** – A regra `TIME_PERIOD` funciona apenas com datas *reais*. Se uma célula contiver texto (por exemplo, “N/A”), a regra será ignorada, evitando alterações de cor inesperadas.

---

## Salvando a planilha – add conditional formatting python

Por fim, gravamos a planilha no disco. O arquivo pode ser aberto em qualquer programa de planilhas para verificar as cores.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Resultado esperado**  

| I19 (verde → rosa) | J19 (verde) | K19 (verde) |
|--------------------|------------|------------|
| 30/07/2008 (ontem) | – | – |
| **I20**: rótulo “Ontem” | – | – |
| I21‑K21 (verde)    | – | – |

A célula **I19** aparece com fundo rosa porque sua data corresponde ao período “Ontem”, enquanto **K20** permanece verde.

---

## Perguntas frequentes e dicas práticas

* **Posso usar um intervalo de datas personalizado em vez de um período interno?**  
  Sim. Substitua `condition.time_period` por `condition.formula1 = "TODAY()-1"` e defina `condition.type = FormatConditionType.FORMULA`.

* **E se minha planilha já contiver dados?**  
  Use `worksheet.cells.import_data` para carregar dados em massa antes de adicionar a coleção de formatação condicional.

* **Desempenho com planilhas grandes?**  
  Adicionar muitas condições pode deixar a renderização mais lenta. Agrupe células com a mesma regra em um único intervalo (por exemplo, “A1:C1000”) para manter o número de condições baixo.

* **Compatibilidade entre plataformas?**  
  O arquivo XLSX gerado segue o padrão Office Open XML, portanto funciona em aplicações de planilhas no Windows, macOS e Linux.

---

## Conclusão

Agora você sabe como **criar formatação condicional** em uma planilha Excel usando Python. O tutorial abordou a criação da planilha, a definição de um **add conditional formatting range**, a aplicação de uma regra **how to highlight dates**, e a gravação do arquivo — tudo com a abordagem **add conditional formatting python** fornecida pelo Aspose.Cells.

A partir daqui você pode:

* Expandir o conjunto de regras com outros valores `TimePeriodType` (por exemplo, `TODAY`, `LAST_MONTH`).  
* Combinar múltiplas condições no mesmo intervalo para pistas visuais mais ricas.  
* Integrar esse fluxo de trabalho em pipelines de relatórios automatizados ou serviços web.

Boa codificação, e sinta-se à vontade para experimentar diferentes cores, intervalos e lógica de datas para atender às suas necessidades de relatório!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}