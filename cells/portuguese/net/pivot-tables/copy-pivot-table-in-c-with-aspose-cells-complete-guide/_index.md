---
category: general
date: 2026-08-11
description: Copie a tabela dinâmica usando C# e Aspose.Cells. Aprenda como carregar
  uma pasta de trabalho do Excel, duplicar uma tabela dinâmica e preservar sua formatação
  rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: pt
lastmod: 2026-08-11
og_description: Copiar tabela dinâmica em C# com Aspose.Cells. Este guia mostra como
  carregar uma pasta de trabalho do Excel, duplicar uma tabela dinâmica e manter toda
  a formatação intacta.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Copiar tabela dinâmica em C# – tutorial passo a passo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Copiar tabela dinâmica em C# com Aspose.Cells – guia completo
url: /pt/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Tabela Dinâmica em C# com Aspose.Cells – guia completo

Se você precisar **copy pivot table** de um local para outro em uma pasta de trabalho Excel usando C#, este tutorial mostra como fazer. Você verá uma solução concisa, de ponta a ponta, que carrega a pasta de trabalho, duplica a tabela dinâmica e preserva todos os detalhes de formatação.

Trabalhar com Excel programaticamente costuma significar lidar com objetos complexos como tabelas dinâmicas. Neste guia, você aprenderá a **duplicate pivot table excel** sem perder filtros, campos calculados ou estilos. O único pré-requisito é uma referência à biblioteca Aspose.Cells, que lhe dá controle total sobre arquivos Excel a partir do .NET.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior (o código também funciona no .NET Framework 4.7+)
* Uma licença válida do Aspose.Cells for .NET (você pode usar a versão de avaliação gratuita para testes)
* Um arquivo Excel (`Source.xlsx`) que contém uma tabela dinâmica que você deseja copiar
* Um ambiente de desenvolvimento, como o Visual Studio 2022

## Como copiar tabela dinâmica com Aspose.Cells

Os passos principais são:

1. **Load Excel workbook C#** – abra o arquivo de origem.
2. **Select the range that contains the pivot table** – inclua toda a área da tabela dinâmica.
3. **Copy the range to a new location** – a tabela dinâmica permanece intacta.
4. **Save the workbook** – o novo arquivo contém a tabela dinâmica duplicada.

Cada passo é explicado abaixo com código completo.

### Etapa 1: Load Excel workbook C#

Carregar a pasta de trabalho é a primeira ação quando você **load excel workbook c#**. Aspose.Cells lê o arquivo na memória, proporcionando acesso a planilhas, células e tabelas dinâmicas.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Por que isso importa:** Carregar a pasta de trabalho cria um objeto `Workbook` que representa todo o arquivo Excel. Todas as operações subsequentes trabalham nessa representação em memória, que é mais rápida do que acessar repetidamente o sistema de arquivos.

### Etapa 2: Identify and copy the pivot table range

Uma tabela dinâmica reside dentro de um intervalo retangular de células. Para **move pivot table cell** com segurança, você deve copiar todo o intervalo, não apenas células individuais.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Por que isso funciona:** `Range.Copy` duplica não apenas os valores das células, mas também o cache subjacente da tabela dinâmica e a formatação. Esta é a maneira recomendada de **duplicate pivot table excel** sem reconstruir a tabela dinâmica manualmente.

### Etapa 3: Save the workbook with the copied pivot table

Após a cópia, basta salvar a pasta de trabalho. O novo arquivo conterá tanto a tabela dinâmica original quanto a duplicada.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Por que você deve preservar a formatação:** O requisito `preserve pivot formatting` é atendido automaticamente porque Aspose.Cells mantém as informações de estilo durante a operação de cópia. Nenhum código extra de estilo é necessário.

### Exemplo completo em funcionamento

Juntando as três etapas, você obtém um programa completo e executável:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Resultado esperado:**  
Abra `CopyPivot.xlsx` no Excel. Você verá a tabela dinâmica original inalterada e uma segunda tabela dinâmica idêntica começando na célula `I1`. Todos os filtros, campos calculados e estilos visuais correspondem ao original.

## Variações comuns e casos extremos

| Situação | Como lidar |
|-----------|------------------|
| **Tabela dinâmica abrange um intervalo dinâmico** | Use `PivotTable.PivotTableRange` para obter o endereço exato em tempo de execução ao invés de codificar fixamente `"A1:G20"`. |
| **Você precisa mover a tabela dinâmica para outra planilha** | Chame `sourceRange.Copy(otherWorksheet.Cells, "A1")` após criar `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Preservar apenas a formatação, não os dados** | Após copiar, limpe os valores de dados com `targetRange.Clear(ClearOptions.Contents)` mantendo os estilos intactos. |
| **Pastas de trabalho grandes causam pressão de memória** | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` para permitir que Aspose.Cells faça streaming dos dados. |
| **Você quer renomear a tabela dinâmica duplicada** | Acesse a nova tabela dinâmica via `sheet.PivotTables[sheet.PivotTables.Count - 1]` e defina sua propriedade `Name`. |

Essas dicas ajudam você a **move pivot table cell** posições, **duplicate pivot table excel** arquivos, e manter o requisito **preserve pivot formatting** intacto.

## Dicas profissionais para cópia confiável

* **Dica profissional:** Sempre verifique se o intervalo de origem inclui todo o cache da tabela dinâmica. A falta de uma coluna pode quebrar a tabela dinâmica copiada.
* **Cuidado com células mescladas** dentro do intervalo; elas podem fazer com que `Copy` lance uma exceção. Desmescle antes de copiar ou ajuste o intervalo.
* **Dica de desempenho:** Se você precisar copiar apenas a definição da tabela dinâmica (sem dados), use `PivotTable.Clone` ao invés de copiar todo o intervalo.

## Conclusão

Agora você sabe como **copy pivot table** programaticamente em C# usando Aspose.Cells enquanto **preserve pivot formatting**, **load excel workbook c#**, e até **move pivot table cell** posições entre planilhas. A solução completa carrega a pasta de trabalho, duplica o intervalo da tabela dinâmica e salva um novo arquivo com ambas as tabelas intactas.

Em seguida, você pode explorar cenários de **duplicate pivot table excel**, como copiar entre diferentes pastas de trabalho, ou automatizar a geração de relatórios com múltiplas tabelas dinâmicas. Para personalizações mais avançadas, confira a API PivotTable do Aspose.Cells para modificar filtros, campos calculados ou conexões de gráficos.

Feliz codificação, e sinta‑se à vontade para experimentar o código e adaptá‑lo às suas necessidades específicas de automação do Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar Nova Pasta de Trabalho Excel – Copiar & Duplicar Tabela Dinâmica](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Criar uma Tabela Dinâmica no Excel Usando Aspose.Cells para .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Alterar Efetivamente Layouts de Tabelas Dinâmicas no Excel Usando Aspose.Cells para .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}