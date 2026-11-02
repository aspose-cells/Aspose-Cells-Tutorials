---
category: general
date: 2026-03-21
description: Exportar tabela de dados do Excel para um DataTable com cabeçalhos, limitar
  casas decimais e exportar as primeiras 100 linhas usando Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: pt
og_description: Aprenda a exportar uma tabela de dados do Excel para um DataTable,
  manter os cabeçalhos, limitar casas decimais e obter as primeiras 100 linhas em
  C#.
og_title: Exportar Tabela de Dados do Excel em C# – Guia Passo a Passo
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Exportar Tabela de Dados do Excel em C# – Guia Completo
url: /pt/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel Data Table – Full C# Walkthrough

Precisa **exportar a tabela de dados do Excel** de uma pasta de trabalho para um `DataTable` .NET? Você está no lugar certo — este guia mostra exatamente como fazer isso, manter os cabeçalhos das colunas, limitar casas decimais e extrair apenas as primeiras 100 linhas.  

Se você já ficou olhando para uma planilha e pensou: “Como faço para levar isso para o meu app sem perder formatação?” você não está sozinho. Nos próximos minutos vamos transformar esse “e se” em uma solução concreta, copiar‑colar, que funciona com Aspose.Cells, uma biblioteca popular para manipulação de Excel.

## O que você vai aprender

- Como **exportar excel para datatable** usando o método `ExportDataTable`.  
- Como manter os nomes originais das colunas (`export excel with headers`).  
- Como **limitar casas decimais excel** configurando `ExportTableOptions`.  
- Como recuperar com segurança apenas as 100 primeiras linhas (`export first 100 rows`).  

Sem scripts externos, sem strings mágicas — apenas C# puro que você pode inserir em qualquer projeto .NET.

## Pré‑requisitos

| Requisito | Por que importa |
|-----------|-----------------|
| .NET 6 ou posterior (ou .NET Framework 4.7+) | Aspose.Cells suporta ambos, mas runtimes mais recentes oferecem APIs prontas para async. |
| Pacote NuGet Aspose.Cells for .NET | Fornece `Workbook`, `ExportTableOptions` e o helper `ExportDataTable`. |
| Um arquivo Excel de exemplo (por exemplo, `Numbers.xlsx`) | A fonte dos dados que você exportará. |
| Conhecimento básico de C# | Você seguirá os trechos de código, mas nada avançado é necessário. |

Se algum desses itens lhe for desconhecido, obtenha o pacote NuGet com `dotnet add package Aspose.Cells` e crie um pequeno arquivo Excel com alguns números — seus dados de teste.

![exemplo de exportação de tabela de dados do excel](excel-data-table.png "Captura de tela de uma planilha Excel que será exportada para um DataTable")

## Etapa 1: Carregar a Pasta de Trabalho (export excel data table)

A primeira coisa que você precisa é uma instância de `Workbook` que aponte para o seu arquivo Excel. Pense nisso como abrir um livro antes de ler os capítulos.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Por que isso importa:** Carregar a pasta de trabalho lhe dá acesso às suas planilhas, células e estilos. Se o caminho do arquivo estiver errado, o Aspose lançará uma `FileNotFoundException`, então verifique o local.

## Etapa 2: Configurar Opções de Exportação – limit decimal places excel

Por padrão o Aspose exporta todo valor numérico com precisão total. Muitas vezes você precisa apenas de alguns dígitos significativos, especialmente ao alimentar os dados em uma grade de UI ou em uma API que espera números arredondados.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Dica de especialista:** Se precisar de uma estratégia de arredondamento diferente (por exemplo, sempre arredondar para cima), você pode pós‑processar o `DataTable` após a exportação. A configuração `SignificantDigits` é a maneira mais rápida de **limitar casas decimais excel** sem escrever loops extras.

## Etapa 3: Exportar o Intervalo Desejado (export first 100 rows)

Agora informamos ao Aspose qual bloco de células queremos puxar para um `DataTable`. Neste tutorial pegamos as primeiras 100 linhas e as primeiras 10 colunas, mas você pode ajustar esses números conforme sua necessidade.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Caso de borda:** Se a planilha contiver menos de 100 linhas, o Aspose simplesmente exportará o que existir sem lançar erro. Contudo, pode ser interessante proteger contra um intervalo inesperadamente pequeno:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Etapa 4: Verificar o Resultado – Dump Rápido no Console

Ver os dados no depurador é bom, mas imprimir algumas linhas no console confirma que o **export excel to datatable** realmente funcionou e que as casas decimais foram truncadas.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Saída esperada

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Observe como as colunas numéricas agora exibem apenas quatro dígitos significativos, correspondendo à configuração `SignificantDigits = 4` que aplicamos anteriormente.

## Etapa 5: Envolver Tudo – Um Exemplo Completo e Executável

Abaixo está o programa completo que você pode copiar‑colar em um aplicativo console. Ele inclui tratamento de erros, a proteção opcional de contagem de linhas e o método auxiliar para impressão.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Execute o programa e você verá as primeiras 100 linhas da sua planilha, arredondadas adequadamente, com os nomes das colunas preservados.

## Perguntas Frequentes & Armadilhas

| Pergunta | Resposta |
|----------|----------|
| **E se minha planilha tiver células mescladas?** | `ExportDataTable` achata células mescladas pegando o valor da célula superior‑esquerda. Se precisar de tratamento customizado, desfaça a mesclagem primeiro ou leia os objetos `Cell` diretamente. |
| **Posso exportar para um `DataSet` em vez disso?** | Sim — use `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}