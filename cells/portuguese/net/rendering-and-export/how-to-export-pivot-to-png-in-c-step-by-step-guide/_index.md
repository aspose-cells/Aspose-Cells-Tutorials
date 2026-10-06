---
category: general
date: 2026-02-14
description: como exportar uma tabela dinâmica de uma pasta de trabalho do Excel para
  PNG usando Aspose.Cells. Aprenda a carregar a pasta de trabalho do Excel, renderizar
  a tabela dinâmica como imagem e salvar a imagem da tabela dinâmica sem esforço.
draft: false
keywords:
- how to export pivot
- export excel pivot
- load excel workbook
- pivot table to png
- save pivot image
language: pt
og_description: como exportar pivot do Excel para PNG em C#. Este guia mostra como
  carregar a pasta de trabalho do Excel, renderizar uma tabela dinâmica para PNG e
  salvar a imagem da tabela dinâmica.
og_title: Como exportar pivot para PNG em C# – Tutorial completo
tags:
- Aspose.Cells
- C#
- Excel automation
title: como exportar pivot para png em C# – Guia passo a passo
url: /pt/net/rendering-and-export/how-to-export-pivot-to-png-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como exportar pivot para PNG em C# – Tutorial Completo

Já se perguntou **como exportar pivot** de uma planilha Excel como um arquivo PNG nítido? Você não está sozinho — desenvolvedores frequentemente precisam de uma visualização rápida de uma tabela dinâmica para relatórios, dashboards ou anexos de e‑mail. A boa notícia? Com Aspose.Cells você pode carregar a pasta de trabalho Excel, obter a primeira tabela dinâmica, transformá‑la em imagem e **salvar a imagem da pivot** em apenas algumas linhas de C#.

Neste tutorial vamos percorrer tudo que você precisa: desde os fundamentos de **carregar pasta de trabalho Excel**, até renderizar uma **tabela dinâmica para png**, e finalmente persistir o arquivo no disco. Ao final, você terá um programa autocontido e executável que pode ser inserido em qualquer projeto .NET.

---

## O que você precisará

- **.NET 6 ou superior** (o código também funciona no .NET Framework 4.7+)
- **Aspose.Cells for .NET** pacote NuGet (versão 23.12 na data deste tutorial)
- Um arquivo Excel (`input.xlsx`) que contenha ao menos uma tabela dinâmica
- Um ambiente Visual Studio ou VS Code com o qual você se sinta confortável

Sem bibliotecas extras, sem interop COM e sem necessidade de instalação do Excel — Aspose.Cells cuida de tudo na memória.

---

## Passo 1 – Carregar a pasta de trabalho do Excel

A primeira coisa é trazer a pasta de trabalho para a memória. É aqui que a palavra‑chave **carregar pasta de trabalho Excel** brilha.

```csharp
using System.Drawing;
using Aspose.Cells;

class PivotExport
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        // Adjust the path to where your input.xlsx lives
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Grab the first worksheet (you can also select by name)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Por que isso importa:**  
> Carregar a pasta de trabalho uma única vez mantém a operação rápida e evita bloquear o arquivo fonte. Aspose.Cells lê o arquivo para um stream gerenciado, permitindo inclusive carregar a partir de um array de bytes ou de um local de rede posteriormente.

---

## Passo 2 – Renderizar a Tabela Dinâmica para uma Imagem

Agora que a pasta de trabalho está na memória, podemos acessar suas tabelas dinâmicas. A API oferece o conveniente método `ToImage()` que devolve um `System.Drawing.Image`.

```csharp
        // Step 2: Find the first pivot table on the worksheet
        if (worksheet.PivotTables.Count == 0)
        {
            System.Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        // Export the first pivot table as an image
        Image pivotImage = worksheet.PivotTables[0].ToImage();

        // Optional: tweak image quality or size here
        // pivotImage.SetResolution(300, 300);
```

> **Dica profissional:** Se sua pasta de trabalho contém várias tabelas dinâmicas, basta iterar sobre `worksheet.PivotTables` e exportar cada uma. A chamada `ToImage()` respeita a visualização atual (filtros, slicers, etc.), então você obtém exatamente o que o usuário vê.

---

## Passo 3 – Salvar o Arquivo PNG Gerado

Por fim, persistimos o bitmap no disco. A sobrecarga `Save` escolhe automaticamente o formato com base na extensão do arquivo.

```csharp
        // Step 3: Save the image as PNG
        var outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivotImage.Save(outputPath, System.Drawing.Imaging.ImageFormat.Png);

        System.Console.WriteLine($"Pivot table exported successfully to {outputPath}");
    }
}
```

Executar o programa gera um `pivot.png` que se parece exatamente com a tabela dinâmica dentro do Excel. Abra-o com qualquer visualizador de imagens e você verá linhas, colunas e totais renderizados pixel‑perfeitamente.

---

## Tratando Casos de Borda Comuns

### Múltiplas Planilhas ou Tabelas Dinâmicas

Se sua pasta de trabalho armazena a pivot em outra planilha, altere o índice da planilha ou use o nome da planilha:

```csharp
Worksheet ws = workbook.Worksheets["SalesData"];
```

Então faça o loop:

```csharp
foreach (PivotTable pt in ws.PivotTables)
{
    Image img = pt.ToImage();
    img.Save($"pivot_{pt.Name}.png", ImageFormat.Png);
}
```

### Tabelas Dinâmicas Grandes

Para pivôs muito grandes, o tamanho padrão da imagem pode ficar enorme. Você pode controlar o tamanho de renderização ajustando o fator de zoom da planilha antes de chamar `ToImage()`:

```csharp
worksheet.PageSetup.Zoom = 75; // renders at 75 % of original size
```

### Gerenciamento de Memória

`System.Drawing.Image` implementa `IDisposable`. Em código de produção, envolva a imagem em um bloco `using` para liberar os recursos nativos prontamente:

```csharp
using (Image pivotImage = worksheet.PivotTables[0].ToImage())
{
    pivotImage.Save(outputPath, ImageFormat.Png);
}
```

---

## Exemplo Completo Funcionando

Abaixo está o programa completo, pronto‑para‑executar. Cole-o em um novo projeto de console, ajuste os caminhos dos arquivos e pressione **F5**.

```csharp
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;

