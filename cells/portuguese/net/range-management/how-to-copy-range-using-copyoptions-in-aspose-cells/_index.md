---
category: general
date: 2026-11-19
description: Aprenda como copiar intervalos usando CopyOptions no Aspose.Cells, preservando
  a formatação e as tabelas dinâmicas ao copiar um intervalo do Excel com formatação.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: pt
lastmod: 2026-11-19
og_description: Copiar intervalo usando CopyOptions no Aspose.Cells permite duplicar
  dados do Excel com formatação completa e tabelas dinâmicas preservadas, possibilitando
  a manipulação confiável da pasta de trabalho.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Copiar intervalo usando CopyOptions no Aspose.Cells – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como copiar intervalo usando CopyOptions no Aspose.Cells
url: /pt/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar intervalo usando CopyOptions no Aspose.Cells

Se você precisar **copy range using CopyOptions** no Aspose.Cells, este guia mostra exatamente como duplicar um bloco de células mantendo toda a formatação e tabelas dinâmicas incorporadas intactas. Muitos desenvolvedores têm dificuldade em preservar o estilo ao mover dados entre planilhas, e a classe `CopyOptions` resolve esse problema sem etapas manuais adicionais.

Neste tutorial você aprenderá a:

* Definir áreas de origem e destino em uma pasta de trabalho do Excel.  
* Usar `CopyOptions` para manter a formatação das células, larguras de coluna e tabelas dinâmicas.  
* Salvar o resultado em um novo arquivo pronto para processamento posterior.

O exemplo funciona com qualquer arquivo `.xlsx` e requer apenas a biblioteca Aspose.Cells for .NET.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior instalado.  
* Uma licença válida do Aspose.Cells for .NET (ou uma chave de avaliação gratuita).  
* Visual Studio 2022 ou qualquer IDE C# de sua preferência.  

Nenhum pacote NuGet adicional é necessário além de `Aspose.Cells`.

## Etapa 1: Configurar o projeto e importar namespaces

Crie uma nova aplicação console e adicione a referência ao Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

A diretiva `using Aspose.Cells;` fornece acesso a `Workbook`, `CellArea` e `CopyOptions`.

## Etapa 2: Carregar a pasta de trabalho que você deseja modificar

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` representa o arquivo Excel completo. Substitua `YOUR_DIRECTORY` pela pasta que contém seu arquivo de origem.

## Etapa 3: Definir os intervalos de origem e destino

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` cria uma área retangular com base nos endereços das células superior‑esquerda e inferior‑direita. Você pode ajustar as coordenadas para corresponder ao tamanho do bloco que precisa copiar.

## Etapa 4: Copiar o intervalo preservando a formatação e tabelas dinâmicas

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

O objeto `CopyOptions` informa ao Aspose.Cells exatamente o que manter. Definir `CopyPivotTables = true` é a chave para **copy range using CopyOptions** quando sua origem inclui tabelas dinâmicas. As demais flags garantem que **copy excel range with formatting** seja alcançado automaticamente — nenhum código extra é necessário para reaplicar estilos após a cópia.

### Por que `CopyOptions` é importante

* **Performance** – A biblioteca realiza uma única operação interna em vez de copiar células uma a uma.  
* **Accuracy** – Todos os aspectos visuais (fontes, cores, bordas) permanecem após a movimentação, o que elimina desvios visuais em relatórios gerados.  
* **Reliability** – As tabelas dinâmicas permanecem funcionais porque seu cache e referências de origem são duplicados.

## Etapa 5: Salvar a pasta de trabalho modificada

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Após chamar `Save`, o arquivo `output.xlsx` contém os dados originais mais o bloco duplicado na localização de destino, completo com formatação e tabelas dinâmicas.

## Código-fonte completo para referência

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Executar este programa exibe:

```
Range copied successfully. Output saved to output.xlsx
```

Abra `output.xlsx` no Excel – você verá o bloco A1:H30 duplicado em A35:H64, com todas as cores de célula, bordas, formatos numéricos e quaisquer tabelas dinâmicas intactas.

## Perguntas comuns e tratamento de casos extremos

### E se a área de destino sobrepor a origem?

Aspose.Cells lança uma `ArgumentException`. Para evitar isso, calcule um destino que não intersecte a origem, ou copie para uma planilha diferente:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Como copiar entre diferentes pastas de trabalho?

Crie uma segunda instância `Workbook` para o arquivo de destino e use o mesmo objeto `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### O `CopyOptions` também copia células mescladas?

Sim. A flag `CopyStyle` inclui informações de células mescladas. Se precisar de controle mais fino, defina `options.CopyMergedCells = true` (disponível em versões mais recentes).

### E quanto a intervalos grandes (milhares de linhas)?

A operação é eficiente em memória, mas você pode querer aumentar o `WorkbookSettings` `MemorySetting` para `MemorySetting.MemoryPreference` em arquivos muito grandes.

## Dicas profissionais

* **Reuse the same `CopyOptions`** instance for multiple copy operations – it reduces object allocation overhead.  
* **Validate ranges** before copying: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` ajuda a detectar erros de digitação cedo.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) ao copiar grandes conjuntos de dados para acelerar o processo, depois chame `workbook.CalculateFormula()` após a cópia se precisar de resultados atualizados.

## Conclusão

Agora você sabe como **copy range using CopyOptions** no Aspose.Cells, alcançando um completo **copy excel range with formatting** enquanto preserva tabelas dinâmicas e outros recursos avançados. Essa abordagem elimina a reaplicação manual de estilos e garante que sua automação Excel permaneça robusta e mantível.

Próximos passos que você pode explorar:

* Usar `CopyOptions` para duplicar planilhas inteiras.  
* Combinar a operação de cópia com `WorksheetCollection.AddCopy` para geração de relatórios baseada em modelo.  
* Integrar o código em uma API ASP.NET Core para fornecer transformações Excel em tempo real.

Sinta‑se à vontade para experimentar diferentes coordenadas de origem/destino e compartilhar seus resultados nos comentários!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}