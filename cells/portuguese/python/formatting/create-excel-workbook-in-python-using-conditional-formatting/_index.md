---
category: general
date: 2026-09-21
description: Aprenda a criar uma pasta de trabalho do Excel em Python, definir a cor
  de fundo das células e aplicar formatação condicional baseada em datas com o Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: pt
lastmod: 2026-09-21
og_description: Crie uma pasta de trabalho Excel em Python, defina a cor de fundo
  da célula e aplique formatação condicional baseada em datas usando Aspose.Cells.
  Siga o guia passo a passo.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Criar pasta de trabalho Excel em Python com formatação condicional
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Criar pasta de trabalho do Excel em Python usando formatação condicional
url: /pt/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel em Python usando formatação condicional

Se você precisa de scripts **create Excel workbook python** que realçam datas automaticamente, este guia mostra exatamente como fazer. Você verá como **set cell background color**, adicionar uma regra “Yesterday” e salvar o arquivo — tudo com Aspose.Cells para Python.

Trabalhar com arquivos Excel programaticamente costuma significar repetir a mesma lógica de formatação em várias planilhas. Ao final deste tutorial, você terá um padrão reutilizável para **excel conditional formatting python** que pode ser inserido em qualquer projeto.

## Pré-requisitos

- Python 3.8+ instalado  
- pacote `aspose-cells` (`pip install aspose-cells`)  
- Familiaridade básica com funções Python e o módulo datetime  

Nenhuma biblioteca adicional é necessária; Aspose.Cells lida com todas as operações do Excel.

## Etapa 1: Criar a pasta de trabalho e acessar a primeira planilha

O primeiro passo é **create excel workbook python** objetos e obter a planilha padrão. Isso fornece uma tela limpa para estilização adicional.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Por que isso importa:* `Workbook()` cria um arquivo Excel na memória. Acessar `worksheets[0]` evita codificar nomes de planilhas e funciona mesmo se o nome padrão mudar.

## Etapa 2: Auxiliar para adicionar uma formatação condicional TIME_PERIOD

Para manter o código organizado, encapsulamos a criação da formatação condicional em um auxiliar. Ele recebe um intervalo de células, uma cor de fundo e a regra de período de tempo desejada.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Por que isso importa:* O auxiliar abstrai as etapas repetitivas de criação de uma formatação condicional, facilitando a reutilização para outras regras baseadas em datas, como “Today” ou “Last Week”.

## Etapa 3: Aplicar a regra “Yesterday” a um intervalo

Agora usamos o auxiliar para realçar células que contêm a data de ontem. O intervalo `I19:K20` ficará **medium sea green** quando a condição for atendida.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Por que isso importa:* `TimePeriodType.YESTERDAY` faz parte da enumeração interna do Aspose.Cells, portanto você não precisa calcular datas manualmente. A biblioteca avalia a regra toda vez que a pasta de trabalho é aberta.

## Etapa 4: Preencher o intervalo com datas de exemplo

Para ver a regra em ação, escrevemos duas datas — uma que corresponde a “Yesterday” e outra que não corresponde. O estilo `number` `30` corresponde a um formato de data interno.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Por que isso importa:* Ao inserir datas concretas, você pode verificar que a formatação condicional funciona sem precisar abrir o arquivo em um dia específico.

## Etapa 5: Adicionar um rótulo descritivo e ajustar automaticamente a coluna

Um pequeno rótulo esclarece o propósito do intervalo formatado, e `auto_fit_column` torna a planilha legível.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Etapa 6: Salvar a pasta de trabalho

Finalmente, grave a pasta de trabalho no disco. A chamada `os.makedirs` garante que a pasta de destino exista.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Ao abrir *TimePeriodDemo.xlsx* você verá:

- A célula **I19** sombreada em **medium sea green** porque seu valor corresponde à regra “Yesterday”.  
- A célula **K20** mantém o fundo padrão porque sua data não satisfaz a condição.  

Isso demonstra **format cells by date** usando uma única linha de código Python.

## Exemplo completo, executável

Juntando todas as peças, aqui está o script completo que você pode copiar‑colar e executar:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Execute o script, abra o arquivo resultante e você verá a formatação condicional em ação.

## Variações comuns e casos de borda

| Variação | Como implementar | Quando usar |
|-----------|------------------|-------------|
| **Highlight “Today”** | Substitua `TimePeriodType.YESTERDAY` por `TimePeriodType.TODAY` | Painéis em tempo real |
| **Multiple ranges** | Chame `add_time_period` para cada intervalo, passando cores diferentes | Relatórios complexos |
| **Dynamic date range** | Use `TimePeriodType.LAST_7_DAYS` ou `TimePeriodType.NEXT_MONTH` | Relatórios contínuos |
| **Custom color** | Use `Color.from_argb(255, r, g, b)` para criar qualquer tonalidade | Estilização consistente com a marca |

**Dica profissional:** Sempre defina `condition.style.pattern = BackgroundType.SOLID` quando quiser um preenchimento sólido; caso contrário, o Excel pode exibir um gradiente que parece inconsistente entre versões.

## Conclusão

Agora você sabe como criar scripts **create Excel workbook python** que **set cell background color**, aplicam **excel conditional formatting python** e **format cells by date** usando Aspose.Cells. O exemplo cobre um cenário de **date based conditional formatting**, mas o mesmo padrão funciona para qualquer regra de período de tempo.

Em seguida, você pode explorar:

- Adicionar barras de dados ou conjuntos de ícones (`FormatConditionType.DATA_BAR`)  
- Combinar múltiplas regras condicionais no mesmo intervalo  
- Exportar a pasta de trabalho para PDF (`SaveFormat.PDF`) para relatórios  

Sinta-se à vontade para experimentar diferentes cores, intervalos e tipos de período de tempo para atender às suas necessidades específicas de relatório. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Domine a formatação de células Excel e o gerenciamento de pastas de trabalho com Aspose.Cells para .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Automação de Excel com Aspose.Cells .NET&#58; Criar Pasta de Trabalho & Definir Links Externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Como criar intervalos nomeados com escopo de pasta de trabalho no Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}