---
category: general
date: 2026-06-17
description: Converta a planilha em DataTable em C# rapidamente. Aprenda como ler
  um arquivo Excel para DataTable em C# e exportar Excel para DataTable em C# com
  código real.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: pt
og_description: Converter planilha para DataTable em C# rapidamente. Este tutorial
  mostra como ler um arquivo Excel para DataTable em C# e exportar Excel para DataTable
  em C# com um exemplo completo.
og_title: Converter Planilha para DataTable em C# – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Converter Planilha para DataTable em C# – Guia Completo de Programação
url: /pt/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter Planilha para DataTable em C# – Guia Completo de Programação

Já precisou **convert worksheet to DataTable** mas não tinha certeza de qual API chamar? Você não está sozinho — muitos desenvolvedores encontram esse obstáculo ao automatizar relatórios ou alimentar dados do Excel em um banco de dados. A boa notícia? Com algumas linhas de C# você pode ler um arquivo Excel em um `DataTable` e estar pronto para executar consultas LINQ, inserções em massa ou o que vier a seguir.

Neste guia, vamos percorrer o carregamento de uma pasta de trabalho Excel, extrair a primeira planilha e o estilo **export excel to DataTable C#** — sem mágica, apenas código claro. Ao final, você terá um método reutilizável que transforma qualquer planilha em um `DataTable` totalmente tipado. (E sim, também abordaremos o cenário “read Excel file into DataTable C#” para quem prefere uma única linha.)

## Pré-requisitos – O que Você Precisa

- .NET 6.0 ou posterior (o código funciona também no .NET Framework 4.6+)
- Uma referência ao **Aspose.Cells** (ou qualquer outra biblioteca que ofereça `ExportDataTable`; o exemplo usa Aspose porque é simples)
- Um arquivo Excel (`.xlsx`) que você deseja processar
- Um IDE básico de C# (Visual Studio, Rider ou VS Code)

É isso — sem pacotes NuGet extras além da própria biblioteca Excel. Pronto? Vamos lá.

## Etapa 1: Carregar Pasta de Trabalho Excel C# – Obtendo o Arquivo na Memória

Primeiro de tudo: precisamos **load excel workbook c#** estilo. Pense na pasta de trabalho como o contêiner que contém todas as planilhas, estilos e metadados. Abrí‑la corretamente garante que não bloquearemos o arquivo nem vazaremos recursos.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Por que isso importa:** A classe `Workbook` abstrai o formato de arquivo de baixo nível, então você não precisa analisar XML manualmente. Ela também libera o stream subjacente quando o objeto sai de escopo, evitando erros de arquivo em uso.

### Dica profissional
Se você estiver lidando com planilhas enormes, considere usar `LoadOptions` para habilitar **memory‑optimized loading**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Etapa 2: Acessar a Planilha Desejada – Normalmente a Primeira

A maioria dos scripts de início rápido simplesmente pega a primeira planilha, mas você pode escolher qualquer uma por nome ou índice. Aqui está a abordagem clássica de “primeira planilha”, que cobre o caso de uso **convert worksheet to DataTable** para arquivos simples.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Caso de borda:** Se sua pasta de trabalho contém planilhas ocultas ou você precisa de uma aba específica, substitua `0` por `workbook.Worksheets["MySheet"]`.

## Etapa 3: Configurar Opções de Exportação – Exportar como String para Tipos Previsíveis

Ao converter para um `DataTable`, você geralmente quer cada célula como string para evitar dores de cabeça de conversão de tipo depois. Isso é exatamente o que a flag **export excel to datatable c#** faz.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Por que forçar strings? Porque as células do Excel podem conter datas, números ou fórmulas. Exportando tudo como texto você evita tipos de coluna incompatíveis quando posteriormente inserir os dados em uma tabela SQL.

## Etapa 4: Executar a Exportação – A Lógica Central de Convert Worksheet to DataTable

Agora a mágica acontece. Chamamos `ExportDataTable` no objeto `Worksheet`, passando a linha/coluna inicial, total de linhas/colunas, uma flag para incluir cabeçalhos de coluna e nossas opções.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### O que você obtém
`dataTable` agora reflete a planilha:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Todos os valores são strings, tornando o processamento subsequente previsível.

## Etapa 5: Verificar o Resultado – Verificação rápida (read excel file into datatable c#)

Uma maneira rápida de confirmar que a conversão foi bem‑sucedida é imprimir as primeiras linhas no console. Isso também demonstra o padrão **read excel file into datatable c#** na prática.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Se você vir os valores esperados separados por pipe, você converteu a planilha para DataTable com sucesso.

## Etapa 6: Concluir — Um Método Auxiliar Reutilizável

A maioria dos projetos precisará dessa conversão em vários lugares, então vamos empacotar tudo em um único método estático. Isso torna a chamada **read excel file into datatable c#** tão simples quanto uma linha.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Exemplo de uso:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

Essa é a história completa — sem loops extras, sem interop COM, apenas dados limpos e tipados.

## Armadilhas Comuns & Como Evitá‑las

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| **Arquivo bloqueado por outro processo** | Abrindo a pasta de trabalho sem `LoadOptions` pode manter o manipulador de arquivo aberto. | Use `LoadOptions` com `MemorySetting.MemoryPreference` ou envolva o `Workbook` em um bloco `using`. |
| **Cabeçalhos de coluna ausentes** | Se a primeira linha contém dados em vez de cabeçalhos, `ExportDataTable` a tratará como dados. | Passe `false` para o parâmetro `includeColumnNames` e adicione os nomes das colunas manualmente. |
| **Tipos de dados mistos causam exceções** | Quando `ExportAsString` é `false`, células numéricas tornam‑se `double`, datas tornam‑se `DateTime`. | Mantenha `ExportAsString = true` a menos que precise de tipagem forte, então trate as conversões você mesmo. |
| **Planilhas muito grandes causam OutOfMemory** | Exportar milhões de linhas de uma vez pode estourar a memória heap. | Exporte em blocos: faça loop sobre blocos de linhas e concatene `DataTable`s. |

## Bônus: Exportar Várias Planilhas de Uma Vez

Se você precisar **export excel to datatable c#** para cada planilha, basta iterar sobre `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Agora `tables` contém um `DataTable` por planilha, indexado pelo nome da planilha — útil para importações em lote.

## Conclusão

Nós o levamos de um arquivo Excel em branco a um `DataTable` totalmente preenchido usando um fluxo de trabalho conciso, **convert worksheet to DataTable**. As etapas cobriram o carregamento da pasta de trabalho, a seleção da planilha, a configuração das opções de exportação e, finalmente, a extração dos dados para um `DataTable`. Com o método auxiliar reutilizável, você agora pode **read excel file into datatable c#** em qualquer parte da sua base de código, e ainda tem um padrão para **export excel to datatable c#** em várias planilhas.

O que vem a seguir? Tente inserir o `DataTable` resultante no `BulkInsert` do Entity Framework, gerar relatórios CSV ou aplicar filtros LINQ para extrair insights. O céu é o limite quando seus dados do Excel vivem na memória como uma tabela adequada.

Tem perguntas ou um arquivo Excel complicado que você não consegue resolver? Deixe um comentário abaixo, e feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como Importar DataTable para Excel Usando Aspose.Cells para .NET (Guia Passo a Passo)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Exportar Dados do Excel para DataTable Usando Aspose.Cells para .NET: Um Guia Completo](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Exportar Strings HTML do Excel para DataTable usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}