---
category: general
date: 2026-09-27
description: Aprenda como copiar uma tabela dinâmica em C# usando Aspose.Cells. Inclui
  copiar linhas com formatação, copiar a tabela dinâmica para outra planilha e exportar
  a tabela dinâmica para uma nova pasta de trabalho.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: pt
lastmod: 2026-09-27
og_description: Como copiar uma tabela dinâmica em C# usando Aspose.Cells. Siga o
  guia passo a passo para copiar linhas com formatação, mover uma tabela dinâmica
  para outra planilha e exportá‑la para uma nova pasta de trabalho.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Como copiar uma tabela dinâmica em C# – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Como copiar uma tabela dinâmica em C# com Aspose.Cells
url: /pt/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar uma tabela dinâmica em C# com Aspose.Cells

Se você precisa **copiar uma tabela dinâmica** de uma planilha para outra, aprender **como copiar tabela dinâmica** em C# com Aspose.Cells pode economizar horas de trabalho manual. A abordagem também permite **copiar linhas com formatação**, manter o cache da tabela dinâmica intacto e até **exportar tabela dinâmica para uma nova pasta de trabalho** quando você precisar de um arquivo independente.

Este tutorial guia você por todo o fluxo de trabalho:

* criar uma pasta de trabalho,  
* copiar o intervalo da tabela dinâmica preservando a formatação,  
* colocar os dados copiados em uma nova planilha e  
* salvar o resultado como um arquivo separado.

Você verá por que o método interno `CopyRows` é a maneira mais confiável de **copiar tabela dinâmica para outra planilha**, e receberá dicas para lidar com casos extremos, como linhas ocultas ou fontes de dados externas.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

