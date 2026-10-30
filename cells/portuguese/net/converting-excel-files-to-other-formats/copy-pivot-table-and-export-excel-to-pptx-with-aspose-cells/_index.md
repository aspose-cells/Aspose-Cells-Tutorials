---
category: general
date: 2026-09-11
description: Copie a tabela dinâmica e exporte o Excel para PPTX usando Aspose.Cells.
  Aprenda a gerar um PPTX editável e salvar a pasta de trabalho como PPTX em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: pt
lastmod: 2026-09-11
og_description: Copiar tabela dinâmica e exportar Excel para PPTX em C# usando Aspose.Cells.
  Gerar PPTX editável e salvar a pasta de trabalho como PPTX com poucas linhas de
  código.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Copiar tabela dinâmica e exportar Excel para PPTX – guia completo de C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Copiar tabela dinâmica e exportar Excel para PPTX com Aspose.Cells
url: /pt/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar tabela dinâmica e exportar Excel para PPTX com Aspose.Cells

Se você precisa copiar uma tabela dinâmica de uma planilha para outra e, em seguida, exportar o arquivo Excel para uma apresentação PowerPoint, este guia mostra como fazer isso. Usando Aspose.Cells, você pode gerar um PPTX editável e salvar a pasta de trabalho como PPTX em apenas algumas linhas de código C#.

O tutorial cobre cada passo necessário para mover uma tabela dinâmica, preservar sua funcionalidade e produzir um arquivo PPTX onde o gráfico e as formas permanecem editáveis. Nenhuma ferramenta externa é necessária — apenas a biblioteca Aspose.Cells e um ambiente de desenvolvimento .NET.

## O que você vai alcançar

* **Copiar tabela dinâmica** de uma planilha de origem para uma planilha de destino mantendo todas as conexões de dados intactas.  
* **Exportar Excel para PPTX** para que o slide resultante possa ser editado no PowerPoint.  
* **Gerar PPTX editável** onde gráficos, tabelas e formas não são achatados em imagens.  
* **Salvar a pasta de trabalho como PPTX** usando a mesma chamada de API do Aspose.Cells.  

### Pré-requisitos

* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.6+).  
* Aspose.Cells para .NET (pacote NuGet `Aspose.Cells`).  
* Um entendimento básico de aplicações console em C#.  

> **Dica profissional:** Instale o pacote NuGet via CLI para garantir que você tenha a versão mais recente:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Como copiar tabela dinâmica entre planilhas

A primeira operação é mover a tabela dinâmica preservando sua definição. Aspose.Cells fornece o método `CopyRange` com um objeto `CopyOptions` que inclui a flag `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Por que isso funciona:**  
`CopyRange` copia dados de células, formatação e, quando `CopyPivotTable` está true, o cache e os metadados da tabela dinâmica. O intervalo de destino começa na célula `A1` (linha 0, coluna 0), mas você pode alterar os deslocamentos para posicionar a tabela dinâmica em outro local.

**Caso comum:** Se a planilha de destino já contiver uma tabela dinâmica com o mesmo nome, Aspose.Cells renomeará automaticamente a que está sendo importada, evitando conflitos de nome.

## Exportar Excel para PPTX e gerar PPTX editável

Depois que a tabela dinâmica estiver no lugar, você pode exportar toda a pasta de trabalho para um arquivo PPTX. A classe `ImageOrPrintOptions` permite especificar `ExportImageFormat = ImageFormat.Pptx`, o que indica ao Aspose.Cells que o resultado deve ser tratado como uma apresentação PowerPoint e não como uma imagem raster.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Por que isso funciona:**  
Quando `ExportImageFormat` está definido como `Pptx`, Aspose.Cells converte cada planilha em um slide. Formas, gráficos e tabelas dinâmicas são gravados como objetos nativos do PowerPoint, de modo que você pode dar duplo‑clique neles no PowerPoint e editar os dados subjacentes.

**Dica para pastas de trabalho grandes:** Se você precisar apenas de um subconjunto de planilhas, use `workbook.Worksheets.RemoveAt(index)` nas planilhas que não deseja exportar antes de chamar `Save`. Isso reduz o tamanho do arquivo PPTX.

## Exemplo completo e executável

Abaixo está o programa completo que une os passos anteriores. Substitua `YOUR_DIRECTORY` pelo caminho real em sua máquina.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Saída esperada

Ao executar o programa, ele imprime:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Quando você abrir `output.pptx` no Microsoft PowerPoint, verá um slide que contém a tabela dinâmica copiada como um gráfico editável. Dar duplo‑clique no gráfico abre o editor de gráficos do PowerPoint, permitindo modificar séries, eixos e rótulos de dados sem precisar voltar ao Excel.

## Lidando com armadilhas típicas

| Problema | Causa | Solução |
|----------|-------|---------|
| Tabela dinâmica aparece como imagem estática | Flag `CopyPivotTable` omitida ou `ExportImageFormat` definido como `Png` | Garanta `CopyPivotTable = true` e `ExportImageFormat = ImageFormat.Pptx`. |
| Planilha de destino mostra células em branco | Intervalo de origem não cobre toda a área da tabela dinâmica | Expanda o intervalo (ex.: `"A1:H30"`) para incluir todos os campos da tabela dinâmica. |
| PPTX exportado é muito grande | Planilhas desnecessárias foram incluídas | Remova as planilhas indesejadas antes de chamar `Save`. |
| PowerPoint não permite editar o gráfico | Uso de versão antiga do Aspose.Cells que não suporta PPTX | Atualize para a versão mais recente do Aspose.Cells (verifique as notas de lançamento). |

## Próximos passos e tópicos relacionados

* **Exportar planilha Excel para PPTX com layouts de slide personalizados** – explore `WorksheetToPdfConverter` para controle mais fino da aparência dos slides.  
* **Exportar Excel para PDF** – substitua `ImageFormat.Pptx` por `ImageFormat.Pdf` para gerar um PDF.  
* **Modificar programaticamente o PPTX após a exportação** – use a biblioteca `Aspose.Slides` para adicionar animações ou notas do apresentador.  

Ao dominar **copiar tabela dinâmica**, **exportar excel para pptx** e **gerar pptx editável**, você pode criar pipelines de relatório de ponta a ponta que movem dados de planilhas diretamente para decks de apresentação sem perder a editabilidade.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como copiar tabela dinâmica em C# – Converter Excel para PPTX, copiar intervalo e criar caixa de texto](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Criar nova pasta de trabalho Excel – Copiar e duplicar tabela dinâmica](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Criar uma tabela dinâmica no Excel usando Aspose.Cells para .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}