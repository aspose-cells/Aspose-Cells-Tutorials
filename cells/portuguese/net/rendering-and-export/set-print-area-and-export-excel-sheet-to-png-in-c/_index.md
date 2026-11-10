---
category: general
date: 2026-10-26
description: Defina a área de impressão e exporte uma planilha do Excel para PNG em
  C#. Aprenda as opções de exportação de imagem, como exportar PNG e obter uma imagem
  imprimível a partir de uma pasta de trabalho.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: pt
lastmod: 2026-10-26
og_description: Defina a área de impressão e exporte uma planilha do Excel para PNG
  em C#. Este tutorial passo a passo aborda as opções de exportação de imagem e como
  exportar PNG de uma pasta de trabalho.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Defina a área de impressão e exporte a planilha do Excel para PNG – Guia
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Definir área de impressão e exportar planilha do Excel para PNG em C#
url: /pt/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definir área de impressão e exportar planilha Excel para PNG em C#

Se você precisar **definir a área de impressão** antes de exportar uma planilha Excel para PNG, este guia mostra como fazer. Você verá um exemplo completo em C# que configura as opções de exportação de imagem, ajusta a área de impressão da planilha e salva o resultado como uma imagem.

Exportar uma planilha Excel para PNG é uma necessidade comum quando você deseja incorporar uma captura da planilha em um relatório, e‑mail ou página da web. O código abaixo funciona com qualquer pasta de trabalho que contenha uma tabela dinâmica, mas a técnica também se aplica a intervalos de dados regulares. Nenhuma ferramenta externa é necessária — apenas a biblioteca Aspose.Cells para .NET.

## Pré-requisitos

- .NET 6.0 ou posterior (o exemplo tem como alvo .NET 6, mas qualquer versão recente do .NET funciona)
- Aspose.Cells para .NET (instale via NuGet: `Install-Package Aspose.Cells`)
- Familiaridade básica com C# e conceitos do Excel, como planilhas e áreas de impressão

## Etapa 1: Configurar opções de exportação de imagem

A primeira coisa que você faz é criar uma instância de `ImageOrPrintOptions`. Esse objeto informa ao Aspose.Cells como renderizar a planilha como uma imagem.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Por que isso importa:** `ImageOrPrintOptions` controla o formato de saída, a resolução e outros detalhes de renderização. Usar PNG garante qualidade sem perdas, o que é ideal para relatórios que exigem texto e gráficos nítidos.

## Etapa 2: Carregar a pasta de trabalho e acessar a planilha de destino

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Por que isso importa:** Você deve trabalhar com um objeto `Worksheet` específico porque a área de impressão é uma configuração ao nível da planilha.

## Etapa 3: Identificar o intervalo que você deseja imprimir

Em muitos cenários, os dados que você deseja estão dentro de uma tabela dinâmica. O código a seguir extrai o intervalo de dados da primeira tabela dinâmica na planilha.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Se sua planilha não contiver uma tabela dinâmica, você pode substituir `pivotDataRange` por qualquer `CellArea` que criar manualmente, por exemplo:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Etapa 4: **Definir área de impressão** para corresponder ao intervalo selecionado

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Por que isso importa:** A área de impressão indica ao Excel (e ao Aspose.Cells) quais células incluir ao renderizar a planilha como imagem. Ao alinhar a área de impressão com o intervalo de dados da tabela dinâmica, você evita margens em branco e garante que o PNG exportado contenha apenas os dados relevantes.

## Etapa 5: Exportar a planilha para uma imagem PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Por que isso importa:** `worksheet.ToImage` respeita a área de impressão definida anteriormente, portanto o arquivo PNG contém exatamente as células que você definiu. Atribuir a imagem a uma forma de imagem permite incorporá‑la novamente na pasta de trabalho, se necessário, enquanto salvá‑la no disco fornece um arquivo independente.

## Exemplo completo em funcionamento

Juntando todas as etapas, obtém‑se um programa autônomo que pode ser executado imediatamente.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Saída esperada

Executar o programa cria `C:\Temp\WorksheetExport.png`. Ao abrir o arquivo, você vê uma imagem PNG nítida que contém apenas as células definidas pela **área de impressão definida** (os dados da tabela dinâmica neste exemplo). A imagem pode ser inserida em documentos Word, slides PowerPoint ou páginas da web sem etapas adicionais de conversão.

## Manipulando múltiplas planilhas ou tabelas dinâmicas

- **Múltiplas planilhas:** Percorra `wb.Worksheets` e repita as etapas 3‑5 para cada planilha que precisar exportar.
- **Múltiplas tabelas dinâmicas:** Escolha o `PivotTables[index]` apropriado ou itere sobre `worksheet.PivotTables` para exportar cada tabela individualmente.
- **Sem tabela dinâmica:** Crie um `CellArea` manualmente (veja o comentário na Etapa 3) e atribua‑o a `PrintArea`.

## Dicas práticas (E‑E‑A‑T)

- **Dica profissional:** Defina `HorizontalResolution` e `VerticalResolution` para 300 DPI para PNGs prontos para impressão; valores menores reduzem o tamanho do arquivo para uso na web.
- **Atenção a formas de imagem vazias:** Se a planilha não tiver formas de imagem, adicione uma antes de atribuir a imagem:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Desempenho:** Reutilizar uma única instância de `ImageOrPrintOptions` para várias planilhas evita alocações desnecessárias.
- **Compatibilidade:** Aspose.Cells 23.9+ suporta totalmente .NET 6 e posteriores; versões anteriores podem exigir ajustes nos nomes da API.

## Conclusão

Agora você sabe como **definir a área de impressão** e exportar um Excel

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como exportar Excel para PNG – guia completo passo a passo](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Como exportar intervalo do Excel como imagem com C# e Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [planilha Excel para PNG – Exportar uma Tabela Dinâmica como PNG em C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}