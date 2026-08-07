---
category: general
date: 2026-06-21
description: Aprenda como escrever lambda no Excel usando Python. Este tutorial também
  aborda como criar uma pasta de trabalho Excel com Python e como ler células com
  Aspose.Cells.
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: pt
og_description: Como escrever lambda no Excel usando Python explicado. Siga nossos
  passos claros para criar uma planilha Excel em Python, aplicar BYROW e ler os resultados
  das células.
og_title: Como escrever Lambda no Excel com Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: Como escrever Lambda no Excel com Python – Guia passo a passo
url: /pt/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como escrever Lambda no Excel com Python – Guia passo a passo

Já se perguntou **how to write lambda** em uma fórmula do Excel quando você está automatizando planilhas a partir do Python? Você não está sozinho. Muitos desenvolvedores encontram dificuldades ao tentar combinar o poder das novas funções de array dinâmico do Excel com um fluxo de trabalho impulsionado por Python. Neste tutorial, percorreremos um exemplo completo e executável que mostra exatamente isso — além de abordarmos **create excel workbook python**, **how to read cells**, e o útil padrão **how to use byrow**.

Ao final deste guia, você terá uma nova pasta de trabalho, uma fórmula BYROW que utiliza um lambda, e uma maneira simples de trazer os resultados de volta ao seu script Python. Nenhum suplemento extra do Excel é necessário, apenas Aspose.Cells para Python e um pouco de código.

## Pré-requisitos

- Python 3.8 ou mais recente instalado.
- O pacote `aspose-cells` (`pip install aspose-cells`).
- Um entendimento básico de listas e funções em Python.
- (Opcional) Uma IDE ou editor de texto com o qual você se sinta confortável.

É isso. Se algum desses itens lhe for desconhecido, faça uma pausa e instale o pacote primeiro; o restante das etapas funcionará em qualquer plataforma que execute Python.

## Criar pasta de trabalho Excel com Python

A primeira coisa que precisamos é um objeto de pasta de trabalho limpo. Aspose.Cells nos fornece a classe `Workbook` que representa um arquivo Excel completo na memória.

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

Por que começar com uma pasta de trabalho nova? Porque isso garante um ambiente determinístico—sem fórmulas ocultas, sem formatação inesperada, apenas uma tela em branco. Esta é a base para qualquer tutorial **create excel workbook python**.

## Preencher a planilha com dados

Em seguida, preenchemos uma tabela numérica 5 × 3 começando na célula **A1**. Os dados são deliberadamente simples para que você possa ver a matemática claramente.

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

Observe como usamos `put_value` com uma lista Python aninhada; Aspose.Cells mapeia automaticamente linhas e colunas para nós. Se você precisar importar dados de um CSV ou de um banco de dados, basta substituir `table_data` por essa fonte—nada mais muda.

## Como escrever Lambda na fórmula BYROW (Python)

Agora vem a parte interessante: **how to write lambda** que o mecanismo do Excel avaliará. A função `BYROW` do Excel itera sobre cada linha de um intervalo, passando a linha para um `LAMBDA` que você fornece. No nosso caso queremos a média de cada linha.

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

Vamos analisar isso:

- `BYROW(A1:C5, …)` indica ao Excel para observar cada linha no intervalo A1:C5.
- `LAMBDA(r, AVERAGE(r))` define uma função anônima (`r` é o array da linha) que retorna a média dessa linha.
- O resultado é derramado automaticamente em D1:D5 porque BYROW retorna um array.

Essa única linha é a resposta para **how to write lambda** em cálculos linha a linha. Você pode substituir `AVERAGE` por `SUM`, `MAX` ou qualquer outro agregado—basta mudar o corpo do lambda.

## Forçar o cálculo da fórmula

Aspose.Cells não avalia fórmulas automaticamente quando você as define, então precisamos instruí-lo a recalcular.

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

Se você pular esta etapa, as células na coluna D ainda conterão o texto da fórmula, não os números calculados. Essa é uma armadilha comum quando as pessoas **how to use byrow** sem disparar uma passagem de cálculo.

## Como ler células após o cálculo

Finalmente, vamos trazer os resultados de volta ao Python. Isso ilustra **how to read cells** de uma forma que funciona para qualquer saída de fórmula.

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

Uma rápida list‑comprehension percorre as cinco linhas, captura o `.value` de cada célula e o armazena em `row_averages`. A lista impressa confirma que nosso lambda funcionou exatamente como esperado.

### Dica profissional
Se precisar ler um grande bloco de resultados, use `worksheet.cells.get_range("D1:D5").value` para buscar todo o array em uma única chamada—muito mais rápido para planilhas grandes.

## Usar função Lambda no Excel para médias de linhas (Script completo)

Juntando tudo, aqui está o script completo, pronto‑para‑executar:

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

Executar este script imprime:

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

Esse é o ciclo completo: **create excel workbook python**, preencher dados, **how to use byrow**, **how to write lambda**, e finalmente **how to read cells**.

## Casos de borda e perguntas comuns

- **E se meus dados não forem contíguos?**  
  BYROW works on any rectangular range. If you have gaps, just reference a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).

- **Posso passar mais de um argumento para o lambda?**  
  Sim. O primeiro argumento é sempre a linha (ou coluna para `BYCOL`). Argumentos adicionais podem ser fornecidos após o intervalo, como `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`.

- **Isso é compatível com versões mais antigas do Excel?**  
  BYROW e LAMBDA estão disponíveis a partir do Excel 365 (arrays dinâmicos). Se precisar de suporte legado, você teria que emular a lógica com VBA ou várias colunas auxiliares.

- **Preciso salvar a pasta de trabalho no disco?**  
  Não para esta demonstração, mas você pode chamar `workbook.save("output.xlsx")` se quiser um arquivo físico.

## Conclusão

Cobremos **how to write lambda** em uma fórmula Excel BYROW a partir do Python, demonstramos um fluxo completo **create excel workbook python**, e mostramos a maneira mais simples de **how to read cells** após o cálculo. Ao usar Aspose.Cells você evita dores de cabeça com interop COM, e o mesmo padrão escala para milhares de linhas com mudanças mínimas de código.

Pronto para o próximo desafio? Experimente trocar `AVERAGE` por `MEDIAN`, adicionar lógica condicional dentro do lambda, ou gerar um conjunto completo de relatórios automaticamente. A combinação de Python e as funções modernas do Excel abre um mundo de possibilidades para automação orientada a dados.

Tem perguntas ou quer compartilhar seus próprios truques de lambda? Deixe um comentário abaixo, e feliz codificação!  

![como escrever lambda no Excel usando Python](image.png){alt="como escrever lambda no Excel usando Python"}

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar e salvar uma pasta de trabalho Excel como ODS usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Como carregar uma pasta de trabalho Excel sem nomes definidos usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [Como criar intervalos nomeados com escopo de pasta de trabalho no Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}