---
category: general
date: 2026-05-23
description: Vytvořte excelový sešit v C# a naučte se, jak použít vlastní číselný
  formát, nastavit styl buňky programově, formátovat buňku ve vědecké notaci a poté
  uložit sešit do formátu xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: cs
og_description: Rychle vytvořte Excel sešit v C#. Naučte se použít vlastní číselný
  formát, programově stylovat buňky, formátovat vědecký zápis a uložit do formátu
  xlsx.
og_title: Vytvořte Excel sešit v C# – Použijte vlastní formát čísel
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Vytvořte Excel sešit v C# – Použijte vlastní číselný formát
url: /cs/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel Workbook v C# – Použití vlastního číselného formátu

Vytvořit Excel workbook v C# je jednodušší, než si možná myslíte. V tomto průvodci vás provedeme aplikací vlastního číselného formátu, formátováním buňky ve vědecké notaci, nastavením stylu buňky programově a nakonec uložením sešitu do souboru xlsx.

Pokud jste někdy zírali na prázdnou tabulku a přemýšleli, jak automatizovat celý proces – od naplnění dat až po zobrazení čísel přesně tak, jak potřebujete – tento tutoriál je pro vás. Na konci budete mít plně funkční Excel soubor, který můžete otevřít v jakémkoli tabulkovém programu, a pochopíte **proč** je každý krok důležitý, nejen **jak** kód napsat.

## Co budete potřebovat

- **.NET 6+** (nebo jakýkoli recentní .NET Framework, který knihovnu podporuje)  
- **Aspose.Cells for .NET** (nebo jiné API, které vystavuje třídy `Workbook`, `Cell` a `CellFormat`)  
- Mírné zkušenosti s C# – pokud umíte napsat `Console.WriteLine`, jste připraveni.  

Žádné extra konfigurační soubory, žádné COM interop a rozhodně žádná ruční instalace Excelu nejsou potřeba.

---

## Vytvoření Excel Workbook – Inicializace objektu Workbook

Prvním krokem je vytvořit prázdný workbook. Třídu `Workbook` si představte jako prázdné plátno, na které budete kreslit řádky, sloupce a styly.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

A to je vše – jeden řádek a máte v paměti zbrusu nový Excel soubor. Konstruktor `Workbook` vytvoří výchozí kolekci listů, takže můžete okamžitě začít přidávat data.

> **Tip:** Pokud potřebujete více listů, můžete zavolat `workbook.Worksheets.Add()` předtím, než začnete vyplňovat buňky.

![Příklad vytvoření Excel workbook](image-placeholder.png "Snímek obrazovky vytvoření Excel workbook")

*Text alternativy obrázku: příklad vytvoření Excel workbook ukazující prázdný Excel list v IDE.*

## Použití vlastního číselného formátu na buňku

Nyní, když workbook existuje, vložme číslo do buňky **A1** a přiřaďme mu vlastní formát. Vlastní číselné formáty vám umožňují řídit, jak se čísla zobrazují – měna, procenta, data nebo, v našem případě, vědecká notace.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Proč nejprve získat styl? Protože objekt `Cell` ukládá objekt **Style**, který obsahuje písma, ohraničení, zarovnání a formátování čísel na jednom místě. Úpravou vlastnosti `Custom` řekneme Excelu: „zobraz tuto hodnotu ve vědecké notaci se dvěma desetinnými místy.“

> **Často kladená otázka:** *Mohu použít vestavěný formát místo vlastního?*  
> Ano – nastavte `style.Number = 10` pro vestavěný vědecký formát, ale vlastní řetězec vám poskytuje přesnou kontrolu nad počtem desetinných míst.

## Nastavení stylu buňky programově (mimo číselný formát)

Často budete chtít více než jen číselný formát. Přidejme tučný font a světle šedé pozadí, aby buňka vynikla.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Všimněte si, že znovu používáme stejný objekt `style`, který jsme upravili dříve. To je krása **set cell style programmatically** – styl načtete jen jednou, upravíte potřebné vlastnosti a zapíšete ho zpět. Není nutné znovu vytvářet objekty ani ztratit již nastavený číselný formát.

## Formátování buňky ve vědecké notaci (zvládání okrajových případů)

Pokud pracujete s velmi velkými nebo velmi malými čísly, vědecká notace je záchrana. Vlastní formát, který jsme použili (`0.00E+00`), zaručuje dvě číslice za desetinnou čárkou a vynutí znaménko plus u exponentu. Zde je rychlá kontrola:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Když otevřete výsledný soubor, buňka B2 se zobrazí jako `1.23E-05`, což potvrzuje, že direktiva **format cell scientific notation** funguje jak pro velká, tak pro malá čísla.

## Uložení workbooku do XLSX

Vše končí, když skutečně zapíšete soubor na disk. Metoda `Save` provádí těžkou práci, převádí paměťovou reprezentaci do správného balíčku `.xlsx`.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Tento řádek splňuje cíl **save workbook to xlsx**. Pokud adresář neexistuje, `Save` vyhodí výjimku – proto se ujistěte, že složka je vytvořena předem, nebo obalte volání do bloku try/catch.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Nyní máte připravený Excel soubor ke sdílení s pěkně naformátovaným vědeckým číslem, tučným stylem a světle šedým pozadím.

## Kompletní funkční příklad

Níže je kompletní program připravený ke zkopírování, který spojuje všechny části dohromady. Kompiluje se jako konzolová aplikace, ale logiku můžete vložit do libovolného C# projektu.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Očekávaný výsledek:** Otevřete `CustomFormatted.xlsx` a uvidíte:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Obě buňky jsou tučné, mají světle šedé vyplnění a zobrazují čísla ve vědecké notaci se dvěma desetinnými místy.

---

## Závěr

Právě jsme **create excel workbook** od začátku, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically** a **save workbook to xlsx** – vše během několika řádků C#. Přístup je škálovatelný: stačí projít řádky ve smyčce, klonovat objekt `style` a během okamžiku budete mít plně stylovanou zprávu.

### Co dál?

- **Dynamic formatting:** Přepínání formátů podle velikosti hodnoty (např. měna vs. procenta).  
- **Multiple sheets:** Použijte `workbook.Worksheets.Add("Summary")` k vytvoření dashboardů.  
- **Advanced styling:** Ohraničení, podmíněné formátování a validace dat

## Související tutoriály

- [Jak vytvořit a uložit Excel Workbook jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Vytvořit a uložit Excel Workbook Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Vytvořit a uložit Excel Workbook PDF Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}