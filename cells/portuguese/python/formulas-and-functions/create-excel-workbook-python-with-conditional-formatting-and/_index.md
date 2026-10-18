---
category: general
date: 2026-10-04
description: Crie uma planilha Excel em Python usando Aspose.Cells. Aprenda formatação
  condicional no Excel com Python, cor de fundo da célula com Python e formatação
  de data nas células com Python em um exemplo completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: pt
lastmod: 2026-10-04
og_description: Crie uma pasta de trabalho Excel em Python com Aspose.Cells. Este
  tutorial mostra formatação condicional no Excel com Python, cor de fundo da célula
  com Python e formatação de data nas células com Python passo a passo.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Criar planilha Excel em Python – guia completo com formatação condicional
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Criar planilha Excel em Python com formatação condicional e cor de fundo das
  células
url: /pt/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel python com formatação condicional e cor de fundo da célula

Se você precisa **create Excel workbook python** rapidamente, este guia mostra exatamente como. Você verá um exemplo completo e executável que adiciona **excel conditional formatting python**, altera o **cell background color python** e **format cells date python** para um destaque de “Yesterday”.

Em muitos cenários de relatórios, a pista visual de uma célula colorida torna os dados instantaneamente compreensíveis. Este tutorial percorre cada linha de código, explica por que cada passo importa e fornece um script pronto‑para‑executar que você pode adaptar aos seus próprios projetos.

## O que você vai alcançar

Ao final deste artigo você será capaz de:

1. **create Excel workbook python** usando a biblioteca Aspose.Cells.  
2. Aplicar **excel conditional formatting python** que destaca automaticamente datas que caem em “Yesterday”.  
3. Definir o **cell background color python** para rosa (ou qualquer cor que preferir).  
4. **format cells date python** para que as datas apareçam no estilo padrão de data do Excel.  

Nenhuma experiência prévia com Aspose.Cells é necessária — apenas um ambiente Python 3 funcional e acesso ao pip.

## Pré-requisitos

- Python 3.8 ou mais recente instalado.  
- Pacotes `aspose-cells` e `aspose-pydrawing` instalados via `pip install aspose-cells aspose-pydrawing`.  
- Familiaridade básica com a sintaxe Python e conceitos do Excel (workbooks, worksheets, cells).  

> **Dica profissional:** Se você executar o script em um ambiente virtual, evita conflitos de versão com outros projetos.

## Etapa 1: Configurar o projeto e importar as classes necessárias

O primeiro passo ao **create Excel workbook python** é importar as classes Aspose.Cells que você precisará. Essas classes dão acesso direto à criação de workbooks, formatação condicional e estilização.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Por que isso importa:* Importar apenas os símbolos necessários mantém o namespace organizado e torna o script mais fácil de ler. `Workbook` é o ponto de entrada para **create Excel workbook python**, enquanto `FormatConditionType` e `TimePeriodType` são essenciais para **excel conditional formatting python**.

## Etapa 2: Criar um novo workbook e obter a primeira planilha

Agora realmente **create Excel workbook python**. O construtor `Workbook()` fornece um arquivo Excel vazio com uma planilha padrão.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explicação:* Cada arquivo Excel começa com, pelo menos, uma planilha. Por padrão, o Aspose.Cells a nomeia como “Sheet1”. Você pode adicionar mais planilhas depois, mas para esta demonstração uma única planilha mantém o exemplo focado.

## Etapa 3: Definir o intervalo alvo para a formatação condicional

A formatação condicional funciona em um intervalo retangular. Aqui escolhemos o intervalo `I19:K20`, que nos dá três colunas e duas linhas para trabalhar.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Por que fazemos isso:* O método `get` retorna um objeto `ConditionalFormatting` ligado ao intervalo especificado. Se o intervalo ainda não possuir formatação, o Aspose.Cells cria uma nova coleção automaticamente.

## Etapa 4: Adicionar uma condição TIME_PERIOD e definir a cor de fundo

Este é o núcleo da **excel conditional formatting python**. Adicionamos uma regra `TIME_PERIOD` que destaca células contendo datas que caem em “Yesterday”.

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Análise aprofundada:*  
- `FormatConditionType.TIME_PERIOD` informa ao Excel para avaliar datas em relação à data atual.  
- `TimePeriodType.YESTERDAY` é um enum interno que atualiza automaticamente a cada dia, de modo que o workbook sempre destaque o “Yesterday” mais recente.  
- Ao definir `background_color` para `Color.pink` e o padrão para `SOLID`, conseguimos o efeito de **cell background color python** sem código VBA adicional.

## Etapa 5: Preencher o intervalo com datas de exemplo e aplicar formatação de data

Para ver a formatação condicional em ação, precisamos de valores de data reais. Também precisamos **format cells date python** para que o Excel os trate como datas e não como números simples.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explicação:*  
- A linha `style.number = 30` é o passo de **format cells date python**. O código de formato 30 corresponde ao formato de data curta (`m/d/yy`).  
- Usar uma função auxiliar mantém o código DRY (Don’t Repeat Yourself) e facilita a adição de mais datas posteriormente.

## Etapa 6: Adicionar um rótulo descritivo

Um pequeno rótulo ajuda quem abrir o workbook a entender por que as células estão coloridas.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Etapa 7: Salvar o workbook no disco

Finalmente, nós **create Excel workbook python** no disco chamando `save`. A constante `SaveFormat.XLSX` garante que o arquivo esteja no formato moderno Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Ao abrir `TimePeriodDemo.xlsx` no Excel, você verá:

- Células `I19` e `K20` contêm datas.  
- A célula que corresponde a “Yesterday” (neste exemplo estático, `I19`) está destacada em rosa.  
- O rótulo “Yesterday” aparece em `I20`.  

> **Dica:** Se você executar o script em um dia diferente, a formatação condicional ainda destacará a célula cuja data é exatamente um dia antes da data atual do sistema — sem necessidade de alterar o código.

## Script completo – pronto para copiar e executar

Abaixo está o programa completo e autocontido que incorpora todas as etapas acima. Copie-o para um arquivo chamado `conditional_format_demo.py`, ajuste `YOUR_DIRECTORY` e execute com `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Saída esperada

A execução do script imprime uma linha de confirmação:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Abrir o arquivo gerado mostra o fundo rosa na célula que corresponde à regra “Yesterday”, confirmando que **excel conditional formatting python** e **cell background color python** estão funcionando juntos.

## Variações comuns e casos de borda

| Situação | Como adaptar o código |
|-----------|-----------------------|
| **Cor de destaque diferente** | Alterar `Color.pink` para qualquer outra constante `Color`, por exemplo, `Color.light_green`. |
| **Destacar “Today” em vez de “Yesterday”** | Definir `condition.time_period = TimePeriodType.TODAY`. |
| **Aplicar formatação a uma coluna inteira** | Usar um intervalo como `"A:A"` e ajustar a variável `target_range` de acordo. |
| **Usar um formato de data personalizado** | Substituir `style.number = 30` por `style.custom = "dd-mmm-yyyy"` para um formato mais legível. |
| **Múltiplas condições no mesmo intervalo** |  |

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel Python – Guia Completo com Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Criar e Salvar Pasta de Trabalho Excel como PDF em ASP.NET Usando Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Como Criar e Salvar uma Pasta de Trabalho Excel como ODS Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}