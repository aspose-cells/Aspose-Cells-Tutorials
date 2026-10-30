---
category: general
date: 2026-08-07
description: Exclua linhas de uma tabela do Excel usando C#. Aprenda a remover linhas
  de dados do Excel com segurança, protegendo a linha de cabeçalho, em apenas alguns
  passos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- remove data rows excel
- protect header row excel
language: pt
lastmod: 2026-08-07
og_description: Excluir linhas de uma tabela do Excel programaticamente. Este guia
  mostra como remover linhas de dados do Excel com segurança e proteger a linha de
  cabeçalho do Excel com Aspose.Cells.
og_image_alt: Screenshot of C# code that deletes rows from an Excel table while keeping
  the header intact
og_title: Excluir linhas de tabela do Excel – solução rápida em C#
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  headline: Delete rows from Excel table – complete C# guide
  type: TechArticle
- description: Delete rows from Excel table using C#. Learn how to remove data rows
    Excel safely while protecting header row Excel in just a few steps.
  name: Delete rows from Excel table – complete C# guide
  steps:
  - name: Run the program with a sample workbook that has at least five data rows.
    text: Run the program with a sample workbook that has at least five data rows.
  - name: Verify that the console prints “Rows deleted and workbook saved successfully.”
    text: Verify that the console prints “Rows deleted and workbook saved successfully.”
  - name: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
    text: 'Open `TableHeaderProtected.xlsx` in Excel and confirm:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Data manipulation
title: Excluir linhas de tabela do Excel – guia completo de C#
url: /pt/net/row-and-column-management/delete-rows-from-excel-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excluir linhas de tabela do Excel – guia completo em C#

Se você precisa **excluir linhas de tabela do Excel** em um projeto .NET, este tutorial mostra uma maneira confiável de fazer isso. Seja limpando dados importados ou reduzindo um relatório, você verá como remover linhas de dados do Excel enquanto a API protege automaticamente **protect header row excel** contra exclusão acidental.

Nas etapas abaixo, você aprenderá como carregar uma pasta de trabalho, excluir linhas com segurança e, finalmente, salvar as alterações. O guia também aborda o erro comum de tentar excluir a linha de cabeçalho e explica por que a biblioteca a impede. Ao final, você poderá **remove data rows excel** com confiança em qualquer solução baseada em Aspose.Cells.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- .NET 6.0 ou superior instalado.
- O pacote NuGet **Aspose.Cells for .NET** (versão 23.10 ou mais recente). Instale‑o com:

  ```bash
  dotnet add package Aspose.Cells
  ```

- Um arquivo Excel (`TableWithHeader.xlsx`) que contém uma tabela estruturada com uma linha de cabeçalho na primeira planilha.
- Familiaridade básica com C# e Visual Studio (ou qualquer IDE de sua preferência).

## Etapa 1: Carregar a pasta de trabalho que contém uma tabela com linha de cabeçalho

A primeira operação é abrir a pasta de trabalho que contém a tabela que você deseja modificar. Aspose.Cells lê o arquivo na memória sem exigir que o Excel esteja instalado.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the workbook from disk
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\TableWithHeader.xlsx");

        // Continue with the next steps...
```

**Por que isso importa:** Carregar a pasta de trabalho cria um objeto `Workbook` que lhe dá acesso a planilhas, tabelas e células. Sem esse objeto, você não pode manipular a estrutura do Excel.

## Etapa 2: Acessar a primeira planilha e sua primeira tabela

A maioria dos exemplos simples mantém a tabela na primeira planilha e no índice 0, mas você pode ajustar os índices conforme seu cenário.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (Excel table) on that worksheet
        ListObject table = worksheet.Tables[0];
```

**Por que isso importa:** `ListObject` representa uma tabela do Excel, que inclui a linha de cabeçalho, linhas de dados e qualquer formatação. Trabalhar com o objeto de tabela garante que você respeite a semântica das tabelas do Excel, como a proteção da linha de cabeçalho.

## Etapa 3: Tentar excluir a linha de cabeçalho (demonstrando a proteção)

Aspose.Cells lança uma exceção se você tentar excluir a linha de cabeçalho porque a API **protect header row excel** por design. Mostrar esse comportamento ajuda a entender por que uma exclusão direta falha.

```csharp
        try
        {
            // Attempt to delete the header row (index 0) and the row below it
            table.DeleteRows(0, 2);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Deletion prevented: " + ex.Message);
        }
```

**Saída esperada**

```
Deletion prevented: Cannot delete the header row of a table.
```

**Explicação:** O método `DeleteRows` recebe um índice inicial baseado em zero e uma contagem. O índice 0 aponta para a linha de cabeçalho, que a biblioteca protege para manter a estrutura da tabela intacta.

## Etapa 4: Excluir apenas linhas de dados – a forma correta de **remove data rows excel**

