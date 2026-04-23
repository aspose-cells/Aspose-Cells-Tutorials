---
category: general
date: 2026-03-30
description: Naučte se, jak formátovat číslo s oddělovačem pomocí Aspose.Cells v C#.
  Zahrnuje nastavení vlastního formátu čísla, přidání oddělovače tisíců, formátování
  desetinných míst a jak formátovat buňku.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: cs
og_description: Formátování čísla s oddělovačem v C#. Tento průvodce ukazuje, jak
  nastavit vlastní formát čísla, přidat oddělovač tisíců, formátovat desetinná místa
  a jak formátovat buňku pomocí Aspose.Cells.
og_title: Formátování čísla s oddělovačem v C# – tutoriál Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Formátování čísel s oddělovačem v C# – Kompletní průvodce Aspose.Cells
url: /cs/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formátování čísel s oddělovačem v C# – Kompletní průvodce Aspose.Cells

Už jste někdy potřebovali **formátovat číslo s oddělovačem** v tabulce, ale nebyli jste si jisti, kterou API metodu použít? Nejste v tom sami – vývojáři neustále bojují s tisícovými oddělovači, desetinnými místy a vlastními vzory při exportu dat.  

Dobrá zpráva: Aspose.Cells to dělá hračkou. V tomto tutoriálu projdeme reálný příklad, který **nastavuje vlastní formát čísla**, **přidává tisícový oddělovač**, **formátuje desetinná místa** a ukazuje **jak formátovat buňku** pro výstup jako řetězec. Na konci budete mít připravený úryvek kódu, který můžete vložit do libovolného .NET projektu.

## Co tento průvodce zahrnuje

* Přesný NuGet balíček, který potřebujete, a jak jej nainstalovat.  
* Krok‑za‑krokem kód, který vytvoří sešit, zapíše číselnou hodnotu a použije vlastní formát.  
* Proč je `ExportTableOptions.ExportAsString` preferovaným způsobem, jak získat formátovanou hodnotu.  
* Časté úskalí – například zapomenutí povolit `ExportAsString` nebo použití nesprávné masky formátu.  
* Jak upravit masku formátu, pokud potřebujete jiný počet desetinných míst nebo jiný styl oddělovače.

Žádné externí odkazy na dokumentaci nejsou potřeba; vše, co potřebujete, je zde. Pojďme na to.

---

## Prerequisites

