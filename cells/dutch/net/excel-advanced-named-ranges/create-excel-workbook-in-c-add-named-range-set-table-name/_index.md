---
category: general
date: 2026-07-13
description: Maak een Excel-werkmap in C# en leer hoe je een benoemd bereik toevoegt,
  een naam aan een tabel toewijst en naamconflicten afhandelt — allemaal in één duidelijk
  voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: nl
lastmod: 2026-07-13
og_description: Maak een Excel-werkmap in C# met Aspose.Cells. Leer hoe je een benoemd
  bereik toevoegt, een tabelnaam instelt en naamconflicten oplost in een beknopte,
  praktische gids.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Excel-werkboek maken in C# – Naamgegeven bereik toevoegen & tabelnaam instellen
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
title: Excel-werkboek maken in C# – Naamgegeven bereik toevoegen & tabelnaam instellen
url: /nl/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel Workbook in C# – Complete gids voor het toevoegen van benoemde bereiken en het instellen van tabelnamen

Heb je ooit **een Excel workbook** vanaf nul moeten maken en je afgevraagd waar je een benoemd bereik moet plaatsen of hoe je een tabel een eigen identifier geeft? Je bent niet de enige. In veel rapportage- of data‑exportscenario's kom je terecht bij het jongleren met bereiken, tabellen en af en toe een naamconflict.

In deze tutorial lopen we een volledig uitvoerbaar voorbeeld door dat **een Excel workbook** **maakt**, **een benoemd bereik toevoegt**, en vervolgens **een naam aan een tabel toekent**—en je precies laat zien wat je moet doen wanneer de namen botsen. Aan het einde ken je het “hoe” en het “waarom” achter elke stap, plus een paar tips om je code schoon te houden.

> **Snelle winst:** De code maakt gebruik van de **Aspose.Cells**-bibliotheek, die werkt met .NET 6+ en geen Excel‑installatie op de server vereist.

---

## Wat je nodig hebt

- **.NET 6 SDK** (of een recente .NET‑versie)  
- **Aspose.Cells for .NET** NuGet‑pakket  
- Een degelijke IDE (Visual Studio, Rider, of VS Code)  
- Basis C#‑kennis—niets bijzonders, gewoon de gebruikelijke `using`‑statements  

Als je die hebt, kunnen we meteen naar het **create excel workbook**‑proces springen.

---

## ## Maak Excel Workbook – Stapsgewijs overzicht

Hieronder staat het volledige, kant‑klaar te kopiëren programma. Het demonstreert alles, van het maken van een workbook tot het afhandelen van een naamconflict wanneer je probeert **een naam aan een tabel toe te wijzen**.

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

**Verwachte output** wanneer je het programma uitvoert:

```
Naming conflict detected:
A name with the same text already exists.
```

En als je *DemoWorkbook.xlsx* opent, zie je een tabel met de naam **Table1** en een benoemd bereik genaamd **MyRange**—precies wat we bedoelden, zonder het conflict.

---

## ## Voeg benoemd bereik toe – Waarom het belangrijk is

Een **named range** is in wezen een alias voor een celblok. In plaats van steeds te verwijzen naar `A1:B5`, kun je `MyRange` schrijven in formules, gegevensvalidaties, of zelfs in code. Dit verbetert de leesbaarheid en verkleint de kans op typefouten‑gerelateerde bugs.

In het bovenstaande fragment roepen we aan:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- Het eerste argument is de **name** die je later zult gebruiken.  
- Het tweede argument is het **address** (relatief ten opzichte van het werkblad).  

Als je ooit **hoe je een bereik dynamisch toevoegt** nodig hebt, kun je de adres‑string opbouwen met `Cell.GetRefersTo()` of `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)` gebruiken.

---

## ## Ken naam toe aan tabel – Conflicten afhandelen

Tabellen (ook wel *list objects* genoemd) hebben al een ingebouwde name‑eigenschap. Standaard noemt Aspose.Cells ze `Table1`, `Table2`, enz. Wanneer je een tabel dezelfde identifier geeft als een bestaand named range, gooit de bibliotheek een uitzondering—net als Excel.

Waarom gebeurt dit?

- Het naamgevingsbereik van Excel is **workbook‑wide** voor zowel bereiken als tabellen.  
- Dubbele namen zouden formules dubbelzinnig maken, dus blokkeert de engine dit.

### Pro‑tip

Als je echt een tabel een logische naam wilt laten delen met een bereik, overweeg dan om **een prefix** toe te voegen aan één van hen, bijv.:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Of hernoem eerst het bereik:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Beide benaderingen houden de naamruimte netjes en voorkomen runtime‑fouten.

---

## ## Stel tabelnaam in – Best practices

Wanneer je **table name** programmatically instelt, houd dan rekening met deze richtlijnen:

1. **Gebruik een consistente prefix** (`tbl_`, `rng_`, etc.) – het geeft meteen aan wat het object is.  
2. **Blijf binnen 255 tekens** – de limiet van Excel voor namen.  
3. **Vermijd spaties en speciale tekens** – alleen letters, cijfers en underscores zijn veilig.  
4. **Valideer vóór toewijzing** – een snelle `if (!sheet.Names.Contains(name))`‑check voorkomt het conflict dat we hebben gedemonstreerd.  

Hier is een hulpfunctie die je in elk project kunt opnemen:

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

Het aanroepen van `SafeSetTableName(sheet, table, "MyRange")` zal `MyRange` automatisch omzetten naar `MyRange_1` als er een conflict bestaat, waardoor de **create excel workbook**‑operatie nooit onverwacht wordt afgebroken.

---

## ## Volledig werkend voorbeeld – Alles samenvoegen

Hieronder staat een compacte versie die je direct in een console‑app kunt kopiëren. Het bevat de veiligheidsroutine en demonstreert de end‑to‑end‑stroom.

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

Het uitvoeren van dit script produceert `FinalDemo.xlsx` waarin de tabel `MyRange_1` heet (of een andere unieke suffix) en het bereik blijft `MyRange`. Geen uitzondering, geen mysterie—gewoon een schone, deterministische naamgeving.

---

## ## Veelgestelde vragen (FAQ)

**Q: Kan ik een named range toevoegen die zich uitstrekt over meerdere werkbladen?**  
A: Ja, maar je moet het adres kwalificeren met de sheet‑naam, bijv. `"Sheet1!A1:B5"`. De `Names.Add`‑methode accepteert dat formaat.

**Q: Ondersteunt Aspose.Cells dynamische named ranges (zoals OFFSET‑formules)?**  
A: Absoluut. Je kunt een formule‑string doorgeven in plaats van een statisch adres, zoals `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: Wat als ik een bestaande tabel moet hernoemen?**  
A: Stel gewoon `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}