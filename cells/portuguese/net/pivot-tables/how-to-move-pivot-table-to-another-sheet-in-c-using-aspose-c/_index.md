---
category: general
date: 2026-10-26
description: mover tabela dinâmica para outra planilha em C# com um guia passo a passo
  que também mostra como carregar a pasta de trabalho do Excel em C# de forma eficiente
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- move pivot table to another sheet
- load excel workbook c#
- copy rows with pivot table
- Aspose.Cells pivot table
- C# Excel automation
language: pt
lastmod: 2026-10-26
og_description: mover tabela dinâmica para outra planilha em C# usando Aspose.Cells.
  Siga este tutorial conciso para carregar a pasta de trabalho Excel em C# e copiar
  tabelas dinâmicas com segurança.
og_image_alt: Screenshot of a pivot table moved to another sheet using C#
og_title: Mover tabela dinâmica para outra planilha em C# – guia completo do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: move pivot table to another sheet in C# with a step‑by‑step guide that
    also shows how to load Excel workbook C# efficiently
  headline: How to move pivot table to another sheet in C# using Aspose.Cells
  type: TechArticle
- description: move pivot table to another sheet in C# with a step‑by‑step guide that
    also shows how to load Excel workbook C# efficiently
  name: How to move pivot table to another sheet in C# using Aspose.Cells
  steps:
  - name: Expected result
    text: '* The file **CopyPivot.xlsx** contains a new worksheet **PivotCopy**. *
      The pivot table appears exactly as it did on the original sheet, preserving
      filters, row/column fields, and data source connections. * All original data
      remains in the source worksheet, so you have effectively **moved pivot tabl'
  - name: Multiple pivot tables on the same sheet
    text: 'If the source sheet hosts several pivots, repeat steps 3–5 for each `PivotTable`
      object:'
  - name: Copying to an existing sheet with data
    text: 'When the destination sheet already contains data, calculate the next free
      row:'
  - name: Preserving formatting
    text: '`CopyRows` copies cell values, formulas, and formatting by default. If
      you need to exclude formatting, use the overload that accepts a `CopyOptions`
      object and set `CopyOptions.CopyStyle = false`.'
  - name: What to explore next
    text: '* **Load Excel workbook C#** and modify formulas programmatically – see
      the Aspose.Cells documentation on `Formula` objects. * **Export pivot tables
      to PDF** using `Workbook.Save` with `SaveFormat.Pdf`. * **Create pivot tables
      from scratch** with the `PivotTable` API for dynamic report generation.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Como mover a tabela dinâmica para outra planilha em C# usando Aspose.Cells
url: /pt/net/pivot-tables/how-to-move-pivot-table-to-another-sheet-in-c-using-aspose-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como mover uma tabela dinâmica para outra planilha em C# usando Aspose.Cells

Se você precisa **mover uma tabela dinâmica para outra planilha** em um arquivo .xlsx, este guia mostra os passos exatos. Você também aprenderá como **carregar a pasta de trabalho Excel C#** com Aspose.Cells, copiar a tabela dinâmica associada e salvar o resultado sem perder nenhuma conexão de dados.

O tutorial cobre tudo que é necessário para uma implementação pronta para produção: pacotes NuGet necessários, código-fonte completo, explicações sobre por que cada chamada de API é importante e dicas para lidar com casos de borda comuns, como múltiplas tabelas dinâmicas ou planilhas de destino que já existem.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior instalado  
* Visual Studio 2022 (ou qualquer IDE que suporte .NET)  
* Pacote NuGet Aspose.Cells for .NET (`Aspose.Cells`) – a biblioteca que fornece as classes `Workbook`, `Worksheet` e `CellArea` usadas no exemplo  

Não é necessário ter o Microsoft Office instalado; o Aspose.Cells trabalha diretamente com o formato de arquivo.

## Etapa 1: Carregar a pasta de trabalho Excel em C#

A primeira operação é ler o arquivo de origem do disco. Carregar a pasta de trabalho cria uma representação em memória de cada planilha, célula e cache de tabela dinâmica.

```csharp
using Aspose.Cells;

namespace PivotTableMover
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            var sourcePath = @"C:\Data\Source.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            // Continue with pivot table handling...
        }
    }
}
```

*Por que esta etapa é importante* – `Workbook` analisa o pacote XLSX, preenche a coleção `Worksheets` e prepara os objetos de cache de tabela dinâmica para que possam ser referenciados posteriormente. Sem carregar a pasta de trabalho, nenhuma manipulação adicional é possível.

