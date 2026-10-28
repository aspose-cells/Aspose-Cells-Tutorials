---
category: general
date: 2026-08-11
description: Vytvořte programově soubor Excel v C# pomocí Aspose.Cells. Rozparsujte
  japonské datum v éře, zapište jej do buňky a uložte sešit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel file programmatically
- datetime.parseexact custom format
- write date to excel cell
- how to save excel file c#
language: cs
lastmod: 2026-08-11
og_description: Vytvořte programově soubor Excel v C# pomocí Aspose.Cells. Naučte
  se, jak pomocí vlastního formátu DateTime.ParseExact parsovat japonské datum podle
  éry, zapsat datum do buňky Excelu a efektivně uložit sešit.
og_image_alt: Screenshot of an Excel workbook with a parsed Japanese era date in cell
  A1
og_title: Vytvořte Excel soubor programově v C# – kompletní návod
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel file programmatically in C# using Aspose.Cells. Parse
    a Japanese era date, write it to a cell, and save the workbook.
  headline: Create excel file programmatically in C# – tutorial
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- DateTime parsing
title: Vytvoření souboru Excel programově v C# – návod
url: /cs/net/excel-file-handling/create-excel-file-programmatically-in-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Excel souboru programově v C# – tutoriál

Pokud potřebujete **vytvořit excel soubor programově**, můžete to udělat v několika řádcích C# kódu. Tento průvodce vám ukáže, jak vygenerovat Excel sešit pomocí Aspose.Cells, parsovat japonské datum éry pomocí **DateTime.ParseExact vlastního formátu**, zapsat toto datum do buňky listu a nakonec **uložit Excel soubor v C#** stylu. Na konci budete mít připravený *.xlsx* soubor, který obsahuje správně převedené gregoriánské datum.

Naučíte se, jak:

* Inicializovat sešit bez šablony.  
* Převést řetězec založený na éře, např. `"R3/04/01"`, na `DateTime`.  
* Vložit hodnotu `DateTime` do konkrétní buňky (`A1`).  
* Uložit sešit na disk jedním voláním `Save`.

Žádné další knihovny kromě Aspose.Cells a .NET základní knihovny tříd nejsou vyžadovány.

---

## Předpoklady

* **.NET 6.0** nebo novější nainstalovaný (kód také funguje s .NET Framework 4.6+).  
* Platná licence **Aspose.Cells** nebo bezplatná evaluační kopie.  
* Základní znalost syntaxe C# a Visual Studia (nebo libovolného IDE, které preferujete).

---

## Vytvoření excel souboru programově – inicializace sešitu

Prvním krokem je vytvořit prázdný objekt sešitu. Aspose.Cells poskytuje třídu `Workbook`, která představuje celý Excel soubor v paměti.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();               // creates an empty .xlsx structure
        var worksheet = workbook.Worksheets[0];      // the default first sheet is named "Sheet1"
```

**Proč je to důležité:**  
Vytvoření sešitu programově eliminuje potřebu fyzického souboru šablony, což udržuje nasazovací stopu malou a umožňuje generovat soubory za běhu pro zprávy, faktury nebo export dat.

---

## Použití DateTime.ParseExact vlastního formátu pro japonská data éry

Řetězce datumů, které obsahují japonské symboly éry (např. `"R"` pro Reiwa), nelze parsovat pomocí výchozího `DateTime.Parse`. Musíte poskytnout **vlastní formát** a japonskou kulturu, která rozpozná označení éry.

```csharp
        // Step 2: Define the era‑based date string (Reiwa 3, April 1)
        string eraDate = "R3/04/01";

        // Step 3: Create a CultureInfo that knows Japanese eras
        var japaneseCulture = new CultureInfo("ja-JP");

        // Step 4: Parse the era date using a custom format string
        //   "g"  = era designator (R, H, etc.)
        //   "yy" = two‑digit year within the era
        //   "MM" = month (01‑12)
        //   "dd" = day of month (01‑31)
        DateTime parsedDate = DateTime.ParseExact(
            eraDate,
            "ggy/MM/dd",
            japaneseCulture,
            DateTimeStyles.None);
