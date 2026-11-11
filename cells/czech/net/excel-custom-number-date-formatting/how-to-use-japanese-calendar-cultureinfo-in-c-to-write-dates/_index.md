---
category: general
date: 2026-10-26
description: Naučte se, jak v C# použít CultureInfo japonského kalendáře při parsování
  dat epoch a jejich vkládání do listu Excelu pomocí NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: cs
lastmod: 2026-10-26
og_description: Použijte v C# CultureInfo japonského kalendáře k parsování dat z éry
  Reiwa a zapište je do listu Excel. Kompletní, spustitelný kód s vysvětlením.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Použijte japonský kalendář CultureInfo v C# – kompletní příklad v Excelu
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: Jak použít japonský kalendář CultureInfo v C# k zápisu dat do Excelu
url: /cs/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít CultureInfo japonského kalendáře v C# pro zápis dat do Excelu

Pokud potřebujete **používat CultureInfo japonského kalendáře** při práci s daty v C#, tento průvodce vám přesně ukáže, jak na to. Naučíte se rozparsovat řetězec data, který obsahuje japonský název éry (například *Reiwa 2/5/1*), a poté zapsat vzniklý `DateTime` do první buňky listu Excelu pomocí knihovny NPOI.

Parsování dat založených na éře bez správného `CultureInfo` vede k `FormatException` nebo nesprávným hodnotám měsíce/dne. Nastavením `CultureInfo` na japonský kalendář zajistíte, že .NET runtime interpretuje éru správně a že hodnota uložená v Excelu odpovídá původnímu japonskému zápisu.

V tomto tutoriálu se naučíte:

* Vytvořit objekt `CultureInfo`, který používá japonský kalendář.
* Rozparsovat řetězec data japonské éry pomocí `DateTime.Parse`.
* Vložit rozparsovaný `DateTime` do buňky listu NPOI.
* Zobrazit kompletní spustitelný program a očekávaný výstup.

> **Požadavky** – .NET 6.0+ (nebo .NET Core 3.1+), balíček **NPOI** NuGet a základní znalost C# a práce se soubory Excel.

---

## Co budete potřebovat

| Položka | Důvod |
|------|--------|
| **.NET SDK** (6.0 or later) | Poskytuje runtime a knihovny pro `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Umožňuje vytvářet a manipulovat se soubory Excel bez nainstalovaného Office. |
| **Visual Studio Code**, **Visual Studio**, or any C# IDE | Pro kompilaci a spuštění příkladu. |
| **Japanese era date string** (e.g., `"Reiwa 2/5/1"`) | Ukazuje použití japonského kalendáře. |

---

## Krok 1: Instalace NPOI

Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package NPOI --version 2.6.1
```

Balíček poskytuje typy `IWorkbook`, `ISheet` a `ICell`, které jsou použity později.

---

## Krok 2: Vytvoření CultureInfo, který používá japonský kalendář

Japonský kalendář je kalendář založený na érách. Musíte požádat o *japonskou* variantu locale `ja-JP` a explicitně nastavit kalendář na `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Proč je to důležité** – Výchozí kultura `ja-JP` používá gregoriánský kalendář. Přidělením vlastnosti `Calendar` zajistíte, že názvy éry jako *Reiwa* jsou při parsování rozpoznány.

---

## Krok 3: Parsování řetězce data japonské éry

Nyní, když je `CultureInfo` nakonfigurován, můžete bezpečně parsovat řetězec, který obsahuje název éry.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Výstup**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse` metoda interpretuje *Reiwa 2* jako gregoriánský rok 2020, měsíc 5, den 1.

### Okrajový případ: zpracování neplatných éry

Pokud uživatel zadá nepodporovanou éru (např. `"Heisei 31/4/30"` po ukončení éry Heisei), `DateTime.Parse` vyhodí `FormatException`. Zabalte volání do bloku try‑catch, aby se zobrazila přátelská chybová zpráva:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Krok 4: Zapsání rozparsovaného DateTime do listu Excel

S připraveným objektem `DateTime` jej můžete uložit do buňky Excelu. NPOI automaticky formátuje hodnoty `DateTime` jako data v Excelu.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Výsledek** – Po otevření *JapaneseEraDate.xlsx* se v buňce A1 zobrazí datum **2020‑05‑01**.

### Proč používat NPOI?

*Funguje na jakékoli platformě* (Windows, Linux, macOS) a **nevyžaduje** Microsoft Office. To činí řešení vhodným pro CI pipeline, Docker kontejnery nebo server‑side zpracování.

---

## Krok 5: Kompletní spustitelný program

Když spojíme vše dohromady, zde je kompletní konzolová aplikace, která demonstruje celý tok:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Jak spustit**

```bash
dotnet run
```

Po spuštění najdete `JapaneseEraDate.xlsx` ve složce projektu s korektně parsovaným datem.

---

## Časté úskalí a tipy na nejlepší postupy

| Problém | Řešení / Doporučení |
|---------|----------------------|
| Zapomenutí nastavit `japaneseCulture.DateTimeFormat.Calendar` | Vždy přiřaďte instanci `JapaneseCalendar`; jinak není název éry rozpoznán. |
| Použití `DateTime.TryParse` bez vlastního `CultureInfo` | Předávejte stejný `japaneseCulture` do `TryParse`, aby chování zůstalo konzistentní. |
| Očekávání, že Excel zobrazí název éry | Vestavěné formáty data v Excelu jsou pouze gregoriánské. Pokud potřebujete zobrazit éru, uložte původní řetězec do samostatného sloupce nebo vytvořte vlastní textový formát. |
| Nedispozice `FileStream` | Použijte blok `using` (jak je ukázáno), aby byl souborový handle uvolněn okamžitě. |
| Míchání objektů `CultureInfo` napříč vlákny | `CultureInfo` je vlákny‑bezpečný pro operace pouze ke čtení, ale vyhněte se změně jeho vlastnosti `Calendar` po počátečním nastavení. |

---

## Závěr

Nyní víte, jak **používat CultureInfo japonského kalendáře** v C# k přesnému parsování dat japonských éry a zápisu výsledného `DateTime` do listu Excelu pomocí NPOI. Kompletní příklad zahrnuje konfiguraci, parsování, zpracování chyb a výstup do Excelu, což vám poskytuje pevný základ pro jakýkoli internacionalizovaný reporting nebo scénář výměny dat.

Dále můžete zkoumat:

* **Formátování dat pomocí vlastního textu** pro zachování názvu éry v Excelu.
* **Čtení dat z Excelu** pomocí `cell.DateCellValue` s ohledem na japonský kalendář.
* **Použití stejné techniky** pro jiné kalendáře založené na érách (např. thajský buddhistický kalendář) výměnou `JapaneseCalendar` za odpovídající podtřídu `Calendar`.

Neváhejte experimentovat s různými řetězci éry, většími datovými sadami nebo integrovat tuto logiku do ASP.NET Core API, které generují Excelové reporty za běhu. Šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Vytvořit Excel sešit s daty japonského kalendáře – Kompletní průvodce](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parsování japonských dat podle éry v Excelu – Kompletní průvodce pro vývojáře C#](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [Jak vytvořit Excel sešit a parsovat japonská data v C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}