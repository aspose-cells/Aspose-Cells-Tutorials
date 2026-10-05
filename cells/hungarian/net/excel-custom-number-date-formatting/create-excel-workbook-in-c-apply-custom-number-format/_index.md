---
category: general
date: 2026-05-23
description: Excel munkafüzet létrehozása C#-ban, és megtanulni, hogyan alkalmazzunk
  egyéni számformátumot, programozottan állítsuk be a cella stílusát, tudományos jelölésben
  formázzuk a cellát, majd mentsük a munkafüzetet xlsx formátumba.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: hu
og_description: Hozzon létre Excel munkafüzetet C#-ban gyorsan. Tanulja meg, hogyan
  alkalmazzon egyéni számformátumot, programozottan formázza a cellákat, formázza
  a tudományos jelölést, és mentse xlsx formátumban.
og_title: Excel munkafüzet létrehozása C#‑ban – Egyéni számformátum alkalmazása
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Excel munkafüzet létrehozása C#‑ban – Egyéni számformátum alkalmazása
url: /hu/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása C#‑ban – Egyéni számformátum alkalmazása

Excel munkafüzet létrehozása C#‑ban könnyebb, mint gondolnád. Ebben az útmutatóban végigvezetünk egy egyéni számformátum alkalmazásán, egy cella tudományos jelölésben való formázásán, a cellastílus programozott beállításán, és végül a munkafüzet xlsx fájlba mentésén.

Ha már valaha is egy üres táblázatot néztél, és azon tűnődtél, hogyan lehet automatizálni az egészet – az adatok feltöltésétől a számok pontos megjelenítéséig – ez a tutorial neked szól. A végére egy teljesen működő Excel fájlt kapsz, amelyet bármely táblázatkezelő programban megnyithatsz, és megérted, **miért** fontos minden lépés, nem csak **hogyan** kell beírni a kódot.

## Amire szükséged lesz

- **.NET 6+** (vagy bármelyik friss .NET Framework, amely támogatja a könyvtárat)  
- **Aspose.Cells for .NET** (vagy egy másik API, amely elérhetővé teszi a `Workbook`, `Cell` és `CellFormat` osztályokat)  
- Mérsékelt C# tapasztalat – ha tudsz `Console.WriteLine`‑t írni, már indulhatsz.  

Nincs szükség extra konfigurációs fájlokra, COM interopra, és egyáltalán nem kell manuálisan telepíteni az Excelt.

---

## Excel munkafüzet létrehozása – a Workbook objektum inicializálása

Az első dolog, amit meg kell tennünk, egy üres munkafüzet létrehozása. Gondolj a `Workbook` osztályra úgy, mint egy üres vászonra, amelyre sorokat, oszlopokat és stílusokat festhetsz.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Ennyi – egy sor, és már van egy vadonatúj Excel fájl a memóriában. A `Workbook` konstruktor létrehozza az alapértelmezett munkalap-gyűjteményt, így azonnal elkezdhetsz adatot hozzáadni.

> **Pro tip:** Ha több lapra van szükséged, meghívhatod a `workbook.Worksheets.Add()`‑t, mielőtt elkezdenéd feltölteni a cellákat.

![Excel munkafüzet létrehozása példa](image-placeholder.png "Excel munkafüzet létrehozása képernyőkép")

*Kép alternatív szöveg: Excel munkafüzet létrehozása példa, amely egy üres Excel lapot mutat az IDE‑ben.*

## Egyéni számformátum alkalmazása egy cellára

Most, hogy a munkafüzet létezik, tegyünk egy számot a **A1** cellába, és adjunk neki egy egyéni formátumot. Az egyéni számformátumok lehetővé teszik, hogy szabályozd, hogyan jelenjenek meg a számok – valuta, százalék, dátum vagy, a mi esetünkben, tudományos jelölés.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Miért húzzuk előbb a stílust? Mert a `Cell` objektum egy **Style** objektumot tárol, amely egy helyen tartalmazza a betűtípusokat, szegélyeket, igazítást és a számformázást. A `Custom` tulajdonság szerkesztésével azt mondjuk az Excelnek, hogy „mutassa ezt az értéket tudományos jelöléssel, két tizedesjeggyel”.

