---
category: general
date: 2026-08-11
description: Exportar Excel para txt em C# com um guia passo a passo. Aprenda como
  converter xlsx para texto simples usando Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: pt
lastmod: 2026-08-11
og_description: Exporte Excel para txt em C# rapidamente. Este tutorial mostra como
  converter xlsx para texto simples, configurar formatos e lidar com planilhas grandes.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Exportar Excel para TXT em C# – guia passo a passo para desenvolvedores
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Exportar Excel para TXT em C# – guia completo de programação
url: /pt/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar excel para txt em C# – guia completo de programação

Se você precisa **exportar excel para txt**, pode obter o resultado com algumas linhas de código C#. Este guia mostra como converter uma pasta de trabalho `.xlsx` em um arquivo de texto simples enquanto preserva o formato de dados que você definir.

Exportar planilhas como arquivos de texto é uma necessidade comum quando sistemas downstream aceitam apenas dados delimitados ou quando você precisa auditar os valores brutos das células. Nas seções a seguir, você aprenderá como configurar formatos de data e número, lidar com planilhas grandes e evitar armadilhas típicas.

## Pré-requisitos para converter xlsx para texto simples

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 (ou superior) instalado – o código tem como alvo .NET Standard 2.0, portanto funciona também com .NET Framework 4.6+.
* Uma licença para **Aspose.Cells** (a avaliação gratuita funciona para testes).
* Uma IDE como Visual Studio 2022 ou Visual Studio Code.
* Um arquivo Excel chamado `input.xlsx` colocado em uma pasta que você possa referenciar a partir do seu projeto.

Esses itens são os únicos requisitos externos; o tutorial não depende de pacotes NuGet adicionais.

## Como exportar excel para txt usando Aspose.Cells

Aspose.Cells fornece a classe `ExportTableOptions` que permite controlar como os valores das células são renderizados como strings. Definindo `ExportAsString` como `true`, você força cada célula a ser gravada como texto, o que é essencial quando se deseja uma saída de texto simples determinística.

### Etapa 1 – carregar a pasta de trabalho

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*O construtor `Workbook` lê o arquivo Excel para a memória. Se o arquivo não existir, uma exceção será lançada, portanto você pode querer envolver esta chamada em um bloco try‑catch para código de produção.*

### Etapa 2 – obter a primeira planilha

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*As planilhas são indexadas a partir de zero, portanto o índice 0 refere‑se à primeira aba. Você pode substituir o índice por um nome de planilha (`workbook.Worksheets["Sheet1"]`) quando precisar direcionar uma aba específica.*

### Etapa 3 – definir opções de exportação para conversão de texto

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` garante que cada célula, independentemente do tipo original, se torne uma string no arquivo de saída. As propriedades `DateTimeFormat` e `NumberFormat` permitem controlar como datas e números aparecem, o que é crucial ao **converter xlsx para texto simples** para sistemas que esperam um padrão específico.*

### Etapa 4 – exportar planilha como arquivo de texto

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` grava o conteúdo da planilha em um arquivo de texto simples usando as opções fornecidas. O delimitador padrão é o caractere de tabulação (`\t`). Se precisar de um delimitador diferente, você pode usar a sobrecarga que aceita uma instância de `ExportTableOptions` e especificar `ExportTableOptions.Separator`. O arquivo resultante pode ser aberto em qualquer editor de texto ou importado para um banco de dados.*

#### Saída esperada

Suponha que `input.xlsx` contenha:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

Com as opções acima, o arquivo `Exported.txt` conterá:

```
2023-05-01	1,234.50	Sample text
```

Cada coluna está separada por uma tabulação, as datas seguem o formato `yyyy‑MM‑dd` e os números usam vírgula como separador de milhares e duas casas decimais.

## Armadilhas comuns ao exportar planilha como arquivo de texto

| Problema | Por que acontece | Como evitar |
|----------|------------------|--------------|
| Formatação numérica dependente de local | O formato padrão respeita a cultura do SO, o que pode gerar vírgulas ou pontos de forma inconsistente. | Defina explicitamente `NumberFormat` em `ExportTableOptions`. |
| Linhas ou colunas ocultas aparecem na saída | Aspose.Cells exporta todo o intervalo usado, incluindo linhas ocultas. | Defina `ExportTableOptions.ExportHiddenRows = false` e `ExportHiddenColumns = false` se quiser ignorá‑las. |
| Planilhas grandes causam pressão de memória | A pasta de trabalho inteira é carregada na memória antes da exportação. | Use `Workbook.LoadOptions` com `LoadDataOnly = true` para reduzir o uso de memória, ou processe o arquivo em partes. |
| Células de data armazenadas como texto no arquivo de origem | Se uma célula já contém uma string formatada, o exportador a trata como texto e ignora `DateTimeFormat`. | Garanta que a pasta de trabalho fonte armazene datas como tipos de data próprios do Excel. |

Abordar essas questões torna o processo de **como exportar planilha Excel como texto** confiável em diferentes ambientes.

## Estendendo a solução – delimitadores personalizados e exportação em streaming

Se você precisar de um arquivo de valores separados por vírgula (CSV) em vez de um arquivo delimitado por tabulação, modifique as opções:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

Para arquivos maiores que 500 MB, o streaming da saída impede que a aplicação esgote a RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

A sobrecarga que aceita um `Stream` grava linhas incrementalmente, o que é ideal para jobs em lote ou serviços web que retornam o arquivo de texto diretamente ao cliente.

## Verifique o resultado programaticamente

Após a exportação terminar, você pode ler a primeira linha de volta para a memória para confirmar o formato:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Executar este trecho deve imprimir a mesma linha mostrada na seção *Saída esperada*, dando confiança de que a conversão foi bem‑sucedida.

## Recapitulação do código completo

Juntando todas as peças, obtém‑se um programa autônomo que você pode copiar para uma aplicação console:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Compile e execute o programa; o arquivo `Exported.txt` aparecerá no mesmo diretório da pasta de trabalho fonte.

## Próximos passos e tópicos relacionados

* **Exportar planilha como arquivo de texto** – experimente diferentes delimitadores, codificações (UTF‑8 vs. ASCII) e estilos de terminação de linha para compatibilidade multiplataforma.
* **Conversão em massa** – percorra `workbook.Worksheets` para gerar um arquivo de texto separado para cada aba.
* **Integração com bancos de dados** – canalize o texto gerado diretamente para uma operação de inserção em massa no SQL Server ou PostgreSQL.
* **

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}