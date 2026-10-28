---
category: general
date: 2026-08-07
description: Definujte pojmenovaný rozsah v Excelu pomocí C# a naučte se přidat tabulku
  do listu, poté programově uložte sešit do souboru.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define named range excel
- save workbook to file
- add named range excel
- add table to worksheet
- create excel workbook programmatically
language: cs
lastmod: 2026-08-07
og_description: Definujte pojmenovaný rozsah v Excelu pomocí C# a podívejte se, jak
  přidat tabulku, vytvořit sešit programově a uložit sešit do souboru v jednom postupu.
og_image_alt: Screenshot of C# code that creates an Excel workbook, adds a table,
  defines a named range, and saves the file
og_title: Definujte pojmenovaný rozsah v Excelu pomocí C# – kompletní tutoriál celého
  sešitu
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Define named range in Excel with C# and learn how to add a table to
    a worksheet, then save workbook to file programmatically.
  headline: Define named range in Excel with C# – create workbook
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- named range
- programmatic Excel
title: Definovat pojmenovaný rozsah v Excelu pomocí C# – vytvořit sešit
url: /cs/net/excel-working-with-named-ranges/define-named-range-in-excel-with-c-create-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definovat pojmenovaný rozsah v Excelu pomocí C# – vytvořit sešit

Pokud potřebujete **definovat pojmenovaný rozsah v Excelu** z C# kódu, tento tutoriál vám přesně ukáže, jak na to. Také uvidíte, jak **přidat tabulku do listu**, vytvořit sešit **programaticky** a nakonec **uložit sešit do souboru** bez opuštění IDE.

Práce s Excel soubory programaticky šetří čas, eliminuje ruční chyby a umožňuje automatizované reportingové pipeline. V tomto průvodci budete:

* Vytvořit nový Excel sešit od nuly.  
* Přidat tabulku, která zahrnuje konkrétní rozsah buněk.  
* Definovat pojmenovaný rozsah a řešit konflikty v názvech.  
* Uložit sešit na disk.

Všechny kroky používají knihovnu **Aspose.Cells for .NET**, která funguje s .NET 6+ a .NET Framework 4.6+. Není vyžadována žádná další COM interop nebo instalace Office.

## Požadavky

* .NET 6 SDK (nebo .NET Framework 4.6+).  
* Visual Studio 2022 nebo jakékoli C#‑kompatibilní IDE.  
* NuGet balíček Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  

> **Tip:** Použijte bezplatnou zkušební licenci během testování; před nasazením ji nahraďte produkční licencí.

## Krok 1: Vytvořit Excel sešit programaticky

Prvním krokem je vytvořit instanci objektu `Workbook`. Tento objekt představuje celý Excel soubor v paměti.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();               // create an empty workbook
        Worksheet worksheet = workbook.Worksheets[0];    // get the first (default) worksheet
```

*Proč je to důležité*: Vytvoření sešitu v kódu vám dává plnou kontrolu nad listy, styly a daty, ještě předtím, než se soubor dotkne disku.

## Krok 2: Přidat tabulku do listu

Tabulka (také známá jako ListObject) poskytuje vestavěné filtrování, řazení a stylování. Zde vytvoříme tabulku, která zahrnuje buňky **A1:B5** a dáme jí název **SalesData**.

```csharp
        // Step 2: Define a range and convert it into a table
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Populate the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");
        worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");
        worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries");
        worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");
        worksheet.Cells["B5"].PutValue(30);
