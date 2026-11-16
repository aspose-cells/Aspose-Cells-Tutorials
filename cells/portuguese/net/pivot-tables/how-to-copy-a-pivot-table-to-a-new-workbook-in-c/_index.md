---
category: general
date: 2026-11-16
description: Como copiar tabela dinâmica de um arquivo Excel para uma nova pasta de
  trabalho usando C#. Aprenda a carregar a pasta de trabalho, copiar o intervalo e
  preservar as tabelas dinâmicas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: pt
lastmod: 2026-11-16
og_description: Como copiar tabela dinâmica de uma pasta de trabalho existente para
  uma nova pasta de trabalho usando C#. Siga este guia completo para carregar a pasta
  de trabalho do Excel, copiar o intervalo e manter a tabela dinâmica intacta.
og_image_alt: how to copy pivot table example in C#
og_title: Como copiar uma tabela dinâmica para uma nova planilha em C# – guia passo
  a passo
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Como copiar uma tabela dinâmica para uma nova pasta de trabalho em C#
url: /pt/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como copiar uma tabela dinâmica para uma nova pasta de trabalho em C#

Se você precisa **copiar uma tabela dinâmica** de um arquivo Excel para uma nova pasta de trabalho, este guia mostra os passos exatos. Você aprenderá como **carregar pasta de trabalho Excel c#**, definir o intervalo de origem e **copiar intervalo para nova pasta de trabalho** mantendo a tabela dinâmica intacta.

Copiar uma tabela dinâmica é uma necessidade comum quando você deseja reutilizar um modelo de relatório, migrar dados entre projetos ou gerar um arquivo leve para distribuição. O exemplo de código abaixo usa Aspose.Cells, uma biblioteca .NET totalmente gerenciada que funciona sem o Microsoft Office instalado. Ao final deste tutorial você terá um programa executável que cria uma nova pasta de trabalho contendo a tabela dinâmica original, pronta para processamento adicional ou compartilhamento.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 SDK ou superior (o exemplo funciona com .NET Core e .NET Framework)
* Visual Studio 2022 ou qualquer editor C# de sua preferência
* Uma licença do Aspose.Cells for .NET (a avaliação gratuita funciona para testes)
* Um arquivo Excel de origem (`Source.xlsx`) que contenha ao menos uma tabela dinâmica

> **Dica profissional:** Se estiver usando a avaliação gratuita, defina a licença no código para evitar marcas d'água de avaliação.

## Etapa 1: Carregar a pasta de trabalho de origem (load excel workbook c#)

A primeira ação é abrir a pasta de trabalho que contém a tabela dinâmica. Aspose.Cells lê o arquivo para a memória, dando acesso total a planilhas, células e objetos de tabela dinâmica.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Por que isso importa*: Carregar a pasta de trabalho é a base para qualquer automação Excel. Sem um objeto `Workbook` válido você não pode inspecionar a tabela dinâmica nem copiar seus dados.

## Etapa 2: Definir a área de células que engloba a tabela dinâmica (copy range to new workbook)

Uma tabela dinâmica vive dentro de um bloco retangular de células. Você deve especificar esse bloco para que a operação de cópia saiba o que mover. O construtor `CellArea` usa índices baseados em zero: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Por que isso importa*: Ao definir explicitamente o intervalo você evita copiar dados não relacionados e garante que o cache da tabela dinâmica seja incluído. O intervalo pode ser calculado dinamicamente se precisar lidar com tamanhos de tabela variáveis.

## Etapa 3: Criar uma nova pasta de trabalho e obter sua primeira planilha

Agora crie a pasta de trabalho de destino que receberá as linhas copiadas. Aspose.Cells adiciona automaticamente uma planilha padrão, que usaremos como alvo.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Por que isso importa*: Começar com uma pasta de trabalho limpa garante que apenas a tabela dinâmica (e suas linhas de suporte) terminem no arquivo, mantendo a saída leve.

## Etapa 4: Copiar linhas do intervalo de origem para a planilha de destino (how to copy pivot table)

