---
category: general
date: 2026-07-13
description: Crie uma pasta de trabalho do Excel em C# e aprenda como adicionar intervalo
  nomeado, atribuir nome a uma tabela e lidar com conflitos de nomes — tudo em um
  exemplo claro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: pt
lastmod: 2026-07-13
og_description: Crie uma pasta de trabalho Excel em C# com Aspose.Cells. Aprenda como
  adicionar intervalo nomeado, definir o nome da tabela e resolver conflitos de nomenclatura
  em um guia conciso e executável.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Criar pasta de trabalho Excel em C# – Adicionar intervalo nomeado e definir
  nome da tabela
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Criar Pasta de Trabalho do Excel em C# – Adicionar Intervalo Nomeado e Definir
  Nome da Tabela
url: /pt/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Pasta de Trabalho Excel em C# – Guia Completo para Adicionar Intervalos Nomeados e Definir Nomes de Tabelas

Já precisou **criar uma pasta de trabalho Excel** do zero e se perguntou onde colocar um intervalo nomeado ou como dar a uma tabela seu próprio identificador? Você não está sozinho. Em muitos cenários de relatórios ou exportação de dados, você se verá lidando com intervalos, tabelas e o ocasional conflito de nomes.  

Neste tutorial vamos percorrer um exemplo totalmente executável que **cria uma pasta de trabalho Excel**, **adiciona um intervalo nomeado**, e então **atribui um nome a uma tabela**—mostrando exatamente o que fazer quando os nomes colidem. Ao final, você saberá o “como” e o “porquê” de cada passo, além de algumas dicas para manter seu código limpo.

> **Quick win:** O código usa a biblioteca **Aspose.Cells**, que funciona com .NET 6+ e não requer instalação do Excel no servidor.

---

## O que você precisará

- **.NET 6 SDK** (ou qualquer versão recente do .NET)  
- **Aspose.Cells for .NET** pacote NuGet  
- Uma IDE decente (Visual Studio, Rider ou VS Code)  
- Conhecimento básico de C#—nada de extravagante, apenas as declarações `using` habituais

Se você tem tudo isso, podemos ir direto ao processo de **create excel workbook**.

---

## ## Create Excel Workbook – Visão Geral Passo a Passo

Abaixo está o programa completo, pronto para copiar e colar. Ele demonstra tudo, desde a criação da pasta de trabalho até o tratamento de um conflito de nomes quando você tenta **assign name to table**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Expected output** ao executar o programa:

```
Naming conflict detected:
A name with the same text already exists.
```

E se você abrir *DemoWorkbook.xlsx* verá uma tabela chamada **Table1** e um intervalo nomeado chamado **MyRange**—exatamente o que pretendíamos, sem o conflito.

---

## ## Add Named Range – Por que é Importante

Um **named range** é essencialmente um alias para um bloco de células. Em vez de referir‑se constantemente a `A1:B5`, você pode escrever `MyRange` em fórmulas, validações de dados ou até no código. Isso melhora a legibilidade e reduz a chance de erros de digitação.

No trecho acima chamamos:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- O primeiro argumento é o **name** que você usará depois.  
- O segundo argumento é o **address** (relativo à planilha).  

Se precisar **how to add range** dinamicamente, pode montar a string de endereço com `Cell.GetRefersTo()` ou usar `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Assign Name to Table – Tratando Conflitos

Tabelas (também chamadas *list objects*) já possuem uma propriedade de nome incorporada. Por padrão, Aspose.Cells as nomeia `Table1`, `Table2`, etc. Quando você tenta dar a uma tabela o mesmo identificador de um intervalo nomeado existente, a biblioteca lança uma exceção—exatamente como o Excel faz.

Por que isso acontece?

- O escopo de nomes do Excel é **workbook‑wide** tanto para intervalos quanto para tabelas.  
- Nomes duplicados deixariam as fórmulas ambíguas, então o motor bloqueia isso.

### Pro tip

Se realmente precisar que uma tabela compartilhe um nome lógico com um intervalo, considere **prefixar** um deles, por exemplo:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Ou renomear o intervalo primeiro:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Ambas as abordagens mantêm o espaço de nomes organizado e evitam erros em tempo de execução.

---

## ## Set Table Name – Boas Práticas

Ao **set table name** programaticamente, tenha em mente estas diretrizes:

1. **Use um prefixo consistente** (`tbl_`, `rng_`, etc.) – ele indica instantaneamente que tipo de objeto é.
2. **Fique dentro de 255 caracteres** – limite do Excel para nomes.
3. **Evite espaços e caracteres especiais** – apenas letras, números e underscores são seguros.
4. **Valide antes de atribuir** – uma verificação rápida `if (!sheet.Names.Contains(name))` impede o conflito que demonstramos.

Aqui está um método auxiliar que você pode inserir em qualquer projeto:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Chamar `SafeSetTableName(sheet, table, "MyRange")` transformará automaticamente `MyRange` em `MyRange_1` caso exista um conflito, garantindo que a operação **create excel workbook** nunca abortará inesperadamente.

---

## ## Full Working Example – Juntando Tudo

Abaixo está uma versão compacta que você pode copiar direto para um aplicativo console. Ela inclui a rotina de segurança e demonstra o fluxo completo de ponta a ponta.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Executar este script gera `FinalDemo.xlsx` onde a tabela se chama `MyRange_1` (ou outro sufixo único) e o intervalo permanece `MyRange`. Sem exceção, sem mistério—apenas nomes limpos e determinísticos.

---

## ## Perguntas Frequentes (FAQ)

**Q: Posso adicionar um intervalo nomeado que abranja várias planilhas?**  
A: Sim, mas você deve qualificar o endereço com o nome da planilha, por exemplo, `"Sheet1!A1:B5"`. O método `Names.Add` aceita esse formato.

**Q: O Aspose.Cells suporta intervalos nomeados dinâmicos (como fórmulas OFFSET)?**  
A: Absolutamente. Você pode passar uma string de fórmula em vez de um endereço estático, como `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: O que fazer se eu precisar renomear uma tabela existente?**  
A: Basta definir `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}