namespace PivotExportDemo
{
    class Program
    {
        static void Main()
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook (load excel workbook)
            // -----------------------------------------------------------------
            string inputFile = @"YOUR_DIRECTORY\input.xlsx";
            Workbook wb = new Workbook(inputFile);
            Worksheet ws = wb.Worksheets[0]; // first worksheet

            // -----------------------------------------------------------------
            // 2️⃣ Ensure a pivot table exists and export it (how to export pivot)
            // -----------------------------------------------------------------
            if (ws.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found. Exiting.");
                return;
            }

            // Export the first pivot table as a PNG image (pivot table to png)
            using (Image img = ws.PivotTables[0].ToImage())
            {
                // -----------------------------------------------------------------
                // 3️⃣ Save the pivot image to disk (save pivot image)
                // -----------------------------------------------------------------
                string outputFile = @"YOUR_DIRECTORY\pivot.png";
                img.Save(outputFile, ImageFormat.Png);
                Console.WriteLine($"Pivot exported successfully → {outputFile}");
            }
        }
    }
}
```

**Saída esperada:**  
```
Pivot exported successfully → YOUR_DIRECTORY\pivot.png
```

E o arquivo `pivot.png` conterá uma réplica visual da tabela dinâmica original.

---

## Perguntas Frequentes

- **Isso funciona com arquivos .xlsx que contêm gráficos?**  
  Sim. O método `ToImage()` se preocupa apenas com o layout da tabela dinâmica; os gráficos permanecem inalterados.

- **Posso exportar para JPEG ou BMP em vez de PNG?**  
  Absolutamente — basta mudar o argumento `ImageFormat` em `Save`. PNG é sem perdas, por isso o recomendamos para dados nítidos.

- **E se a pasta de trabalho estiver protegida por senha?**  
  Carregue-a usando a sobrecarga de senha:  
  `Workbook wb = new Workbook(inputFile, new LoadOptions { Password = "mySecret" });`

---

## Encerramento

Acabamos de cobrir **como exportar pivot** de um arquivo Excel para uma imagem PNG usando Aspose.Cells. Os passos — **carregar pasta de trabalho Excel**, localizar a **tabela dinâmica para png**, e **salvar a imagem da pivot** — são simples, mas poderosos o suficiente para pipelines de relatórios do mundo real.

Em seguida, você pode explorar:

- Automatizar a exportação de todas as tabelas dinâmicas em uma pasta (exportar pivôs Excel em lote)  
- Incorporar o PNG em um PDF ou e‑mail HTML (combinar com iTextSharp ou Razor)  
- Adicionar marcas d’água ou estilos personalizados à imagem exportada  

Experimente essas opções e deixe as imagens falarem por você no próximo dashboard.

---

![exemplo de exportação de pivot](assets/pivot-export-example.png "exemplo de exportação de pivot")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}