O método `CopyRows` copia linhas inteiras, preservando fórmulas, formatação e—crucialmente—tabelas dinâmicas. Os parâmetros do método são: linha inicial, linha final, coleção de células de destino e o índice da linha no destino onde a cópia começa (aqui `0` para iniciar na primeira linha).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Por que isso importa*: Usar `CopyRows` em vez de copiar células individuais assegura que o cache da tabela dinâmica permaneça ligado aos dados copiados. Aspose.Cells trata das estruturas XML subjacentes, de modo que você não precisa reconstruir a tabela manualmente.

## Etapa 5: Salvar a pasta de trabalho resultante (copy range to new workbook)

Por fim, grave o novo arquivo no disco. A pasta de trabalho de destino agora contém uma tabela dinâmica idêntica que funciona independentemente do arquivo original.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Saída esperada

Executar o programa produz `CopyWithPivot.xlsx`. Abrir o arquivo no Excel mostra:

* O mesmo layout de tabela dinâmica de `Source.xlsx`
* Todas as linhas de dados de origem que faziam parte do cache da tabela dinâmica
* Nenhuma referência à pasta de trabalho original (a tabela funciona offline)

## Lidando com variações comuns

### Copiando múltiplas tabelas dinâmicas

Se sua planilha de origem contém várias tabelas dinâmicas, expanda o `CellArea` para cobrir a união de todos os intervalos, ou repita a etapa de cópia para cada área distinta.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Preservando estilos e formatação condicional

`CopyRows` copia estilos de célula automaticamente. Se precisar preservar estilos nomeados em toda a pasta de trabalho ou formatos numéricos personalizados, chame `destWorkbook.Worksheets[0].CopyStyle` antes de salvar.

### Trabalhando com pastas de trabalho grandes

Para arquivos maiores que 100 MB, considere usar `Workbook.LoadOptions` com a propriedade `MemorySetting` definida como `MemorySetting.MemoryPreference` para reduzir a pressão de memória.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Código-fonte completo (pronto para executar)

Abaixo está o programa completo, incluindo diretivas `using` e comentários. Copie-o para um novo projeto de console e substitua `YOUR_DIRECTORY` pelo caminho da pasta real.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Execute o programa (`dotnet run` ou `Ctrl+F5` no Visual Studio). Após a execução, abra `CopyWithPivot.xlsx` para verificar que a tabela dinâmica se comporta exatamente como a original.

## Perguntas frequentes

**P: Isso funciona com arquivos que contêm macros ou workbooks habilitados para VBA?**  
R: Aspose.Cells pode ler arquivos habilitados para macro (`.xlsm`), mas o código da macro não é copiado. A própria tabela dinâmica é preservada porque faz parte do XML da planilha.

**P: E se a tabela dinâmica usar uma fonte de dados externa?**  
R: A operação de cópia inclui apenas os dados em cache. Se a pasta de trabalho de destino precisar atualizar a partir da fonte original, será necessário reconfigurar a conexão de dados manualmente.

**P: Posso copiar a tabela dinâmica sem as linhas de dados subjacentes?**  
R: Não. Uma tabela dinâmica precisa do seu cache. A maneira mais confiável é copiar as linhas que contêm o cache, como demonstrado. Você pode ocultar essas linhas posteriormente, se não quiser que fiquem visíveis.

## Conclusão

Agora você sabe **como copiar uma tabela dinâmica** de um arquivo Excel para outro usando C#. O tutorial abordou **load excel workbook c#**, definiu o **copy range to new workbook** e utilizou o método `CopyRows` do Aspose.Cells para manter a tabela dinâmica intacta. Com o exemplo completo e executável, você pode integrar esse padrão em pipelines de relatórios, ferramentas de exportação automatizadas ou qualquer cenário onde uma tabela dinâmica precise ser transferida entre pastas de trabalho.

### Próximos passos

* Explore recursos do **Aspose.Cells** como atualização de tabelas dinâmicas programaticamente.  
* Combine esta abordagem com **ExcelPackage** (EPPlus) se precisar de uma alternativa open‑source.  
* Automatize a cópia entre várias planilhas percorrendo `srcWorkbook.Worksheets`.  

Sinta‑se à vontade para experimentar diferentes intervalos, adicionar estilos personalizados ou incorporar a lógica em um serviço maior de processamento de dados. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Criar nova pasta de trabalho em C# – Copiar Tabela Dinâmica](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [Como copiar tabela dinâmica no Excel com C# e Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copiar tabela dinâmica para nova pasta de trabalho, exportar forma para PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}