| Requisito | Por que é importante |
|-----------|----------------------|
| .NET 6.0 ou superior | Aspose.Cells oferece suporte a .NET 6+ e proporciona o melhor desempenho. |
| Visual Studio 2022 (ou qualquer IDE C#) | Você precisa de um editor que possa restaurar pacotes NuGet. |
| Aspose.Cells for .NET (pacote NuGet `Aspose.Cells`) | Esta biblioteca fornece a API `CopyRows` usada no exemplo. |
| Um arquivo Excel fonte (`source.xlsx`) que contém uma tabela dinâmica no intervalo `A1:G20` | O código copia esse intervalo específico; ajuste o intervalo se sua tabela dinâmica for maior. |

Instale a biblioteca com o NuGet CLI ou o Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Etapa 1: Carregar a pasta de trabalho que contém a tabela dinâmica

A primeira linha cria um objeto `Workbook` que representa todo o arquivo Excel. Carregar o arquivo uma única vez lhe dá acesso de leitura/escrita a todas as planilhas.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Por que esta etapa é importante** – Sem carregar a pasta de trabalho, nenhuma das chamadas subsequentes de `CopyRows` pode referenciar os dados de origem ou o cache da tabela dinâmica.

## Etapa 2: Preparar as planilhas de origem e destino

Você precisa de uma planilha de destino onde a tabela dinâmica copiada ficará. O código abaixo obtém a primeira planilha (onde a tabela dinâmica original está) e adiciona uma nova planilha chamada **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Dica profissional:** Se a planilha de destino já existir, chame `Worksheets.RemoveAt(index)` primeiro para evitar nomes duplicados.

## Etapa 3: Definir a área de células que envolve a tabela dinâmica

Um objeto `CellArea` descreve as células superior‑esquerda e inferior‑direita do intervalo que você deseja mover. Neste exemplo a tabela dinâmica ocupa `A1:G20`. Ajuste as coordenadas para tabelas maiores.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Etapa 4: Copiar linhas com formatação e preservar o cache da tabela dinâmica

O método `CopyRows` copia **linhas** da planilha de origem para a planilha de destino. Ao passar `CopyOptions.CopyAll` você garante que valores, formatação, gráficos e objetos incorporados — tudo que faz parte de uma tabela dinâmica — sejam transferidos.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Por que `CopyRows` funciona melhor que `Copy` para tabelas dinâmicas

* `CopyRows` respeita o cache interno da tabela dinâmica, de modo que a tabela copiada permanece funcional.  
* Ele preserva **copiar linhas com formatação** exatamente como aparecem na planilha original.  
* Diferente de um simples `Copy` de um intervalo, ele também move linhas ocultas e quaisquer segmentações associadas.

## Etapa 5: Salvar a pasta de trabalho com a tabela dinâmica copiada

Por fim, grave a pasta de trabalho modificada no disco. O novo arquivo contém a planilha original mais uma planilha **Copy** que contém um duplicado totalmente funcional da tabela dinâmica original.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Resultado esperado

Ao abrir `pivot_copied.xlsx`:

* A planilha **Sheet1** ainda contém os dados e a tabela dinâmica originais.  
* A planilha **Copy** exibe uma tabela dinâmica idêntica, com o mesmo layout, filtros e formatação.  
* Todas as fórmulas e conexões de dados permanecem intactas porque o cache da tabela dinâmica foi copiado junto com as linhas.

## Como copiar a tabela dinâmica para outra planilha no mesmo arquivo

Se você precisar da tabela dinâmica em uma planilha existente diferente (por exemplo, “Report”), substitua a etapa de criação de destino por uma referência à planilha alvo:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Este trecho demonstra **copiar tabela dinâmica para outra planilha** sem criar uma nova planilha.

## Exportar a tabela dinâmica para uma nova pasta de trabalho

Às vezes você deseja a tabela dinâmica em um arquivo completamente separado. Após a operação de cópia, você pode remover todas as planilhas, exceto a que contém a tabela dinâmica copiada, e então salvar:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Agora `pivot_only.xlsx` contém uma única planilha com a tabela dinâmica duplicada, atendendo ao requisito de **exportar tabela dinâmica para nova pasta de trabalho**.

## Como copiar linhas do Excel sem perder a formatação

A mesma chamada `CopyRows` funciona para qualquer intervalo, não apenas para tabelas dinâmicas. Se precisar **copiar linhas do Excel** que incluam formatação condicional, validação de dados ou células mescladas, use o mesmo método:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Como `CopyOptions.CopyAll` transfere tudo, as linhas de destino ficam exatamente iguais às linhas de origem.

## Armadilhas comuns e como evitá‑las

| Armadilha | Sintoma | Solução |
|-----------|---------|---------|
| O intervalo de origem não inclui toda a tabela dinâmica | A tabela dinâmica copiada aparece truncada. | Verifique se o `CellArea` cobre todas as linhas/colunas da tabela dinâmica. |
| A planilha de destino já contém dados | Linhas sobrescritas causam perda de dados. | Escolha uma planilha nova ou comece a copiar a partir de um índice de linha mais alto. |
| A tabela dinâmica usa uma fonte de dados externa | A cópia perde a conexão. | Após copiar, chame `pivotTable.RefreshData()` para restabelecer o vínculo. |
| Linhas ocultas são omitidas | Algumas linhas desaparecem na cópia. | `CopyRows` copia automaticamente linhas ocultas; certifique‑se de não estar usando `CopyOptions.CopyValuesOnly`. |

## Exemplo completo, executável

Abaixo está um programa autocontido que você pode colar em um novo projeto de console. Ele demonstra cada passo discutido acima.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Executar o programa** cria `pivot_copied.xlsx` com um duplicado da tabela dinâmica original em uma nova planilha chamada **Copy**.

## Conclusão

Agora você sabe **como copiar uma tabela dinâmica** em C# usando

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Nova Pasta de Trabalho – Como Copiar uma Planilha com uma Tabela Dinâmica](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copiar Tabela Dinâmica em C# – Guia Completo Passo a Passo](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Como copiar intervalo com tabelas dinâmicas em C# – Guia Completo](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}