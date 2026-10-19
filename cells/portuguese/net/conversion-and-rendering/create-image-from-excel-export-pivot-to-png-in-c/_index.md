---
category: general
date: 2026-03-21
description: Criar imagem a partir do Excel em C# usando Aspose.Cells. Aprenda como
  converter Excel em imagem, exportar pivot e salvar a imagem como PNG com um exemplo
  completo e executável.
draft: false
keywords:
- create image from excel
- convert excel to image
- how to export pivot
- how to save image
- export excel to png
language: pt
og_description: Crie imagem a partir do Excel em C# rapidamente. Este guia mostra
  como converter Excel em imagem, exportar pivô e salvar a imagem como PNG com código
  claro.
og_title: Criar imagem a partir do Excel – Exportar Tabela Dinâmica para PNG em C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Criar imagem a partir do Excel – Exportar Tabela Dinâmica para PNG em C#
url: /pt/net/conversion-and-rendering/create-image-from-excel-export-pivot-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Imagem a partir do Excel – Exportar Pivot para PNG em C#

Já precisou **criar imagem a partir do Excel** mas não tinha certeza de qual API usar? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo ao tentar transformar uma tabela dinâmica ao vivo em um PNG compartilhável.  

Neste tutorial vamos percorrer uma solução completa, pronta‑para‑executar, que **converte Excel em imagem**, mostra **como exportar pivot** e explica **como salvar a imagem** como um arquivo PNG. Ao final, você terá um único método que realiza todo o trabalho, além de dicas para casos extremos que você pode encontrar.

## O que você precisará

- **Aspose.Cells for .NET** (o pacote NuGet `Aspose.Cells`). É uma biblioteca comercial, mas oferece um modo de avaliação gratuito—perfeito para testes.  
- .NET 6+ (ou .NET Framework 4.6+).  
- Uma planilha Excel simples (`Pivot.xlsx`) que contém ao menos uma tabela dinâmica.  
- Qualquer IDE que você prefira—Visual Studio, Rider ou até mesmo VS Code funciona.

É isso. Sem DLLs extras, sem interop COM, e sem truques complicados de automação do Excel.  

Agora, vamos mergulhar no código.

## Etapa 1: Carregar a Pasta de Trabalho – Criar Imagem a partir do Excel

A primeira coisa que fazemos é abrir o arquivo Excel que contém a tabela dinâmica. Esta etapa é crucial porque o renderizador trabalha contra um objeto `Workbook` em memória.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

public class ExcelImageExporter
{
    /// <summary>
    /// Loads the workbook and prepares it for rendering.
    /// </summary>
    /// <param name="excelPath">Full path to the source .xlsx file.</param>
    /// <returns>The worksheet that contains the pivot.</returns>
    private static Worksheet LoadPivotWorksheet(string excelPath)
    {
        // Step 1: Load the workbook that contains the pivot table
        Workbook workbook = new Workbook(excelPath);

        // Assume the first sheet holds the pivot; adjust index if needed
        Worksheet pivotWorksheet = workbook.Worksheets[0];
        return pivotWorksheet;
    }
}
```

*Por que isso importa:* Carregar a pasta de trabalho nos dá acesso ao **pivot** e a qualquer formatação que será respeitada quando posteriormente **converter Excel em imagem**. Se você pular isso, o renderizador não terá nada com o que trabalhar.

## Etapa 2: Configurar Opções de Exportação – Converter Excel em Imagem

Em seguida, informamos à Aspose como queremos que a imagem final apareça. A classe `ImageOrPrintOptions` nos permite escolher PNG, definir DPI e até controlar a cor de fundo.

```csharp
private static ImageOrPrintOptions GetImageOptions()
{
    // Step 3: Configure image export options – we want a PNG image
    ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
    {
        ImageFormat = ImageFormat.Png,      // Export Excel to PNG
        HorizontalResolution = 300,         // High‑resolution output
        VerticalResolution = 300,
        OnePagePerSheet = true               // Render the whole sheet as one page
    };
    return imageOptions;
}
```

*Por que isso importa:* Definindo um DPI alto garantimos que o **export Excel to PNG** fique nítido, mesmo quando o pivot contém muitas linhas. Você pode reduzir o DPI se o tamanho do arquivo for uma preocupação.

## Etapa 3: Renderizar a Planilha – Como Exportar Pivot

Agora vem o coração do processo: transformar a planilha (com seu pivot) em uma imagem. A classe `WorksheetRender` faz o trabalho pesado.

```csharp
private static void RenderWorksheetToImage(Worksheet sheet, string outputPath)
{
    // Step 4: Create a renderer for the worksheet using the options
    WorksheetRender renderer = new WorksheetRender(sheet, GetImageOptions());

    // Step 5: Render the first page (index 0) to an image file
    renderer.ToImage(0, outputPath);
}
```

*Por que isso importa:* É aqui que **como exportar pivot** para um formato visual. O renderizador respeita toda a formatação do pivot, segmentações e estilos condicionais, de modo que o PNG parece exatamente como você vê no Excel.

## Etapa 4: Juntar Tudo – Como Salvar a Imagem

Finalmente, expomos um único método público que une todas as partes. Este é o método que você chamará a partir do seu aplicativo, serviço ou ferramenta de console.

```csharp
/// <summary>
/// Converts an Excel file containing a pivot table into a PNG image.
/// </summary>
/// <param name="excelFile">Path to the source .xlsx file.</param>
/// <param name="imageFile">Desired path for the output PNG.</param>
public static void ExportPivotToPng(string excelFile, string imageFile)
{
    Worksheet pivotWorksheet = LoadPivotWorksheet(excelFile);
    RenderWorksheetToImage(pivotWorksheet, imageFile);
}
```

### Exemplo Completo Funcional

Crie um novo projeto de console, adicione o pacote NuGet `Aspose.Cells`, e então coloque o seguinte `Program.cs` dentro:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to your environment
            string excelPath = @"C:\Temp\Pivot.xlsx";
            string pngPath   = @"C:\Temp\PivotImage.png";

            try
            {
                ExcelImageExporter.ExportPivotToPng(excelPath, pngPath);
                Console.WriteLine($"✅ Image saved successfully: {pngPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed: {ex.Message}");
            }
        }
    }

    // ----- Helper class from earlier steps -----
    public class ExcelImageExporter
    {
        private static Worksheet LoadPivotWorksheet(string excelPath)
        {
            Workbook workbook = new Workbook(excelPath);
            Worksheet pivotWorksheet = workbook.Worksheets[0];
            return pivotWorksheet;
        }

        private static ImageOrPrintOptions GetImageOptions()
        {
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300,
                OnePagePerSheet = true
            };
            return imageOptions;
        }

        private static void RenderWorksheetToImage(Worksheet sheet, string outputPath)
        {
            WorksheetRender renderer = new WorksheetRender(sheet, GetImageOptions());
            renderer.ToImage(0, outputPath);
        }

        public static void ExportPivotToPng(string excelFile, string imageFile)
        {
            Worksheet pivotWorksheet = LoadPivotWorksheet(excelFile);
            RenderWorksheetToImage(pivotWorksheet, imageFile);
        }
    }
}
```

