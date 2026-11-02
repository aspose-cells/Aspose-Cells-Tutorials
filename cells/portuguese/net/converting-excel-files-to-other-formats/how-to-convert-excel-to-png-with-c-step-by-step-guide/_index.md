---
category: general
date: 2026-10-10
description: Converter Excel para PNG rapidamente usando Aspose.Cells em C#. Aprenda
  a exportar intervalo do Excel, salvar Excel como PNG e converter planilha em imagem
  em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: pt
lastmod: 2026-10-10
og_description: Converta o Excel para PNG instantaneamente com Aspose.Cells. Este
  tutorial mostra como exportar um intervalo do Excel, salvar o Excel como PNG e converter
  a planilha em imagem.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Converter Excel para PNG com C# – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Como converter Excel para PNG com C# – guia passo a passo
url: /pt/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter Excel para PNG com C# – guia passo a passo

Se você precisa **converter Excel para PNG** programaticamente, este guia mostra exatamente como fazer isso usando Aspose.Cells for .NET. Seja construindo um serviço de relatórios ou um painel automatizado, você aprenderá a exportar um intervalo do Excel, salvar o resultado como um arquivo PNG e lidar com casos de borda comuns.

Você percorrerá cada passo necessário—desde adicionar o pacote NuGet até renderizar uma área específica da planilha—para que possa integrar a solução em qualquer projeto C# sem precisar buscar recursos adicionais.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior (o código também funciona com .NET Framework 4.6+)
* Visual Studio 2022 (ou qualquer IDE que suporte C#)
* Uma licença válida do Aspose.Cells for .NET (a avaliação gratuita funciona para testes)
* Um arquivo Excel chamado **Pivot.xlsx** localizado em uma pasta que você pode referenciar (o tutorial usa `YOUR_DIRECTORY` como placeholder)

> **Dica:** Instale o pacote Aspose.Cells via o Console do Gerenciador de Pacotes NuGet:  
> `Install-Package Aspose.Cells`

## Converter Excel para PNG – walkthrough completo do código

O programa completo a seguir carrega uma pasta de trabalho, configura opções de imagem e renderiza um intervalo de células definido para um arquivo PNG. Todas as diretivas `using` necessárias estão incluídas, para que você possa copiar o código para um novo projeto de console e executá‑lo imediatamente.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Como o código funciona

* **Carregando a pasta de trabalho** – `Workbook` lê o arquivo `.xlsx` na memória, proporcionando acesso a todas as planilhas.
* **ImageOrPrintOptions** – Este objeto indica ao Aspose.Cells que produza um PNG (`ImageFormat.Png`). Você também pode ajustar DPI, escala ou cor de fundo, se necessário.
* **RenderRangeToImage** – O método `RenderRangeToImage` recebe três argumentos: o intervalo de células (`"A1:H30"`), o caminho do arquivo de destino e as opções de imagem. Esta é a operação principal que **exporta intervalo do Excel** para uma imagem PNG.
* **Resultado** – Após a execução, você encontrará `Pivot.png` na pasta especificada, contendo uma representação visual exata das células selecionadas.

## Exportar intervalo do Excel para PNG – personalizando a saída

Se você precisar **exportar intervalo do Excel** diferente de `A1:H30`, basta alterar a variável `range`. O método aceita qualquer endereço no estilo Excel, incluindo intervalos nomeados:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Você também pode exportar a planilha inteira usando `"A1:Z1000"` (ou um endereço maior) ou chamando `RenderToImage` sem um parâmetro de intervalo.

## Salvar Excel como PNG com configurações adicionais

Às vezes você deseja que o PNG corresponda a uma resolução específica para impressão ou uso na web. Ajuste o `ImageOrPrintOptions` da seguinte forma:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Essas configurações ilustram como **salvar Excel como PNG** com DPI e transparência personalizados, proporcionando controle total sobre a qualidade final da imagem.

## Como exportar Excel – lidando com múltiplas planilhas

O exemplo tem como alvo a primeira planilha (`Worksheets[0]`). Para **converter planilha em imagem** de outra aba, referencie-a por índice ou nome:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Processar cada aba em um loop é simples:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Casos de borda e solução de problemas

| Situação | Abordagem recomendada |
|-----------|----------------------|
| **Intervalo muito grande** (ex., toda a pasta de trabalho) | Aumente `HorizontalResolution`/`VerticalResolution` gradualmente para evitar `OutOfMemoryException`. Considere exportar cada aba separadamente. |
| **Células mescladas** | Aspose.Cells preserva visualmente as células mescladas automaticamente, mas verifique a saída se você depender de larguras de coluna exatas. |
| **Fórmulas que referenciam arquivos externos** | Certifique‑se de que esses arquivos estejam acessíveis antes de carregar a pasta de trabalho; caso contrário, a imagem renderizada pode mostrar valores desatualizados. |
| **Licença ausente** | A versão de avaliação adiciona uma marca d’água. Aplique uma licença válida (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) antes de renderizar para produzir um PNG limpo. |

## Exemplo completo em funcionamento

Abaixo está o programa autônomo que você pode compilar e executar. Substitua `YOUR_DIRECTORY` por um caminho de pasta real na sua máquina.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Saída esperada**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Abra `Pivot.png` com qualquer visualizador de imagens—você verá o layout visual exato das células A1 até H30, incluindo formatação, cores e bordas.

## Conclusão

Agora você tem um método confiável para **converter Excel para PNG** usando C#. O tutorial abordou como **exportar intervalo do Excel**, **salvar Excel como PNG**, e **converter planilha em imagem** com opções personalizáveis e dicas de boas práticas.

A partir daqui você pode:

* Integrar o código em uma API web para gerar imagens sob demanda.  
* Combinar a saída PNG com geração de PDF para relatórios multiformato.  
* Explorar outros formatos de imagem (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) ajustando a propriedade `ImageFormat`.

Sinta‑se à vontade para experimentar diferentes intervalos, resoluções e seleções de planilhas para atender ao seu cenário específico de automação.

---


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Exportar uma Planilha Excel para PNG Usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Converter Excel para PNG, TIFF e PDF em Java usando Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Dominar Aspose.Cells Java: Converter Excel para PNG com um Provedor de Stream Personalizado](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}