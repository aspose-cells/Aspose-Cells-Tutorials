---
category: general
date: 2026-09-15
description: Aprenda como aplicar formatação condicional por período de tempo e salvar
  a pasta de trabalho como XLSX com Aspose.Cells em Python. Inclui código passo a
  passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: pt
lastmod: 2026-09-15
og_description: Aplique formatação condicional de período de tempo no Excel usando
  Python e salve a pasta de trabalho como XLSX. Siga este guia completo para Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Aplicar formatação condicional por período de tempo no Excel com Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Como aplicar formatação condicional de período de tempo no Excel usando Python
url: /pt/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como aplicar formatação condicional por período de tempo no Excel usando Python

Se você precisa de **formatação condicional por período de tempo** em um arquivo Excel, este tutorial mostra exatamente como fazer isso com Python. Você verá um exemplo completo e executável que cria uma pasta de trabalho, destaca as datas de ontem e **salva a pasta de trabalho como XLSX** em apenas algumas linhas de código.

A formatação condicional é uma maneira poderosa de chamar a atenção para dados que atendem a uma regra específica. Neste guia focamos no período de tempo “Yesterday”, mas o mesmo padrão funciona para outros períodos incorporados, como Today, LastWeek e NextMonth. Ao final do tutorial você será capaz de **how to create excel workbook python**‑style scripts prontos para produção.

## Pré‑requisitos

- Python 3.8+ instalado  
- Pacotes `aspose-cells` e `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Familiaridade básica com a sintaxe Python  

Nenhuma instalação adicional do Office é necessária porque o Aspose.Cells lida com a geração do arquivo internamente.

## Formatação condicional por período de tempo com Aspose.Cells em Python

Esta seção percorre cada linha de código necessária para a tarefa principal. O bloco de código abaixo é o script completo; os comentários explicam o propósito de cada passo.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Por que cada passo importa

1. **Criar a pasta de trabalho** fornece um arquivo Excel em memória que pode ser manipulado sem abrir o Excel.  
2. **Definir o intervalo** (`I19:K20`) indica ao Aspose.Cells onde a regra se aplica, mantendo a lógica isolada.  
3. **Adicionar uma condição TIME_PERIOD** usa a enumeração incorporada `TimePeriodType.YESTERDAY` da Aspose. Isso evita cálculos manuais de datas e atualiza automaticamente quando o arquivo é aberto em outro dia.  
4. **Definir o estilo** (`background_color` e `pattern`) determina como as células destacadas aparecerão. Usar `Color.pink` torna a regra fácil de identificar.  
5. **Escrever datas de exemplo** com o formato numérico 30 garante que o Excel as exiba como datas curtas em vez de números seriais.  
6. **Ajustar automaticamente a coluna** melhora a legibilidade para quem abrir o arquivo mais tarde.  
7. **Salvar como XLSX** produz um arquivo amplamente compatível que pode ser aberto no Excel, Google Sheets ou qualquer programa de planilha moderno.

## Como criar pasta de trabalho Excel no estilo Python com Aspose.Cells

O script acima já demonstra os passos mínimos para **how to create excel workbook python**. Na prática, você pode querer:

- Adicionar várias planilhas (`workbook.worksheets.add("Report")`).  
- Popular grandes tabelas de dados com loops ou DataFrames pandas (`worksheet.cells.import_data_table`).  
- Aplicar formatação adicional (fontes, bordas) usando `cell.get_style()`.

Todas essas ações seguem o mesmo padrão: obter o objeto, modificar suas propriedades e chamar `set_style` ou `save`.

## Adicionar formatação condicional Python – outros padrões úteis

Além do exemplo “Yesterday”, o Aspose.Cells suporta vários tipos de formatação condicional:

| FormatConditionType | Caso de uso típico |
|---------------------|--------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Fórmulas personalizadas (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Comparações simples (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Escalas de cores gradientes |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Visualização de barra dentro da célula |

Para **add conditional formatting python** para um limite numérico, você substituiria `FormatConditionType.TIME_PERIOD` por `FormatConditionType.CELL_VALUE` e definiria `condition.operator_type` e `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Salvar pasta de trabalho como XLSX – boas práticas

Ao **save workbook as xlsx**, considere:

- **Especificar o `SaveFormat` correto** (`SaveFormat.XLSX`) para evitar formatos legados.  
- **Usar um nome de arquivo determinístico** se o script for executado em loop (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Fechar recursos** (`workbook.dispose()`) em serviços de longa execução para liberar memória nativa.

O exemplo já usa `SaveFormat.XLSX`, que produz uma pasta de trabalho moderna, baseada em zip, que mantém todas as regras de formatação condicional.

## Destacar ontem no Excel – passos de verificação

Depois de executar o script, abra `TimePeriodExample.xlsx`:

1. As células `I19` e `K20` contêm as datas `30‑07‑2008` e `03‑08‑2008`.  
2. A célula `I20` mostra o texto “Yesterday”.  
3. Se você alterar a data do sistema para **30 de julho de 2008** e reabrir o arquivo, as células com datas correspondentes são preenchidas automaticamente com rosa.  
4. Alterar a data do sistema para qualquer outro dia remove o preenchimento rosa, confirmando que a regra reage à lógica de **time period conditional formatting**.

## Armadilhas comuns e como evitá‑las

- **Falta do `aspose-pydrawing`** – a classe `Color` está neste pacote; esquecer de instalá‑lo gera um `ImportError`.  
- **Formato numérico incorreto** – usar o formato padrão General exibe números seriais (ex.: 39822). Sempre defina `style.number = 30` para datas curtas.  
- **Descompasso de intervalo** – o intervalo da formatação condicional deve incluir as células que você pretende destacar; caso contrário a regra não terá efeito.

## Dica profissional: reutilizar a rotina de formatação

Se você precisar da mesma regra “Yesterday” em várias pastas de trabalho, encapsule a lógica em uma função auxiliar:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Chame `apply_yesterday_highlight(worksheet, "A1:A10")` onde for necessário.

## Conclusão

Este guia mostrou como implementar **time period conditional formatting** no Excel usando Python, como **save workbook as XLSX** e como **highlight yesterday in Excel** com um único script reutilizável. Agora você tem uma base sólida para **add conditional formatting python** em qualquer projeto de automação, seja gerando relatórios diários, construindo dashboards ou preparando exportações de dados.

**Próximos passos**

- Explore outros valores de `TimePeriodType` como `TODAY` ou `LAST_WEEK`.  
- Combine múltiplas regras condicionais no mesmo intervalo para pistas visuais mais ricas.  
- Integre a geração da pasta de trabalho em um serviço web ou tarefa agendada.

Boa codificação e aproveite a clareza visual que a formatação condicional traz para sua automação Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}