## Etapa 2: Identificar a planilha que contém a tabela dinâmica

Normalmente a primeira planilha contém a tabela dinâmica, mas você pode pesquisar por nome ou verificando a coleção `PivotTables`. Para clareza, este exemplo usa a primeira planilha.

```csharp
// Get the first worksheet that contains the pivot table
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

Se a pasta de trabalho contiver várias planilhas com tabelas dinâmicas, itere sobre `sourceWorkbook.Worksheets` e inspecione `sheet.PivotTables.Count` para escolher a correta.

## Etapa 3: Definir o intervalo de células que engloba a tabela dinâmica

Aspose.Cells requer uma estrutura `CellArea` para especificar o bloco retangular que você deseja copiar. O intervalo deve incluir toda a tabela dinâmica, incluindo suas linhas de cabeçalho e quaisquer colunas calculadas.

```csharp
// Define the area covering the pivot table (adjust rows/columns as needed)
CellArea pivotRange = new CellArea
{
    StartRow = 0,          // zero‑based index, first row of the pivot
    StartColumn = 0,       // first column of the pivot
    EndRow = 30,           // last row of the pivot (inclusive)
    EndColumn = 10         // last column of the pivot (inclusive)
};
```

*Por que esta etapa é importante* – O método `CopyRows` funciona em um intervalo de linhas, mas ao passar um `CellArea` você garante que todas as células pertencentes à tabela dinâmica sejam incluídas. Se o intervalo for pequeno demais, a tabela dinâmica perderá seus dados de origem; se for grande demais, células desnecessárias serão copiadas.

## Etapa 4: Criar (ou selecionar) a planilha de destino

Você pode mover a tabela dinâmica para uma planilha existente ou criar uma nova. O exemplo cria uma planilha nova chamada **"PivotCopy"** e coloca as linhas copiadas a partir da linha 0.

```csharp
// Create a new worksheet for the copied pivot table
Worksheet destSheet = sourceWorkbook.Worksheets[sourceWorkbook.Worksheets.Add()];
destSheet.Name = "PivotCopy";
```

Se preferir mover a tabela dinâmica para uma planilha existente, substitua o código de criação por uma referência a essa planilha:

```csharp
// Worksheet destSheet = sourceWorkbook.Worksheets["ExistingSheetName"];
```

## Etapa 5: Copiar as linhas — incluindo a tabela dinâmica associada — para a planilha de destino

O método `CopyRows` aceita um parâmetro (`true`) que indica ao Aspose.Cells para copiar quaisquer tabelas dinâmicas vinculadas às linhas. Esse parâmetro é essencial; sem ele a definição da tabela dinâmica seria perdida.

```csharp
// Copy rows from sourceSheet to destSheet, preserving pivot tables
sourceSheet.CopyRows(
    sourceRowIndex: 0,          // start row in source sheet
    totalRows: 40,              // number of rows to copy (covers the pivot range)
    sourceArea: pivotRange,     // the cell area that defines the pivot
    copyAssociatedPivotTables: true, // preserve pivot tables
    destinationSheet: destSheet,
    destinationRowIndex: 0);    // start row in the destination sheet
```

*Por que esta etapa é importante* – O argumento `copyAssociatedPivotTables` garante que o cache da tabela dinâmica e as configurações de campo viajem com as linhas copiadas. A planilha de destino recebe uma tabela dinâmica totalmente funcional que aponta para a mesma fonte de dados da original.

## Etapa 6: Salvar a pasta de trabalho modificada

Após a operação de cópia, persista a pasta de trabalho em um novo arquivo. Manter o arquivo original intacto torna o processo seguro para pipelines automatizados.

```csharp
// Save the workbook with the moved pivot table
var outputPath = @"C:\Data\CopyPivot.xlsx";
sourceWorkbook.Save(outputPath);
```

Ao abrir **CopyPivot.xlsx**, você verá a planilha "PivotCopy" contendo uma réplica exata da tabela dinâmica original, pronta para análise ou distribuição adicional.

## Exemplo completo em funcionamento

Juntando todas as etapas, obtém‑se um aplicativo console autônomo:

```csharp
using Aspose.Cells;

