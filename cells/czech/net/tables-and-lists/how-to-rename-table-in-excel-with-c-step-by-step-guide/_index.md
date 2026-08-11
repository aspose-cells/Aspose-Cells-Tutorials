---
category: general
date: 2026-08-11
description: Jak přejmenovat tabulku v Excelu pomocí C# a Aspose.Cells. Naučte se
  vytvořit sešit Excel, přidat pojmenovaný rozsah a vyhnout se konfliktům při přejmenování.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: cs
lastmod: 2026-08-11
og_description: Jak přejmenovat tabulku v Excelu pomocí C# a Aspose.Cells. Tento průvodce
  vám ukáže, jak vytvořit sešit Excel, přidat pojmenovaný rozsah a bezpečně přejmenovat
  tabulku v Excelu.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: Jak přejmenovat tabulku v Excelu pomocí C# – kompletní programovací tutoriál
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
title: Jak přejmenovat tabulku v Excelu pomocí C# – krok za krokem
url: /cs/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak přejmenovat tabulku v Excelu pomocí C# – krok‑za‑krokem průvodce

Pokud potřebujete **jak přejmenovat tabulku** v souboru Excel programově, tento tutoriál vám ukáže přesný postup pomocí Aspose.Cells pro .NET. Uvidíte, jak **vytvořit Excel sešit**, definovat **pojmenovaný rozsah** a přejmenovat existující Excel tabulku, aniž by došlo ke konfliktu názvů.

Řešení funguje pro jakýkoli .NET projekt, který cílí na .NET 6 nebo novější, a vyžaduje pouze balíček Aspose.Cells NuGet. Na konci průvodce budete umět bezpečně přejmenovat Excel tabulku a pochopíte, proč může vzniknout konflikt, když se název tabulky shoduje s definovaným rozsahem.

## Požadavky

- .NET 6 SDK nebo novější nainstalovaný  
- Visual Studio 2022 (nebo jakékoli C# IDE)  
- Aspose.Cells pro .NET balíček (`dotnet add package Aspose.Cells`)  

Nejsou potřeba žádné další Excel interop sestavy, protože Aspose.Cells pracuje zcela v paměti.

## Přehled řešení

1. **Create Excel workbook** – vytvořit instanci `Workbook` a přidat ukázková data.  
2. **Add a named range** – použít `Worksheets.Names.Add` k vytvoření rozsahu s názvem `MyRange`.  
3. **Create an Excel table (ListObject)** – převést data na tabulku, abychom měli co přejmenovat.  
4. **Rename the table** – pokusit se nastavit vlastnost `Name` tabulky na stejný identifikátor jako pojmenovaný rozsah.  
5. **Handle name conflicts** – zachytit výjimku, vysvětlit, proč nastává, a ukázat bezpečnou strategii přejmenování.

Každý krok je podrobně vysvětlen níže.

## Krok 1: Jak vytvořit Excel sešit a naplnit data

Vytvoření sešitu je základem pro jakýkoli úkol automatizace v Excelu. Třída `Workbook` představuje celý soubor v paměti.

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

**Proč je to důležité:** Sešit musí obsahovat data, než můžete vytvořit tabulku. Aspose.Cells ukládá data v nulově indexované kolekci, takže `Worksheets[0]` vždy odkazuje na první list.

## Krok 2: Jak přidat pojmenovaný rozsah do listu

**Named range** vám umožní odkazovat na konkrétní buňku nebo oblast pomocí přátelského identifikátoru. Přidání rozsahu je jednoduché:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Proč je to důležité:** Pojmenované rozsahy jsou uloženy v globální kolekci názvů sešitu. Pokud tabulka později získá stejný název, Aspose.Cells vyhodí `CellException`, protože Excel neumožňuje duplicitní názvy.

## Krok 3: Jak přidat Excel tabulku (ListObject)

Tabulka poskytuje strukturované zpracování dat, filtrování a stylování. V Aspose.Cells se nazývá **ListObject**.

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

**Proč je to důležité:** Tabulka nyní existuje s názvem `InitialTable`. Její přejmenování demonstruje proces **jak přejmenovat tabulku**.

## Krok 4: Jak přejmenovat Excel tabulku a řešit konflikty

Pokus o přejmenování tabulky na `MyRange` bude kolidovat s pojmenovaným rozsahem, který jsme vytvořili dříve. Následující kód ukazuje správný vzor pro detekci a řešení konfliktu.

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

### Co kód dělá

| Krok | Akce | Důvod |
|------|------|-------|
| **Zkusit přejmenovat** | `table.Name = "MyRange"` | Ukazuje scénář konfliktu. |
| **Zachytit výjimku** | Vytiskne zprávu o konfliktu. | Poskytuje okamžitou zpětnou vazbu o problému. |
| **Vygenerovat bezpečný název** | `GetUniqueTableName` přidává číselnou příponu, dokud není název volný. | Zaručuje, že nový název tabulky **se** nekříží s žádným existujícím pojmenovaným rozsahem nebo tabulkou. |
| **Uložit sešit** | `workbook.Save("RenamedTable.xlsx")` | Ukládá změny, abyste mohli soubor otevřít v Excelu a ověřit výsledek. |

**Očekávaný výstup** při spuštění programu:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Otevření `RenamedTable.xlsx` ukazuje tabulku pojmenovanou `MyRange_1` a samostatný pojmenovaný rozsah `MyRange` ukazující na buňku A1.

## Proč dochází ke konfliktu a osvědčené postupy pro přejmenování Excel tabulky

- Excel ukládá **named ranges** a **table names** ve stejném jmenném prostoru.  
- Když se pokusíte přiřadit název tabulky, který již existuje jako rozsah, Aspose.Cells vyhodí `CellException`.  
- Doporučený přístup je **nejprve zkontrolovat existující názvy** (jak je ukázáno v `NameExists`) nebo použít pojmenovací konvenci, která zaručuje jedinečnost (např. předpona tabulek `tbl_`).  

Použití tohoto vzoru zabraňuje chybám za běhu a činí vaši automatizaci robustní.

## Další tipy pro práci s Aspose.Cells

- **Pro tip:** Použijte `Workbook.Worksheets.Names.Remove("MyRange")`, pokud úmyslně chcete nahradit rozsah názvem tabulky.  
- **Dejte pozor na citlivost na velikost písmen:** Excel zachází s názvy bez rozlišení velkých a malých písmen; pomocné metody používají `OrdinalIgnoreCase` k napodobení chování Excelu.  
- **Výkon:** Pokud zpracováváte mnoho listů, cacheujte kolekci názvů místo opakovaného iterování.

## Kompletní příklad v jednom bloku

Níže je celý program, který můžete zkopírovat a vložit do konzolového projektu. Obsahuje všechny kroky od vytvoření sešitu až po bezpečné přejmenování tabulky.



## Co se naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich vlastních projektech.

- [Jak vytvořit pojmenované rozsahy v sešitu v Excelu pomocí Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Jak implementovat vzorce s pojmenovanými rozsahy v .NET pomocí Aspose.Cells pro automatizaci Excelu](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Jak přidat řezače do Excel tabulek pomocí Aspose.Cells pro .NET: Komplexní průvodce](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}