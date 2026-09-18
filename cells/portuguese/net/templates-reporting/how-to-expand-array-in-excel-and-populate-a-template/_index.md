---
category: general
date: 2026-09-18
description: Aprenda a expandir arrays no Excel usando a função EXPAND, preencher
  um modelo do Excel e criar uma planilha do Excel com intervalo dinâmico em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: pt
lastmod: 2026-09-18
og_description: Como expandir uma matriz no Excel com a função EXPAND, preencher um
  modelo do Excel e criar uma solução de intervalo dinâmico no Excel usando código
  C#.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Como expandir uma matriz no Excel e preencher um modelo
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Como expandir a matriz no Excel e preencher um modelo
url: /pt/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como expandir arrays no Excel e preencher um modelo

Se você precisa **como expandir array** no Excel ao preencher um modelo pré‑desenhado, este guia mostra uma solução completa, de ponta a ponta. Usando a função `EXPAND` junto com os Smart Markers do Aspose.Cells, você pode transformar uma única referência de célula em um intervalo 5 × 5 e substituir automaticamente marcadores como `{IsActive}` por dados reais.

Você verá como **preencher modelo excel**, criar um **dynamic range excel**, e usar corretamente a **função expand** em um projeto C#. Ao final do tutorial, você terá um programa executável que carrega um arquivo `.xlsx`, expande uma fórmula de array, aplica Smart Markers e salva o resultado.

## Prerequisites

* .NET 6.0 ou posterior (o código também funciona com .NET Core 3.1+)
* Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`)
* Uma pasta de trabalho Excel que contém uma célula de fórmula placeholder (por exemplo, `B2`) e um Smart Marker como `{IsActive}`
* Familiaridade básica com C# e fórmulas do Excel

> **Dica profissional:** A função `EXPAND` está disponível apenas no Excel para Microsoft 365 e Excel 2021+. Versões mais antigas retornarão o erro `#NAME?`.

## Etapa 1: Como expandir array com a função EXPAND

O primeiro passo é carregar a pasta de trabalho e escrever uma fórmula `EXPAND` que transforma uma única célula de origem em uma matriz maior.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Por que isso importa: `EXPAND` elimina a necessidade de copiar manualmente fórmulas através de linhas e colunas. Quando a célula de origem (`A2`) muda, todo o bloco 5 × 5 é atualizado automaticamente, proporcionando um **dynamic range excel** que reage às alterações de dados.

## Etapa 2: Preencher modelo Excel usando Smart Markers

Smart Markers permitem incorporar placeholders dentro do modelo que são substituídos por valores de um objeto C#. Esta é a maneira mais conveniente de **preencher modelo excel** sem escrever código célula por célula.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

A chamada `SmartMarkersProcessor().Apply` varre toda a planilha, encontra `{IsActive}` e injeta o valor booleano. A fórmula então avalia para `"Active"` ou `"Inactive"` automaticamente.

## Etapa 3: Verificar o intervalo expandido e o resultado preenchido

Após aplicar tanto a fórmula `EXPAND` quanto os Smart Markers, você pode ler programaticamente algumas células para garantir que tudo funcionou como esperado.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Executar o programa deve imprimir o valor original de `A2` (ou o resultado do array) e **Active** ou **Inactive** dependendo da flag `IsActive`.

## Etapa 4: Salvar a pasta de trabalho – a saída final

Finalmente, escreva a pasta de trabalho modificada no disco. Esta etapa demonstra o fluxo completo desde o carregamento, expansão, preenchimento, até a persistência do arquivo.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

O `output.xlsx` salvo agora contém uma matriz 5 × 5 gerada pela fórmula `EXPAND` e uma célula que reflete o valor de `{IsActive}`. Abra o arquivo no Excel para ver o dynamic range em ação.

## Casos limites e boas práticas

| Situação                               | Recomendação                                                                 |
|----------------------------------------|------------------------------------------------------------------------------|
| Versão do Excel não suporta `EXPAND`  | Recorrer às fórmulas clássicas `=OFFSET` ou `=INDEX`, ou atualizar para Office 365. |
| Necessidade de expandir para um tamanho variável | Use `ROWS(source)` e `COLUMNS(source)` dentro do `EXPAND` para verdadeira dinamismo. |
| Múltiplos Smart Markers na mesma planilha | Chame `SmartMarkersProcessor().Apply` uma vez com um objeto de dados composto. |
| Pastas de trabalho grandes ( > 10 000 linhas) | Desative o cálculo ao escrever fórmulas (`workbook.Settings.CheckFormula = false`). |

## Exemplo completo em funcionamento

Abaixo está o programa completo e autônomo que você pode copiar‑colar em um novo projeto de console.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Saída esperada ao executar o programa** (supondo que `A2` contenha o número `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Abrir `output.xlsx` mostra um bloco 5 × 5 preenchido com os valores derivados de `A2` e uma célula que exibe **Active**.

## Conclusão

Agora você sabe **como expandir array** no Excel usando a função `EXPAND`, como **preencher modelo excel** com Smart Markers, e como construir um **dynamic range excel** que se adapta automaticamente aos dados de origem. O exemplo também demonstra a forma correta de **usar a função expand** e a **fórmula expand array** em um cenário real de automação C#.

Em seguida, considere expandir a solução:

* Substitua as dimensões fixas `5,5` por `ROWS(A2:A10), COLUMNS(A2:E2)` para intervalos realmente variáveis.
* Combine múltiplos Smart Markers para gerar relatórios completos (por exemplo, listas de funcionários, tabelas de vendas).
* Explore a API de estilo do Aspose.Cells para formatar o bloco expandido automaticamente.

Sinta-se à vontade para experimentar diferentes arrays de origem, nomes de marcadores e layouts de pasta de trabalho. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Exportar Dados para Excel: Preencher um Modelo a partir de um Array em C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [Como criar array no Excel com C# – Guia passo a passo](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processamento de Dados Usando Função Array no Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}