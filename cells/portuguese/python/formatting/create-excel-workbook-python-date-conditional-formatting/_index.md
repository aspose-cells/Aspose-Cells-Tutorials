---
category: general
date: 2026-08-08
description: Criar pasta de trabalho Excel em Python e adicionar formatação condicional
  baseada em data. Guia passo a passo usando Aspose.Cells para destacar as células
  de ontem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: pt
lastmod: 2026-08-08
og_description: Crie uma pasta de trabalho Excel em Python com Aspose.Cells e aplique
  formatação condicional baseada em data para planilhas dinâmicas.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Criar arquivo Excel em Python – formatação condicional de data
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Criar formatação condicional de data em planilha Excel com Python
url: /pt/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar workbook Excel Python com formatação condicional de data

Se você precisa **criar Excel workbook Python** e destacar automaticamente células que correspondam a uma data específica, este tutorial mostra exatamente como fazer. Você aprenderá a aplicar **formatação condicional baseada em data** para que as datas de ontem fiquem em rosa, usando a biblioteca Aspose.Cells.

O guia percorre cada passo — desde a instalação do SDK até a gravação do arquivo final .xlsx — para que você possa copiar‑colar um exemplo funcional em seu próprio projeto. Nenhuma documentação externa é necessária; todo o código e as explicações estão contidos aqui.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8 ou mais recente instalado.
* Pacote `aspose-cells` (o wrapper Python para Aspose.Cells). Instale‑o com:
  ```bash
  pip install aspose-cells
  ```
* Familiaridade básica com Python e conceitos do Excel, como planilhas e estilos de célula.

> **Dica profissional:** Aspose.Cells funciona sem a necessidade de ter o Microsoft Excel instalado, tornando‑o ideal para automação server‑side.

## Etapa 1: Criar o workbook Excel em Python

A primeira tarefa é instanciar um novo workbook e obter a planilha padrão. Esse objeto representa todo o arquivo Excel e fornece acesso a linhas, colunas e APIs de formatação.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Criar o workbook é a base para qualquer manipulação posterior, seja adicionando dados, fórmulas ou regras de formatação.

## Etapa 2: Definir uma formatação condicional baseada em data

Agora adicionamos **formatação condicional baseada em data**. O enum `FormatConditionType.TIME_PERIOD` permite especificar períodos de tempo predefinidos, como Yesterday, Today ou LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Por que essa etapa importa: o Excel avalia a condição para cada célula no intervalo. Quando o valor de uma célula cai dentro do período definido (ontem), o estilo que atribuímos é aplicado automaticamente.

## Etapa 3: Preencher o intervalo com datas de exemplo

Para ver a regra em ação, escrevemos alguns objetos `datetime` nas células alvo. Um deles é deliberadamente definido para a data de ontem em relação ao sistema interno de datas do workbook.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

A linha `number = 30` indica ao Excel que exiba o valor usando seu formato de data curta padrão. Você pode mudar esse índice para qualquer formato numérico interno se preferir outra apresentação.

## Etapa 4: Ajustar a largura da coluna para legibilidade

Ajustar automaticamente a largura da coluna que contém as datas facilita a leitura da saída, especialmente quando o workbook é aberto no Excel ou em um visualizador.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Etapa 5: Salvar o workbook no disco

Por fim, grave o workbook como um arquivo .xlsx. Substitua `"YOUR_DIRECTORY"` por um caminho real em sua máquina.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Ao abrir `TimePeriodDemo.out.xlsx` no Excel, a célula **I19** aparecerá com fundo rosa porque seu valor corresponde à regra “Yesterday”, enquanto **K20** permanecerá sem alterações.

### Saída esperada

| I19 (data) | I20 (rótulo) | J19 | J20 | K19 | K20 (data) |
|------------|--------------|-----|-----|-----|------------|
| *2008‑07‑30* (fundo rosa) | Ontem | – | – | – | *2008‑08‑03* (sem formatação) |

A sombreamento rosa confirma que **formatação condicional baseada em data** funciona como esperado.

## Variações comuns e casos de borda

| Situação | Como adaptar o código |
|----------|-----------------------|
| **Realçar “Hoje” em vez de “Ontem”** | Alterar `condition.time_period = TimePeriodType.TODAY` |
| **Aplicar a regra a uma coluna inteira** | Usar `worksheet.get_range("A:A").format_conditions` |
| **Usar um intervalo de datas personalizado (ex.: últimos 7 dias)** | Substituir a condição de período‑de‑tempo por uma condição de fórmula: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Cores de fundo diferentes** | Definir `condition.style.background_color = Color.light_green` (ou qualquer `Color` que preferir) |
| **Executar no Linux sem exibição** | Aspose.Cells funciona totalmente em modo headless; nenhuma configuração extra necessária. |

## Exemplo completo, executável

Abaixo está o script completo que você pode executar tal‑como (após atualizar o diretório de saída). Todas as importações, comentários e noções básicas de tratamento de erros estão incluídos.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Executar o script gera um arquivo Excel onde a célula “Yesterday” é destacada automaticamente, demonstrando **create Excel workbook Python** combinado com **conditional formatting based on date**.

## Conclusão

Agora você sabe como **create Excel workbook Python** objetos, definir uma **formatação condicional baseada em data** e salvar o resultado.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}