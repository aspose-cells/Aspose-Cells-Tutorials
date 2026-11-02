---
category: general
date: 2026-09-27
description: Aprenda como excluir linhas de uma tabela do Excel em C# com um guia
  passo a passo que também mostra como carregar rapidamente uma pasta de trabalho
  do Excel em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: pt
lastmod: 2026-09-27
og_description: Excluir linhas de uma tabela do Excel em C# com um exemplo claro.
  Este tutorial também aborda como carregar uma pasta de trabalho do Excel em C# e
  lidar com casos de borda comuns.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Excluir linhas de tabela do Excel em C# – guia completo de código
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Como excluir linhas de uma tabela do Excel usando C#
url: /pt/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excluir linhas de tabela do Excel em C# – guia completo de programação

Se você precisa **excluir linhas de tabela do Excel** em um arquivo .xlsx, este tutorial mostra exatamente como fazer isso com C#. Você verá um exemplo conciso e executável que carrega uma pasta de trabalho Excel, remove linhas específicas da primeira tabela e salva o resultado. A abordagem funciona com a popular biblioteca Aspose.Cells e pode ser adaptada para outras APIs Excel .NET.

Remover linhas de uma tabela é uma tarefa comum ao limpar dados importados, reduzir seções de relatórios ou automatizar atualizações de planilhas. Ao final deste guia, você será capaz de **carregar pasta de trabalho Excel C#**, localizar uma tabela (ListObject), excluir quaisquer linhas que desejar e gravar o arquivo modificado de volta ao disco.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou posterior instalado (o código também funciona com .NET Framework 4.7+).
* Uma referência ao pacote NuGet **Aspose.Cells** (ou qualquer biblioteca compatível que exponha os tipos `Workbook`, `Worksheet` e `ListObject`).
* Um arquivo de entrada chamado `input.xlsx` colocado em uma pasta que você pode referenciar a partir do seu projeto.
* Familiaridade básica com a sintaxe C# e Visual Studio (ou sua IDE preferida).

> **Dica profissional:** Se você prefere uma alternativa de código aberto, a mesma lógica pode ser aplicada com **ClosedXML** – basta substituir as classes específicas do Aspose por `XLWorkbook`, `IXLWorksheet` e `IXLTable`.

## Etapa 1: Carregar a pasta de trabalho Excel em C#

A primeira operação é ler o arquivo de origem para a memória. Carregar a pasta de trabalho é barato para tamanhos típicos de planilhas e fornece acesso total a planilhas, tabelas e valores de células.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Por que isso importa:* `Workbook` analisa a estrutura Open XML do arquivo .xlsx, expondo uma coleção de objetos `Worksheet`. Se o arquivo não for encontrado, o Aspose lança uma `FileNotFoundException`, portanto, verifique se o caminho está correto.

## Etapa 2: Acessar a planilha de destino

A maioria das planilhas contém várias abas; você precisa escolher a que contém a tabela que deseja modificar. Aqui usamos a primeira aba (`Worksheets[0]`), que é um padrão seguro para arquivos simples.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Por que isso importa:* `Worksheet` é o contêiner para tabelas (`ListObjects`). Acessar a aba correta evita alterações acidentais em dados não relacionados.

## Etapa 3: Excluir linhas da tabela do Excel

Tabelas do Excel são representadas por objetos `ListObject`. A primeira tabela na aba é `ListObjects[0]`. O método `DeleteRows(startIndex, rowCount)` remove linhas **relativas à área de dados da tabela**, não aos números absolutos de linha da planilha.  

