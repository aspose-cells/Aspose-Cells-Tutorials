---
category: general
date: 2026-07-20
description: Criar pasta de trabalho Excel em Python com Aspose.Cells, definir a cor
  de fundo da célula e adicionar formatação condicional em Python para estilizar células
  por data.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: pt
lastmod: 2026-07-20
og_description: Crie uma pasta de trabalho Excel em Python usando Aspose.Cells. Aprenda
  como definir a cor de fundo da célula e adicionar formatação condicional em Python
  para formatar células por data.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Criar Pasta de Trabalho Excel em Python – Adicionar Formatação Condicional
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Criar Pasta de Trabalho do Excel em Python – Guia de Formatação Condicional
url: /pt/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Excel Workbook Python – Guia de Formatação Condicional

Já se perguntou como **criar Excel workbook Python** do zero e deixá‑lo com aparência profissional sem abrir a interface? Você não está sozinho. Muitos desenvolvedores encontram dificuldades quando precisam **definir cor de fundo da célula** ou aplicar estilos baseados em datas programaticamente.  

Neste tutorial, percorreremos um exemplo completo e executável que usa Aspose.Cells para **add conditional formatting python** regras, formatar células por data e salvar o resultado como um arquivo XLSX moderno. Ao final, você terá um script autônomo que pode inserir em qualquer projeto.

## O que você aprenderá

- Como inicializar uma workbook e obter a primeira worksheet.  
- Formas de **set cell background color** para um intervalo inteiro.  
- Usando **aspose cells conditional formatting** para destacar datas de “Yesterday”.  
- Ajuste automático de colunas e persistência do arquivo no disco.  

Nenhuma configuração externa é necessária — apenas Python 3 e o pacote Aspose.Cells. Se você já instalou `aspose-cells`, está pronto para usar; caso contrário, um rápido `pip install aspose-cells` resolve.

## Pré‑requisitos

- Python 3.8+ (o código funciona em 3.9, 3.10 e versões mais recentes).  
- Aspose.Cells para Python via .NET (`aspose-cells` wrapper NuGet).  
- Familiaridade básica com conceitos do Excel (células, intervalos, formatação).  

Tem tudo isso? Ótimo — vamos mergulhar.

## Criar Excel Workbook Python – Configuração e Worksheet

Primeiro de tudo: precisamos de um novo objeto workbook e de uma referência à worksheet padrão. Esta é a tela onde todas as operações subsequentes acontecerão.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Por que isso importa:** `Workbook()` cria um arquivo Excel em memória, eliminando a necessidade de arquivos temporários. A variável `worksheet` é nosso ponto de entrada para ações ao nível de célula.

## Definir cor de fundo da célula

Antes de adicionarmos quaisquer regras, é bom dar ao intervalo alvo uma cor base para que a formatação condicional se destaque. O helper abaixo recupera (ou cria) um `FormatConditionCollection` para um intervalo especificado e pinta as células com um fundo sólido.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Dica profissional:** Se você planeja reutilizar o mesmo intervalo com várias regras, chame este helper uma vez e mantenha a coleção retornada; isso economiza algumas chamadas de API.

## Adicionar Conditional Formatting Python para Intervalos de Data

Agora a parte divertida: criaremos uma regra de **time‑period conditional formatting** que destaca células contendo a data de ontem. Isso demonstra o poder de **format cells by date** usando Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Por que usar `TIME_PERIOD`?** Ele abstrai a necessidade de escrever fórmulas personalizadas. Aspose.Cells avalia a data em relação à data do sistema atual, então a regra permanece sempre relevante.

### Executando a Regra

```python
apply_yesterday_rule()
```

Ao abrir o arquivo resultante, as células `I19` ficarão rosa (porque são “Yesterday”), enquanto `K20` permanecerá na cor verde base.

## Auto‑Ajustar Colunas e Salvar Workbook

Uma planilha organizada parece profissional. O auto‑ajuste garante que nossos dados não fiquem apertados.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Caso de borda:** Se você apontar para um diretório que não existe, `workbook.save` gerará um erro. Envolva a chamada de salvamento em um bloco `try/except` se precisar de um tratamento mais elegante.

### Script Completo (Pronto para Copiar‑Colar)

Abaixo está o script completo, pronto para executar. Basta substituir `YOUR_DIRECTORY` por uma pasta válida na sua máquina.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Executar este script produzirá `TimePeriodExample.xlsx` com a formatação condicional que descrevemos.

## Perguntas Frequentes & Dicas

- **Posso direcionar um intervalo de datas diferente?**  
  Absolutamente. Altere `"I19:K20"` para qualquer intervalo no estilo A1 e ajuste as datas de exemplo conforme necessário.

- **E se eu precisar de uma fórmula personalizada em vez de `YESTERDAY`?**  
  Use `FormatConditionType.FORMULA` e defina `condition.formula1 = "YOUR_FORMULA"` — por exemplo, `=TODAY()-A1=1` para imitar ontem.

- **Como aplicar múltiplas regras ao mesmo intervalo?**  
  Chame `conditions.add_condition` novamente com um `FormatConditionType` diferente. A ordem importa; regras posteriores podem sobrescrever as anteriores.

- **Existe uma forma de definir a cor da fonte junto com o fundo?**  
  Sim — modifique `condition.style.font.color = Color.white` (ou qualquer outro `Color`).

## Conclusão

Agora você sabe como **create Excel workbook Python** usando Aspose.Cells, **set cell background color**, e **add conditional formatting python** que formata células por data. O script está totalmente funcional, trata casos de borda como diretórios ausentes, e pode ser estendido para cenários mais sofisticados, como lógica condicional de múltiplas regras ou detecção dinâmica de intervalos.

Pronto para o próximo passo? Experimente trocar a regra “Yesterday” por “Last Week”, experimente preenchimentos em gradiente, ou gere um relatório completo com dezenas de tabelas formatadas. Os blocos de construção estão todos aqui, e você acabou de dominar o núcleo de **aspose cells conditional formatting** em Python.

Feliz codificação, e sinta‑se à vontade para compartilhar suas próprias variações nos comentários!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}