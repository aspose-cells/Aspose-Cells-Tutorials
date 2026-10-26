---
category: general
date: 2026-10-26
description: ExportTableOptions personalizados quando ExportAsStrin permite exportar
  dados do Excel como strings em C#. Siga o guia passo a passo para configurar e executar
  a exportação.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: pt
lastmod: 2026-10-26
og_description: ExportTableOptions personalizados quando ExportAsStrin habilita exportação
  do Excel apenas como string. Aprenda os passos exatos para configurar e executar
  a exportação em C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: ExportTableOptions personalizados ao usar ExportAsStrin – exportar Excel
  como string em C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Opções Personalizadas de ExportTable ao usar ExportAsStrin para Excel
url: /pt/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – export Excel as string in C#

Se você precisa de **Custom ExportTableOptions when ExportAsStrin** para obter o valor de cada célula como uma string simples, este guia mostra exatamente como fazer isso. Seja construindo um pipeline de importação de dados ou precisando de um dump pronto para CSV, você verá por que configurar as opções dessa forma evita surpresas de conversão de tipo.

Neste tutorial você aprenderá **como exportar excel como string** usando a biblioteca Aspose.Cells, verá o código completo e executável e entenderá o raciocínio por trás de cada configuração. Nenhuma documentação externa é necessária – tudo o que você precisa está aqui.

## Prerequisites

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou posterior instalado  
* Visual Studio 2022 (ou qualquer IDE que suporte .NET)  
* Pacote Aspose.Cells for .NET (instale via NuGet: `Install-Package Aspose.Cells`)  
* Uma pasta de trabalho Excel (`sample.xlsx`) colocada na raiz do projeto  

Estes itens são as únicas dependências; o código funciona no Windows, Linux ou macOS sem bibliotecas adicionais.

## Step 1: Load the workbook you want to export

A primeira coisa que você faz ao usar **Custom ExportTableOptions when ExportAsStrin** é obter um objeto `Worksheet` a partir de uma pasta de trabalho carregada. Esse objeto dá acesso a linhas, colunas e à API de exportação.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Por que isso importa:*  
`Workbook` lê o arquivo uma única vez e mantém todas as informações de formatação na memória. Ao selecionar uma `Worksheet` específica, você limita o escopo da exportação e evita o processamento desnecessário de planilhas ocultas.

## Step 2: Configure ExportTableOptions with ExportAsString = true

O núcleo de **Custom ExportTableOptions when ExportAsStrin** é o objeto `ExportTableOptions`. Definir `ExportAsString` força o exportador a tratar cada célula como uma string, independentemente do tipo de dado original (data, número, booleano etc.). Habilitar `PreserveFormatting` mantém o estilo visual (por exemplo, símbolos de moeda) na string resultante.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Por que isso importa:*  
Quando você posteriormente chama `ExportDataTable`, a biblioteca normalmente tenta inferir o tipo .NET de cada coluna. Com `ExportAsString = true`, essa etapa de inferência é pulada, evitando conversões inesperadas de `DateTime` ou `double` que podem quebrar analisadores CSV posteriores.

## Step 3: Export a range to a DataTable using the custom options

Agora você pode exportar um intervalo retangular (linhas 0‑9, colunas 0‑4) da planilha. O método retorna um `DataTable` onde cada campo é uma `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Por que isso importa:*  
`ExportDataTable` é a forma mais conveniente de mover dados do Excel para uma estrutura relacional que muitas APIs .NET já entendem (por exemplo, Entity Framework, Dapper). Ao passar as **Custom ExportTableOptions when ExportAsStrin**, você garante que cada `DataColumn.DataType` será `typeof(string)`.

## Step 4: Verify the result – all values are strings

É uma boa prática confirmar que a exportação se comportou como esperado. O loop a seguir imprime cada célula e seu tipo em tempo de execução.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Saída esperada**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Cada célula mostra `String` como seu tipo, confirmando que **Custom ExportTableOptions when ExportAsStrin** funcionou corretamente.

## Step 5: Optional – write the DataTable to CSV

Se o seu objetivo final é um arquivo de texto simples, você pode serializar facilmente o `DataTable` para CSV:



## What Should You Learn Next?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}