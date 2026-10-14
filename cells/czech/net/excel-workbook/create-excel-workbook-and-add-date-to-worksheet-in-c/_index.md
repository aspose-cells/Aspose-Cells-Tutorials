---
category: general
date: 2026-10-13
description: Vytvořte Excel sešit v C# a zapište datum do Excelu pomocí Aspose.Cells.
  Naučte se uložit soubor Excel jako xlsx a přidat datum do listu s kompletním kódem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: cs
lastmod: 2026-10-13
og_description: Vytvořte excelový sešit v C# a zapište datum do Excelu. Postupujte
  podle tohoto kompletního návodu, jak uložit excelový soubor jako xlsx a přidat datum
  do listu pomocí Aspose.Cells.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Vytvořte sešit Excel a přidejte datum do listu – C# krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vytvořte sešit Excel a přidejte datum do listu v C#
url: /cs/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření excel sešitu a přidání data do listu v C#

Pokud potřebujete **vytvořit excel sešit** programově, tento návod vám ukáže, jak **zapsat datum do excelu** a **uložit excel soubor** jako *.xlsx* sešit. Uvidíte kompletní, spustitelný příklad, který parsuje řetězec japonské císařské éry a uloží výsledný `DateTime` do buňky A1.

Práce s Excelem z C# často vyžaduje tři kroky: vytvořit sešit, vložit data do listu a nakonec soubor uložit. Tento tutoriál pokrývá každý krok, vysvětluje, proč je kód napsán takto, a upozorňuje na běžné úskalí, jako je kultuře specifické parsování a oprávnění souborového systému. Na konci budete umět **přidat datum do listu**, **uložit sešit jako xlsx** a přizpůsobit vzor pro jakýkoli typ dat.

> **Předpoklad** – Vzorek používá knihovnu **Aspose.Cells for .NET** (verze 23.10 nebo novější). Nainstalujte ji přes NuGet:

```bash
dotnet add package Aspose.Cells
```

Také potřebujete .NET 6+ SDK a zapisovatelný adresář pro výstupní soubor.

---

## Vytvoření excel sešitu a konfigurace listu

Prvním krokem je vytvořit prázdný sešit a získat jeho výchozí list. Aspose.Cells automaticky vytvoří sešit s jedním listem pojmenovaným „Sheet1“.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Proč je to důležité** – `Workbook` je vstupní bod pro všechny operace s Excelem. Vytvořením bez parametrů získáte čistý sešit, který můžete později **uložit excel soubor** v libovolném formátu.

---

## Parsování japonského císařského data

Japonská císařská data používají symbol éry (např. „R“ pro Reiwa) následovaný dvouciferným rokem. Metoda .NET `DateTime.ParseExact` dokáže tento formát zpracovat, pokud poskytnete vlastní objekt `DateTimeParseOptions`, který parseru říká použít japonský císařský kalendář.

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Vysvětlení** –  
* `gg` čte označení éry (`R` pro Reiwa).  
* `yy` čte dvouciferný rok v rámci této éry.  
* `MM/dd` čte měsíc a den.  

Pokud vynecháte `parseOptions`, parser předpokládá gregoriánský kalendář a vyhodí `FormatException`. Jedná se o běžný okrajový případ při práci s ne‑gregoriánskými kalendáři.

---

## Zapsání data do listu

Nyní, když máte hodnotu `DateTime`, můžete ji umístit do buňky. Aspose.Cells automaticky formátuje buňku podle typu hodnoty.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Proč nastavit styl?** – Bez stylu může Excel zobrazit datum ve výchozím formátu systému, což může být matoucí pro uživatele v jiných localech. Explicitním nastavením `"yyyy-mm-dd"` zajistíte jednotný vzhled.

---

## Uložení excel souboru jako xlsx

Nakonec sešit uložte na disk. Metoda `Save` určuje výstupní formát podle přípony souboru, takže použití „.xlsx“ automaticky spustí formát Office Open XML.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Tip** – Pokud cílový adresář neexistuje nebo nemáte oprávnění k zápisu, `Save` vyhodí `IOException`. Vždy před voláním `Save` ověřte cestu.

---

## Kompletní spustitelný příklad

Níže je celý program, který můžete zkopírovat, vložit a spustit. Obsahuje všechny `using` direktivy, ošetření chyb a komentáře, které objasňují každou operaci.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Očekávaný výsledek**

Když otevřete `JapaneseDate.xlsx`, buňka A1 obsahuje datum **2021‑04‑01** (gregoriánský ekvivalent Reiwa 3 / 04 / 01) zobrazené ve formátu `yyyy‑mm‑dd`.

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="Snímek obrazovky Excel sešitu zobrazujícího japonské císařské datum v buňce A1"}

---

## Časté otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když se změní era (např. Heisei na Reiwa)?* | Kalendář `JapaneseEmperor` automaticky mapuje symboly éry (`H`, `R`, atd.) na správný gregoriánský rozsah, takže stačí aktualizovat vstupní řetězec. |
| *Mohu zapsat více dat v jednom sloupci?* | Ano. Projděte svá data v cyklu a pro každý řádek zavolejte `sheet.Cells[row, column].PutValue(dateValue)`. |
| *Co když potřebuji jiný formát data?* | Změňte `dateStyle.Custom` na libovolný řetězec formátu data v Excelu, např. `"dd-mmm-yyyy"` nebo `"mm/dd/yyyy"`. |
| *Existuje způsob, jak chránit list po zapsání data?* | Použijte `sheet.Protect(ProtectOptions.All, "password")` před uložením. |
| *Jak zacházet s časovými pásmy?* | `DateTime` ukládá UTC nebo místní čas. Před voláním `PutValue` jej převeďte pomocí `DateTime.SpecifyKind` nebo `TimeZoneInfo.ConvertTime`. |

---

## Závěr

Nyní víte, jak **vytvořit excel sešit**, **zapsat datum do excelu**, **přidat datum do listu** a **uložit sešit jako xlsx** pomocí Aspose.Cells v C#. Kompletní příklad demonstruje parsování řetězce japonského císařského kalendáře, aplikaci konzistentního stylu a řešení problémů se souborovým systémem.  

Od tady můžete

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit Excel sešit C# – Přidat komentář a uložit jako XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Vytvořit nový sešit v C# – Přidat vzorec a uložit Excel soubor](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Vytvořit Excel sešit – Zalamovat sloupce a uložit jako XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}