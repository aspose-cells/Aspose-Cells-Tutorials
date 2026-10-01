---
category: general
date: 2026-10-01
description: Aprenda como converter Excel para SVG e salvar o arquivo Excel como SVG
  usando Aspose.Cells. Siga este tutorial completo para exportar planilhas do Excel
  como imagens SVG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to svg
- save excel file as svg
- how to export excel to svg
- export excel worksheet as svg
language: pt
lastmod: 2026-10-01
og_description: Converter Excel para SVG usando Aspose.Cells. Este tutorial explica
  como exportar planilhas do Excel como imagens SVG, abordando a configuração, o código
  e casos extremos.
og_image_alt: Diagram illustrating the convert excel to svg workflow
og_title: Converter Excel para SVG com Aspose.Cells – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  headline: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert Excel to SVG and save Excel file as SVG using
    Aspose.Cells. Follow this complete tutorial to export Excel worksheets as SVG
    images.
  name: How to convert Excel to SVG with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Exporting multiple worksheets at once
    text: 'When a workbook contains several sheets, you can let Aspose.Cells generate
      a separate SVG for each sheet automatically:'
  - name: Controlling SVG dimensions
    text: 'SVG files are vector‑based, but you can still influence the viewport size:'
  - name: Handling formulas and calculated values
    text: 'By default, Aspose.Cells evaluates formulas before rendering. If you want
      to export raw formulas as text, set:'
  - name: Performance tips
    text: '- **Reuse `ImageOrPrintOptions`**: Create the options once and reuse them
      for multiple workbooks to avoid unnecessary allocations. - **Stream output**:
      If you are building a web API, write the SVG directly to a `MemoryStream` and
      return it as a file result instead of saving to disk.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- SVG export
title: Como converter Excel para SVG com Aspose.Cells – guia passo a passo
url: /pt/net/conversion-and-rendering/how-to-convert-excel-to-svg-with-aspose-cells-step-by-step-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter Excel para SVG com Aspose.Cells – guia passo a passo

Se você precisa **converter Excel para SVG**, este guia mostra exatamente como exportar uma planilha do Excel como uma imagem SVG usando Aspose.Cells. Você verá um exemplo completo e executável que salva um arquivo Excel como SVG e entenderá por que cada configuração é importante.

Exportar planilhas como gráficos vetoriais escaláveis é útil quando você deseja renderização nítida em páginas da web, relatórios ou documentação sem perder qualidade. As etapas abaixo cobrem tudo, desde a instalação da biblioteca até o tratamento de várias planilhas e armadilhas comuns.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7.2+)
- Uma licença válida do Aspose.Cells ou uma chave de avaliação gratuita
- Uma pasta de trabalho Excel (`input.xlsx`) que você deseja converter
- Visual Studio 2022 ou qualquer editor C# de sua escolha

Nenhum pacote NuGet adicional é necessário além do `Aspose.Cells`.

## Etapa 1: Instalar Aspose.Cells

A abordagem padrão é adicionar o pacote Aspose.Cells via NuGet. Abra um terminal na pasta do seu projeto e execute:

```bash
dotnet add package Aspose.Cells --version 24.10
```

Este comando baixa a versão estável mais recente (24.10 no momento da escrita) e atualiza seu arquivo de projeto. Usar a versão mais recente garante compatibilidade com os recursos mais novos do Excel e melhorias no SVG.

## Etapa 2: Carregar a pasta de trabalho Excel

