---
category: general
date: 2026-10-01
description: Aprenda a excluir linhas de uma tabela do Excel e a alterar o nome da
  tabela do Excel usando C#. Guia passo a passo com código completo e melhores práticas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: pt
lastmod: 2026-10-01
og_description: Exclua linhas de uma tabela do Excel e altere o nome da tabela do
  Excel em C#. Siga este tutorial completo para carregar uma pasta de trabalho, modificar
  a tabela e salvar o resultado.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Excluir linhas de uma tabela Excel e alterar seu nome em C# – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Como excluir linhas de uma tabela do Excel e alterar seu nome em C#
url: /pt/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como excluir linhas de uma tabela do Excel e alterar seu nome em C#

Se você precisa **excluir linhas de uma tabela do Excel** ao trabalhar com C#, este guia mostra as etapas exatas necessárias. Você verá como **carregar uma pasta de trabalho do Excel em C#**, remover linhas específicas de uma tabela e, em seguida, **atualizar o nome da tabela do Excel** para que o arquivo permaneça consistente.

O tutorial cobre tudo o que você precisa saber: pacotes NuGet necessários, código completo executável e armadilhas comuns, como violações da estrutura da tabela. Ao final do artigo, você poderá modificar qualquer tabela do Excel programaticamente sem intervenção manual.

## Pré-requisitos

Antes de começar, certifique-se de que você tem:

