---
category: general
date: 2026-06-21
description: Copie a pasta de trabalho em C# e exporte a tabela para outra planilha
  usando Aspose.Cells. Siga este guia passo a passo para uma solução limpa e reutilizável.
draft: false
keywords:
- copy workbook in c#
- export table to another worksheet
language: pt
og_description: Copie a pasta de trabalho em C# e exporte a tabela para outra planilha
  com um exemplo completo e executável. Saiba por que essa abordagem funciona melhor.
og_title: Copiar Pasta de Trabalho em C# – Exportar Tabela para Outra Planilha
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  headline: Copy Workbook in C# – Export Table to Another Worksheet
  type: TechArticle
- description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  name: Copy Workbook in C# – Export Table to Another Worksheet
  steps:
  - name: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
    text: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
  - name: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
    text: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
  - name: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
    text: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
  type: HowTo
tags:
- csharp
- aspose.cells
- excel automation
title: Copiar Pasta de Trabalho em C# – Exportar Tabela para Outra Planilha
url: /pt/net/excel-copy-worksheet/copy-workbook-in-c-export-table-to-another-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copiar Pasta de Trabalho em C# – Exportar Tabela para Outra Planilha

Já se perguntou como **copiar pasta de trabalho em C#** enquanto também move um intervalo específico de dados para uma nova planilha? Você não está sozinho. Muitos desenvolvedores encontram esse obstáculo ao automatizar relatórios, faturas ou migrações de dados. A boa notícia? Com algumas linhas de código Aspose.Cells você pode duplicar a pasta de trabalho e **exportar tabela para outra planilha** em um único fluxo de trabalho organizado.

Neste tutorial vamos percorrer todo o processo — desde o carregamento do arquivo fonte, clonagem, exportação de um intervalo como string, até colar essa string na planilha de destino. Ao final, você terá um trecho de código autônomo, pronto para produção, que pode ser inserido em qualquer projeto .NET.

## O Que Você Precisa

Antes de começarmos, certifique‑se de que tem:

