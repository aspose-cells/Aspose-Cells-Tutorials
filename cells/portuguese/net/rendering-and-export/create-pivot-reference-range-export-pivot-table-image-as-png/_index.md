---
category: general
date: 2026-02-09
description: Crie intervalo de referência de tabela dinâmica em C# e exporte a imagem
  da tabela dinâmica. Aprenda como salvar um intervalo do Excel como PNG usando Aspose.Cells
  – guia rápido e completo.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: pt
og_description: Crie intervalo de referência de tabela dinâmica em C# e exporte a
  imagem da tabela dinâmica para PNG. Guia completo passo a passo para salvar um intervalo
  do Excel como PNG.
og_title: Criar intervalo de referência de tabela dinâmica – Exportar imagem da tabela
  dinâmica como PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Criar intervalo de referência da tabela dinâmica – Exportar imagem da tabela
  dinâmica como PNG
url: /pt/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Intervalo de Referência da Tabela Dinâmica – Exportar Imagem da Tabela Dinâmica como PNG

Precisa **criar um intervalo de referência da tabela dinâmica** em uma planilha Excel usando C#? Você também pode **exportar a imagem da tabela dinâmica** e **salvar o intervalo do Excel como png** com apenas algumas linhas de código. Na minha experiência, transformar uma tabela dinâmica ao vivo em uma imagem estática é uma maneira prática de incorporar análises em relatórios, e‑mails ou dashboards sem precisar transportar a planilha inteira.

Neste tutorial vamos percorrer tudo o que você precisa saber: as bibliotecas necessárias, o código exato, por que cada chamada é importante e alguns detalhes que podem causar problemas. Ao final, você será capaz de gerar um arquivo PNG de qualquer tabela dinâmica com confiança e entenderá como adaptar o padrão para múltiplas planilhas ou formatos de imagem personalizados.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- **Aspose.Cells for .NET** (a versão de avaliação gratuita funciona bem para testes).  
- **.NET 6.0** ou superior – a API que usamos é totalmente compatível com .NET Standard 2.0+, portanto frameworks mais antigos também compilarão.  
- Um projeto básico em C# (Console App, WinForms ou ASP.NET – qualquer coisa que possa referenciar um pacote NuGet).  

Se ainda não instalou o Aspose.Cells, execute:

```bash
dotnet add package Aspose.Cells
```

É só isso – sem interop COM, sem Excel instalado no servidor.

## Etapa 1: Abrir a Planilha e Acessar a Primeira Worksheet

A primeira coisa a fazer é carregar o arquivo da planilha e obter a worksheet que contém a tabela dinâmica. Deliberadamente escolhemos a **primeira worksheet** (`Worksheets[0]`) porque a maioria dos arquivos de demonstração coloca a tabela dinâmica lá, mas você pode substituir o índice por um nome, se preferir.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Por que isso importa:* `Worksheet` é o ponto de entrada para qualquer operação baseada em intervalo. Se você apontar para a planilha errada, a chamada subsequente `PivotTables[0]` lançará uma `IndexOutOfRangeException`.

## Etapa 2: Criar Intervalo de Referência da Tabela Dinâmica

Agora pedimos à própria tabela dinâmica que nos forneça um **intervalo de referência**. Esse intervalo representa as células exatas que compõem a tabela dinâmica – cabeçalhos, linhas de dados e totais. O método `CreateReferenceRange()` faz o trabalho pesado internamente, lidando com células mescladas e linhas ocultas para você.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Dica profissional:** Se sua planilha contém várias tabelas dinâmicas, itere `worksheet.PivotTables` e escolha a que precisar pela propriedade `Name`.

## Etapa 3: Renderizar o Intervalo de Referência como Imagem

