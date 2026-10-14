---
category: general
date: 2026-10-13
description: Excel munkafüzet létrehozása C#-ban, és dátum írása Excelbe az Aspose.Cells
  segítségével. Tanulja meg, hogyan mentse el az Excel fájlt xlsx formátumban, és
  hogyan adjon dátumot a munkalaphoz teljes kóddal.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: hu
lastmod: 2026-10-13
og_description: Excel munkafüzet létrehozása C#-ban és dátum írása az Excelbe. Kövesse
  ezt a teljes útmutatót az Excel fájl xlsx formátumban való mentéséhez és a dátum
  hozzáadásához a munkalaphoz az Aspose.Cells segítségével.
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: Excel munkafüzet létrehozása és dátum hozzáadása a munkalaphoz – C# lépésről‑lépésre
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
title: Excel munkafüzet létrehozása és dátum hozzáadása a munkalaphoz C#‑ban
url: /hu/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása és dátum hozzáadása a munkalaphoz C#-ban

Ha programozott módon **excel munkafüzetet** kell létrehoznod, ez az útmutató megmutatja, hogyan **írj dátumot az excelbe** és **mentsd el az excel fájlt** *.xlsx* munkafüzetként. Egy teljes, futtatható példát látsz, amely egy japán császári korszak karakterláncot dolgoz fel, és az eredményül kapott `DateTime`-ot az A1 cellába helyezi.

Az Excel C#-ból való kezelése gyakran három lépést igényel: a munkafüzet példányosítása, adatok elhelyezése egy munkalapon, és végül a fájl mentése. Ez az útmutató lefedi mindegyik lépést, elmagyarázza, miért így van megírva a kód, és kiemeli a gyakori buktatókat, mint például a kultúrára specifikus feldolgozás és a fájlrendszer jogosultságai. A végére **dátumot adhat a munkalaphoz**, **mentheti a munkafüzetet xlsx formátumban**, és alkalmazhatja a mintát bármilyen adat típusra.

> **Előfeltétel** – A példa a **Aspose.Cells for .NET** könyvtárat használja (23.10 vagy újabb verzió). Telepítsd NuGet-en keresztül:

```bash
dotnet add package Aspose.Cells
```

Szükséged van egy .NET 6+ SDK-ra és egy írható könyvtárra a kimeneti fájl számára.

---

## Excel munkafüzet létrehozása és munkalap konfigurálása

Az első lépés egy üres munkafüzet példányosítása és az alapértelmezett munkalap lekérése. Az Aspose.Cells automatikusan egy, “Sheet1” nevű lapot tartalmazó munkafüzetet hoz létre.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Miért fontos** – A `Workbook` az összes Excel művelet belépési pontja. Ha paraméterek nélkül hozod létre, egy tiszta munkafüzetet kapsz, amelyet később **excel fájlként menthetsz** bármilyen formátumban, amit választasz.

## Japán császári dátum feldolgozása

A japán császári dátumok egy korszak szimbólumot (pl. “R” a Reiwa számára) használnak, amelyet egy kétjegyű év követ. A .NET `DateTime.ParseExact` metódus képes kezelni ezt a formátumot, ha egy egyedi `DateTimeParseOptions` objektumot adsz meg, amely a feldolgozónak a japán császári naptár használatát mondja.

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

**Magyarázat** –  
* `gg` olvassa a korszak jelölőt (`R` a Reiwa esetén).  
* `yy` olvassa a kétjegyű évet az adott korszakban.  
* `MM/dd` olvassa a hónapot és a napot.  

Ha kihagyod a `parseOptions`-t, a feldolgozó a Gergely-naptárat feltételezi, és `FormatException`-t dob. Ez egy gyakori széljegyzet, amikor nem‑Gergely naptárakkal dolgozol.

## Dátum írása a munkalapra

Most, hogy van egy `DateTime` értéked, elhelyezheted egy cellában. Az Aspose.Cells automatikusan formázza a cellát az érték típusa alapján.

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Miért állíts be stílust?** – Stílus nélkül az Excel a rendszer alapértelmezett formátumában jelenítheti meg a dátumot, ami zavaró lehet más helyi beállítású felhasználók számára. Az `"yyyy-mm-dd"` kifejezett meghatározása biztosítja a konzisztens megjelenést.

## Excel fájl mentése xlsx-ként

Végül, mentsd a munkafüzetet lemezre. A `Save` metódus a fájl kiterjesztéséből határozza meg a kimeneti formátumot, így a “.xlsx” használata automatikusan az Office Open XML formátumot indítja.

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Tipp** – Ha a célkönyvtár nem létezik, vagy nincs írási jogosultságod, a `Save` `IOException`-t dob. Mindig ellenőrizd az útvonalat a `Save` hívása előtt.

## Teljes futtatható példa

Az alábbiakban a teljes program található, amelyet másolhatsz, beilleszthetsz és futtathatsz. Tartalmazza az összes `using` direktívát, hibakezelést és megjegyzéseket, amelyek tisztázzák az egyes műveleteket.

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

**Várható eredmény**

Amikor megnyitod a `JapaneseDate.xlsx` fájlt, az A1 cella a **2021‑04‑01** dátumot tartalmazza (a Reiwa 3 / 04 / 01 Gergely-naptári megfelelője), amely a `yyyy‑mm‑dd` formátumban jelenik meg.

![Excel munkafüzet dátummal az A1 cellában](excel-date-screenshot.png){alt="Képernyőkép egy Excel munkafüzetről, amely egy japán császári dátumot mutat az A1 cellában"}

---

## Gyakori kérdések és széljegyzetek

| Kérdés | Válasz |
|----------|--------|
| *Mi van, ha a korszak megváltozik (pl. Heisei-ről Reiwa-ra)?* | A `JapaneseEmperor` naptár automatikusan a korszak szimbólumokat (`H`, `R`, stb.) a megfelelő Gergely-naptári tartományra térképezi, így csak a bemeneti karakterláncot kell frissítened. |
| *Írhatok több dátumot egy oszlopba?* | Igen. Iterálj az adataidon, és minden sorra hívd a `sheet.Cells[row, column].PutValue(dateValue)` metódust. |
| *Mi van, ha más dátumformátumra van szükségem?* | Módosítsd a `dateStyle.Custom` értékét bármely Excel dátumformátumra, például `"dd-mmm-yyyy"` vagy `"mm/dd/yyyy"`. |
| *Van mód a munkalap védelmére a dátum írása után?* | Használd a `sheet.Protect(ProtectOptions.All, "password")` metódust a mentés előtt. |
| *Hogyan kezelem az időzónákat?* | A `DateTime` UTC vagy helyi időt tárol. Konvertáld a `DateTime.SpecifyKind` vagy `TimeZoneInfo.ConvertTime` segítségével, mielőtt meghívnád a `PutValue`-t. |

## Összegzés

Most már tudod, hogyan **excel munkafüzetet hozhatsz létre**, **dátumot írhatsz az excelbe**, **dátumot adsz a munkalaphoz**, és **mentheted a munkafüzetet xlsx-ként** az Aspose.Cells használatával C#-ban. A teljes példa bemutatja egy japán császári naptár karakterlánc feldolgozását, egy konzisztens stílus alkalmazását, és a fájlrendszeri kérdések kezelését.  

Innen tovább

## Mi legyen a következő tanulnivalód?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljesen működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Excel munkafüzet létrehozása C# – Megjegyzés hozzáadása és mentés XLSX-ként](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Új munkafüzet létrehozása C#-ban – Képlet hozzáadása és Excel fájl mentése](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel munkafüzet létrehozása – Oszlopok tördelése és mentés XLSX-ként](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}