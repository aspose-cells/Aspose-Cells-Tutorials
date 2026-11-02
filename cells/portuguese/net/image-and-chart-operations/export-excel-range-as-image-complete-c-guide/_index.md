---
category: general
date: 2026-06-08
description: Exporte um intervalo do Excel como imagem usando C# e Aspose.Cells. Aprenda
  como salvar a planilha do Excel como imagem em apenas alguns passos simples.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: pt
og_description: Exportar intervalo do Excel como imagem com C#. Este tutorial mostra
  como salvar a planilha do Excel como imagem de forma rápida e confiável.
og_title: Exportar intervalo do Excel como imagem – Guia completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Exportar intervalo do Excel como imagem – Guia completo de C#
url: /pt/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar intervalo do Excel como imagem – Guia completo em C#

Já precisou **exportar intervalo do Excel como imagem** mas não sabia qual chamada de API usar? Você não está sozinho. Seja construindo um painel de relatórios ou precisando de uma captura de uma tabela dinâmica para um slide do PowerPoint, transformar um bloco de células em PNG é um truque útil.

Neste guia, vamos percorrer um exemplo autônomo que não só **exporta intervalo do Excel como imagem** mas também mostra como **salvar planilha do Excel como imagem** para a planilha inteira. Sem scripts externos, apenas C# puro e Aspose.Cells, para que você possa copiar‑colar o código e vê‑lo funcionar instantaneamente.

## O que você aprenderá

- Carregar uma pasta de trabalho existente e localizar um intervalo específico (tabela dinâmica ou qualquer bloco de células).  
- Configurar opções de exportação de imagem, como formato, resolução e dimensionamento.  
- Exportar um único intervalo para PNG, JPEG ou BMP.  
- Estender a mesma lógica para **salvar planilha do Excel como imagem** em uma única linha.  
- Dicas para lidar com múltiplas tabelas dinâmicas, intervalos grandes e armadilhas comuns.

### Pré-requisitos

- .NET 6.0 ou superior (o código também funciona no .NET Framework 4.7+).  
- Aspose.Cells para .NET ≥ 23.9 (você pode obter uma avaliação gratuita no site da Aspose).  
- Um entendimento básico de C# e I/O de arquivos.  

Se você tem isso, vamos mergulhar.

## Etapa 1: Configurar o Projeto e Importar Namespaces

Primeiro, crie um novo aplicativo console (ou integre o código em qualquer projeto existente). Adicione o pacote NuGet Aspose.Cells:

```bash
dotnet add package Aspose.Cells
```

Em seguida, traga os namespaces necessários para o escopo:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Dica profissional:** Mantenha suas declarações `using` no topo do arquivo; isso facilita a leitura do código—especialmente quando você adicionar mais recursos da Aspose.

## Etapa 2: Carregar a Pasta de Trabalho contendo o Intervalo Alvo

Você precisa de uma pasta de trabalho no disco. Substitua `YOUR_DIRECTORY/input.xlsx` pelo caminho real do seu arquivo.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Por que esta etapa importa: o objeto `Workbook` é o ponto de entrada para todas as operações do Aspose.Cells. Sem ele, você não pode referenciar planilhas, intervalos ou tabelas dinâmicas.

## Etapa 3: Identificar o Intervalo a Exportar

Você tem dois cenários comuns:

1. **Uma tabela dinâmica específica** – o código que você postou usa `PivotTables[0].PivotTableRange`.  
2. **Um bloco de células arbitrário** – você pode usar `worksheet.Cells.CreateRange("B2:D10")`.

Abaixo tratamos ambos, permitindo que você escolha o que se encaixa no seu caso.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Por que verificamos tabelas dinâmicas primeiro:** Muitos arquivos de relatório dependem de dados dinâmicos de tabelas dinâmicas. Se não houver nenhuma, a alternativa garante que o tutorial ainda funcione.

## Etapa 4: Configurar Opções de Exportação de Imagem

Aspose.Cells oferece controle detalhado sobre a imagem de saída. As configurações mais comuns são formato, resolução (DPI) e se deve incluir linhas de grade.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

Você pode trocar `ImageFormat.Jpeg` ou `ImageFormat.Bmp` se seu sistema downstream preferir esses tipos. A configuração DPI importa quando você incorpora a imagem em PDFs de alta resolução ou apresentações.

## Etapa 5: Exportar o Intervalo (ou a Planilha Inteira) como Imagem

Agora a mágica acontece. O método `ToImage` grava a representação visual do intervalo diretamente no disco.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### O que o código faz

- `exportRange.ToImage` captura apenas as células dentro do intervalo (tabela dinâmica ou bloco personalizado).  
- `worksheet.ToImage` captura a *área inteira* visível da planilha, efetivamente **salvar planilha do Excel como imagem**.  

Ambas as chamadas respeitam as opções definidas anteriormente—assim você obterá arquivos PNG com resolução de 300 DPI.

## Lidando com Casos Limites e Perguntas Frequentes

### Múltiplas Tabelas Dinâmicas

Se sua pasta de trabalho contém mais de uma tabela dinâmica, você pode percorrê‑las:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Intervalos Muito Grandes

Exportar um intervalo massivo (por exemplo, milhares de linhas) pode consumir muita memória. Mitigue isso por:

- Reduzir `HorizontalResolution` / `VerticalResolution`.  
- Exportar em seções (dividir o intervalo em blocos menores).  

### Fundos Transparentes

Se você precisar de um fundo transparente (útil para sobrepor em páginas web), defina a cor de fundo para `Color.Transparent` antes da exportação:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Permissões de Arquivo

Certifique‑se de que o diretório de destino exista e que seu processo tenha permissão de gravação. Caso contrário, `ToImage` lança uma `IOException`.

## Exemplo Completo Funcional

Juntando tudo, aqui está um programa console pronto‑para‑executar:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Saída esperada** (console):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Abra os arquivos PNG gerados e você verá uma captura pixel‑perfeita do intervalo selecionado e da planilha completa, respectivamente.

## Conclusão

Acabamos de cobrir tudo o que você precisa para **exportar intervalo do Excel como imagem** e também como **salvar planilha do Excel como imagem** usando Aspose.Cells e C#. Desde o carregamento da pasta de trabalho até o ajuste fino das opções de imagem e o tratamento de múltiplas tabelas dinâmicas, os passos são simples e totalmente reproduzíveis.

Em seguida, você pode querer:

- Experimentar com diferentes valores de `ImageFormat` (JPEG, BMP).  
- Combinar a imagem com um PDF usando a classe `Document` para geração de relatórios.  
- Automatizar o processo para um lote de arquivos em uma pasta.

Sinta‑se à vontade para adaptar o trecho ao seu fluxo de trabalho—seja alimentando imagens em uma API web, incorporando‑as em e‑mails ou gerando relatórios imprimíveis. Boa codificação, e deixe as imagens falarem pelos seus dados do Excel!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Exportar Células do Excel para Imagem usando Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Exportar Pasta de Trabalho do Excel como Imagem usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Exportar Pasta de Trabalho do Excel como Imagem usando Aspose Cells para Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}