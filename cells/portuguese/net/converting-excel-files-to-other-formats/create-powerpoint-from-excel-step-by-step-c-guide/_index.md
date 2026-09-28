---
category: general
date: 2026-03-30
description: Crie PowerPoint a partir do Excel rapidamente usando Aspose.Cells e Aspose.Slides.
  Aprenda como exportar a planilha como imagem e salvar a apresentação como PPTX em
  C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: pt
og_description: Crie PowerPoint a partir do Excel em C# com Aspose. Exporte a planilha
  como imagem, mantenha as formas editáveis e salve o resultado como PPTX.
og_title: Criar PowerPoint a partir do Excel – Tutorial Completo de C#
tags:
- Aspose
- C#
- Office Automation
title: Criar PowerPoint a partir do Excel – Guia passo a passo em C#
url: /pt/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PowerPoint a partir do Excel – Tutorial Completo em C#

Já precisou **criar PowerPoint a partir do Excel** mas não tinha certeza de qual biblioteca poderia manter seus gráficos editáveis? Você não está sozinho. Em muitos cenários de relatório você desejará transformar uma planilha em um conjunto de slides sem perder a capacidade de ajustar caixas de texto posteriormente. Este guia mostra exatamente como **converter Excel para PowerPoint** usando Aspose.Cells e Aspose.Slides, além de abordar como **exportar a planilha como imagem** e, finalmente, **salvar a apresentação como PPTX**.

Vamos percorrer cada linha de código, explicar *por que* cada configuração importa e até discutir o que fazer se sua pasta de trabalho contiver gráficos complexos que você prefira exportar como imagem. Ao final, você terá um aplicativo console C# pronto‑para‑executar que recebe `ShapesDemo.xlsx` e gera `Result.pptx` – tudo com caixas de texto editáveis e imagens nítidas.

## O que você precisará

- .NET 6.0 ou posterior (a API funciona também com .NET Framework, mas .NET 6 é o ponto ideal).  
- Pacotes NuGet **Aspose.Cells** e **Aspose.Slides** (licenças de avaliação gratuitas funcionam para testes).  
- Um conhecimento básico da sintaxe C# – se você consegue escrever um `Console.WriteLine`, está pronto para prosseguir.  

Sem interop COM adicional, sem Office instalado no servidor e sem copiar‑colar manual de imagens. Tudo é tratado programaticamente.

---

## Criar PowerPoint a partir do Excel – Carregar a Pasta de Trabalho e Definir Opções de Exportação

A primeira coisa que fazemos é abrir o arquivo Excel e informar ao Aspose.Cells como queremos que a planilha seja renderizada. O objeto `ImageOrPrintOptions` é onde a mágica acontece: habilitamos `ExportShapes` e `ExportEditableTextBoxes` para que quaisquer formas (incluindo gráficos) se tornem parte do slide **e** permaneçam editáveis após a conversão.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Por que essas flags?**  
- `OnePagePerSheet` impede que a planilha seja dividida em vários slides – você obtém uma única imagem em tamanho completo.  
- `ExportShapes` instrui o Aspose.Cells a rasterizar gráficos *e* formas vetoriais, preservando sua aparência.  
- `ExportEditableTextBoxes` é o ingrediente secreto que permite dar um duplo clique em uma caixa de texto no PowerPoint e editar o texto sem abrir o Excel novamente.

> **Dica profissional:** Se você precisar apenas de uma imagem estática de um gráfico, defina `ExportShapes = false` e use o método `ExportExcelChartAsPicture` mais tarde (veja a seção final).

## Converter Excel para PowerPoint – Gerar Imagem a partir da Planilha

Com as opções prontas, agora transformamos a planilha em um `System.Drawing.Image`. O `WorksheetToImageConverter` faz o trabalho pesado, aplicando as configurações que acabamos de definir.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

O argumento `0` indica a primeira página (temos apenas uma por causa do `OnePagePerSheet`). O `sheetImage` resultante mantém o DPI original, então seu slide não ficará pixelado mesmo em telas de alta resolução.