```

**Proč je to důležité:**  
`DateTime.ParseExact` zajišťuje, že vstup odpovídá zadanému vzoru, čímž zabraňuje nejednoznačnostem závislým na locale. Vzor `"ggy/MM/dd"` říká .NET, aby první znak považoval za éru (`g`), následovaný dvouciferným rokem (`yy`), měsícem a dnem. Použití `japaneseCulture` zajišťuje správnou interpretaci symbolů éry, což vede k gregoriánskému `DateTime` (`2021‑04‑01` v příkladu).

---

## Zapsání data do buňky Excelu pomocí Aspose.Cells

Nyní, když máte instanci `DateTime`, můžete ji umístit do libovolné buňky listu. Aspose.Cells automaticky formátuje buňku podle výchozího datového stylu sešitu.

```csharp
        // Step 5: Write the DateTime value into cell A1
        worksheet.Cells["A1"].PutValue(parsedDate);

        // Optional: Apply a custom number format if you want a specific display
        worksheet.Cells["A1"].Style.Number = 14; // 14 = "m/d/yyyy" in Excel
```

**Proč je to důležité:**  
Použití `PutValue` umožňuje Aspose.Cells odvodit typ buňky (datum, číslo, text) z .NET typu, který poskytnete. Tento přístup je bezpečnější než zapisování formátovaného řetězce, protože Excel zachová datumovou semantiku—umožňuje řazení, filtrování nebo provádění výpočtů ve sloupci později.

---

## Jak uložit excel soubor v C# – dokončení sešitu

Posledním krokem je uložení sešitu z paměti do fyzického souboru. Aspose.Cells podporuje mnoho formátů; zde používáme moderní formát `.xlsx`.

```csharp
        // Step 6: Save the workbook to the desired location
        string outputPath = @"C:\Temp\JapaneseEra.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Proč je to důležité:**  
Volání `Save` s `SaveFormat.Xlsx` zapíše standardy splňující soubor Office Open XML, který lze otevřít v Excelu, LibreOffice nebo v jakémkoli prohlížeči podporujícím tento formát. Metoda také zajišťuje veškerou podkladovou kompresi a balení, takže nemusíte sami spravovat zip streamy.

---

## Očekávaný výsledek

Když spustíte program:

| Buňka | Zobrazená hodnota | Skrytý typ |
|------|-------------------|------------|
| A1   | 4/1/2021          | Date (DateTime) |

Soubor `JapaneseEra.xlsx` bude obsahovat jediný list pojmenovaný **Sheet1** s gregoriánským datem `2021‑04‑01` v buňce **A1**. Excel bude buňku považovat za datum, což umožní další výpočty, např. `=A1+30` pro přidání 30 dnů.

---

## Běžné varianty a okrajové případy

| Situace | Řešení |
|-----------|----------|
| **Různá éra** (např. Heisei `H30/12/31`) | Změňte vstupní řetězec; stejný vzor `"ggy/MM/dd"` funguje, protože japonský `CultureInfo` zná všechny éry. |
| **Čtyřciferný rok** (např. `"R2023/04/01"`) | Použijte `"ggyyyy/MM/dd"` jako formátovací řetězec. |
| **Chybějící symbol éry** | Poskytněte náhradní formát jako `"yyyy/MM/dd"` a zkuste `DateTime.TryParseExact` s více vzory. |
| **Neplatné datum** (např. `"R3/13/01"`) | Zabalte `ParseExact` do bloku `try/catch` nebo použijte `DateTime.TryParseExact` pro elegantní zpracování selhání parsování. |

**Tip:** Vždy ověřte parsovaný `DateTime` před zápisem do listu, zejména pokud data pocházejí od uživatele nebo z externích souborů.

---

## Shrnutí

* Vytvořili jste **excel soubor programově** pomocí Aspose.Cells.  
* Parsovali jste japonský řetězec éry pomocí **DateTime.ParseExact vlastního formátu**.  
* Zapsali jste **datum do excel buňky** pomocí `PutValue`.  
* Naučili jste se **jak uložit excel soubor v C#** jedním voláním `Save`.

Tyto čtyři kroky tvoří znovupoužitelný vzor pro jakýkoli scénář, kde potřebujete importovat kulturně specifická data do Excelových reportů.

---

## Další kroky

* Prozkoumejte **stylování buněk** (písma, barvy, okraje), aby vaše reporty vypadaly profesionálně.  
* Použijte **Workbook.Save** s jinými formáty (`Csv`, `Pdf`) pro export dat různým publikům.  
* Kombinujte tuto techniku s **hromadným vkládáním dat** (`Cells.ImportDataTable`) pro rozsáhlé importy.  

Neváhejte experimentovat s různými symboly éry, vlastními číselnými formáty nebo více listy. Stejná základní logika—vytvořit, parsovat, zapsat, uložit—platí pro všechny úlohy automatizace Excelu v C#.

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak vytvořit a uložit Excel sešit jako ODS pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Jak uložit konkrétní stránky Excel souboru jako PDF pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Jak vytvořit a uložit Excel sešit jako SVG pomocí Aspose.Cells pro Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}