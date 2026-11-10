---
category: general
date: 2026-10-26
description: Naučte se, jak nastavit vlastní formát čísel v souboru Excel v C# konfigurací
  významných číslic, vytvořením sešitu Excel a jeho uložením jako dokumentu XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: cs
lastmod: 2026-10-26
og_description: Vlastní formát čísel v Excelu v C# vám umožňuje ovládat významné číslice,
  vytvořit sešit Excel a uložit jej jako XLSX. Sledujte tento kompletní návod.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Vlastní formát čísel v Excelu v C# – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak použít vlastní číselný formát v Excelu v C#
url: /cs/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít vlastní číselný formát v Excelu v C#

Pokud potřebujete **custom number format excel**, který zobrazuje konkrétní počet významných číslic, tento průvodce vám přesně ukáže, jak to provést v C#. Uvidíte, jak nastavit významné číslice, vytvořit Excel sešit a uložit jej jako soubor XLSX – vše pomocí několika řádků kódu.

Práce s Excel soubory programově často vyžaduje kontrolu toho, jak se čísla zobrazují. Pomocí Aspose.Cells pro .NET můžete definovat globální nastavení formátu čísla, které vynutí, aby každá číselná buňka respektovala zadaný počet významných číslic. Tento tutoriál pokrývá kompletní workflow, od nastavení projektu až po ověření výstupu v Excelu.

## Požadavky

* .NET 6.0 nebo novější nainstalovaný (kód také funguje s .NET Framework 4.7.2+)
* Visual Studio 2022 nebo jakékoli C# IDE, které preferujete
* Balíček **Aspose.Cells** NuGet (`Install-Package Aspose.Cells`) – plně spravovaná knihovna pro manipulaci s Excelem
* Základní znalost syntaxe C#

## Krok 1: Vytvoření Excel sešitu v C#

Prvním krokem je vytvořit novou instanci objektu `Workbook`. Tento objekt představuje celý Excel soubor v paměti.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Proč je to důležité:** `Workbook` je vstupním bodem pro každou operaci s Excelem. Vytvořením jej jako první zajistíte čistý soubor, který můžete později uložit jako XLSX.

## Krok 2: Nastavení formátu čísla pro určení významných číslic

Aspose.Cells poskytuje globální nastavení nazvané `NumberFormatOptions`. Přiřazením `SignificantDigits = 4` se každá číselná buňka zobrazí až se čtyřmi významnými číslicemi, pokud ji nepřepíše konkrétnější formát.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Proč je to důležité:** Použití `SetNumberFormatOptions` vám umožní definovat **custom number format excel** bez psaní formátového řetězce pro každou buňku. Odpovídá volbě „Significant Digits“, kterou najdete v dialogu Excelu *Formát buněk → Číslo → Vlastní*.

## Krok 3: Zapsání hodnot a ověření vlastního číselného formátu

Nyní vložte číselnou hodnotu do buňky. Globální nastavení automaticky použije pravidlo 4‑ciferných číslic.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

Když otevřete uložený soubor, buňka **A1** zobrazí `123.5` (zaokrouhleno na čtyři významné číslice). Původní hodnota zůstane v podkladových datech nezměněna, což můžete ověřit pohledem na řádek vzorců.

**Tip pro okrajové případy:** Pokud uložíte velmi velké číslo jako `12345678.9`, stejné nastavení zobrazí `1.235E+07` (vědecká notace), protože Excel zvolí nejkompaktnější reprezentaci při zachování čtyř významných číslic.

## Krok 4: Uložení sešitu jako XLSX

Nakonec uložte sešit na disk. Metoda `Save` automaticky zvolí formát souboru podle přípony.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Proč je to důležité:** Uložení jako **XLSX** (`save workbook xlsx`) zajišťuje maximální kompatibilitu s moderními verzemi Excelu, Office 365 a dalšími tabulkovými nástroji.

## Očekávaný výsledek

Otevřete *C:\Temp\SigDigits.xlsx* v Microsoft Excelu. Měli byste vidět:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Původní hodnota: | **123.456789**  |

*Buňka A1* zobrazuje číslo zaokrouhlené na čtyři významné číslice, zatímco *C1* zachovává plnou přesnost pro srovnání.

## Běžné varianty a jak nastavit formát čísla pro konkrétní buňky

### Použití vlastního formátovacího řetězce místo globálních možností

Pokud potřebujete formát, který se použije jen na jeden rozsah, můžete přímo přiřadit formátovací řetězec:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Aplikace nastavení na celý sloupec

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Práce s zápornými čísly

Globální volba `SignificantDigits` funguje jednotně pro kladná i záporná čísla. Pokud chcete odlišné zobrazení pro záporná, kombinujte ji s vlastním formátem:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Profesionální tipy a úskalí

* **Pro tip:** Nastavte možnosti formátu čísla **před** zápisem jakýchkoli dat. Změna nastavení po naplnění buněk neformátuje zpětně existující hodnoty.
* **Dejte pozor na:** Použití `PutValue` s **řetězcem**, který vypadá jako číslo (např. `"123.45"`). Excel jej bude považovat za text a vlastní formát se neuplatní.
* **Poznámka o výkonu:** Globální nastavení jsou nenáročná, ale aplikace stylu na miliony buněk může zvýšit spotřebu paměti. Používejte formátování na úrovni sloupce, pokud je to možné.

## Další kroky

Nyní, když můžete **custom number format excel** soubory s významnými číslicemi, můžete zkoumat:

* **Jak nastavit formát čísla** pro data a měny pomocí `Style.Custom`.
* **Vytváření grafů**, které respektují vaše vlastní formáty.
* **Export do CSV** při zachování číselné přesnosti (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

Tyto témata staví na stejných konceptech `Workbook` a `Worksheet`, které jsou zde předvedeny.

---

**Summary**

Naučili jste se, jak **custom number format excel** pomocí konfigurace `NumberFormatOptions` k **nastavení významných číslic**, vytvořit Excel sešit v C#, zapisovat hodnoty a **uložit sešit jako XLSX** soubor. Kompletní, spustitelný kód výše ukazuje každý krok, vysvětluje, proč je každá část potřebná, a poskytuje tipy pro běžné varianty. Klidně přizpůsobte úryvky svým projektům a experimentujte s dalšími scénáři formátování.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vlastní číselný formát Excel v C# – Kompletní průvodce](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Vytvoření Excel sešitu C# – Omezení významných číslic v Excelu](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [Jak použít číselný formát excel s Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}