**Resultado esperado:** Depois de executar o programa, `PivotImage.png` aparecerá na pasta que você especificou, mostrando uma captura de tela pixel‑perfeita da tabela dinâmica.

![exemplo de criação de imagem a partir do Excel mostrando a tabela dinâmica exportada como PNG](https://example.com/placeholder.png "Exemplo de criação de imagem a partir do Excel")

*Alt text:* exemplo de criação de imagem a partir do Excel mostrando a tabela dinâmica exportada como PNG.

## Perguntas Frequentes & Casos Limite

### E se minha pasta de trabalho tiver várias planilhas?

O helper atualmente obtém `Worksheets[0]`. Para direcionar uma planilha específica, passe o nome da planilha:

```csharp
Worksheet pivotWorksheet = workbook.Worksheets["SalesPivot"];
```

### O PNG está borrado—como corrigir?

Aumente `HorizontalResolution` e `VerticalResolution` em `GetImageOptions`. Valores entre 300–600 DPI geralmente produzem resultados nítidos. Lembre-se, DPI mais alto significa tamanho de arquivo maior.

### Meu pivot abrange mais de uma página—posso exportar todas as páginas?

Sim. Percorra `renderer.PageCount` e chame `ToImage(pageIndex, ...)` para cada página, ou defina `OnePagePerSheet = false` para obter imagens separadas por página.

### Preciso apenas de uma parte da planilha (por exemplo, um intervalo específico)?

Use `ImageOrPrintOptions` para definir `PrintArea`:

```csharp
imageOptions.PrintArea = "A1:D20";
```

Dessa forma você **converte Excel em imagem** apenas para a área que lhe interessa.

### Isso funciona com arquivos .xls (Excel 97‑2003)?

Absolutamente. Aspose.Cells abstrai o formato do arquivo, então você pode fornecer `.xls`, `.xlsx`, `.xlsm` ou até mesmo `.ods` e ainda **exportar excel para png**.

## Dicas Profissionais & Armadilhas

- **Licença importa**: No modo de avaliação, Aspose adiciona uma marca d'água. Implante uma licença adequada para produção.  
- **Uso de memória**: Renderizar pastas de trabalho grandes pode consumir muita memória. Libere o objeto `Workbook` prontamente ou envolva-o em um bloco `using`.  
- **Segurança de thread**: `Workbook` não é thread‑safe. Crie uma nova instância por requisição se você estiver em um serviço web.  
- **Flexibilidade de formato de imagem**: Se precisar de JPEG ou BMP, basta mudar `ImageFormat` em `GetImageOptions`.  

## Conclusão

Agora você tem uma receita sólida, de ponta a ponta, para **criar imagem a partir do Excel**, especificamente para **exportar pivot** como PNG de alta qualidade. O trecho acima mostra o código completo e executável, explica **como salvar a imagem**, e cobre variações como múltiplas planilhas ou áreas de impressão personalizadas.  

Próximos passos? Tente encadear este exportador com um serviço de e‑mail para enviar o PNG automaticamente, ou experimente `ImageOrPrintOptions` para gerar PDFs em vez de PNGs. O mesmo padrão funciona para tarefas de **converter excel em imagem** em diversos formatos.

Tem mais perguntas? Deixe um comentário, e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}