| Požadavek | Důvod |
|-------------|--------|
| .NET 6.0 nebo novější | Aspose.Cells 23.10+ cílí na .NET Standard 2.0+, takže .NET 6 je bezpečný a aktuální. |
| Visual Studio 2022 (nebo jakékoli C# IDE) | Usnadňuje ladění a správu balíčků. |
| Aspose.Cells for .NET NuGet package | Poskytuje třídy `Workbook`, `Worksheet` a `ExportTableOptions`, které použijeme. |

Balíček můžete nainstalovat pomocí Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

A to je vše – žádné další DLL, žádná COM interop, jen jediná reference na NuGet.

---

## Krok 1: Inicializace nového Workbooku (Jak formátovat buňku)

První, co uděláme, je vytvořit novou instanci `Workbook`. Představte si ji jako prázdný soubor Excel připravený přijmout data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Proč je to důležité:** `Workbook` je vstupní bod pro každou operaci v Aspose.Cells. Získáním první listu (`Worksheets[0]`) získáme čisté plátno, aniž bychom museli pojmenovávat list.

---

## Krok 2: Zapsání číselné hodnoty do cílové buňky

Dále vložíme surové číslo do buňky **A1**. Hodnota zatím není formátovaná – je to jen `double`.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Tip:** Použijte `PutValue` místo `PutString`, pokud chcete později aplikovat číselné formátování. Tím zachováte podkladový datový typ, což umožní výpočty kompatibilní s Excelem.

---

## Krok 3: Nastavení vlastního formátu čísla (Přidání tisícového oddělovače a formátování desetinných míst)

Nyní přichází jádro tutoriálu: definování masky formátu, která říká Aspose.Cells, jak číslo zobrazit. Maska `#,##0.00` dělá tři věci:

1. **`#,##0`** – přidá tisícový oddělovač (čárka ve výchozím nastavení).  
2. **`.00`** – vynutí přesně dvě desetinná místa.  

Pokud potřebujete jiný počet desetinných míst, stačí změnit počet `0` za desetinnou čárkou.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Proč používáme `ExportAsString`**: Ve výchozím nastavení `ExportString` vrací surovou hodnotu. Nastavením `ExportAsString = true` přinutíme API aplikovat masku `NumberFormat` před konverzí na text. To je nezbytné, když potřebujete přesnou řetězcovou reprezentaci pro reporty, JSON payloady nebo UI zobrazení.

---

## Krok 4: Export formátovaného textu (Jak formátovat buňku)

S připravenými možnostmi zavoláme `ExportString` na stejné buňce. Metoda respektuje masku, kterou jsme právě definovali, a vrátí pěkně formátovaný řetězec.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Spuštěním programu se na konzoli vypíše **`12,345.68`** – přesně ve formátu, který jsme požadovali.

> **Hraniční případ:** Pokud má vstupní číslo více než dvě desetinná místa, maska jej zaokrouhlí. Pokud potřebujete místo zaokrouhlení oříznutí, musíte hodnotu před voláním `PutValue` předzpracovat pomocí `Math.Truncate`.

---

## Krok 5: Úprava formátu – běžné varianty

### 5.1 Změna přesnosti desetinných míst

Chcete tři desetinná místa? Stačí nahradit masku:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Použití jiného tisícového oddělovače

Některé lokály preferují mezeru nebo tečku. Můžete znak vložit přímo:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Nebo se spolehnout na nastavení kultury sešitu:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Předpona nebo přípona (Měna, Procenta)

Přidejte dolarový znak nebo znak procenta přímo do masky:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Poznámka:** Maska rozlišuje velká a malá písmena. `$` a `%` jsou doslovné symboly; nemění podkladovou číselnou hodnotu.

---

## Krok 6: Kompletní funkční příklad (Ready‑to‑Copy)

Níže je celý program, který můžete zkopírovat do nové konzolové aplikace. Obsahuje všechny kroky, komentáře a ověření výstupu.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Program spusťte (`dotnet run` v terminálu nebo stiskněte F5 ve Visual Studiu) a uvidíte formátované číslo vytištěné přesně tak, jak je uvedeno.

---

## Často kladené otázky (FAQ)

**Q: Funguje to i se staršími verzemi Excelu?**  
A: Ano. Maska formátu používá nativní syntaxi Excelu, takže jakákoli verze, která rozumí `#,##0.00`, zobrazí stejný řetězec.

**Q: Co když potřebuji formátovat rozsah buněk?**  
A: Projděte požadovaný rozsah a aplikujte stejný `ExportTableOptions` na každou buňku, nebo nastavte vlastnost `Style.Custom` na rozsah a pak zavolejte `ExportString` na jedné buňce.

**Q: Můžu exportovat přímo do CSV s těmito formáty?**  
A: Rozhodně. Použijte `Workbook.Save("output.csv", SaveFormat.CSV);` po nastavení formátu na každé buňce. Aspose.Cells respektuje styl buňky při generování CSV.

---

## Závěr

Ukázali jsme, jak **formátovat číslo s oddělovačem** v C# pomocí Aspose.Cells, od **nastavení vlastního formátu čísla** přes **přidání tisícového oddělovače**, **formátování desetinných míst** až po nezbytné **jak formátovat buňku** pro export jako řetězec. Kód je zcela samostatný, funguje s .NET 6+ a lze jej přizpůsobit libovolnému locale nebo požadavku na přesnost.

Dále můžete zkusit:

* Použít stejnou techniku pro datum a čas (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automatizovat hromadné exporty, kde každá sloupec potřebuje jinou masku.  
* Integrovat formátované řetězce do PDF reportů pomocí Aspose.Words.

Vyzkoušejte to a rychle se stanete osobou, na kterou se tým obrací ohledně formátování tabulek. Šťastné kódování!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formátované číslo s oddělovačem zobrazené v Aspose.Cells výstupu"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}