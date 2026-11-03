---
category: general
date: 2026-10-01
description: Tanulja meg, hogyan hozhat létre Excel munkafüzetet C#-ban, alkalmazzon
  egyéni számformátumot, állítsa be a cellák tizedesjegyeit, és mentse a munkafüzetet
  XLSX formátumban egy teljes lépésről‑lépésre útmutatóban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: hu
lastmod: 2026-10-01
og_description: Excel munkafüzet létrehozása C#-ban egyedi számformátummal, a cellák
  tizedesjegyeinek beállítása, és a munkafüzet mentése XLSX formátumban. Kövesse ezt
  a teljes útmutatót a pontos numerikus kimenet érdekében.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Excel munkafüzet létrehozása C#‑ban – egyéni számformátum és XLSX export
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hogyan készítsünk Excel munkafüzetet C#-ban egyedi számformázással
url: /hu/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozzunk létre Excel munkafüzetet C#‑ban egyedi számformázással

Ha **excel workbook c#**‑t kell létrehoznod, amely a számokat pontosan úgy jeleníti meg, ahogy szeretnéd, ez az útmutató néhány egyszerű lépésben megmutatja, hogyan teheted meg. Megtanulod, hogyan alkalmazz egyedi számformátumot, hogyan állíts be tizedesjegyeket a cellában, és végül hogyan **save workbook as xlsx** a további felhasználáshoz.

A numerikus adatok kezelése gyakran a pontosság és az olvashatóság egyensúlyát jelenti. A tutorial végére egy újrahasználható mintát kapsz, amely a megjelenített számjegyeket egy meghatározott számú jelentős számjegyre korlátozza, miközben az eredeti érték megmarad a fájlban. Nem szükséges külső szkript – csak C# és az Aspose.Cells könyvtár.

## Előkövetelmények

Mielőtt elkezdenéd, győződj meg róla, hogy a következők telepítve vannak:

* .NET 6.0 SDK vagy újabb  
* Visual Studio 2022 (vagy bármely C# IDE)  
* A **Aspose.Cells for .NET** NuGet csomag (`Install-Package Aspose.Cells`) – ez a könyvtár biztosítja a `Workbook`, `Worksheet` és `ExportTableOptions` osztályokat, amelyeket a példákban használunk.  

Ezek a követelmények minimálisak; ugyanaz a kód működik .NET Core, .NET Framework és akár Azure Functions környezetben is.

## 1. lépés: Excel munkafüzet létrehozása C#‑ban – a fájl inicializálása

Az első művelet egy új `Workbook` objektum példányosítása. Ez az objektum a teljes Excel fájlt reprezentálja a memóriában, és automatikusan tartalmaz egy alapértelmezett munkalapot.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Miért fontos:**  
A munkafüzet előzetes létrehozása tiszta vásznat biztosít. Az alapértelmezett munkalap (`Worksheets[0]`) készen áll az adatok bevitelére, így nem kell új lapot hozzáadnod, hacsak a szituációd nem igényel több fület.

## 2. lépés: Numerikus érték írása egy cellába

Most helyezz egy mintaszámot az **A1** cellába. A használt érték (`123.456789`) több tizedesjegyet tartalmaz, mint amennyit végül meg szeretnénk jeleníteni, ezáltal lehetővé téve a későbbi kerekítést.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tipp:** A `PutValue` automatikusan felismeri az adat típusát, így nem kell a számot karakterlánccá konvertálni.

## 3. lépés: Egyedi számformátum alkalmazása – látható tizedesjegyek korlátozása

Az Excel megjelenítésének szabályozásához egy `Style` objektumot hozunk létre **egyedi számformátummal**. A `"0.######"` minta azt mondja az Excelnek, hogy legfeljebb hat tizedesjegyet jelenítsen meg, de a felesleges nullákat hagyja el.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**Hogyan működik:**  
A formátumkarakterlánc az Excel egyedi formátum szintaxisát követi. A `0` kötelező számjegyet kényszerít, míg a `#` csak akkor jelenít meg számjegyet, ha az jelentős. Ezek kombinálásával rugalmas megjelenítést kapsz, amely még mindig tiszteletben tartja az eredeti pontosságot.

## 4. lépés: Cellatizedesjegyek beállítása – ExportTableOptions használatával

Ha **set cell decimal places**‑t kell megadnod az exportált adatokhoz (például DataTable konvertálásakor), az Aspose.Cells lehetővé teszi a **significant digits** számának megadását. Ez a lépés biztosítja, hogy a CSV vagy DataTable ugyanazt a kerekítési szabályt kövesse, mint a munkafüzetben.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Miért a `SignificantDigits`?**  
A fix tizedesjegy számával ellentétben a jelentős számjegyek megőrzik a szám nagyságrendjét, miközben a pontosságot korlátozzák – ez gyakran az, amit az elemzők elvárnak az adatok összegzésénél.

## 5. lépés: A munkalap adatainak exportálása és **save workbook as xlsx**

Végül exportáljuk az adatokat (ha szükség van DataTable-re), és elmentjük a munkafüzetet a lemezen. Az `ExportDataTable` hívás figyelembe veszi a konfigurált `ExportTableOptions`‑t, a `workbook.Save` pedig egy szabványos XLSX fájlt ír.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Várható eredmény:**  
Amikor megnyitod a *SigDigits.xlsx* fájlt Excelben, az **A1** cella `123.5`‑öt mutat. Az alaptárolt érték továbbra is `123.456789`, de a megjelenített szám a 4‑jelentős‑szám szabályt követi. Ha a lapot DataTable‑be exportálod, a táblázatban is `123.5` lesz a érték.

---

## Egyedi számformátum alkalmazása további cellákra

Ha egy tartományt kell formázni egyetlen cella helyett, újrahasználhatod a `Style` objektumot:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tipp:** A stílusobjektum újrahasználata csökkenti a memóriaigényt és garantálja a konzisztens formázást a teljes munkalapon.

## Hogyan formázzuk a számokat Excelben C#‑bal – gyakori variációk

| Forgatókönyv | Formátum karakterlánc | Eredmény |
|--------------|-----------------------|----------|
| Két tizedesjegy rögzítve | `"0.00"` | `123.46` |
| Pénznem (US) | `"$#,##0.00"` | `$123.46` |
| Százalék egy tizedessel | `"0.0%"` | `12,346.0%` |
| Tudományos jelölés | `"0.00E+00"` | `1.23E+02` |

Válaszd ki azt a mintát, amely a jelentési igényeidnek megfelel. Minden minta kompatibilis a korábban bemutatott `Style.Custom` tulajdonsággal.

## Cellatizedesjegyek dinamikus beállítása felhasználói bemenet alapján

Néha a szükséges pontosság nem ismert fordítási időben. A formátumkarakterláncot futásidőben is összeállíthatod:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Szél eset:** Ha a `decimals` értéke nulla, a formátum `"0"` lesz (egész szám megjelenítés). Mindig ellenőrizd a felhasználói bemenetet, hogy elkerüld a hibás formátumkarakterláncok létrejöttét.

## Save workbook as XLSX – legjobb gyakorlatok

* **Használj abszolút útvonalakat** a jól meghatározott könyvtárba íráskor (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** a `Workbook`‑ot, ha `using` blokkban használod, hogy a nem kezelt erőforrások gyorsan felszabaduljanak:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Verziókompatibilitás:** Az Aspose.Cells olyan fájlokat ír, amelyek kompatibilisek az Excel 2010‑2023‑mal, így a downstream felhasználók nem fognak formátumproblémákkal szembesülni.

---

## Teljes működő példa

Az alábbiakban a teljes programot találod, amelyet másolhatsz, beilleszthetsz és azonnal futtathatsz. Tartalmazza az összes szükséges `using` direktívát, megjegyzéseket és hibakezelést.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Ellenőrző lépések**

1. Futtasd a programot (`dotnet run`).  
2. Nyisd meg a `SigDigits.xlsx` fájlt.  
3. Ellenőrizd, hogy az **A1** `123.5`‑öt mutat.  
4. Ha megnyitod a fájl XML‑ét (`.xlsx` egy zip archívum), látni fogod a `"0.######"` egyedi formátumot a `<c>` elem `s` attribútumában tárolva.

---

## Összegzés

Ebben a tutorialban megtanultad, hogyan **create excel workbook c#**, **apply custom number format**, **set cell decimal places**, és **save workbook as xlsx** az Aspose.Cells segítségével. A megoldás mind a vizuális formázást Excelben, mind az adat‑export kerekítést demonstrálja a `ExportTableOptions`‑on keresztül.

Innen tovább:

* Bővítsd a megközelítést teljes tartományokra vagy táblázatokra.  
* Kombináld több stílust (betűtípusok, szegélyek) a `StyleFlag`‑kel.  
* Automatizáld a jelentéskészítést úgy, hogy adatforrásokon iterálsz és ugyanazt a formázási logikát alkalmazod.  

Nyugodtan kísérletezz különböző formátumkarakterláncokkal, tizedesjegy‑számokkal vagy exportálási beállításokkal, hogy megfeleljenek a saját jelentési igényeidnek. Boldog kódolást!

## Mit érdemes legközelebb megtanulnod?

A következő tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódpéldákat lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási módokat a saját projektjeidben.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}