> **Gyakori kérdés:** *Használhatok beépített formátumot egy egyéni helyett?*  
> Igen – állítsd be a `style.Number = 10`‑et egy beépített tudományos formátumhoz, de az egyéni karakterlánc pontos kontrollt biztosít a tizedesjegyek felett.

## Cellastílus programozott beállítása (a számformátumon túl)

Gyakran többre van szükség, mint csak egy számformátumra. Adjunk hozzá félkövér betűt és egy világosszürke háttérszínt, hogy a cella kitűnjön.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Vedd észre, hogy ugyanazt a `style` objektumot használjuk újra, amelyet korábban módosítottunk. Ez a **cellastílus programozott beállítása** szépsége – egyszer kérdezed le a stílust, módosítod a szükséges tulajdonságokat, és visszaírod. Nem kell új objektumokat létrehozni, vagy elveszíteni a már beállított számformátumot.

## Cell formázása tudományos jelöléssel (szélsőséges esetek kezelése)

Ha nagyon nagy vagy nagyon kicsi számokkal dolgozol, a tudományos jelölés életmentő. Az általunk használt egyéni formátum (`0.00E+00`) garantálja, hogy két számjegy legyen a tizedespont után, és a kitevő előtt plusz jelet helyez el. Itt egy gyors ellenőrzés:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

Amikor megnyitod a létrehozott fájlt, a B2 cella `1.23E-05`‑ként jelenik meg, ami megerősíti, hogy a **cell formázása tudományos jelöléssel** utasítás mind nagy, mind kis számokra működik.

## Munkafüzet mentése XLSX‑be

Az egész móka akkor ér véget, amikor ténylegesen a lemezre írod a fájlt. A `Save` metódus végzi a nehéz munkát, átalakítva a memóriában lévő reprezentációt egy megfelelő `.xlsx` csomaggá.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

Ez a sor teljesíti a **save workbook to xlsx** célt. Ha a könyvtár nem létezik, a `Save` kivételt dob – ezért győződj meg róla, hogy a mappa előre létre van hozva, vagy tedd a hívást try/catch blokkba.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Most már van egy megosztható Excel fájlod, amelyben egy szép formázott tudományos szám, félkövér stílus és egy világosszürke háttér található.

## Teljes működő példa

Az alábbiakban a teljes, másolásra kész program látható, amely minden részt összekapcsol. Konzolos alkalmazásként fordítható, de a logikát bármely C# projektbe beillesztheted.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Várható eredmény:** Nyisd meg a `CustomFormatted.xlsx` fájlt, és a következőt fogod látni:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Mindkét cella félkövér, világosszürke kitöltéssel rendelkezik, és a számok tudományos jelöléssel, két tizedesjeggyel jelennek meg.

---

## Összegzés

Épp most **create excel workbook**‑t hoztunk létre a semmiből, **apply custom number format**‑ot alkalmaztunk, **format cell scientific notation**‑t hajtottunk végre, **set cell style programmatically**‑t állítottunk be, és **save workbook to xlsx**‑t mentettünk – mindezt néhány C# sorban. A megközelítés skálázható: csak iterálj a sorokon, klónozd a `style` objektumot, és néhány másodperc alatt teljesen formázott jelentést kapsz.

### Mi a következő?

- **Dinamikus formázás:** Formátumok váltása az érték nagysága alapján (pl. valuta vs. százalék).  
- **Több lap:** Használd a `workbook.Worksheets.Add("Summary")`‑t dashboardok építéséhez.  
- **Haladó stílusok:** Szegélyek, feltételes formázás és adatellenőrzés

## Kapcsolódó oktatóanyagok

- [Hogyan hozzunk létre és mentsünk egy Excel munkafüzetet ODS formátumban az Aspose.Cells for .NET használatával](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Excel munkafüzet létrehozása és mentése Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Excel munkafüzet létrehozása és mentése PDF‑ként Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}