---
category: general
date: 2026-07-13
description: Konverze japonského kalendáře v C# s krok‑za‑krokem kódem. Naučte se,
  jak extrahovat DateTime z Excelu a efektivně pracovat s japonskými érami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- japanese calendar conversion
- extract datetime from excel
- excel date parsing c#
- aspnet excel cultureinfo
- japanese era date handling
language: cs
lastmod: 2026-07-13
og_description: Japonská konverze kalendáře v C# vysvětlená. Ovládněte získávání DateTime
  z buněk Excelu a převod japonských era řetězců na gregoriánská data.
og_image_alt: Code screenshot illustrating Japanese calendar conversion in a C# console
  app
og_title: Převod japonského kalendáře v C# – Kompletní programovací průvodce
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  headline: Japanese Calendar Conversion in C# – Full Guide
  type: TechArticle
- description: Japanese calendar conversion in C# with step‑by‑step code. Learn how
    to extract DateTime from Excel and handle Japanese era dates efficiently.
  name: Japanese Calendar Conversion in C# – Full Guide
  steps:
  - name: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
    text: Recognizes era names (e.g., *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
  - name: Parses the year number relative to the era’s start.
    text: Parses the year number relative to the era’s start.
  - name: Constructs the corresponding Gregorian `DateTime`.
    text: Constructs the corresponding Gregorian `DateTime`.
  type: HowTo
tags:
- C#
- Excel
- DateTime
- Localization
title: Převod japonského kalendáře v C# – Kompletní průvodce
url: /cs/net/excel-custom-number-date-formatting/japanese-calendar-conversion-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japonská konverze kalendáře v C# – Kompletní průvodce

Potřebovali jste někdy **japanese calendar conversion** při načítání dat z Excelu? Nejsi jediný, kdo se trápí s tím, jak převést „Reiwa 3‑04‑01“ na správný .NET `DateTime`. V tomto tutoriálu vás provedeme čistým, end‑to‑end řešením, které nejen převádí japonské datumy epoch, ale také vám ukáže, jak **extract datetime from excel** buňky pomocí Aspose.Cells. Na konci budete mít připravenou konzolovou aplikaci a solidní pochopení, proč jsou nastavení kultury důležitá.

## Požadavky

- .NET 6.0 nebo novější (kód funguje jak na .NET Core, tak na .NET Framework)
- Aspose.Cells pro .NET (bezplatná zkušební NuGet balíček `Aspose.Cells`)
- Základní znalost C# a konzolových aplikací
- Excel soubor (nebo nový sešit), kde je datum uloženo jako řetězec v japonském formátu epoch

Pokud vám něco z toho chybí, stáhněte si NuGet balíček pomocí:

```bash
dotnet add package Aspose.Cells
```

Teď se ponořme.

## Krok 1: Vytvořte sešit a nastavte japonskou kulturu

První věc, kterou musíte udělat, je říct Aspose.Cells, že sešit by měl interpretovat data pomocí japonského kalendáře. Zde **japanese calendar conversion** skutečně začíná.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook instance
        Workbook workbook = new Workbook();

        // 2️⃣ Apply Japanese culture (Japanese calendar) to the workbook settings
        workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

        // The rest of the steps follow...
```

**Proč je to důležité:** `CultureInfo` nese nejen jazyk, ale také informace o kalendáři. Přepnutím na `"ja-JP-u-ca-japanese"` umožníme knihovně rozpoznat názvy epoch jako *Reiwa* nebo *Heisei*, když se objeví v buňkách.

## Krok 2: Zapište japonské datum epochy do buňky

Pro demonstraci vložíme japonský řetězec epochy přímo do buňky **A1**. V reálném scénáři pravděpodobně načítáte existující sešit, ale princip zůstává stejný.

```csharp
        // 3️⃣ Write a Japanese era date string into cell A1 (row 0, column 0)
        workbook.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");
```

> **Pro tip:** Pokud zdrojový Excel již ukládá data jako správná Excelová sériová čísla, můžete krok `PutValue` přeskočit a jít rovnou k extrakci. Logika konverze funguje v obou případech.

## Krok 3: Extrahujte DateTime z Excelu – Jádro „extract datetime from excel“

Nyní přichází část, kde **extract datetime from excel**. Aspose.Cells poskytuje pohodlnou metodu `GetDateTime`, která respektuje nastavení kultury sešitu.

```csharp
        // 4️⃣ Retrieve the cell value as a .NET DateTime object
        DateTime gregorianDate = workbook.Worksheets[0].Cells[0, 0].GetDateTime();
```

V pozadí Aspose zohlední dříve nastavenou kulturu, parsuje „Reiwa 3‑04‑01“ a vrátí ekvivalentní gregoriánské datum (`2021‑04‑01`).

## Krok 4: Zobrazte výsledek

Nakonec vytiskněme převedené datum do konzole, abyste mohli ověřit, že **japanese calendar conversion** byla úspěšná.

```csharp
        // 5️⃣ Show the converted Gregorian date
        Console.WriteLine(gregorianDate.ToString("yyyy‑MM‑dd"));
        // Expected output: 2021‑04‑01
    }
}
```

Spusťte program (`dotnet run`) a měli byste vidět:

```
2021‑04‑01
```

To je celý cyklus: vytvořit sešit, nastavit japonskou kulturu, zapsat datum epochy, extrahovat `DateTime` a zobrazit jej.

---

## Podrobný pohled: Jak funguje japonský kalendář v .NET

Japonský kalendář je *lunisolární* systém, který seskupuje roky do epoch pojmenovaných podle vládnoucího císaře. Třída `JapaneseCalendar` v .NET mapuje každou epochu na rozsah gregoriánských let. Když požádáte o `CultureInfo`, který obsahuje `-u-ca-japanese`, runtime automaticky:

1. Rozpozná názvy epoch (např. *Meiji*, *Taishō*, *Shōwa*, *Heisei*, *Reiwa*).
2. Rozparsuje číslo roku relativně k začátku epochy.
3. Vytvoří odpovídající gregoriánský `DateTime`.

Pokud někdy potřebujete převést opačným směrem—z gregoriánského na japonskou epochu—můžete použít:

```csharp
var japaneseCal = new System.Globalization.JapaneseCalendar();
int era = japaneseCal.GetEra(gregorianDate);
string eraName = japaneseCal.Eras[era - 1]; // .Eras is zero‑based
int yearInEra = japaneseCal.GetYear(gregorianDate);
Console.WriteLine($"{eraName} {yearInEra:D2}-{gregorianDate:MM-dd}");
```

### Řešení okrajových případů

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|---------------|
| **Chybějící název epochy** (např. “03‑04‑01”) | `GetDateTime` vyhodí `FormatException`. | Předvalidujte řetězec nebo přejděte na `DateTime.ParseExact` s vlastním vzorem. |
| **Budoucí epocha** (nový císař) | Aktuální `JapaneseCalendar` nemusí znát novou epochu až do aktualizace OS. | Aktualizujte .NET runtime nebo použijte vlastní mapovací tabulku, dokud OS nedojde k aktualizaci. |
| **Smíšené kalendáře v jednom sešitu** | Některé buňky mohou používat gregoriánský kalendář, zatímco jiné japonský. | Nastavte `CultureInfo` na buňku pomocí `cell.Style.CultureInfo`, pokud je to potřeba. |

## Extrahování DateTime z existujících Excel souborů

Pokud již máte soubor `.xlsx` s japonskými daty, kód pro extrakci je téměř stejný—stačí nahradit vytvoření sešitu voláním načtení:

```csharp
Workbook workbook = new Workbook("Path/To/YourFile.xlsx");
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