Carregar a pasta de trabalho é a primeira operação concreta no pipeline de **convert excel to svg**. A classe `Workbook` representa todo o arquivo Excel e fornece acesso às suas planilhas, fórmulas e formatações.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the source workbook
var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Optional: verify that the workbook loaded correctly
Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");
```

**Por que isso importa:**  
Se o arquivo não puder ser aberto (por exemplo, caminho errado ou formato não suportado), o Aspose.Cells lança uma exceção informativa que você pode capturar e registrar. Validar a contagem de planilhas logo no início ajuda a decidir se você exporta uma única planilha ou a pasta de trabalho inteira.

## Etapa 3: Configurar opções de renderização SVG

Para **save excel file as svg**, você deve criar uma instância de `ImageOrPrintOptions` e definir seu `SaveFormat` como `SaveFormat.Svg`. Também é possível ajustar a qualidade da imagem, escala e se as fontes serão incorporadas.

```csharp
// Set up rendering options for SVG output
var imageOptions = new ImageOrPrintOptions
{
    // Export format must be SVG
    SaveFormat = SaveFormat.Svg,

    // Preserve the original aspect ratio
    OnePagePerSheet = true,

    // Optional: increase resolution for sharper vectors
    // (SVG is resolution‑independent, but this affects rasterized elements)
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Explicação:**  
`OnePagePerSheet = true` força cada planilha a ficar em uma única página SVG, que geralmente é o que você deseja para incorporação na web. Alterar a resolução influencia como imagens raster incorporadas (por exemplo, fotos dentro de células) são renderizadas dentro do SVG.

## Etapa 4: Salvar a pasta de trabalho como imagem SVG

Agora você pode **export excel worksheet as svg** chamando `Workbook.Save` com o caminho de destino e as opções que acabou de configurar.

```csharp
// Define the output path
string outputPath = @"YOUR_DIRECTORY\output.svg";

// Save the workbook (or a specific worksheet) as SVG
workbook.Save(outputPath, imageOptions);

Console.WriteLine($"Workbook exported to SVG at: {outputPath}");
```

Se precisar exportar apenas uma única planilha em vez da pasta de trabalho inteira, recupere a planilha e use `SheetRender`:

```csharp
// Export only the first worksheet
var sheet = workbook.Worksheets[0];
var sheetRender = new SheetRender(sheet, imageOptions);
sheetRender.ToImage(0, outputPath); // 0 = first page
```

**Por que isso funciona:**  
`Workbook.Save` itera sobre todas as planilhas quando `OnePagePerSheet` está true, gerando um arquivo SVG por planilha se o caminho de saída contiver um placeholder (por exemplo, `output_{0}.svg`). Usar `SheetRender` dá controle preciso sobre quais planilha(s) você exporta.

## Etapa 5: Verificar a saída SVG

Após a conversão terminar, abra o arquivo `.svg` resultante em um navegador ou editor SVG (por exemplo, Inkscape). Você deverá ver texto, bordas de células e quaisquer imagens incorporadas renderizadas como vetores escaláveis.

```bash
# On macOS or Linux you can open the file directly:
open YOUR_DIRECTORY/output.svg
```

Se o SVG aparecer vazio ou com formatação ausente, verifique:

1. Se a pasta de trabalho realmente contém dados na planilha de destino.
2. Se linhas/colunas ocultas estão mascarando o conteúdo (use `sheet.IsVisible`).
3. Se as fontes usadas na pasta de trabalho estão instaladas na máquina; caso contrário, o Aspose.Cells as substitui, o que pode afetar a aparência.

## Considerações avançadas

### Exportar várias planilhas de uma vez

Quando uma pasta de trabalho contém várias planilhas, você pode deixar o Aspose.Cells gerar um SVG separado para cada planilha automaticamente:

```csharp
// Use a placeholder {0} for sheet index
string multiOutput = @"YOUR_DIRECTORY\output_{0}.svg";
workbook.Save(multiOutput, imageOptions);
```

A biblioteca substitui `{0}` pelo índice da planilha (começando em 0). Isso é útil para processamento em lote de relatórios grandes.

### Controlar dimensões do SVG

Arquivos SVG são baseados em vetores, mas ainda é possível influenciar o tamanho da viewport:

```csharp
imageOptions.PageWidth = 800;   // width in pixels (converted to SVG points)
imageOptions.PageHeight = 600;  // height in pixels
```

Definir dimensões explícitas garante layout consistente ao incorporar o SVG em contêineres HTML.

### Manipular fórmulas e valores calculados

Por padrão, o Aspose.Cells avalia fórmulas antes da renderização. Se quiser exportar as fórmulas brutas como texto, defina:

```csharp
imageOptions.ExportFormulasAsString = true;
```

Esta opção é útil para documentação onde você precisa mostrar a fórmula real do Excel em vez do seu resultado calculado.

### Dicas de desempenho

- **Reutilizar `ImageOrPrintOptions`**: Crie as opções uma única vez e reutilize‑as para várias pastas de trabalho, evitando alocações desnecessárias.
- **Fluxo de saída**: Se você estiver construindo uma API web, escreva o SVG diretamente para um `MemoryStream` e retorne‑o como resultado de arquivo em vez de salvá‑lo no disco.

```csharp
using (var stream = new MemoryStream())
{
    workbook.Save(stream, imageOptions);
    // Reset position before reading
    stream.Position = 0;
    // Return stream to caller (e.g., ASP.NET Core FileResult)
}
```

## Armadilhas comuns e como evitá‑las

| Sintoma | Causa | Solução |
|--------|-------|-----|
| Arquivo SVG em branco | Pasta de trabalho fonte tem linhas/colunas ocultas ou planilha de tamanho zero | Desocultar linhas/colunas ou definir `sheet.IsVisible = true` |
| Fontes ausentes | Fonte não instalada no servidor | Instalar a fonte necessária ou incorporá‑la usando `imageOptions.EmbeddedFonts = true` |
| Vários arquivos SVG com nomes inesperados | Caminho de saída não contém placeholder `{0}` | Use `output_{0}.svg` para gerar arquivos por planilha |
| Conversão lenta para pastas de trabalho grandes | Renderizando cada planilha individualmente sem `OnePagePerSheet` | Habilite `OnePagePerSheet` ou processe planilhas em paralelo usando `Task.Run` |

## Exemplo completo e executável

Abaixo está um aplicativo console autocontido que demonstra **como exportar Excel para SVG** do início ao fim. Substitua `YOUR_DIRECTORY` por uma pasta real em sua máquina.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToSvgDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
            var workbook = new Workbook(workbookPath);
            Console.WriteLine($"Loaded {workbook.Worksheets.Count} worksheet(s).");

            // 2️⃣ Configure SVG options
            var svgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Svg,
                OnePagePerSheet = true,
                HorizontalResolution = 300,
                VerticalResolution = 300,
                // Optional: set explicit dimensions
                // PageWidth = 800,
                // PageHeight = 600
            };

            // 3️⃣ Export each sheet as a separate SVG file
            string outputPattern = @"YOUR_DIRECTORY\output_{0}.svg";
            workbook.Save(outputPattern, svgOptions);
            Console.WriteLine("Export completed. SVG files created:");

            for (int i = 0; i < workbook.Worksheets.Count; i++)
            {
                Console.WriteLine($"\t{string.Format(outputPattern, i)}");
            }
        }
    }
}
```

**Saída esperada** (console):

```
Loaded 2 worksheet(s).
Export completed. SVG files created:
    YOUR_DIRECTORY\output_0.svg
    YOUR_DIRECTORY\output_1.svg
```

Abra qualquer um dos arquivos `.svg` gerados em um navegador para verificar se a conversão foi bem‑sucedida.

## Conclusão

Agora você sabe como **converter Excel para SVG** usando Aspose.Cells, desde a instalação da biblioteca até o tratamento de várias planilhas e o ajuste fino das opções de renderização. O tutorial cobriu todo o fluxo de trabalho para **save excel file as svg**, explicou por que cada configuração importa e destacou casos de borda como linhas ocultas, incorporação de fontes e considerações de desempenho.

Em seguida, você pode explorar:

- **Como exportar Excel para SVG** em uma API web (transmitindo o SVG diretamente ao cliente)
- Conversão de Excel para outros formatos vetoriais como PDF ou EMF
- Uso do Aspose.Slides para incorporar o SVG gerado em apresentações PowerPoint

Sinta‑se à vontade para experimentar escala, estilos personalizados ou combinar a saída SVG com HTML/CSS para relatórios interativos. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Convert Excel Sheets to SVG using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/convert-excel-to-svg-aspose-cells-java/)
- [Convert Excel to SVG Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/convert-excel-to-svg-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells in Java](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}