Aspose.Cells pode renderizar qualquer `Range` para uma imagem. O objeto retornado implementa tanto formatos raster (PNG, JPEG) quanto vetoriais (SVG). Aqui solicitamos a imagem raster padrão, que é um objeto compatível com `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*O que está acontecendo nos bastidores?* A API captura o layout visual do intervalo, respeitando estilos de célula, fontes e formatação condicional. É essencialmente o mesmo que tirar uma captura de tela, mas de forma programática e sem interface de usuário.

## Etapa 4: Salvar a Imagem Gerada em um Arquivo

Por fim, persistimos a imagem. O método `Save` escolhe automaticamente PNG quando você fornece a extensão “.png”. Você também pode passar um objeto `SaveOptions` caso precise controlar DPI ou usar outro formato.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Depois que esta linha for executada, abra `pivot.png` e você verá uma captura pixel‑perfect da tabela dinâmica, pronta para ser incorporada onde quiser.

## Exemplo Completo Funcional

Juntando tudo, aqui está um programa de console autônomo que você pode copiar‑colar e executar:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Saída esperada:** um arquivo chamado `pivot.png` localizado em `YOUR_DIRECTORY`. Abra-o com qualquer visualizador de imagens – você deverá ver o layout exato da tabela dinâmica original, incluindo cabeçalhos de coluna, linhas de dados e totais gerais.

## Exportar Imagem da Tabela Dinâmica – Personalizando Tamanho e DPI

Às vezes a imagem padrão fica pequena demais para um slide de apresentação. Você pode controlar a resolução passando um objeto `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Por que ajustar o DPI?* DPI mais alto gera bordas mais nítidas, especialmente quando o PNG é ampliado no PowerPoint ou em um PDF.

## Salvar Intervalo do Excel como PNG – Lidando com Múltiplas Worksheets

Se precisar exportar tabelas dinâmicas de várias planilhas, faça um loop em `Workbook.Worksheets` e repita as etapas. Aqui está um trecho conciso:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Esse padrão **exporta a imagem da tabela dinâmica** para cada pivot da pasta de trabalho, e cada arquivo recebe o nome da sua planilha e do pivot – perfeito para processamento em lote.

## Armadilhas Comuns & Como Evitá‑las

| Problema | Por que acontece | Solução |
|----------|------------------|---------|
| `IndexOutOfRangeException` em `PivotTables[0]` | A worksheet não possui tabelas dinâmicas. | Verifique `worksheet.PivotTables.Count` antes de acessar. |
| Imagem em branco | A tabela dinâmica está filtrada para ocultar todas as linhas. | Garanta que a pivot tenha dados visíveis, ou chame `pivot.RefreshData();` antes de criar o intervalo. |
| PNG de baixa resolução | DPI padrão é 96. | Use `ImageOrVectorSaveOptions.Resolution` conforme mostrado acima. |
| Erros de caminho de arquivo | Caracteres inválidos em `YOUR_DIRECTORY`. | Use `Path.Combine` e `Path.GetInvalidPathChars()` para sanitizar. |

## Verificação – Teste Rápido

Depois de executar o exemplo completo:

1. Abra `pivot.png` no Windows Photo Viewer.  
2. Verifique se os cabeçalhos de coluna, linhas de dados e linhas de total correspondem à visualização no Excel.  
3. Se notar linhas ausentes, confirme que o método **RefreshData** da pivot foi chamado antes de `CreateReferenceRange()`.

## Bônus: Incorporar o PNG em um Documento Word

Como a imagem já está em PNG, você pode enviá‑la diretamente ao Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Agora você tem um relatório Word que contém a captura exata da sua tabela dinâmica – sem necessidade de copiar‑colar manual.

## Conclusão

Você acabou de aprender como **criar intervalo de referência da tabela dinâmica**, **exportar imagem da tabela dinâmica** e **salvar intervalo do Excel como png** usando Aspose.Cells em C#. Os principais pontos são:

- Use `PivotTable.CreateReferenceRange()` para isolar a área visual da pivot.  
- Converta esse intervalo em imagem com `Range.ToImage()`.  
- Persista a imagem como PNG, ajustando DPI opcionalmente para qualidade de impressão.  

A partir daqui, você pode explorar exportação em lote, formatos de imagem diferentes (SVG, JPEG) ou até mesmo incorporar o PNG em PDFs ou documentos Word. O céu é o limite quando você tem a pivot capturada como um gráfico estático.

Tem dúvidas ou um cenário complicado? Deixe um comentário abaixo e feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}