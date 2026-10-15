---
category: general
date: 2026-07-06
description: Criar planilha Excel em Python com código para definir a cor de fundo
  da célula, definir o estilo da célula programaticamente e adicionar formatação condicional
  em Python para destacar a data de hoje.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: pt
lastmod: 2026-07-06
og_description: Crie uma pasta de trabalho Excel com Python instantaneamente. Aprenda
  como definir a cor de fundo da célula, definir o estilo da célula programaticamente
  e adicionar formatação condicional em Python para destacar a data de hoje.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Criar Pasta de Trabalho do Excel em Python – Estilizar Células e Destacar
  Hoje
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Criar Pasta de Trabalho Excel em Python – Guia Completo de Estilização e Formatação
  Condicional
url: /pt/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crie Workbook Excel Python – Guia Completo de Estilização e Formatação Condicional

Já se perguntou como **criar Excel workbook Python** do zero sem abrir o Excel manualmente? Você não está sozinho. Muitos desenvolvedores precisam gerar relatórios, dashboards ou até mesmo logs de dados simples em tempo real, e fazer isso programaticamente economiza horas de trabalho manual.

Neste tutorial vamos percorrer todo o processo: desde a criação de um workbook novinho em folha, até **set cell background color**, passando por **set cell style programmatically**, e finalmente **highlight today date excel** usando **add conditional formatting python**. Ao final, você terá um script pronto‑para‑executar que produz um arquivo .xlsx polido em segundos.

---

## O que você vai construir

- Um novo arquivo Excel com algumas células preenchidas.
- Células coloridas com um fundo personalizado.
- Valores numéricos e de data formatados com um estilo numérico específico.
- Uma regra condicional que destaca automaticamente a célula contendo a data de hoje.

Nenhuma instalação externa do Excel é necessária — Aspose.Cells for Python via .NET faz todo o trabalho pesado.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| Python 3.8+ | Sintaxe moderna e dicas de tipo |
| `aspose-cells` package | Biblioteca central para manipulação de workbooks |
| `aspose-pydrawing` (instalado com Aspose.Cells) | Fornece a classe `Color` |
| Familiaridade básica com conceitos do Excel (células, intervalos, formatação) | Facilita o fluxo do tutorial |

Instale a biblioteca com:

```bash
pip install aspose-cells
```

---

## Etapa 1: Inicializar o Workbook e a Worksheet

A primeira coisa que você faz ao **create excel workbook python** é instanciar um objeto `Workbook` e obter a worksheet padrão. Pense no workbook como todo o arquivo Excel, enquanto a worksheet é uma única aba dentro dele.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Dica profissional:** Se precisar de várias planilhas, use `book.worksheets.add("MySheet")` para acrescentar mais abas.

---

## Etapa 2: Classe Auxiliar para Estilização e Formatação Condicional

A seguir está uma classe compacta porém completa `ConditionalFormatting`. Ela encapsula as tarefas repetitivas de:

1. Converter um intervalo como `"A1:C3"` em um `CellArea`.
2. Preencher cada célula nessa área com um número sequencial (apenas para demonstração).
3. Aplicar uma cor de fundo sólida **set cell background color**.
4. Adicionar uma regra condicional que **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Por que uma Classe Auxiliar?

- **Reusabilidade:** Você pode chamar `add_time_period_1()` para qualquer planilha sem reescrever a lógica.
- **Clareza:** Cada método faz uma coisa – uma marca de código limpo.
- **Extensibilidade:** Quer adicionar mais regras? Basta adicionar outro método seguindo o mesmo padrão.

---

## Etapa 3: Aplicar a Formatação e Salvar o Arquivo

Agora juntamos tudo: instanciamos a classe auxiliar, executamos a rotina de formatação e, finalmente, gravamos o workbook no disco.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Ao abrir *styled_workbook.xlsx* você deverá ver:

- Células **A1:C3** numeradas de 0‑8 com preenchimento azul‑celeste claro.
- Célula **I1** mostrando a data de hoje com fundo rosa (graças à regra condicional).
- Célula **K2** exibindo a data estática *2008‑07‑30* para comparação.
- Célula **I2** contendo o texto “Today”.

Essa pista visual é exatamente o que o requisito **highlight today date excel** pede.

---

## Etapa 4: Aprofundar – Personalizando Estilos

Se precisar ajustar fontes, bordas ou formatos numéricos, você pode estender o método `fill_cell` ou criar um novo auxiliar:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Você poderia então chamar `apply_custom_style(cell, bold=True)` dentro do loop para **set cell style programmatically** em cada célula de um intervalo.

---

## Armadilhas Comuns & Como Evitá‑las

| Sintoma | Causa provável | Correção |
|---------|----------------|----------|
| Células permanecem brancas apesar de `Color.light_sky_blue` | O estilo não foi aplicado após definir `foreground_color` | Sempre chame `cell.set_style(style)` após modificar o objeto de estilo. |
| Regra condicional nunca dispara | `style.number` não definido para células de data, então o Excel trata o valor como string | Defina `style.number = 30` (ou qualquer formato de data) antes de `cell.put_value(datetime…)`. |
| Workbook salva como .xls apesar de `SaveFormat.XLSX` | Versão antiga do Aspose que usa o formato legado por padrão | Atualize para o pacote `aspose-cells` mais recente. |
| Intervalo como `"A1"` gera erro de índice | Uso de `cells.get("A1")` em uma planilha que não foi inicializada | Garanta que a planilha exista (ela existe logo após `Workbook()`), ou use `cells.get(row, col)` com índices baseados em zero. |

---

## Script Completo para Copiar‑Colar

Abaixo está o **script inteiro** que você pode colocar em um arquivo chamado `create_excel.py` e executar imediatamente.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Automação Excel com Aspose.Cells .NET: Criar Workbook e Definir Links Externos](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Domine a Formatação de Células Excel e Gerenciamento de Workbooks com Aspose.Cells para .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Automação Excel: Crie um Workbook e Adicione um ListBox Usando Aspose.Cells para .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}