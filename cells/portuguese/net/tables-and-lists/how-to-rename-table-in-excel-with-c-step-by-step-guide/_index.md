---
category: general
date: 2026-08-11
description: Como renomear tabela no Excel com C# usando Aspose.Cells. Aprenda a criar
  uma pasta de trabalho Excel, adicionar intervalo nomeado e evitar conflitos de renomeação.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: pt
lastmod: 2026-08-11
og_description: Como renomear uma tabela no Excel com C# usando Aspose.Cells. Este
  guia mostra como criar uma pasta de trabalho do Excel, adicionar um intervalo nomeado
  e renomear com segurança uma tabela do Excel.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Como renomear tabela no Excel com C# – tutorial completo de programação
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: Como renomear tabela no Excel com C# – guia passo a passo
url: /pt/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como renomear tabela no Excel com C# – guia passo a passo

Se você precisa **renomear tabela** em um arquivo Excel programaticamente, este tutorial mostra a abordagem exata usando Aspose.Cells para .NET. Você verá como **criar uma pasta de trabalho Excel**, definir um **intervalo nomeado** e renomear uma tabela Excel existente sem causar um conflito de nomes.

A solução funciona para qualquer projeto .NET que tenha como alvo .NET 6 ou posterior e requer apenas o pacote NuGet Aspose.Cells. Ao final do guia você poderá renomear uma tabela Excel com segurança e entender por que um conflito pode surgir quando o nome de uma tabela coincide com um intervalo definido.

## Pré-requisitos

- .NET 6 SDK ou mais recente instalado  
- Visual Studio 2022 (ou qualquer IDE C#)  
- Pacote Aspose.Cells para .NET (`dotnet add package Aspose.Cells`)  

Não são necessárias assemblies adicionais de interop do Excel porque o Aspose.Cells funciona completamente na memória.

## Visão geral da solução

1. **Criar pasta de trabalho Excel** – instanciar um `Workbook` e adicionar alguns dados de exemplo.  
2. **Adicionar um intervalo nomeado** – usar `Worksheets.Names.Add` para criar um intervalo chamado `MyRange`.  
3. **Criar uma tabela Excel (ListObject)** – converter os dados em uma tabela para que tenhamos algo para renomear.  
4. **Renomear a tabela** – tentar definir a propriedade `Name` da tabela para o mesmo identificador do intervalo nomeado.  
5. **Tratar conflitos de nomes** – capturar a exceção, explicar por que ocorre e mostrar uma estratégia segura de renomeação.

Cada passo é explicado em detalhes abaixo.

## Etapa 1: Como criar pasta de trabalho Excel e preencher dados

Criar uma pasta de trabalho é a base para qualquer tarefa de automação Excel. A classe `Workbook` representa o arquivo inteiro na memória.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Por que isso importa:** A pasta de trabalho deve conter dados antes que você possa criar uma tabela. O Aspose.Cells armazena dados em uma coleção baseada em zero, portanto `Worksheets[0]` sempre se refere à primeira planilha.

## Etapa 2: Como adicionar intervalo nomeado à planilha

Um **intervalo nomeado** permite referir‑se a uma célula ou intervalo específico por um identificador amigável. Adicionar um intervalo é simples:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Por que isso importa:** Intervalos nomeados são armazenados na coleção global de nomes da pasta de trabalho. Se uma tabela posteriormente receber o mesmo nome, o Aspose.Cells lança uma `CellException` porque o Excel não permite nomes duplicados.

## Etapa 3: Como adicionar uma tabela Excel (ListObject)

Uma tabela fornece manipulação estruturada de dados, filtragem e estilização. No Aspose.Cells ela é chamada de **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Por que isso importa:** A tabela agora existe com o nome `InitialTable`. Renomeá‑la demonstra o processo de **como renomear tabela**.

## Etapa 4: Como renomear tabela Excel e tratar conflitos

Tentar renomear a tabela para `MyRange` entrará em conflito com o intervalo nomeado que criamos anteriormente. O código a seguir mostra o padrão adequado para detectar e resolver o conflito.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### O que o código faz

| Etapa | Ação | Razão |
|------|--------|--------|
| **Tentar renomear** | `table.Name = "MyRange"` | Demonstrar o cenário de conflito. |
| **Capturar exceção** | Imprime a mensagem de conflito. | Fornece feedback imediato sobre o problema. |
| **Gerar nome seguro** | `GetUniqueTableName` adiciona um sufixo numérico até que o nome esteja livre. | Garante que o novo nome da tabela **não** colida com nenhum intervalo nomeado ou tabela existente. |
| **Salvar pasta de trabalho** | `workbook.Save("RenamedTable.xlsx")` | Persiste as alterações para que você possa abrir o arquivo no Excel e verificar o resultado. |

**Saída esperada** ao executar o programa:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Abrindo `RenamedTable.xlsx` mostra uma tabela chamada `MyRange_1` e um intervalo nomeado separado `MyRange` apontando para a célula A1.

## Por que o conflito ocorre e melhores práticas para renomear tabela Excel

- O Excel armazena **intervalos nomeados** e **nomes de tabelas** no mesmo namespace.  
- Quando você tenta atribuir um nome de tabela que já existe como intervalo, o Aspose.Cells lança uma `CellException`.  
- A abordagem recomendada é **verificar nomes existentes primeiro** (conforme mostrado em `NameExists`) ou usar uma convenção de nomenclatura que garanta unicidade (por exemplo, prefixar tabelas com `tbl_`).  

Aplicar este padrão evita erros em tempo de execução e torna sua automação robusta.

## Dicas adicionais para trabalhar com Aspose.Cells

- **Dica profissional:** Use `Workbook.Worksheets.Names.Remove("MyRange")` se você quiser substituir intencionalmente o intervalo por um nome de tabela.  
- **Cuidado com sensibilidade a maiúsculas/minúsculas:** O Excel trata nomes de forma case‑insensitive; os métodos auxiliares usam `OrdinalIgnoreCase` para emular o comportamento do Excel.  
- **Desempenho:** Se você estiver processando muitas planilhas, faça cache da coleção de nomes em vez de iterar repetidamente.

## Exemplo completo em um bloco

Abaixo está o programa completo que você pode copiar‑colar em um projeto de console. Ele inclui todas as etapas, desde a criação da pasta de trabalho até a renomeação segura da tabela.



## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como criar intervalos nomeados com escopo de pasta de trabalho no Excel usando Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Como implementar fórmulas de intervalo nomeado em .NET usando Aspose.Cells para automação Excel](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Como adicionar segmentações a tabelas Excel usando Aspose.Cells para .NET: Um guia abrangente](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}