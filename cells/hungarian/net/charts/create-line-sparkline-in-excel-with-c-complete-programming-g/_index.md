---
category: general
date: 2026-06-30
description: Készíts gyorsan vonal-sparkline-t Excelben C#-al. Tanuld meg, hogyan
  adj hozzá sparkline-t, hogyan hozd létre az Excel munkafüzetet C#-ban, és néhány
  lépésben hogyan helyezd el a sparkline-t egy cellában.
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: hu
og_description: Hozzon létre vonal-sparkline-t Excelben C#-val. Ez az útmutató bemutatja,
  hogyan adjon hozzá sparkline-t, hogyan hozzon létre Excel munkafüzetet C#-ban, és
  hogyan ágyazza be a sparkline-t egy cellába.
og_title: Vonal-sparkline létrehozása Excelben C#‑val – Lépésről lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Vonal-sparkline létrehozása Excelben C#-val – Teljes programozási útmutató
url: /hu/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vonalas sparkline létrehozása Excelben C#‑vel – Teljes programozási útmutató

Gondolkodtál már azon, hogyan **hozz létre vonalas sparkline‑t** egy Excel‑fájlban C#‑vel? Nem vagy egyedül – a fejlesztők gyakran kérdezik: „Hogyan tudok sparkline‑t hozzáadni egy jelentéshez anélkül, hogy manuálisan megnyitnám az Excelt?” A jó hír, hogy néhány kódsorral közvetlenül a munkafüzetben generálhatsz egy elegáns vonalas sparkline‑t, UI nélkül.

Ebben a tutorialban mindent végigvázolunk, amit tudnod kell: a **create Excel workbook C#** alapoktól az adatok feltöltéséig, egészen a **add line sparkline** és **add sparkline to cell** pontos lépéseiig. A végére egy használatra kész *.xlsx* fájlod lesz, amely egy pillantással megjeleníti a havi eladási trendeket. Nincs felesleges szöveg, csak egy gyakorlati, futtatható megoldás.

---

## Mit fogsz építeni

- Egy friss Excel munkafüzet, amelynek neve *KPI_Sparklines.xlsx*  
- Egy **KPI** nevű munkalap, amely minta eladási adatokat tartalmaz  
- Egy **line sparkline**, amely a **D2** cellába kerül, és a **B2:B13** adatcímkét használja  
- Alapvető formázás (szín, vonalvastagság), hogy a sparkline kiemelkedjen  

Előfeltételek? Csak a .NET SDK (3.1+ vagy .NET 6) és az ingyenes Aspose.Cells for .NET könyvtár (elérhető a NuGet‑en). Ha még sosem használtad az Aspose.Cells‑t, gondolj rá úgy, mint egy erőteljes Excel motorra, amelyet kódból hívhatsz – nincs COM interop, nincs szükség Excel telepítésre.

---

