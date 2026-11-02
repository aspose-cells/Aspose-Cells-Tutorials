---
category: general
date: 2026-07-13
description: Skapa Excel-arbetsbok i C# och lär dig hur du lägger till ett namngivet
  område, tilldelar namn till en tabell och hanterar namnkrockar – allt i ett tydligt
  exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: sv
lastmod: 2026-07-13
og_description: Skapa Excel-arbetsbok i C# med Aspose.Cells. Lär dig hur du lägger
  till namngivet område, sätter tabellnamn och löser namnkonflikter i en kortfattad,
  körbar guide.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Skapa Excel-arbetsbok i C# – Lägg till namngivet område och ange tabellnamn
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
title: Skapa Excel-arbetsbok i C# – Lägg till namngivet område och sätt tabellnamn
url: /sv/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel-arbetsbok i C# – Komplett guide för att lägga till namngivna områden och sätta tabellnamn

Har du någonsin behövt **create Excel workbook** från grunden och undrat var du ska placera ett namngivet område eller hur du ger en tabell sin egen identifierare? Du är inte ensam. I många rapporterings- eller data‑export‑scenarier kommer du att jonglera med områden, tabeller och ibland namnkonflikter.  

I den här handledningen går vi igenom ett fullt körbart exempel som **creates an Excel workbook**, **adds a named range**, och sedan **assigns a name to a table** — som visar exakt vad du ska göra när namnen kolliderar. I slutet vet du “hur” och “varför” bakom varje steg, samt några tips för att hålla din kod ren.

> **Quick win:** Koden använder **Aspose.Cells**‑biblioteket, som fungerar med .NET 6+ och kräver ingen Excel‑installation på servern.

---

## Vad du behöver

- **.NET 6 SDK** (eller någon nyare .NET‑version)  
- **Aspose.Cells for .NET** NuGet‑paket  
- En bra IDE (Visual Studio, Rider eller VS Code)  
- Grundläggande C#‑kunskaper — inget avancerat, bara de vanliga `using`‑satserna

Om du har dem kan vi hoppa rakt in i **create excel workbook**‑processen.

---

## ## Create Excel Workbook – Step‑by‑Step Overview

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet. Det demonstrerar allt från arbetsboks‑skapande till hantering av en namnkonflikt när du försöker **assign name to table**.

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

**Förväntad output** när du kör programmet:

```
Naming conflict detected:
A name with the same text already exists.
```

Och om du öppnar *DemoWorkbook.xlsx* ser du en tabell med namnet **Table1** och ett namngivet område som heter **MyRange** — exakt vad vi avsåg, utan konflikten.

---

## ## Lägg till namngivet område – varför det är viktigt

Ett **named range** är i princip ett alias för ett cellblock. Istället för att ständigt referera till `A1:B5` kan du skriva `MyRange` i formler, datavalideringar eller till och med i kod. Detta förbättrar läsbarheten och minskar risken för fel relaterade till stavfel.

I kodsnutten ovan anropar vi:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Det första argumentet är **name** du kommer att använda senare.  
- Det andra argumentet är **address** (relativt till kalkylbladet).  

Om du någonsin behöver **how to add range** dynamiskt, kan du bygga adresssträngen med `Cell.GetRefersTo()` eller använda `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Tilldela namn till tabell – hantera konflikter

Tabeller (även kallade *list objects*) har redan en inbyggd namn‑egenskap. Som standard namnger Aspose.Cells dem `Table1`, `Table2` osv. När du försöker ge en tabell samma identifierare som ett befintligt namngivet område kastar biblioteket ett undantag — precis som Excel gör.

Varför händer detta?

- Excels namnutrymme är **workbook‑wide** för både områden och tabeller.  
- Duplicerade namn skulle göra formler tvetydiga, så motorn blockerar det.

### Pro tip

Om du verkligen behöver att en tabell delar ett logiskt namn med ett område, överväg att **prefixa** en av dem, t.ex.:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Eller byt namn på området först:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Båda tillvägagångssätten håller namnrymden prydlig och undviker körningsfel.

---

## ## Sätt tabellnamn – bästa praxis

När du **set table name** programatiskt, ha dessa riktlinjer i åtanke:

1. **Use a consistent prefix** (`tbl_`, `rng_`, etc.) – det visar omedelbart vad objektet är.  
2. **Stay within 255 characters** – Excels gräns för namn.  
3. **Avoid spaces and special characters** – endast bokstäver, siffror och understreck är säkra.  
4. **Validate before assigning** – en snabb `if (!sheet.Names.Contains(name))`‑kontroll förhindrar den konflikt vi demonstrerade.  

Här är en hjälpfunktion du kan lägga in i vilket projekt som helst:

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

Att anropa `SafeSetTableName(sheet, table, "MyRange")` kommer automatiskt att omvandla `MyRange` till `MyRange_1` om en konflikt finns, vilket säkerställer att **create excel workbook**‑operationen aldrig avbryts oväntat.

---

## ## Fullt fungerande exempel – sätt ihop allt

Nedan är en kompakt version som du kan kopiera rakt in i en konsolapp. Den innehåller säkerhetsrutinen och demonstrerar hela flödet från början till slut.

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

Att köra detta skript producerar `FinalDemo.xlsx` där tabellen heter `MyRange_1` (eller ett annat unikt suffix) och området förblir `MyRange`. Inget undantag, ingen gåta — bara ren, deterministisk namngivning.

---

## ## Vanliga frågor (FAQ)

**Q: Kan jag lägga till ett namngivet område som sträcker sig över flera kalkylblad?**  
A: Ja, men du måste kvalificera adressen med bladnamnet, t.ex. `"Sheet1!A1:B5"`. Metoden `Names.Add` accepterar det formatet.

**Q: Stöder Aspose.Cells dynamiska namngivna områden (som OFFSET‑formler)?**  
A: Absolut. Du kan skicka en formelsträng istället för en statisk adress, t.ex. `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: Vad händer om jag behöver byta namn på en befintlig tabell?**  
A: Just set `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}