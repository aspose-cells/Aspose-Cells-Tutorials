---
category: general
date: 2026-10-07
description: Criar uma planilha Excel em Python, definir a cor de fundo da célula,
  ajustar automaticamente a largura das colunas e preencher datas no Excel com um
  exemplo de código conciso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: pt
lastmod: 2026-10-07
og_description: Crie uma planilha Excel em Python, depois defina a cor de fundo das
  células, ajuste automaticamente a largura das colunas e preencha datas no Excel.
  Siga este guia passo a passo para gerar um arquivo TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Criar planilha Excel em Python – definir fundo e ajuste automático
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Criar pasta de trabalho Excel em Python e definir o fundo da célula
url: /pt/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar pasta de trabalho Excel em Python e definir cor de fundo da célula

Crie uma pasta de trabalho Excel em Python e aplique formatação condicional com apenas algumas linhas de código. Este tutorial mostra **como criar arquivos excel** programaticamente, definir a cor de fundo da célula, ajustar automaticamente as colunas do Excel e preencher datas no Excel usando a biblioteca Aspose.Cells.

Você aprenderá a:
* Inicializar uma workbook e obter a primeira planilha.  
* Definir uma formatação condicional que destaque datas de “Ontem”.  
* Inserir datas de exemplo em células específicas.  
* Ajustar automaticamente as colunas para que os dados fiquem claramente visíveis.  
* Salvar a workbook na pasta escolhida.

O único pré‑requisito é um ambiente Python 3 funcionando com os pacotes `aspose-cells` e `aspose-pydrawing` instalados:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Criar pasta de trabalho Excel em Python – passo a passo

As seções a seguir dividem o processo em etapas manejáveis. Cada etapa inclui o código necessário, uma explicação do **porquê** é importante e uma dica para evitar armadilhas comuns.

### Etapa 1: Importar namespaces necessários e definir uma função auxiliar

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Por que isso importa*: Importar as classes corretas lhe dá acesso à criação de workbooks, formatação condicional e manipulação de cores.  
**Dica profissional**: Mantenha as importações no topo do arquivo; isso facilita a leitura do script e previne erros de importação circular.

### Etapa 2: Criar a workbook e obter a primeira planilha

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

O construtor `Workbook()` cria uma pasta de trabalho Excel vazia na memória.  
**Por que**: Começar com uma workbook nova garante que não haja formatações residuais de execuções anteriores.

### Etapa 3: Definir cor de fundo da célula com formatação condicional

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Por que*: Usar uma condição de **período de tempo** destaca automaticamente qualquer célula que contenha a data de ontem, eliminando verificações manuais de data.  
**Dica**: `Color.pink` é apenas um exemplo; você pode usar qualquer objeto `Color` (`Color.yellow`, `Color.light_green`, etc.).

### Etapa 4: Preencher datas no Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Aqui nós **preenchemos datas nas células** `I19` e `K20` do Excel. A primeira data acionará a formatação condicional, enquanto a segunda não.  
**Por que isso importa**: Demonstrar valores que correspondem e que não correspondem ajuda a verificar se a regra funciona como esperado.

### Etapa 5: Ajustar automaticamente as colunas do Excel para melhor visibilidade

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` ajusta a largura da coluna com base no valor da célula mais longo.  
**Dica**: Chame isso depois de escrever todos os dados; caso contrário, a largura pode ser calculada com conteúdo incompleto.

### Etapa 6: Salvar a workbook

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Salvar o arquivo grava a workbook em memória no disco no formato XLSX moderno.  

### Script completo – juntando tudo

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Saída esperada**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Abra o arquivo gerado no Excel – as células `I19:K20` mostrarão um fundo rosa para a data que corresponde a “Ontem”, e a coluna L ficará larga o suficiente para exibir o rótulo sem corte.

---

## Por que essa abordagem funciona melhor

* **Fluxo de trabalho de passagem única** – Todas as operações acontecem na mesma instância `Workbook`, evitando I/O desnecessário.  
* **Formatação condicional** – Usar `FormatConditionType.TIME_PERIOD` permite que o Excel trate a lógica de datas, o que é mais confiável do que escrever verificações de data personalizadas em Python.  
* **Estilização explícita** – Definir `background_color` e `pattern` garante o resultado visual em diferentes versões do Excel.  
* **Ajuste automático após os dados**  

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Pasta de Trabalho Excel Python – Guia Completo](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Criar Pasta de Trabalho Excel Python – Guia Completo Passo a Passo](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Criar Pasta de Trabalho Excel Python – Guia Completo com Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}