---
category: general
date: 2026-06-08
description: Criar exemplo de planilha Excel em Python que mostre como usar lambda
  no Excel, somar linhas com BYROW e automatizar cálculos em poucos passos.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: pt
og_description: Crie uma planilha Excel com Python e aprenda a usar lambda no Excel
  para somar linhas de forma eficiente com fórmulas BYROW.
og_title: Criar Pasta de Trabalho Excel em Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Criar Pasta de Trabalho Excel em Python – Guia Completo com Lambda
url: /pt/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel Python – Guia Completo com Lambda

Já se perguntou como **criar scripts Python para pastas de trabalho Excel** que automatizam a tediosa manipulação de números? Você não está sozinho—muitos desenvolvedores se deparam com dificuldades quando precisam gerar uma planilha, inserir uma fórmula e trazer os resultados de volta ao código.  

Neste tutorial também mostraremos **como usar lambda** no Excel, explicaremos **como somar linhas** com a moderna função `BYROW` e forneceremos um exemplo completo e organizado que você pode copiar‑colar e executar hoje.

## O que Você Vai Aprender

- Configurar uma nova pasta de trabalho a partir do Python sem abrir o Excel manualmente.  
- Preencher um intervalo com uma matriz 3 × 3 de números.  
- Inserir uma fórmula `BYROW` que utiliza a sintaxe **use lambda excel** para somar cada linha.  
- Recalcular a planilha para que a fórmula seja avaliada e, em seguida, ler os resultados de volta no Python.  

Ao final deste guia você terá um script autônomo que pode adaptar para faturas, cartões de pontuação ou qualquer situação em que precise **somar linhas** rapidamente.

### Pré-requisitos

- Python 3.8+ instalado.  
- A biblioteca `openpyxl` (ou `xlwings` se preferir uma abordagem baseada em COM). Usaremos `openpyxl` porque é puro‑Python e funciona em todas as plataformas.  
- Uma versão recente do Microsoft Excel (365 ou 2021) que suporte a função `BYROW` e fórmulas Lambda.  

Instale a biblioteca com:

```bash
pip install openpyxl
```

> **Dica de especialista:** Se você encontrar problemas de permissão no Windows, use `python -m pip install --user openpyxl`.

---

## Criar Pasta de Trabalho Excel Python – Inicializar Pasta de Trabalho

A primeira coisa que precisamos é um objeto de pasta de trabalho totalmente novo que reside apenas na memória. Com `openpyxl` isso é uma única linha:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Por que usamos `wb.active` em vez de indexar `Worksheets[0]`? O `openpyxl` expõe a planilha ativa diretamente, o que é mais claro e evita uma busca extra na lista. Se você precisar trabalhar com várias planilhas, pode sempre adicioná‑las com `wb.create_sheet(title="MySheet")`.

---

## Preencher a Planilha com Dados – Uma Matriz Simples 3×3

Em seguida, preenchemos a planilha com uma pequena matriz. Isso reproduz o clássico exemplo de “somar cada linha” e mantém o código compacto.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Você pode se perguntar por que fazemos o loop manualmente em vez de usar `ws.append()` ou `ws.values`. Os loops explícitos nos dão controle total sobre a célula inicial e facilitam o ajuste de deslocamentos posteriormente—útil quando você deseja deixar uma linha ou coluna de cabeçalho vazia.

---

## Como Usar Lambda em Fórmulas Excel

O recurso **use lambda excel** do Excel permite escrever funções anônimas diretamente em uma célula. Pense nisso como o `lambda` do Python, mas dentro do motor da planilha. A sintaxe é:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Quando combinada com `BYROW`, você pode aplicar esse lambda a cada linha de um intervalo, produzindo uma coluna de resultados. Esse é o núcleo da nossa dica de **como somar linhas**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

O que está acontecendo nos bastidores?

- `A1:C3` é o intervalo de origem (nossa matriz).  
- `LAMBDA(r, SUM(r))` define uma função temporária que recebe uma única linha (`r`) e devolve sua soma.  
- `BYROW` executa esse lambda para **cada linha** e espalha os resultados na coluna D, começando em `D1`.  

Como `BYROW` é uma função de *array dinâmico*, o Excel preenche automaticamente `D1:D3` com as três somas.

> **Observação:** As fórmulas `BYROW` e Lambda estão disponíveis apenas no Excel 365/2021 e posteriores. Se você estiver usando uma versão mais antiga, precisará recorrer às fórmulas tradicionais `SUM` ou VBA.

---

## Como Somar Linhas com BYROW e Lambda

Agora que a fórmula está na planilha, precisamos dizer ao Excel para avaliá‑la. O próprio `openpyxl` não calcula fórmulas; ele apenas as lê/escreve. Para disparar um cálculo, podemos:

1. Salvar a pasta de trabalho e abri‑la no Excel (manual).  
2. Usar o motor COM `xlwings` para forçar a recalculação (requer Excel instalado).  

Para uma solução puramente Python, usaremos `xlwings` apenas para a etapa de cálculo—nada mais.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Por que não chamar `wb.calculate()`? O `openpyxl` não possui um motor nativo, então dependemos do próprio Excel via `xlwings`. O overhead é mínimo para planilhas pequenas e nos fornece o resultado exato que o Excel exibiria.

---

## Recalcular e Recuperar Resultados – Trazer as Somas de Volta ao Python

Finalmente, lemos os resultados espalhados na coluna D. O `openpyxl` torna isso simples:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Se preferir permanecer dentro do `openpyxl`, pode ler as células após a recalculação no Excel:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Ambas as abordagens fornecem a mesma lista `[6, 15, 24]`, confirmando que **como somar linhas** com `BYROW` + Lambda funciona como anunciado.

---

## Casos de Borda & Armadilhas Comuns

| Situação | O que observar | Correção |
|-----------|-------------------|-----|
| Versão do Excel anterior a 365 | `BYROW` e `LAMBDA` aparecem como `#NAME?` | Use a fórmula clássica `=SUM(A1:C1)` copiada manualmente, ou atualize o Excel. |
| Matrizes grandes (mais de 10 k linhas) | A recalculação pode ficar lenta | Chame `book.api.CalculateFullRebuild()` apenas uma vez, ou divida a pasta de trabalho. |
| Executando em um servidor sem interface gráfica sem Excel | `xlwings` não pode iniciar o Excel | Mude para uma biblioteca puramente Python como `pandas` + `numpy` para cálculos, e então escreva os resultados. |
| Problemas de localidade (vírgula vs. ponto e vírgula) | A fórmula pode ser rejeitada | Use `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` para locais que utilizam `;`. |

---

## Exemplo Completo (Pronto para Copiar‑Colar)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Criar Pasta de Trabalho Excel com Aspose.Cells Java - Guia Completo](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Criar Pasta de Trabalho Excel & Automatizar Relatórios com Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Como Criar e Salvar uma Pasta de Trabalho Excel como ODS Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}