namespace PivotTableMover
{
    class Program
    {
        static void Main()
        {
            // 1. Load the source workbook
            var sourcePath = @"C:\Data\Source.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);

            // 2. Locate the worksheet with the pivot table
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

            // 3. Define the range that includes the pivot table
            CellArea pivotRange = new CellArea
            {
                StartRow = 0,
                StartColumn = 0,
                EndRow = 30,
                EndColumn = 10
            };

            // 4. Create a destination worksheet
            Worksheet destSheet = sourceWorkbook.Worksheets[sourceWorkbook.Worksheets.Add()];
            destSheet.Name = "PivotCopy";

            // 5. Copy rows and associated pivot tables
            sourceSheet.CopyRows(
                sourceRowIndex: 0,
                totalRows: 40,
                sourceArea: pivotRange,
                copyAssociatedPivotTables: true,
                destinationSheet: destSheet,
                destinationRowIndex: 0);

            // 6. Save the result
            var outputPath = @"C:\Data\CopyPivot.xlsx";
            sourceWorkbook.Save(outputPath);
        }
    }
}
```

### Resultado esperado

* O arquivo **CopyPivot.xlsx** contém uma nova planilha **PivotCopy**.  
* A tabela dinâmica aparece exatamente como estava na planilha original, preservando filtros, campos de linha/coluna e conexões de fonte de dados.  
* Todos os dados originais permanecem na planilha de origem, de modo que você efetivamente **moveu a tabela dinâmica para outra planilha** sem perder nenhuma funcionalidade.

## Lidando com variações comuns

### Múltiplas tabelas dinâmicas na mesma planilha
Se a planilha de origem hospedar várias tabelas dinâmicas, repita as etapas 3–5 para cada objeto `PivotTable`:

```csharp
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Determine the exact area of each pivot table
    CellArea ptArea = pt.TableRange;
    // Copy each pivot individually
    sourceSheet.CopyRows(0, ptArea.EndRow - ptArea.StartRow + 1,
        ptArea, true, destSheet, destSheet.Cells.MaxDataRow + 1);
}
```

### Copiando para uma planilha existente com dados
Quando a planilha de destino já contém dados, calcule a próxima linha livre:

```csharp
int destStartRow = destSheet.Cells.MaxDataRow + 1;
sourceSheet.CopyRows(0, 40, pivotRange, true, destSheet, destStartRow);
```

### Preservando formatação
`CopyRows` copia valores de célula, fórmulas e formatação por padrão. Se precisar excluir a formatação, use a sobrecarga que aceita um objeto `CopyOptions` e defina `CopyOptions.CopyStyle = false`.

## Dicas profissionais

* **Validar o intervalo da tabela dinâmica** – antes de copiar, verifique se `pivotRange.EndRow` e `EndColumn` correspondem a `pt.TableRange`. Intervalos incompatíveis podem truncar a tabela dinâmica ou duplicar linhas extras.  
* **Atualizar o cache da tabela dinâmica** após mover a tabela se os dados de origem mudarem. Chame `pt.RefreshData()` na tabela dinâmica de destino para garantir que os cálculos estejam atualizados.  
* **Evitar caminhos codificados** em código de produção. Use `Path.Combine` e arquivos de configuração para tornar a solução portátil entre ambientes.

## Conclusão

Agora você tem um método completo e pronto para produção para **mover uma tabela dinâmica para outra planilha** em C#. O tutorial demonstrou como **carregar a pasta de trabalho Excel C#**, definir o intervalo exato da tabela dinâmica, copiar linhas preservando a definição da tabela e salvar o arquivo atualizado. Com esses blocos de construção, você pode automatizar tarefas complexas de relatórios Excel, integrar a manipulação de tabelas dinâmicas em serviços web ou criar pipelines personalizados de análise de dados.

### O que explorar a seguir

* **Carregar a pasta de trabalho Excel C#** e modificar fórmulas programaticamente – veja a documentação do Aspose.Cells sobre objetos `Formula`.  
* **Exportar tabelas dinâmicas para PDF** usando `Workbook.Save` com `SaveFormat.Pdf`.  
* **Criar tabelas dinâmicas do zero** com a API `PivotTable` para geração dinâmica de relatórios.  

Sinta‑se à vontade para experimentar diferentes arquivos de origem, múltiplas tabelas dinâmicas ou layouts de destino personalizados. O mesmo padrão se aplica independentemente do tamanho ou complexidade da pasta de trabalho. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Copy Pivot Table to Another Sheet – Complete C# Guide](/cells/english/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}