Neste exemplo, excluímos a segunda e a terceira linhas da tabela (o cabeçalho é a linha 0, portanto começamos no índice 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### E se a tabela tiver um nome ou posição diferente?

* **Tabela nomeada:** Use `ws.ListObjects["MyTableName"]` em vez do índice.  
* **Múltiplas tabelas:** Percorra `ws.ListObjects` e escolha a que corresponde a uma condição (por exemplo, nomes de cabeçalhos de coluna).  
* **Contagem de linhas dinâmica:** Você pode calcular `rowCount` em tempo de execução inspecionando `ws.ListObjects[0].DataRange.RowCount`.

### Tratamento de casos extremos

| Situação                              | Alteração de código recomendada                                      |
|---------------------------------------|-----------------------------------------------------------------------|
| A tabela está vazia ou tem menos linhas      | Check `ws.ListObjects[0].DataRange.RowCount` before deleting. |
| Linhas a excluir excedem o tamanho da tabela       | Clamp `rowCount` to `DataRange.RowCount - startIndex`.       |
| Necessário excluir linhas com base em uma condição (por exemplo, valor na coluna C) | Iterate `DataRange.Rows` and collect matching indices, then delete in reverse order to keep indices stable. |

## Etapa 4: Salvar a pasta de trabalho modificada

Após a exclusão, grave a pasta de trabalho de volta em um novo arquivo (ou sobrescreva o original, se preferir). Salvar cria um novo .xlsx que reflete a tabela atualizada.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Por que isso importa:* `Save` serializa a representação em memória para o disco. Se precisar preservar o arquivo original, sempre grave em um caminho diferente.

## Exemplo completo e executável

Juntando todas as etapas, você obtém um programa autocontido que pode copiar, colar e executar.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Saída esperada** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Abra `output.xlsx` – a primeira tabela agora está sem as linhas que você removeu, enquanto a linha de cabeçalho permanece intacta.

## Perguntas comuns e variações

### Como excluir linhas de **todas** as tabelas em uma pasta de trabalho?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Posso excluir linhas com base em um **valor de célula**?

Sim. Verifique o `DataRange` em busca de células correspondentes, colete seus índices baseados em zero e, em seguida, exclua em ordem decrescente:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### E se eu precisar **preservar a formatação**?

`DeleteRows` remove a linha inteira da tabela, mas mantém o estilo da tabela para as linhas restantes. Se precisar manter formatação específica em uma linha que está sendo excluída, copie o estilo para outra linha antes da exclusão.

### Isso funciona com arquivos **.xls** (Excel 97‑2003)?

Sim. O Aspose.Cells detecta automaticamente o formato do arquivo, portanto o mesmo código funciona com `.xls`. Basta alterar a extensão do arquivo no construtor `Workbook`.

## Dicas de desempenho

* **Exclusões em lote:** Excluir muitas linhas uma a uma pode ser mais lento. Use uma única chamada `DeleteRows(start, count)` quando possível.  
* **Evite bloqueio da thread UI:** Se você integrar isso a um aplicativo desktop, execute a manipulação da pasta de trabalho em uma thread em segundo plano para manter a UI responsiva.  
* **Descarte adequado:** Embora o Aspose.Cells use memória gerenciada, envolva o `Workbook` em um bloco `using` se estiver lidando com arquivos grandes para liberar recursos prontamente.

## Conclusão

Agora você tem um exemplo completo e pronto para produção que **exclui linhas de tabela do Excel** usando C#. O guia abordou como **carregar pasta de trabalho Excel C#**, localizar o `ListObject` desejado, remover linhas com segurança e salvar o arquivo atualizado. Com o tratamento de casos extremos e as dicas de desempenho incluídas, você pode adaptar esse padrão a cenários mais complexos, como exclusões condicionais, múltiplas tabelas ou bibliotecas Excel .NET alternativas.

### Próximos passos

* Explore **ClosedXML** ou **EPPlus** se preferir um stack totalmente de código aberto.  
* Combine a exclusão de linhas com **validação de dados** para limpar planilhas antes de importá‑las para um banco de dados.  
* Automatize o processo para uma pasta de pastas de trabalho usando `Directory.GetFiles` e um loop.

Sinta‑se à vontade para experimentar diferentes intervalos de linhas, nomes de tabelas e lógica condicional. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Carregar arquivo Excel C# – Como excluir linhas e remover linhas específicas](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Como inserir e excluir linhas no Excel com Aspose.Cells para .NET: Um guia abrangente](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Como excluir linhas em branco no Excel usando Aspose.Cells .NET para limpeza de dados](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}