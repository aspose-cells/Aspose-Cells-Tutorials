---
category: general
date: 2026-09-05
description: Crie uma pasta de trabalho Excel em Python e adicione formatação condicional
  para destacar as células de ontem. Aprenda o código completo e por que cada passo
  importa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: pt
lastmod: 2026-09-05
og_description: Crie uma pasta de trabalho do Excel em Python e adicione formatação
  condicional para destacar as células de ontem. Siga este guia passo a passo para
  uma solução completa.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Criar planilha Excel em Python – adicionar formatação condicional
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Criar pasta de trabalho Excel em Python com formatação condicional
url: /pt/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel em Python com formatação condicional

Se você precisar **create Excel workbook python** para uma tarefa de relatório, este guia mostra como gerar uma pasta de trabalho e aplicar uma regra de formatação condicional que destaca as datas de ontem. Você verá o código exato, por que cada linha existe e como adaptar a solução para outros intervalos de datas.

Formatação condicional é uma maneira poderosa de chamar a atenção para dados que atendem a uma condição específica. Neste tutorial usamos a biblioteca Aspose.Cells para Python via .NET, que fornece suporte total a recursos do Excel sem exigir o Microsoft Office. Ao final do guia você terá um arquivo onde as células no intervalo *I19:K20* ficam rosa quando contêm a data de ontem.

## Pré-requisitos

* Python 3.9+ instalado
* pacote `aspose-cells` (instale com `pip install aspose-cells`)
* Familiaridade básica com a sintaxe Python
* Permissão de escrita no diretório onde a pasta de trabalho será salva

O código funciona no Windows, macOS e Linux, desde que o runtime .NET esteja disponível.

## Criar pasta de trabalho Excel em Python

O primeiro passo é instanciar um objeto `Workbook` e obter a planilha padrão. Esse objeto representa todo o arquivo Excel na memória.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Por que isso importa*: `Workbook()` cria uma pasta de trabalho vazia com uma única planilha. Acessar `worksheets[0]` fornece um manipulador para adicionar dados, estilos e formatação posteriormente.

## Adicionar intervalo de formatação condicional

Em seguida, definimos a área que será avaliada pela regra condicional. O intervalo `I19:K20` cobre seis células em duas linhas.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Por que isso importa*: Adicionar uma coleção de formatação condicional a um intervalo específico isola a regra, impedindo que ela afete células não relacionadas. Isso satisfaz o requisito **add conditional formatting range**.

## Definir a regra: destacar células com base na data

Agora criamos uma condição do tipo `TIME_PERIOD`. Isso indica ao Excel para comparar o valor de cada célula com uma janela de tempo predefinida.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Por que isso importa*: `TIME_PERIOD` é o único tipo interno que suporta diretamente “Yesterday”, “Today”, “Last Week”, etc. Ao definir `condition.time_period` como `YESTERDAY`, a regra avalia automaticamente o valor de data de cada célula em relação ao dia anterior à data atual.

## Estilizar as células que atendem à condição

A formatação condicional também precisa de um estilo visual. Aqui escolhemos um preenchimento sólido rosa para que as células correspondentes se destaquem.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Por que isso importa*: O objeto de estilo define como o Excel renderizará as células que atendem à condição. Usar um preenchimento sólido rosa satisfaz o requisito **highlight cells based on date** e facilita a verificação do resultado.

## Preencher datas de exemplo para avaliação

Para ver a regra em ação, inserimos duas datas — uma que corresponde à data de ontem e outra que não. O formato `number` `30` corresponde ao formato de data interno `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Por que isso importa*: Fornecer tanto uma data correspondente quanto uma não correspondente permite verificar se a formatação condicional funciona corretamente. Ajuste as datas para o mês atual ao executar o script ou substitua-as por valores dinâmicos.

## Salvar a pasta de trabalho

Finalmente gravamos o arquivo no disco. A constante `SaveFormat.XLSX` garante que a saída seja um arquivo Excel moderno.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Por que isso importa*: Persistir a pasta de trabalho permite abri‑la no Excel, LibreOffice ou qualquer visualizador que suporte XLSX. O caminho impresso confirma onde o arquivo foi gravado.

## Script completo

Juntando todas as partes, o script completo e executável fica assim:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Saída esperada

Ao abrir `TimePeriodExample.xlsx`:

* A célula **I19** aparece com fundo rosa porque seu valor corresponde a ontem.
* A célula **K20** mantém o fundo padrão porque sua data está fora do período.
* O rótulo **“Yesterday”** está na célula I20 para clareza.

## Variações comuns e casos limites

| Situação | Ajuste |
|-----------|------------|
| **Destacar hoje em vez de ontem** | Alterar `condition.time_period = TimePeriodType.TODAY`. |
| **Aplicar a regra a uma área maior** | Atualizar a string de intervalo em `add(\"I19:K20\")` para algo como `\"A1:Z100\"`. |
| **Usar uma cor de preenchimento diferente** | Substituir `DrawingColor.pink` por qualquer outro `DrawingColor` (por exemplo, `DrawingColor.light_green`). |
| **Trabalhar com datas dinâmicas** | Calcular `datetime.now() - timedelta(days=1)` para ontem e gravar esse valor nas células antes de aplicar a regra. |

**Dica profissional:** Ao gerar a pasta de trabalho programaticamente para muitos usuários, mantenha a definição de formatação condicional separada da inserção de dados. Dessa forma, você pode reutilizar o mesmo estilo em várias planilhas sem duplicar código.

## Verificar o resultado programaticamente (opcional)

Se você quiser confirmar a formatação sem abrir o Excel, pode inspecionar o estilo de uma célula após salvar:



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Automação Excel: Criar uma Pasta de Trabalho e Adicionar um ListBox Usando Aspose.Cells para .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Criar Pasta de Trabalho Excel e Adicionar Rótulos com Aspose.Cells para Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Automação Excel Criar Pasta de Trabalho Adicionar ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}