```

*Proč je to důležité*: Přidání tabulky brzy vám umožní později odkazovat na data pomocí **pojmenovaného rozsahu** a strukturovaný odkaz tabulky může být použit ve vzorcích.

## Krok 3: Definovat pojmenovaný rozsah v Excelu – řešení konfliktů

**Pojmenovaný rozsah** je identifikátor, který ukazuje na buňku nebo rozsah, což usnadňuje čtení vzorců. Pokud název již existuje (například název tabulky **SalesData**), Excel vyvolá konflikt. Níže uvedený kód ukazuje, jak zachytit výjimku a pokračovat bezpečně.

```csharp
        // Step 3: Attempt to define a named range with the same identifier as the table
        try
        {
            // This will raise an exception because "SalesData" is already used by the table
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Step 4: Add a different named range – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";
```

*Proč je to důležité*: Řešení kolizí názvů zabraňuje pádům během běhu v automatizovaných úlohách. Druhý pojmenovaný rozsah **SalesTotal** ukazuje odkazování na sloupec tabulky ve vzorci.

## Krok 4: Uložit sešit do souboru

Po všech úpravách uložte sešit na disk. Metoda `Save` podporuje mnoho formátů; zde používáme výchozí `.xlsx`.

```csharp
        // Step 5: Save the workbook to the file system
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

*Proč je to důležité*: Použití **uložení sešitu do souboru** programaticky umožňuje dávkové zpracování, plánovanou generaci reportů a integraci s webovými API.

## Kompletní zdrojový kód v jednom pohledu

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Add a table covering A1:B5 and name it "SalesData"
        Range tableRange = worksheet.Cells.CreateRange("A1:B5", true);
        ListObject table = worksheet.Tables[worksheet.Tables.Add(tableRange, true)];
        table.Name = "SalesData";

        // Fill the table with sample data
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Units");
        worksheet.Cells["A2"].PutValue("Apples");   worksheet.Cells["B2"].PutValue(120);
        worksheet.Cells["A3"].PutValue("Bananas");  worksheet.Cells["B3"].PutValue(85);
        worksheet.Cells["A4"].PutValue("Cherries"); worksheet.Cells["B4"].PutValue(45);
        worksheet.Cells["A5"].PutValue("Dates");    worksheet.Cells["B5"].PutValue(30);

        // Try to create a defined name with the same identifier – handle the conflict
        try
        {
            worksheet.Names.Add("SalesData", "A1");
        }
        catch (Exception ex)
        {
            Console.WriteLine("Name conflict prevented: " + ex.Message);
        }

        // Add a different defined name – this succeeds
        worksheet.Names.Add("SalesTotal", "B6");
        worksheet.Cells["B6"].Formula = "=SUM(SalesData[Units])";

        // Save the workbook
        string outputPath = @"C:\Temp\NameConflictHandled.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved successfully to {outputPath}");
    }
}
```

### Očekávaný výsledek

* Soubor Excel pojmenovaný **NameConflictHandled.xlsx** se objeví v `C:\Temp`.  
* List 1 obsahuje formátovanou tabulku **SalesData** s řádky produkt‑jednotka.  
* Buňka **B6** zobrazuje součet sloupce **Units**, vypočítaný pomocí pojmenovaného rozsahu **SalesTotal**.  
* Konzole vypíše zprávu o konfliktu názvu (pokud existuje) a potvrdí umístění souboru.

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| **Mohu definovat pojmenovaný rozsah, který zahrnuje více listů?** | Ano. Použijte `worksheet.Names.Add("GlobalRange", "'Sheet1'!A1:B5")` a odkažte na něj z libovolného listu. |
| **Co když potřebuji přepsat existující soubor?** | Zavolejte `workbook.Save(path, SaveFormat.Xlsx, new SaveOptions { Overwrite = true })`. |
| **Jak přidat pojmenovaný rozsah bez konfliktu, když název již existuje?** | Použijte `worksheet.Names.Remove("ExistingName")` před přidáním nového, nebo vygenerujte jedinečný identifikátor (např. `Guid.NewGuid().ToString("N")`). |
| **Existuje způsob, jak automaticky aplikovat styl na tabulku?** | Nastavte `table.Style = workbook.Styles[BuiltInStyleId.TableStyleMedium9];` po vytvoření tabulky. |
| **Funguje to na .NET Core?** | Aspose.Cells podporuje .NET Core, .NET 5/6/7 a .NET Framework. Stačí odkazovat na stejný NuGet balíček. |

## Závěr

Nyní víte, jak **definovat pojmenovaný rozsah v Excelu** pomocí C#, **přidat tabulku do listu** a **uložit sešit do souboru** programaticky. Kompletní příklad ukazuje vytvoření Excel sešitu od nuly, řešení konfliktů v názvech a generování použitelného souboru reportu v jednom opakovatelném postupu.

Dále prozkoumejte související témata, jako je **přidávání grafů do listu**, **export do PDF** nebo **čtení existujících sešitů**. Každé z nich staví na stejných základech, které jsou zde pokryty, takže budete připraveni rozšířit řešení na složitější automatizační scénáře. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit pojmenovaný rozsah buněk v Excelu](/cells/english/net/excel-creating-formatting-named-ranges/create-named-range-of-cells/)
- [Jak implementovat vzorce s pojmenovanými rozsahy v .NET pomocí Aspose.Cells pro automatizaci Excelu](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [Jak vytvořit pojmenované rozsahy omezené na sešit v Excelu pomocí Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}