![Vonalas sparkline létrehozása Excelben C# használatával](https://example.com/images/create-line-sparkline.png "Vonalas sparkline létrehozása Excelben C#‑vel")

*Image alt text: vonalas sparkline létrehozása Excelben C# kódrészlet példával*

---

## 1. lépés: **Create Excel workbook C#** – A fájl és munkalap beállítása

Először is szükségünk van egy munkafüzet objektumra és egy munkalapra, ahol az adatok élnek. Ez minden Excel‑automatizálás alapja, akár később **add line sparkline**‑t vagy képleteket írsz.

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **Why this matters:** A `Workbook` osztály képviseli az egész fájlt, míg a `Worksheet` a sorok, oszlopok és végül a sparkline vászna. A lap nevét már a kezdetekkor megadni segít rendben és önmagát dokumentálni a fájlt.

---

## 2. lépés: Adatok feltöltése – A sparkline forráscíme

A sparkline‑nek adatokra van szüksége a megjelenítéshez. Szimuláljunk 12 hónap eladási adatát. Ezeket lekérdezheted egy adatbázisból, de a tisztaság kedvéért generáljuk őket a helyben.

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **Tip:** A `PutValue` automatikusan felismeri az adat típusát, így nem kell `double`‑ra vagy `int`‑re castelni. Ha valaha formázni szeretnéd a cellákat (pénznem, ezreselválasztó), később alkalmazhatsz egy `Style` objektumot.

---

## 3. lépés: **Create line sparkline** – Sparkline hozzáadása egy konkrét cellához

Most jön a főszereplő: a **line sparkline**. Az Aspose.Cells a sparklinek csoportosítását teszi lehetővé, ezért először egy `SparklineGroup`‑ot hozunk létre `Line` típusúként, majd megadjuk, hol jelenjen meg a vizuális elem.

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **How it works:**  
> - `firstRow/firstColumn` és `lastRow/lastColumn` határozza meg a *célcellát* (ahol a sparkline megjelenik).  
> - `firstDataRow/lastDataRow` a forráscímkét jelöli.  
> Mivel **line sparkline**‑t használunk, a vizuális elem egy egyszerű vékony vonal lesz, amely a számok trendjét követi.

### Opcionális: **How to add sparkline** egyedi stílussal

Ha szeretnéd, hogy a sparkline kitűnjön, állíts be néhány tulajdonságot:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **Why style it?** Egy sötétkék vonal fehér háttéren könnyen olvasható, míg a jelölők gyors tájékoztatást adnak az egyes adatpontokról – hasznos prezentációk során.

---

## 4. lépés: Munkafüzet mentése – Az eredmény ellenőrzése

Miután a sparkline a helyén van, csak a fájlt kell leírni a lemezre. Válassz egy olyan mappát, amelyhez írási jogosultságod van; a példában egy helyőrző útvonal szerepel, amelyet cserélned kell.

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **Verification:** Nyisd meg a generált fájlt Excelben (vagy bármely .xlsx‑t támogató megjelenítőben). Látnod kell egy **line sparkline**‑t a **D2** cellában, amely tükrözi a **B** oszlopban növekvő eladási számokat. A sparkline fölé húzva egy tooltip jelenik meg az alapértékekkel.

---

## 5. lépés: Gyakori hibák, amikor **add sparkline to cell**-t használsz

Még egy egyszerű példa is akadályozhatja a kezdőket. Íme néhány dolog, amire figyelj:

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| Hibás cellakoordináták | A sparkline célja nulla‑bázisú oszlopindexet, de egy‑bázisú sorindexet használ. | Emlékezz arra, hogy a `Cells[row, column]` esetén a `row` és a `column` is nulla‑bázisú. A `SparklineGroup.Add`‑nél a sorok és oszlopok **1‑bázisúak**. |
| Nincs adat megjelenítve | A forráscímke üres vagy nem numerikus értékeket tartalmaz. | Győződj meg arról, hogy a tartomány (pl. `B2:B13`) számokat tartalmaz. Használd a `PutValue`‑t numerikus típusokkal. |
| Sparkline eltűnik mentés után | Könyvtárverzió-eltérés vagy hiányzó licenc. | Használd a legújabb Aspose.Cells csomagot, és adj meg érvényes licencet, ha túllépted a kiértékelési korlátokat. |
| Formázás nem alkalmazódik | Stílusváltoztatás a sparkline hozzáadása előtt történt. | Állítsd be a stílust **a csoport létrehozása után**, ahogy fent mutattuk. |

---

## Teljes forráskód – Egy‑állású másolás‑beillesztés

Az alábbi program teljes, kész‑futásra. Másold be egy új konzolos projektbe, add hozzá az Aspose.Cells NuGet‑csomagot, és nyomd meg az **F5**‑öt.

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Expected output:** Amikor megnyitod a *KPI_Sparklines.xlsx* fájlt, a **B** oszlop tizenkét számot (5 000 → 13 250) listáz, és a **D2** cellában egy sima sötétkék vonalas sparkline jelenik meg, amely fokozatosan emelkedik. A jelölők apró narancssárga‑vörös pontokként jelennek meg, ha engedélyezted a `ShowMarkers`‑t.

---

## Mi a következő? Sparkline‑készségek bővítése

Miután elsajátítottad a **create line sparkline**‑t az Aspose.Cells‑szel, érdemes megvizsgálni ezeket a kapcsolódó témákat:

- **Add column sparkline** – tökéletes a halmozott adatok megjelenítéséhez.  
- **Create multi‑sparkline groups** ugyanazon a lapon, egymás mellé helyezve az összehasonlításhoz.  
- **Export to PDF** a sparklinek megőrzése mellett (az Aspose.Cells támogatja a PDF konverziót).  
- **Dynamic data sources** – valós eladási adatokat húzhatsz egy SQL adatbázisból a keménykódolt értékek helyett.  

Mindegyik a ugyanazon alapelveken épül: **create Excel workbook C#**, adatok feltöltése, és **add sparkline to cell** a kívánt stílusban.

---

### TL;DR

Megmutattuk, hogyan **create line sparkline** egy Excel munkafüzetben C#‑vel. A lépések – *munkafüzet létrehozása, adatok feltöltése, sparkline hozzáadása, stílus beállítása és mentés* – egyetlen, önálló programban vannak összegyűjtve. Nyugodtan módosítsd a színeket, vonalvastagságot vagy a forráscímkét, hogy megfeleljen a jelentéskészítési igényeidnek.

Van egy ötleted, amit megosztanál? Írj egy megjegyzést alább, és jó kódolást!

## Mit tanulj meg legközelebb?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépés‑ről‑lépésre magyarázatokkal, hogy további API‑funkciókat saját projektjeidben is könnyedén felfedezhess és alternatív megvalósítási módokat próbálhass ki.

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}