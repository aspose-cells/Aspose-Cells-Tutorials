---
category: general
date: 2026-08-11
description: Como exportar Excel para PNG e salvar intervalo do Excel como imagem
  usando Aspose.Cells. Aprenda a salvar a imagem da planilha do Excel e exportar a
  imagem da tabela dinâmica em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel to png
- save excel range as image
- save excel sheet picture
- export pivot table image
language: pt
lastmod: 2026-08-11
og_description: Como exportar Excel para PNG rapidamente. Este tutorial mostra como
  salvar um intervalo do Excel como imagem, salvar a imagem da planilha do Excel e
  exportar a imagem da tabela dinâmica com Aspose.Cells.
og_image_alt: Screenshot of C# code exporting an Excel worksheet to a PNG file
og_title: Como exportar Excel para PNG – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to export Excel to PNG and save Excel range as image using Aspose.Cells.
    Learn to save Excel sheet picture and export pivot table image in minutes.
  headline: How to export Excel to PNG – full step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Excel automation
- C#
- image export
title: Como exportar Excel para PNG – guia completo passo a passo
url: /pt/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como exportar Excel para PNG – guia completo passo a passo

Se você precisa **como exportar Excel para PNG**, este guia o conduz por todo o processo usando Aspose.Cells para .NET. Seja para **salvar intervalo do Excel como imagem**, incorporar uma imagem da planilha em um relatório ou **exportar imagem da tabela dinâmica** para um painel, as etapas abaixo fornecem uma solução pronta para uso.