- **Aspose.Cells for .NET** (versão 23.12 ou posterior). É uma biblioteca poderosa que manipula arquivos Excel sem precisar do Office instalado.
- Um ambiente de desenvolvimento .NET (Visual Studio, Rider ou VS Code com a extensão C#).
- Uma pasta de trabalho de exemplo chamada `Formatted.xlsx` colocada em um diretório conhecido (referiremos a ela como `YOUR_DIRECTORY/Formatted.xlsx`).

Nenhum pacote NuGet adicional é necessário além do Aspose.Cells, e o código funciona em .NET 6+, .NET Framework 4.7+ ou .NET Core.

## Implementação Passo a Passo

A seguir está o programa completo e executável. Sinta‑se à vontade para copiar‑colar em um projeto de aplicativo console e pressionar **F5**.

```csharp
using System;
using Aspose.Cells;

namespace WorkbookCopyExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load the source workbook
            // -------------------------------------------------
            // Adjust the path to point at your actual file location.
            string sourcePath = @"YOUR_DIRECTORY/Formatted.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            Console.WriteLine("Source workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Set up export options – we want the range as a string
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true   // This forces the export to return CSV‑style text.
            };
            Console.WriteLine("Export options configured (ExportAsString = true).");

            // -------------------------------------------------
            // Step 3: Copy workbook in C# – creates an isolated clone
            // -------------------------------------------------
            // Using the Copy method ensures the original stays untouched.
            Workbook destinationWorkbook = sourceWorkbook.Copy();
            Console.WriteLine("Destination workbook created as a copy of the source.");

            // -------------------------------------------------
            // Step 4: Export the specified range (B2:B10) from the source sheet
            // -------------------------------------------------
            // The range is taken from the first worksheet (index 0).
            // ExportTable returns a string that can be written directly.
            string exportedTable = sourceWorkbook.Worksheets[0]
                .Cells.ExportTable(sourceWorkbook.Worksheets[0].Cells["B2:B10"],
                                   exportOptions);
            Console.WriteLine("Range B2:B10 exported as string:");
            Console.WriteLine(exportedTable);

            // -------------------------------------------------
            // Step 5: Paste the exported string into the destination sheet
            // -------------------------------------------------
            // We start at cell A1 of the first worksheet in the destination.
            destinationWorkbook.Worksheets[0].Cells["A1"]
                .PutValue(exportedTable);
            Console.WriteLine("Exported data placed at A1 in the destination workbook.");

            // -------------------------------------------------
            // Step 6: Save the result so you can verify it
            // -------------------------------------------------
            string resultPath = @"YOUR_DIRECTORY/Copy_With_ExportedTable.xlsx";
            destinationWorkbook.Save(resultPath);
            Console.WriteLine($"Result saved to {resultPath}");
        }
    }
}
```

### Por Que Essa Abordagem Funciona

1. **`Workbook.Copy()`** realiza uma clonagem profunda de cada planilha, estilo e fórmula. É a forma mais limpa de **copiar pasta de trabalho em C#** sem iterar manualmente sobre as planilhas.
2. **`ExportTableOptions.ExportAsString = true`** indica ao Aspose.Cells que nos devolva uma string no estilo CSV em vez de um bloco binário. Isso facilita inserir os dados em qualquer célula usando `PutValue`.
3. Ao exportar da **pasta de trabalho fonte** e inserir na **pasta de trabalho destino**, mantemos os dois arquivos completamente independentes — sem contaminação acidental de referências.

## Casos Limite & Armadilhas Comuns

| Situação | O Que Observar | Correção / Recomendação |
|-----------|-------------------|-----------------------|
| **Índices de planilha diferentes** | Se a pasta de trabalho fonte ou destino possui várias planilhas, codificar o índice `0` pode apontar para a planilha errada. | Use `Worksheets["SheetName"]` ou itere sobre `Worksheets` para localizar a planilha desejada. |
| **Intervalos grandes** | Exportar um intervalo enorme como string pode atingir limites de memória. | Considere exportar em blocos ou usar `ExportTable` com `ExportAsString = false` e manipular fluxos binários. |
| **Perda de formatação** | `ExportAsString` remove toda a formatação; apenas valores brutos são mantidos. | Se precisar de estilos, exporte como `IEnumerable<CellArea>` e copie as células individualmente. |
| **Problemas com caminho de arquivo** | Caminhos relativos podem falhar quando o app é executado a partir de um diretório de trabalho diferente. | Use `Path.Combine(Environment.CurrentDirectory, "Formatted.xlsx")` ou armazene caminhos em configuração. |

### Dica Profissional

Se você pretende reutilizar os dados exportados em várias pastas de trabalho, encapsule a lógica de exportar‑e‑colar em um método auxiliar:

```csharp
static void ExportRangeToWorkbook(Workbook src, string range, Workbook dest, string destCell)
{
    var opts = new ExportTableOptions { ExportAsString = true };
    string data = src.Worksheets[0].Cells.ExportTable(src.Worksheets[0].Cells[range], opts);
    dest.Worksheets[0].Cells[destCell].PutValue(data);
}
```

Agora você pode chamar `ExportRangeToWorkbook(sourceWorkbook, "B2:B10", destinationWorkbook, "A1");` onde precisar.

## Verificando o Resultado

Abra `Copy_With_ExportedTable.xlsx` no Excel ou em qualquer visualizador de planilhas:

- A primeira planilha deve ficar idêntica a `Formatted.xlsx` **exceto** pelo novo bloco de dados que começa em **A1**.
- As células de A1 a A9 (ou quantas linhas o intervalo B2:B10 ocupar) conterão os valores exportados, cada um separado pelo delimitador padrão (vírgula para CSV). Se precisar de outro delimitador, defina `exportOptions.Separator` antes de exportar.

Essa verificação visual confirma que tanto a operação de **copiar pasta de trabalho em C#** quanto a de **exportar tabela para outra planilha** foram bem‑sucedidas.

## Conclusão

Acabamos de demonstrar um padrão limpo e repetível para **copiar pasta de trabalho em C#** enquanto simultaneamente **exportamos uma tabela para outra planilha**. Os principais aprendizados são:

- Use `Workbook.Copy()` para uma clonagem profunda e segura.
- Aproveite `ExportTableOptions.ExportAsString` para transformar um intervalo em uma string portátil.
- Insira a string onde precisar com `PutValue`.

A partir daqui você pode explorar:

- Exportar múltiplos intervalos não contíguos.
- Converter a string em um array 2‑D para manipulação de dados mais avançada.
- Automatizar o processo em uma pasta de vários arquivos (processamento em lote).

Teste, ajuste o intervalo e veja como essa técnica simplifica seus pipelines de automação Excel. Se encontrar algum obstáculo ou tiver ideias de extensões, deixe um comentário abaixo. Boa codificação!

![Diagrama de exemplo de copiar pasta de trabalho em C#](https://example.com/images/copy-workbook-diagram.png "Diagrama de exemplo de copiar pasta de trabalho em C# mostrando etapas de origem, exportação e destino")


## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Copiar Planilha de Uma Pasta de Trabalho para Outra usando Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Copiar Planilhas Dentro da Mesma Pasta de Trabalho Usando Aspose.Cells para .NET - Guia Passo a Passo](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copiar Dados Dentro da Pasta de Trabalho usando Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-data-within-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}