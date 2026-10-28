---
category: general
date: 2026-07-13
description: Vytvořte Excel sešit v C# a naučte se, jak přidat pojmenovaný rozsah,
  přiřadit název tabulce a řešit konflikty názvů – vše v jednom přehledném příkladu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: cs
lastmod: 2026-07-13
og_description: Vytvořte Excel sešit v C# s Aspose.Cells. Naučte se, jak přidat pojmenovaný
  rozsah, nastavit název tabulky a vyřešit konflikty pojmenování v stručném, spustitelném
  průvodci.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Vytvořte Excel sešit v C# – Přidejte pojmenovaný rozsah a nastavte název
  tabulky
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
title: Vytvořte Excel sešit v C# – Přidejte pojmenovaný rozsah a nastavte název tabulky
url: /cs/net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v C# – Kompletní průvodce přidáváním pojmenovaných oblastí a nastavením názvů tabulek

Už jste někdy potřebovali **vytvořit Excel sešit** od nuly a přemýšleli, kam umístit pojmenovanou oblast nebo jak tabulce přiřadit vlastní identifikátor? Nejste v tom sami. V mnoha scénářích reportování nebo exportu dat se budete potýkat s oblastmi, tabulkami a občasnými kolizemi názvů.  

V tomto tutoriálu projdeme plně spustitelný příklad, který **vytváří Excel sešit**, **přidává pojmenovanou oblast** a poté **přiřazuje název tabulce** – ukážeme vám přesně, co dělat, když se názvy střetnou. Na konci budete znát „jak“ i „proč“ každého kroku a získáte několik tipů, jak udržet kód čistý.

> **Rychlý výsledek:** Kód používá knihovnu **Aspose.Cells**, která funguje s .NET 6+ a nevyžaduje instalaci Excelu na serveru.

---

## Co budete potřebovat

- **.NET 6 SDK** (nebo jakákoli novější verze .NET)  
- **Aspose.Cells for .NET** NuGet balíček  
- Slušné IDE (Visual Studio, Rider nebo VS Code)  
- Základní znalost C# – nic složitého, jen běžné `using` příkazy

Pokud je máte, můžeme rovnou přejít na proces **create excel workbook**.

---

## ## Vytvoření Excel sešitu – Přehled krok za krokem

Níže je kompletní, připravený program ke zkopírování. Ukazuje vše od vytvoření sešitu až po řešení konfliktu názvů, když se pokusíte **assign name to table**.

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

**Očekávaný výstup** při spuštění programu:

```
Naming conflict detected:
A name with the same text already exists.
```

A pokud otevřete *DemoWorkbook.xlsx*, uvidíte tabulku pojmenovanou **Table1** a pojmenovanou oblast nazvanou **MyRange** – právě to, co jsme zamýšleli, bez kolize.

---

## ## Přidání pojmenované oblasti – Proč je to důležité

**Pojmenovaná oblast** je v podstatě alias pro blok buněk. Místo neustálého odkazování na `A1:B5` můžete ve vzorcích, datových ověřováních nebo dokonce v kódu psát `MyRange`. To zlepšuje čitelnost a snižuje šanci na chyby způsobené překlepy.

Ve výše uvedeném úryvku voláme:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- První argument je **název**, který později použijete.  
- Druhý argument je **adresa** (relativní k listu).  

Pokud někdy potřebujete **how to add range** dynamicky, můžete sestavit řetězec adresy pomocí `Cell.GetRefersTo()` nebo použít `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Přiřazení názvu tabulce – Řešení konfliktů

Tabulky (také nazývané *list objects*) již mají vestavěnou vlastnost názvu. Ve výchozím nastavení je Aspose.Cells pojmenovává `Table1`, `Table2` atd. Když se pokusíte tabulce přiřadit stejný identifikátor jako existující pojmenované oblasti, knihovna vyhodí výjimku – stejně jako Excel.

Proč se to děje?

- Rozsah pojmenování v Excelu je **celý sešit** jak pro oblasti, tak pro tabulky.  
- Duplicitní názvy by zpřehlednily vzorce, takže engine je blokuje.

### Tip

Pokud opravdu potřebujete, aby tabulka sdílela logický název s oblastí, zvažte **přidání předpony** jedné z nich, např.:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Nebo nejprve přejmenujte oblast:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Oba přístupy udržují pojmenovací prostor úhledný a zabraňují chybám za běhu.

---

## ## Nastavení názvu tabulky – Nejlepší postupy

Když **set table name** programově, mějte na paměti následující zásady:

1. **Používejte konzistentní předponu** (`tbl_`, `rng_` atd.) – okamžitě naznačuje, o jaký objekt se jedná.  
2. **Zůstaňte pod 255 znaky** – limit Excelu pro názvy.  
3. **Vyhýbejte se mezerám a speciálním znakům** – bezpečné jsou jen písmena, číslice a podtržítka.  
4. **Ověřte před přiřazením** – rychlá kontrola `if (!sheet.Names.Contains(name))` zabrání kolizi, kterou jsme demonstrovali.

Zde je pomocná metoda, kterou můžete vložit do libovolného projektu:

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

Volání `SafeSetTableName(sheet, table, "MyRange")` automaticky změní `MyRange` na `MyRange_1`, pokud existuje konflikt, a zajistí, že operace **create excel workbook** nikdy neočekávaně neukončí.

---

## ## Kompletní funkční příklad – Jak to spojit dohromady

Níže je kompaktní verze, kterou můžete zkopírovat přímo do konzolové aplikace. Obsahuje bezpečnostní rutinu a demonstruje celý tok od začátku do konce.

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

Spuštěním tohoto skriptu vznikne `FinalDemo.xlsx`, kde je tabulka pojmenována `MyRange_1` (nebo jiná unikátní přípona) a oblast zůstává `MyRange`. Žádná výjimka, žádná záhada – jen čisté, deterministické pojmenování.

---

## ## Často kladené otázky (FAQ)

**Q: Můžu přidat pojmenovanou oblast, která zasahuje více listů?**  
A: Ano, ale musíte adresu kvalifikovat názvem listu, např. `"Sheet1!A1:B5"`. Metoda `Names.Add` tento formát akceptuje.

**Q: Podporuje Aspose.Cells dynamické pojmenované oblasti (např. OFFSET vzorce)?**  
A: Rozhodně. Můžete předat řetězec vzorce místo statické adresy, například `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: Co když potřebuji přejmenovat existující tabulku?**  
A: Jednoduše nastavte `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}