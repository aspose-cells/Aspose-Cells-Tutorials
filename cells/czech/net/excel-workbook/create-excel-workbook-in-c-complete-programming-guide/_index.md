---
category: general
date: 2026-06-05
description: Rychle vytvořte Excel sešit v C# a naučte se, jak nastavit formát čísla
  v buňce, exportovat buňku Excelu a převést hodnotu buňky na řetězec s přesností
  na dvě desetinná místa.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: cs
og_description: Vytvořte Excel sešit v C# a ovládněte nastavení formátu čísel v buňce,
  exportování buňky Excelu jako řetězce a formátování čísel na dvě desetinná místa.
og_title: Vytvořte Excel sešit v C# – Kompletní průvodce krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Vytvořte Excel sešit v C# – Kompletní programovací průvodce
url: /cs/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel sešitu v C# – Kompletní programovací průvodce

Už jste se někdy zamýšleli, jak **vytvořit Excel sešit** v C# bez boje s COM interop nebo nešikovnými CSV triky? Nejste sami. Mnoho vývojářů potřebuje čistý, .NET‑native způsob, jak vytvořit soubor .xlsx, vložit číslo do buňky a poté exportovat tuto hodnotu jako hezky formátovaný řetězec.  

V tomto tutoriálu projdeme přesně to – začneme prázdným sešitem, nastavíme formát čísla buňky, naformátujeme číslo na dvě desetinná místa a nakonec se naučíme **jak exportovat Excel buňku** jako řetězec. Na konci také uvidíte, jak **převést hodnotu buňky na řetězec** bez ztráty přesnosti.

> **Tip:** Přístup níže používá knihovnu **Aspose.Cells for .NET**, která je osvědčeným, komerčním API. Pokud hledáte bezplatnou alternativu, EPPlus nebo ClosedXML fungují podobně, ale úryvky kódu se mírně liší.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- .NET 6.0 SDK (nebo jakoukoli novější verzi .NET) nainstalovanou.
- Visual Studio 2022 nebo VS Code s rozšířením C#.
- NuGet balíček **Aspose.Cells** (`Install-Package Aspose.Cells`).

Žádné další závislosti nejsou potřeba – všechno ostatní je součástí knihovny.

## Krok 1: Instalace Aspose.Cells a nastavení projektu

Otevřete terminál (nebo Package Manager Console) a spusťte:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

Tím se vytvoří čerstvá konzolová aplikace pojmenovaná `ExcelDemo` a stáhne se sestava `Aspose.Cells`.  

Proč je tento krok důležitý: bez knihovny nemůžete **vytvořit Excel sešit** objekty ani manipulovat s buňkami typově bezpečným způsobem.

## Krok 2: Vytvoření sešitu a získání první listu

Otevřete `Program.cs` a nahraďte výchozí kód úryvkem níže. Ukazuje první věc, kterou uděláte při **vytvoření Excel sešitu** – instanci třídy `Workbook` a získání reference na výchozí list.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Proč?** Objekt `Workbook` představuje v‑paměti Excel soubor. Ve výchozím nastavení obsahuje jeden list, ke kterému přistupujeme pomocí indexu začínajícího nulou.

## Krok 3: Vložení číselné hodnoty do konkrétní buňky

Cílíme na řádek 5, sloupec 2 (indexy od nuly) a vložíme desetinné číslo. Toto později demonstruje **formátování čísla na dvě desetinná místa**.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

Metoda `PutValue` uloží surové `double`. V tomto okamžiku by Excel zobrazil plnou přesnost, pokud bychom nepoužili formát.

## Krok 4: Nastavení číselného formátu buňky (dvě desetinná místa)

Zde **nastavíme číselný formát buňky**. Použijeme objekt `Style` k definování vlastního číselného formátu `"0.00"` – přesně dvě desetinná místa.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Proč použít styl místo převodu na řetězec? Zachování buňky jako číselného typu uchovává její výpočetní povahu (stále můžete sčítat, průměrovat atd.) a zároveň zobrazuje přesně to, co potřebujete.