Você aprenderá como carregar uma workbook, atualizar uma tabela dinâmica, configurar as opções de imagem e, finalmente, gravar um arquivo PNG que preserva a aparência formatada dos dados de origem. Nenhuma ferramenta externa ou captura de tela manual é necessária.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou superior instalado  
* Visual Studio 2022 (ou qualquer IDE C#)  
* Uma licença do Aspose.Cells for .NET ou uma cópia de avaliação gratuita – faça o download no [site da Aspose.Cells](https://products.aspose.com/cells/net)  
* Um arquivo Excel de exemplo (`PivotTable.xlsx`) que contenha ao menos uma tabela dinâmica  

O código funciona no Windows, macOS e Linux porque o Aspose.Cells é independente de plataforma.

## Etapa 1: Instalar Aspose.Cells via NuGet

Abra a pasta do seu projeto em um terminal e execute:

```bash
dotnet add package Aspose.Cells
```

Isso adiciona a versão estável mais recente do **Aspose.Cells** ao seu `.csproj`. A biblioteca fornece as classes `Workbook`, `Worksheet`, `ImageOrPrintOptions` e outras que usaremos para **salvar imagem da planilha Excel**.

## Etapa 2: Carregar a workbook que contém a tabela dinâmica

```csharp
using Aspose.Cells;
using System;

// Load the Excel file – replace the path with your actual location
string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
Workbook workbook = new Workbook(sourcePath);
```

*Por que isso importa:*  
Carregar a workbook dá acesso a todas as planilhas, células e objetos incorporados. A classe `Workbook` abstrai o formato do arquivo, permitindo trabalhar com `.xlsx`, `.xls` ou até mesmo `.csv` sem código de análise adicional.

## Etapa 3: Selecionar a planilha e atualizar a tabela dinâmica

```csharp
// Get the first worksheet where the pivot table resides
Worksheet sheet = workbook.Worksheets[0];

// Refresh the pivot table so it reflects the latest source data
if (sheet.PivotTables.Count > 0)
{
    sheet.PivotTables[0].Refresh();
}
else
{
    Console.WriteLine("No pivot tables found on the selected worksheet.");
}
```

*Por que isso importa:*  
As tabelas dinâmicas armazenam em cache seus dados de origem. Chamar `Refresh()` garante que a representação visual corresponda a quaisquer alterações recentes, o que é crucial quando você posteriormente **exportar imagem da tabela dinâmica**.

## Etapa 4: Configurar opções de exportação de imagem (formato PNG, preservação de estilo)

```csharp
// Set up export options – PNG keeps lossless quality and supports transparency
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Png,
    // Preserve the pivot table’s style (fonts, colors, borders)
    CalculatePivotTableStyle = true,
    // Optional: set image resolution (DPI) for higher quality
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

*Por que isso importa:*  
`CalculatePivotTableStyle = true` indica ao Aspose.Cells que renderize a tabela dinâmica exatamente como aparece no Excel, incluindo formatação condicional. Ajustar o DPI pode ser útil para impressão ou telas de alta resolução.

## Etapa 5: Capturar o intervalo usado (incluindo a tabela dinâmica) como imagem

```csharp
// Determine the range that contains data – MaxDisplayRange covers the whole used area
CellArea usedRange = sheet.Cells.MaxDisplayRange;

// Add a picture of the used range to the worksheet (position 0,0) and save it
Picture pic = sheet.Pictures.Add(0, 0, usedRange);
pic.Save(@"YOUR_DIRECTORY\PivotImage.png", imgOptions);
```

*Por que isso importa:*  
`MaxDisplayRange` expande automaticamente até a célula mais distante que contém dados, fórmulas ou formatação, garantindo que toda a tabela dinâmica e as células ao redor sejam incluídas. O método `Pictures.Add` cria uma imagem em memória que gravamos imediatamente no disco como um arquivo PNG.

## Exemplo completo executável

Juntando tudo, aqui está um programa de console autocontido que você pode copiar, colar e executar:

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPngExport
{
    class Program
    {
        static void Main()
        {
            // ---------- 1. Load workbook ----------
            string sourcePath = @"YOUR_DIRECTORY\PivotTable.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // ---------- 2. Get first worksheet ----------
            Worksheet sheet = workbook.Worksheets[0];

            // ---------- 3. Refresh pivot table ----------
            if (sheet.PivotTables.Count > 0)
            {
                sheet.PivotTables[0].Refresh();
            }
            else
            {
                Console.WriteLine("No pivot tables found on the selected worksheet.");
                return;
            }

            // ---------- 4. Set image export options ----------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Png,
                CalculatePivotTableStyle = true,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // ---------- 5. Export used range as PNG ----------
            CellArea usedRange = sheet.Cells.MaxDisplayRange;
            Picture pic = sheet.Pictures.Add(0, 0, usedRange);
            string outputPath = @"YOUR_DIRECTORY\PivotImage.png";
            pic.Save(outputPath, imgOptions);

            Console.WriteLine($"Pivot table image saved to: {outputPath}");
        }
    }
}
```

### Saída esperada

Ao executar o programa, o console exibe:

```
Pivot table image saved to: YOUR_DIRECTORY\PivotImage.png
```

E o arquivo `PivotImage.png` aparece na pasta de destino. Abra‑o com qualquer visualizador de imagens — você verá a representação visual exata da planilha Excel, incluindo a tabela dinâmica formatada, cabeçalhos de coluna e quaisquer dados circundantes.

## Variações comuns e casos de borda

| Cenário | Ajuste |
|----------|------------|
| **Exportar apenas um intervalo de células específico** (ex.: `A1:D20`) | Substitua `sheet.Cells.MaxDisplayRange` por `new CellArea { StartRow = 0, StartColumn = 0, EndRow = 19, EndColumn = 3 }`. |
| **Múltiplas planilhas** | Percorra `workbook.Worksheets` e repita as etapas 3‑5 para cada planilha que desejar exportar. |
| **Formato de imagem diferente** (JPEG, BMP) | Altere `SaveFormat = SaveFormat.Jpeg` (ou `Bmp`). PNG é recomendado para qualidade sem perdas. |
| **Planilhas grandes** causando pressão de memória | Use `sheet.Pictures.Add` com um `CellArea` menor ou divida a exportação em várias imagens. |
| **Nenhuma tabela dinâmica presente** | Proteja com `if (sheet.PivotTables.Count == 0)` conforme mostrado; ainda é possível exportar o intervalo regular. |

## Dicas avançadas

* **Licenciar cedo** – Registre sua licença do Aspose.Cells antes de carregar a workbook para evitar a marca d'água de avaliação.  
  ```csharp
  var license = new License();
  license.SetLicense(@"YOUR_DIRECTORY\Aspose.Total.NET.lic");
  ```
* **Exportação em lote** – Para pipelines de relatórios, encapsule a lógica de exportação em um método que retorne um `byte[]`. Isso permite enviar o PNG diretamente para uma API web sem tocar no sistema de arquivos.  
* **Fundo transparente** – PNG já suporta transparência. Se quiser um fundo branco, defina `imgOptions.Transparent = false;`.  

## Conclusão

Agora você sabe **como exportar Excel para PNG** usando Aspose.Cells, cobrindo todo o fluxo de trabalho desde o carregamento da workbook até **salvar intervalo do Excel como imagem**, **salvar imagem da planilha Excel** e **exportar imagem da tabela dinâmica**. O código fornecido está completo, executável e adaptável a cenários reais, como relatórios automatizados ou geração de dashboards.

Pronto para o próximo passo? Explore como **converter o PNG para PDF** para relatórios imprimíveis, ou integrar a imagem em um serviço web que entregue visualizações ao vivo do Excel. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Exportar uma Planilha Excel para PNG Usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Exportar Workbook Excel como Imagem Usando Aspose.Cells para Java: Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Como Exportar Células Excel como Imagens Usando Aspose.Cells para Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}