// Assuming the date is in B2 (row 1, column 1)
DateTime dateFromFile = workbook.Worksheets[0].Cells[1, 1].GetDateTime();
Console.WriteLine(dateFromFile);
```

Všimněte si, že **extract datetime from excel** zůstává stejným voláním metody; jediný další krok je načtení souboru.

---

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní program, který můžete vložit do konzolového projektu. Obsahuje všechny potřebné `using` direktivy, komentáře a zpracování chyb pro profesionální úroveň.

```csharp
using System;
using Aspose.Cells;

class JapaneseCalendarDemo
{
    static void Main()
    {
        try
        {
            // Initialize workbook
            Workbook wb = new Workbook();

            // Apply Japanese calendar culture
            wb.Settings.CultureInfo = new System.Globalization.CultureInfo("ja-JP-u-ca-japanese");

            // Insert a Japanese era date string (could be read from an existing file)
            wb.Worksheets[0].Cells[0, 0].PutValue("Reiwa 3-04-01");

            // Extract as .NET DateTime – this is the core of "extract datetime from excel"
            DateTime gregDate = wb.Worksheets[0].Cells[0, 0].GetDateTime();

            // Output in ISO format
            Console.WriteLine(gregDate.ToString("yyyy-MM-dd"));
        }
        catch (Exception ex)
        {
            // Simple error handling – in real apps you might log this
            Console.Error.WriteLine($"Error during conversion: {ex.Message}");
        }
    }
}
```

**Očekávaný výstup v konzoli**

```
2021-04-01
```

Spusťte jej a uvidíte gregoriánské datum, které odpovídá vstupnímu japonskému datu epochy.

## Často kladené otázky

**Q: Funguje to i se staršími soubory Excel (.xls)?**  
Ano. Aspose.Cells abstrahuje formát souboru, takže stejné volání `GetDateTime` funguje pro `.xls` i `.xlsx`.

**Q: Co když buňka obsahuje skutečné Excelové datum (sériové číslo) místo řetězce?**  
Aspose i nadále respektuje kulturu sešitu a vrátí správný gregoriánský `DateTime`. Žádné další parsování není potřeba.

**Q: Mohu najednou převést celý sloupec japonských dat?**  
Určitě. Projděte řádky ve smyčce:

```csharp
for (int i = 0; i < worksheet.Cells.MaxDataRow + 1; i++)
{
    DateTime dt = worksheet.Cells[i, 0].GetDateTime();
    // Do something with dt
}
```

**Q: Má nastavení kultury vliv na výkon?**  
Negligibilní pro typické datové sady. Kultura se aplikuje jednou na sešit, ne na každou buňku.

## Závěr

Právě jsme dokončili průvodce **japanese calendar conversion**, který přesně ukazuje, jak **extract datetime from excel** pomocí Aspose.Cells. Nastavením `CultureInfo` sešitu na `"ja-JP-u-ca-japanese"` odemknete bezproblémové parsování řetězců epoch, jako je *Reiwa 3‑04‑01*, na standardní .NET `DateTime` objekty. Kód je kompaktní, robustní a připravený pro produkci.

Co dál? Zkuste načíst reálný sešit, převést celý sloupec nebo dokonce zapsat gregoriánská data zpět do nového listu. Můžete také prozkoumat jiné lokály—francouzský republikánský kalendář, islámský hijri kalendář—výměnou řetězce kultury. Vzor zůstává stejný.

Máte vlastní tip, který chcete sdílet? Zanechte komentář a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Ovládněte systém dat 1904 v Excelu pomocí Aspose.Cells Java pro efektivní operace s buňkami](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Převod odkazů na buňky v Excelu pomocí Aspose.Cells .NET: Komplexní průvodce](/cells/english/net/cell-operations/excel-cell-reference-conversion-aspose-cells-net/)
- [Ovládněte konverzi HTML do Excelu pomocí Aspose.Cells pro .NET](/cells/english/net/workbook-operations/aspose-cells-net-html-layout-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}