## Krok 5: Export hodnoty buňky jako formátovaného řetězce

Někdy potřebujete **jak exportovat excel buňku** jako prostý text – například pro zápis do logu nebo odeslání přes webové API. Aspose.Cells vám umožní připojit exportní možnosti k buňce, čímž řeknete knihovně, aby hodnotu vykreslila jako řetězec pomocí stejného číselného formátu.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

Nyní, když čteme hodnotu buňky přes exportní API, získáme řetězec, který již respektuje pravidlo dvou desetinných míst.

## Krok 6: Získání formátovaného řetězce (převod hodnoty buňky na řetězec)

Provedeme skutečný export a podíváme se na výsledek. Metoda `ExportString` vrací obsah buňky jako řetězec a použije všechny `ExportTableOptions`, které jsme připojili.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Po spuštění programu se v konzoli vypíše:

```
Formatted cell value: 12345.68
```

Všimněte si zaokrouhlení z `12345.6789` na `12345.68` – to je efekt **formátování čísla na dvě desetinná místa**.

## Krok 7: (Volitelné) Uložení sešitu na disk

Pokud chcete výsledek vidět i v reálném souboru `.xlsx`, stačí zavolat `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Otevření `DemoWorkbook.xlsx` ukáže stejné číslo v buňce **C6**, formátované na dvě desetinná místa.

## Okrajové případy a časté otázky

### Co když buňka už má styl?

Metoda `GetStyle` vrací kopii existujícího stylu, takže předchozí formátování (písmo, barva atd.) zůstane zachováno. Přepíšete jen vlastnost `Custom`, ostatní nastavení zůstanou nedotčena.

### Jak kultura ovlivňuje desetinný oddělovač?

Aspose.Cells respektuje `CultureInfo` vlákna. Pokud potřebujete čárku místo tečky, nastavte:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Stejný formát `"0.00"` nyní vykreslí `12 345,68`.

### Můžu exportovat oblast buněk najednou?

Ano – použijte `Worksheet.ExportDataTable` nebo `Worksheet.ExportString` s adresou oblasti. `ExportTableOptions`, které jste definovali pro jednu buňku, můžete znovu použít pro celou oblast.

### Co když nechci, aby se hodnota zaokrouhlila, ale jen ořízlá?

Změňte vlastní formát na `"0.00"` s režimem oříznutí, nebo ručně ořízněte hodnotu před vložením:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Kompletní funkční příklad (připravený ke kopírování)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Očekávaný výstup v konzoli**

```
Formatted cell value: 12345.68
```

Otevřete `DemoWorkbook.xlsx` → přejděte na buňku **C6** → uvidíte stejné číslo se dvěma desetinnými místy.

## Závěr

Právě jsme prošli vším, co potřebujete k **vytvoření Excel sešitu** v C#, **nastavení číselného formátu buňky**, **formátování čísla na dvě desetinná místa**, pochopení **jak exportovat Excel buňku** a **převést hodnotu buňky na řetězec** pro další zpracování.  

Klíčové body jsou:

1. Použijte `Workbook` a `Worksheet` k vytvoření Excel souboru v paměti.  
2. Aplikujte vlastní styl (`"0.00"`) pro vynucení zobrazení se dvěma desetinnými místy.  
3. Připojte `ExportTableOptions` k buňce, když potřebujete řetězcovou reprezentaci, která respektuje stejný formát.  

Odtud můžete experimentovat – přidávat další buňky, aplikovat podmíněné formátování nebo dokonce generovat grafy. Pokud vás zajímá stylování písem nebo přidávání vzorců, podívejte se do dokumentace Aspose.Cells na **cell styling** a **formula evaluation**.

Máte další otázky ohledně automatizace Excelu v C#? Zanechte komentář a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}