* .NET 6.0 SDK ou posterior instalado.  
* Visual Studio 2022 (ou qualquer IDE C#) configurado para desenvolvimento .NET.  
* A biblioteca **Aspose.Cells for .NET** adicionada via NuGet (`Install-Package Aspose.Cells`).  
* Uma pasta de trabalho do Excel existente (`Table.xlsx`) que contém ao menos uma planilha com uma tabela.  

Esses itens fornecem o ambiente necessário para **carregar a pasta de trabalho do Excel c#** e executar as operações de forma confiável.

## Etapa 1: Carregar a pasta de trabalho que contém a tabela

A primeira operação é abrir o arquivo da pasta de trabalho. Aspose.Cells lê toda a pasta de trabalho na memória, dando a você controle total sobre planilhas, tabelas e dados das células.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Por que isso importa*: Carregar a pasta de trabalho é a base para qualquer manipulação subsequente de tabelas. O objeto `Workbook` expõe a coleção `Worksheets`, que você usará para localizar a tabela alvo.

## Etapa 2: Acessar a primeira planilha e sua primeira tabela

A maioria dos arquivos Excel armazena tabelas na primeira planilha, mas você pode ajustar o índice se necessário. O código a seguir recupera o primeiro objeto `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Se a planilha não contiver uma tabela, `sheet.Tables.Count` será zero e você deverá tratar esse caso. Tentar acessar `sheet.Tables[0]` quando não houver tabelas gera uma exceção, por isso uma cláusula de proteção é recomendada em código de produção.

## Etapa 3: Excluir linhas da tabela do Excel

Para **remover linhas de uma tabela do Excel**, chame `DeleteRows(startRow, totalRows)`. O parâmetro `startRow` é baseado em zero em relação à primeira linha de dados da tabela (a linha após o cabeçalho).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Por que usar `DeleteRows` em vez de excluir linhas da planilha?

`DeleteRows` atualiza o intervalo interno da tabela, preservando fórmulas, estilos e nomes definidos que pertencem à tabela. Excluir diretamente linhas da planilha pode quebrar a estrutura da tabela e gerar uma exceção.

**Caso extremo**: Se a exclusão deixar a tabela sem linhas de dados, Aspose.Cells lança uma `ArgumentException`. Proteja-se verificando `table.RowCount` antes da exclusão.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Etapa 4: Alterar o nome da tabela do Excel

Depois que as linhas forem removidas, você pode querer dar à tabela um identificador mais descritivo. A propriedade `Name` define o nome definido da tabela, que é usado em fórmulas e VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Por que renomear?* Um nome de tabela claro melhora a legibilidade nas fórmulas (`=SUM(SalesData2026[Amount])`) e evita colisões de nomes quando várias tabelas compartilham propósitos semelhantes.

## Etapa 5: Salvar a pasta de trabalho modificada (opcional)

Persistir as alterações salvando em um novo arquivo ou sobrescrevendo o original. Salvar em um novo local é mais seguro durante o desenvolvimento.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

O método `Save` grava a pasta de trabalho atualizada, incluindo o intervalo da tabela alterado e o novo nome da tabela, no disco.

## Exemplo completo em funcionamento

Juntando todas as etapas, obtém-se um programa autônomo que você pode executar imediatamente.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Saída esperada** (supondo que o arquivo e a tabela existam):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Executar o programa atualiza o arquivo Excel exatamente como descrito: as linhas são removidas, o nome da tabela é alterado e o resultado é salvo sem edição manual.

## Perguntas comuns e solução de problemas

| Pergunta | Resposta |
|----------|----------|
| *O que acontece se a tabela abranger células mescladas?* | `DeleteRows` respeita intervalos mesclados. Se uma célula mesclada atravessar o limite da exclusão, Aspose.Cells ajusta automaticamente a mesclagem. Verifique o resultado visualmente se você depender de mesclagens complexas. |
| *Posso excluir linhas de uma tabela que faz parte de um cache de tabela dinâmica?* | Excluir linhas de uma tabela de origem que alimenta uma tabela dinâmica **não** atualiza automaticamente o cache da tabela dinâmica. Chame `pivotTable.RefreshData()` após modificar a tabela de origem. |
| *É possível excluir linhas com base em uma condição (por exemplo, valor < 0)?* | Sim. Percorra `table.ListObjects` ou `table.Rows` para localizar as linhas correspondentes, então colecione seus índices e chame `DeleteRows` para cada intervalo. |
| *Preciso descartar o objeto `Workbook`?* | `Workbook` implementa `IDisposable`. Envolva-o em um bloco `using` para liberação determinística de recursos, especialmente ao processar arquivos grandes. |
| *Como isso difere de usar EPPlus?* | EPPlus também suporta manipulação de tabelas, mas usa uma API diferente (`ExcelTable`). Os conceitos de carregar uma pasta de trabalho, excluir linhas e renomear a tabela são análogos. Escolha a biblioteca que corresponde aos seus requisitos de licenciamento. |

## Melhores práticas ao modificar tabelas do Excel em C#

* **Validar índices** – Os índices de linhas da tabela são baseados em zero; erros de deslocamento causam exclusões inesperadas.  
* **Verificar colisões de nomes** – O Excel não permite nomes definidos duplicados; sempre verifique a unicidade antes de atribuir um novo nome.  
* **Fazer backup dos arquivos originais** – Scripts automatizados podem corromper dados; mantenha uma cópia da pasta de trabalho fonte.  
* **Usar declarações `using`** – Garante que os manipuladores de arquivos sejam liberados prontamente:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Testar com casos extremos** – Tabelas com uma única linha de dados, tabelas que ocupam toda a planilha e tabelas vinculadas a gráficos devem ser verificadas após as alterações.

## Conclusão

Agora você sabe como **excluir linhas de uma tabela do Excel** e **alterar o nome da tabela do Excel** usando C#. A solução completa carrega a pasta de trabalho, acessa a tabela alvo, remove as linhas desejadas, renomeia a tabela e salva o resultado. Aplique essas técnicas para automatizar a geração de relatórios, limpeza de dados ou qualquer fluxo de trabalho que exija gerenciamento programático de tabelas do Excel.

Em seguida, explore tópicos relacionados, como **atualizar valores de células em uma tabela do Excel**, **adicionar novas linhas programaticamente** e **exportar dados da tabela para CSV**. Dominar essas operações lhe dará controle total sobre arquivos Excel a partir de suas aplicações C#.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completo em funcionamento com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como renomear tabela no Excel com C# – Guia passo a passo](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Criar tabela Excel em C# – Guia passo a passo](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Obter a primeira tabela de uma pasta de trabalho Excel em C# – Guia completo](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}