## Salvar Apresentação como PPTX – Inserir Imagem em um Slide

Agora criamos um novo arquivo PowerPoint, adicionamos um slide e inserimos o bitmap nele. O Aspose.Slides trata a imagem como uma forma de *quadro de imagem*, que você pode redimensionar ou mover posteriormente como qualquer objeto nativo do PowerPoint.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **E se a imagem for maior que o tamanho do slide?**  
> O PowerPoint recortará automaticamente tudo que exceder as dimensões do slide. Uma solução rápida é escalar a imagem antes de inseri‑la:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Você pode então passar `newWidth` e `newHeight` para `AddPictureFrame`.

## Exportar Planilha como Imagem – Salvar o Arquivo PPTX

Finalmente persistimos a apresentação no disco. A flag `SaveFormat.Pptx` garante o formato OpenXML moderno, que funciona em todas as versões recentes do PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Ao abrir `Result.pptx` você verá um único slide que parece exatamente com sua planilha Excel, mas ainda pode clicar em qualquer caixa de texto e editar seu conteúdo diretamente no PowerPoint.

## Exportar Gráfico do Excel como Imagem – Quando Imagens Rasterizadas São Preferidas

Às vezes você não precisa de formas editáveis; um PNG de alta qualidade de um gráfico basta. O Aspose.Cells pode exportar um gráfico específico para uma imagem sem converter a planilha inteira:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Você pode então incorporar `chart.png` em um slide da mesma forma que adicionamos `sheetImage`. Essa abordagem reduz o tamanho do arquivo PPTX e é útil quando os dados ao redor não são necessários no slide.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| **Texto parece borrado** | Exportado com DPI baixo (padrão 96). | Defina `imageOptions.Dpi = 300;` antes da conversão. |
| **Formas desaparecem** | `ExportShapes` deixado como `false`. | Garanta `ExportShapes = true` quando precisar de gráficos editáveis. |
| **Descompasso de tamanho do slide** | Imagem maior que as dimensões do slide. | Escale a imagem (veja o trecho de código) ou altere o tamanho do slide via `presentation.SlideSize`. |
| **Exceção de licença** | Usando versão de avaliação sem ativação adequada. | Chame `License license = new License(); license.SetLicense("Aspose.Total.lic");` no início do `Main`. |

## Exemplo Completo Funcional (Pronto para Copiar‑Colar)

Abaixo está o programa completo, pronto para ser inserido em um novo projeto console. Substitua `YOUR_DIRECTORY` pela pasta que contém seu arquivo Excel.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Saída esperada:**  
Ao executar o programa ele imprime `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Abrindo o PPTX você verá um único slide que espelha a planilha Excel original, com caixas de texto editáveis.

## Recapitulação & Próximos Passos

Agora você sabe como **criar PowerPoint a partir do Excel** usando as poderosas APIs da Aspose, como **exportar a planilha como imagem**, e como **salvar a apresentação como PPTX** preservando a editabilidade. O mesmo padrão funciona para pastas de trabalho com várias planilhas — basta percorrer `workbook.Worksheets` e adicionar um novo slide para cada uma.

**O que explorar a seguir?**  

- **Conversão em lote:** Percorra uma pasta de arquivos Excel e gere um conjunto de slides por arquivo.  
- **Layouts dinâmicos:** Use `slide.LayoutSlide` para aplicar modelos PowerPoint pré‑designados.  
- **Exportação apenas de gráfico:** Combine o trecho “Exportar gráfico do Excel como imagem” com marcadores de posição de slide para um deck mais enxuto.  
- **Estilização avançada:** Aplique fundos de slide personalizados, transições ou animações via Aspose.Slides.  

Sinta‑se à vontade para experimentar — altere o DPI, troque `ShapeType.Ellipse` por um quadro de imagem circular, ou até mesmo incorpore múltiplas imagens por slide. O céu é o limite quando você tem controle programático sobre

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}