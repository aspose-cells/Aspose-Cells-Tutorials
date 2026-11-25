---
category: general
date: 2026-11-25
description: Aprenda como excluir linhas de uma tabela do Excel em C# e também excluir
  várias linhas de uma planilha do Excel de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: pt
lastmod: 2026-11-25
og_description: Exclua linhas de uma tabela do Excel em C# e aprenda a excluir várias
  linhas de uma planilha do Excel com código limpo.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Excluir linhas de tabela do Excel em C# – guia completo
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: Como excluir linhas de uma tabela do Excel com C#
url: /pt/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como excluir linhas de uma tabela do Excel com C#

Se você precisa excluir linhas de uma tabela do Excel usando C#, este guia mostra exatamente como fazer isso. Você também verá como excluir várias linhas de uma planilha do Excel sem afetar outros dados.

Trabalhar com o Excel programaticamente frequentemente requer a remoção de registros desatualizados ou inválidos. Excluir linhas diretamente em uma planilha pode ser arriscado porque a linha de cabeçalho de uma tabela estruturada deve permanecer intacta. Este tutorial orienta você por uma abordagem segura que respeita o cabeçalho da tabela e permite excluir qualquer número de linhas de dados em uma única chamada.

## Pré-requisitos

* .NET 6.0 ou posterior instalado  
* Visual Studio 2022 (ou qualquer IDE compatível)  
* O pacote NuGet **Aspose.Cells** (versão 23.10 ou mais recente) – esta biblioteca fornece as classes `Workbook`, `Worksheet` e `ListObject` usadas nos exemplos  

Você não precisa do Microsoft Office instalado na máquina de desenvolvimento porque o Aspose.Cells trabalha diretamente com o formato de arquivo.

## Excluir linhas de uma tabela do Excel – passo a passo

As seções a seguir descrevem cada passo necessário para excluir linhas de uma tabela do Excel com segurança. A palavra‑chave principal aparece neste título para atender aos requisitos de SEO.

### Etapa 1: Adicionar Aspose.Cells ao seu projeto

Abra o **Package Manager Console** e execute:

```powershell
Install-Package Aspose.Cells
```

O pacote adiciona os assemblies necessários e resolve os tipos `Workbook`, `Worksheet` e `ListObject`.

### Etapa 2: Carregar a pasta de trabalho e localizar a tabela

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Por que isso importa*: O `ListObject` representa uma verdadeira tabela do Excel, que mantém sua própria linha de cabeçalho. Ao trabalhar com o `ListObject`, você evita a remoção acidental do cabeçalho.

### Etapa 3: Excluir as linhas de dados desejadas

O método `DeleteRows` espera um índice de linha **baseado em zero** relativo à tabela, **incluindo** a linha de cabeçalho. Como o cabeçalho não pode ser removido, você deve iniciar no índice 1 para a primeira linha de dados.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

Se você tentar `table.DeleteRows(0, 2)`, o Aspose.Cells lançará uma exceção porque a linha de cabeçalho (índice 0) está protegida. Começar no índice 1 garante que apenas linhas de dados sejam removidas.

### Etapa 4: Salvar a pasta de trabalho modificada

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Executar o programa remove as duas linhas imediatamente abaixo do cabeçalho, mantendo a estrutura da tabela intacta.

### Exemplo completo em funcionamento

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Saída esperada**: O arquivo `table_with_header_modified.xlsx` contém o cabeçalho original da tabela, seguido por todas as linhas, exceto as duas que foram removidas. Nenhuma outra planilha é alterada.

## Excluir várias linhas de uma planilha do Excel

Às vezes você precisa excluir linhas que **não** fazem parte de uma tabela estruturada. A palavra‑chave secundária aparece neste título. A abordagem difere ligeiramente porque você trabalha com a coleção `Rows` da planilha em vez de um `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Por que isso funciona**: `Rows.RemoveAt(startIndex, count)` remove um bloco contíguo de linhas diretamente da planilha. Não há proteção de cabeçalho, portanto você pode iniciar em qualquer índice. O método é eficiente porque atualiza as estruturas de dados internas em uma única operação, o que é ideal quando você precisa excluir várias linhas de uma planilha do Excel.

### Casos de borda e boas práticas

| Situação                               | Tratamento recomendado |
|----------------------------------------|------------------------|
| Excluir linhas além da última linha   | Verifique `worksheet.Rows.Count` antes de chamar `RemoveAt`. |
| Remover todas as linhas, exceto o cabeçalho | Exclua linhas de dados em um loop ou use `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Preservar formatação de células        | A exclusão via `ListObject` desloca automaticamente a formatação; para planilhas brutas, copie a formatação antes da remoção, se necessário. |
| Planilhas grandes ( > 10 000 linhas)   | Execute exclusões em ordem decrescente para evitar deslocamento de índices, ou use `DeleteRows` na tabela, se possível. |

**Dica profissional**: Quando precisar excluir linhas com base em uma condição (por exemplo, linhas onde o valor de uma coluna está vazio), itere o `DataRange` da tabela de trás para frente e chame `DeleteRows` para cada linha correspondente. Excluir de trás para frente evita desalinhamento de índices.

## Perguntas comuns

*Isso funciona com arquivos .xlsx criados pelo Excel 365?*  
Sim. O Aspose.Cells suporta a especificação completa do Office Open XML, portanto o mesmo código funciona para qualquer arquivo `.xlsx` moderno.

*E se a pasta de trabalho contiver várias tabelas?*  
Recupere a tabela desejada pelo nome: `var table = worksheet.ListObjects["MyTable"];` então aplique `DeleteRows` conforme mostrado.

*Posso excluir linhas sem usar uma biblioteca de terceiros?*  
Você poderia usar o COM interop Microsoft.Office.Interop.Excel, mas isso requer que o Excel esteja instalado no servidor e introduz overhead relacionado ao COM. O Aspose.Cells oferece uma alternativa leve e segura para servidores.

## Conclusão

Agora você sabe como excluir linhas de uma tabela do Excel com segurança e como excluir várias linhas de uma planilha do Excel usando C#. A técnica principal baseia‑se no método `ListObject.DeleteRows`, que respeita o cabeçalho da tabela, enquanto a técnica secundária usa `Rows.RemoveAt` para planilhas simples. Aplique esses padrões para limpar dados, automatizar a geração de relatórios ou implementar recursos de edição em massa em suas aplicações.

**Próximos passos**

* Explore outros recursos do Aspose.Cells, como inserir linhas, copiar estilos ou filtrar dados.  
* Experimente as mesmas operações com **ClosedXML** se preferir uma biblioteca de código aberto; a API é semelhante, mas usa `IXLTable` e `IXLRows`.  
* Combine a lógica de exclusão de linhas com consultas LINQ para criar pipelines de limpeza de dados mais complexos.  

Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [como excluir linhas no Excel com C# – proteger cabeçalho da tabela](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [Como usar Aspose.Cells para excluir linhas em uma tabela do Excel mantendo o](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Carregar arquivo Excel C# – Como excluir linhas e remover linhas específicas](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}