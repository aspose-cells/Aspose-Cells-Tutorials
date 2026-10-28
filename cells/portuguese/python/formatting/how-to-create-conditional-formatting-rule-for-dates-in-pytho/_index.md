---
category: general
date: 2026-08-24
description: Create conditional formatting rule in Python using Aspose.Cells to highlight
  dates, with auto‑fit column and background color formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: pt
lastmod: 2026-08-24
og_description: Create conditional formatting rule in Python with Aspose.Cells. Learn
  how to highlight dates, set background colors, and auto‑fit columns in just a few
  lines of code.
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Create a conditional formatting rule for dates in Python – step‑by‑step
  guide
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: How to create conditional formatting rule for dates in Python
url: /pt/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar regra de formatação condicional para datas em Python

Se você precisa **criar regra de formatação condicional** que reage a datas, este guia mostra exatamente como fazer isso com Aspose.Cells for Python. Seja construindo um painel de relatórios ou uma planilha automatizada, você verá como destacar datas de ontem, aplicar uma cor de fundo personalizada e **auto fit column** nas larguras das colunas para que o resultado pareça refinado.

Neste tutorial, abordaremos **formatação condicional por data**, demonstraremos um **formato condicional de cor de fundo**, e concluiremos salvando a pasta de trabalho como um arquivo XLSX. Ao final, você terá um helper reutilizável que pode adaptar a qualquer **formato condicional baseado em data** que precisar.

## O que você aprenderá

* Configurar uma workbook e uma worksheet usando Aspose.Cells.
* Escrever uma função helper que adiciona um **formato condicional baseado em data** a qualquer intervalo de células.
* Preencher células com datas de exemplo para que a regra possa ser avaliada.
* Aplicar **auto fit column** para tornar o conteúdo legível.
* Salvar a workbook e verificar as células destacadas.

O único pré-requisito é um ambiente Python funcional com o pacote `aspose-cells` instalado.

## Pré-requisitos

| Requisito | Detalhes |
|-------------|---------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Conhecimento básico de conceitos do Excel | worksheets, cells, formatting |
| Opcional: IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## Etapa 1: Criar uma workbook e obter a primeira worksheet

O primeiro passo é criar objetos prontos para **criar regra de formatação condicional**: um `Workbook` e sua `Worksheet` padrão. Esses objetos são o ponto de entrada para todas as operações subsequentes.

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Por que isso importa:* O `Workbook` contém todo o arquivo Excel, enquanto a `Worksheet` é onde você aplica células, estilos e **formatação condicional por data**. Sem esses objetos, o restante do código não tem onde agir.

## Etapa 2: Construir um helper para adicionar um formato condicional TIME_PERIOD

Em vez de repetir o mesmo código padrão para cada intervalo, encapsulamos a lógica em uma função helper. Essa função anexa um **formato condicional de cor de fundo** que colore células com base em um `TimePeriodType` (por exemplo, Yesterday, Today, LastWeek).

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Por que usamos um helper:* Ele isola a lógica do **formato condicional baseado em data**, tornando o código mais fácil de ler, testar e reutilizar em várias planilhas ou projetos.

## Etapa 3: Aplicar a regra de formatação condicional a um intervalo específico

Agora usamos o helper para destacar células que contêm “Yesterday”. Este é o núcleo da nossa operação de **criar regra de formatação condicional**.

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

Quando a workbook for aberta, qualquer célula em `I19:K20` cuja data seja igual à data de ontem aparecerá com preenchimento rosa (o estilo que definimos no helper). O argumento `bg_color` mostra como você pode sobrepor um fundo padrão atrás da cor condicional, se desejar.

## Etapa 4: Preencher o intervalo com datas de exemplo

Uma regra condicional só se torna visível depois que a worksheet contém dados que satisfazem a condição. Inseriremos duas datas: uma que corresponde a “Yesterday” e outra que está fora do período.

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Por que isso importa:* Ao usar objetos `datetime` garantimos que o Excel trate os valores como datas reais, o que é necessário para que a **formatação condicional por data** funcione corretamente. O formato numérico (`30`) garante que as células sejam exibidas como datas reconhecíveis.

## Etapa 5: Auto‑ajustar a coluna e salvar a workbook

Depois que os dados e a formatação estão no lugar, o toque final é **auto fit column** nas larguras das colunas para que as datas fiquem totalmente visíveis. Em seguida, gravamos o arquivo no disco.

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

A chamada `auto_fit_column` examina o conteúdo mais longo na coluna 12 (que corresponde à coluna **L** no Excel) e expande a largura de acordo. Esta pequena etapa evita datas truncadas e torna o **formato condicional de cor de fundo** claramente visível.

### Resultado esperado

Ao abrir `TimePeriodDemo.out.xlsx`:

| I19 (date) | I20 (label) | K20 (date) |
|------------|------------|------------|
| 30‑Jul‑2008 (destacado em rosa) | Ontem | 03‑Aug‑2008 (sem destaque) |

* A célula com a data de ontem mostra um fundo rosa porque a **criar regra de formatação condicional** correspondeu ao período `YESTERDAY`.
* Todas as demais células mantêm o fundo padrão (ou o opcional `medium_sea_green` que você forneceu).
* A coluna L é ampliada automaticamente, de modo que as datas fiquem totalmente legíveis.

## Variações comuns e casos extremos

| Situação | Como adaptar o código |
|-----------|-----------------------|
| **Destacar “Today” em vez de “Yesterday”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Use uma cor de fundo diferente** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Aplique a regra a um intervalo não contíguo** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Trabalhe com uma workbook pré‑existente** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Múltiplas condições baseadas em data no mesmo intervalo** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## Conclusão

Agora você sabe como **criar regra de formatação condicional** que reage a datas, aplicar um **formato condicional de cor de fundo**, e **auto fit column** nas larguras usando Aspose.Cells for Python. A função helper abstrai a lógica, permitindo reutilizar o mesmo padrão para qualquer cenário de **formatação condicional por data** — seja “Yesterday”, “LastWeek” ou um intervalo personalizado.

Em seguida, você pode explorar:

* Adicionar **icon sets** ou **data bars** junto com regras de data.
* Gerar relatórios dinâmicos que extraem datas de um banco de dados.
* Combinar múltiplas regras de **formato condicional baseado em data** em uma única planilha.

Sinta-se à vontade para experimentar diferentes cores, períodos e intervalos para atender às necessidades do seu projeto. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Domine a Formatação Condicional no Excel Usando Aspose.Cells .NET: Um Guia Abrangente](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Como Extrair Cores de Formatação Condicional Usando Aspose.Cells para .NET](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Domine a Formatação Condicional com Fontes Personalizadas no Excel usando Aspose.Cells para .NET e C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}