Agora que você sabe que o cabeçalho está protegido, exclua apenas as linhas de dados que começam após o cabeçalho. Na maioria das tabelas, a primeira linha de dados está no índice 1.

```csharp
        // Delete three data rows starting after the header (index 1)
        table.DeleteRows(1, 3); // removes rows 2, 3, and 4 of the worksheet

        // Optionally, you can delete a single row:
        // table.DeleteRows(4, 1);
```

**Por que isso funciona:** Ao iniciar no índice 1 você ignora o cabeçalho, de modo que a operação cumpre a regra **protect header row excel**. O método `DeleteRows` atualiza automaticamente o intervalo interno da tabela.

## Etapa 5: Salvar a pasta de trabalho modificada

Persista as alterações em um novo arquivo para manter o original intacto.

```csharp
        // Save the workbook with the modified table
        workbook.Save(@"YOUR_DIRECTORY\TableHeaderProtected.xlsx");

        Console.WriteLine("Rows deleted and workbook saved successfully.");
    }
}
```

**Resultado:** Após executar o programa, `TableHeaderProtected.xlsx` contém a mesma linha de cabeçalho, mas as linhas de dados especificadas foram removidas. Abrir o arquivo no Excel mostra uma tabela limpa sem as linhas excluídas.

## Armadilhas comuns e como evitá‑las

| Armadilha | Por que acontece | Solução |
|-----------|------------------|---------|
| Tentar excluir a linha de cabeçalho | Aspose.Cells impõe a integridade da tabela | Sempre inicie a exclusão no índice 1 ou superior |
| Excluir mais linhas do que existem | `DeleteRows` lança `ArgumentOutOfRangeException` | Verifique `table.DataRange.RowCount` antes de chamar `DeleteRows` |
| Trabalhar com um intervalo que não é tabela | Métodos de `ListObject` se aplicam apenas a tabelas estruturadas | Converta o intervalo em tabela primeiro (`worksheet.Tables.Add`) se necessário |

**Dica profissional:** Se precisar limpar a tabela inteira, mas manter o cabeçalho, use `table.DeleteRows(1, table.DataRange.RowCount - 1);`. Isso remove todas as linhas de dados, independentemente de quantas linhas a tabela possua no momento.

## Alternativa: Excluir linhas por endereço de célula

Às vezes você pode conhecer o endereço exato da célula em vez do índice da linha. É possível traduzir um endereço para um índice de linha usando a coleção `Cells`:

```csharp
        // Example: delete rows that contain the value "Obsolete"
        for (int i = table.DataRange.FirstRow; i <= table.DataRange.LastRow; i++)
        {
            if (worksheet.Cells[i, table.DataRange.FirstColumn].StringValue == "Obsolete")
            {
                // Subtract one because DeleteRows expects a zero‑based index relative to the table
                table.DeleteRows(i - table.StartRow + 1, 1);
                i--; // Adjust loop counter after deletion
            }
        }
```

Essa abordagem é útil quando as linhas a remover são identificadas pelo conteúdo e não por uma contagem fixa.

## Testando sua implementação

1. Execute o programa com uma pasta de trabalho de exemplo que tenha ao menos cinco linhas de dados.  
2. Verifique se o console imprime “Rows deleted and workbook saved successfully.”  
3. Abra `TableHeaderProtected.xlsx` no Excel e confirme:  
   - A linha de cabeçalho ainda está presente.  
   - Apenas as linhas de dados pretendidas foram removidas.

Se o cabeçalho desaparecer, provavelmente você iniciou a exclusão no índice 0 — revise a **Etapa 4**.

## Conclusão

Agora você sabe como **excluir linhas de tabela do Excel** com segurança usando C#. O guia abordou carregar uma pasta de trabalho, acessar a tabela, respeitar a regra **protect header row excel**, excluir corretamente **remove data rows excel** e salvar o resultado. Seguindo essas etapas, você evita erros comuns e mantém suas tabelas do Excel bem estruturadas.

### Próximos passos

- Explore recursos do **Aspose.Cells** como inserção de linhas, aplicação de estilos ou filtragem de dados.  
- Combine a exclusão de linhas com **fórmulas do Excel** para automatizar a limpeza com base em resultados de cálculo.  
- Consulte tópicos relacionados, como **exportar Excel para CSV** ou **ler pastas de trabalho grandes de forma eficiente**.

Sinta‑se à vontade para experimentar diferentes contagens de linhas, múltiplas tabelas ou exclusões condicionais. Se encontrar casos extremos, volte à manipulação de erros mostrada na **Etapa 3** — a biblioteca sempre protegerá a linha de cabeçalho para você. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Delete Multiple Rows in Excel with Aspose.Cells .NET: A Comprehensive Guide for Data Manipulation](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}