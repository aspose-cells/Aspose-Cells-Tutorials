---
category: general
date: 2026-11-19
description: Hogyan ismételjünk meg munkalapot, miközben tömbadatokkal töltjük fel
  az Excelt. Tanulja meg, hogyan generáljon több munkalapot, és hogyan töltse fel
  a munkalapot listából néhány lépésben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: hu
lastmod: 2026-11-19
og_description: Hogyan ismételjünk meg munkalapot a SmartMarkerProcessor használatával.
  Kövesd ezt az útmutatót, hogy tömb adatokat tölts be az Excelbe, több munkalapot
  generálj, és listából töltsd fel a munkalapot.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Hogyan ismételjünk meg munkalapot az Excelben – lépésről lépésre útmutató
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Hogyan ismételjük meg a munkalapot az Excelben a SmartMarkerProcessor segítségével
url: /hu/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan ismételjünk meg munkalapot Excelben a SmartMarkerProcessor segítségével

Ha **how to repeat worksheet**-re van szükséged Excel jelentések generálásakor, ez az útmutató egy teljes, futtatható megoldást mutat be. A tutorial végére képes leszel **populate Excel with array** adatokat feltölteni, **generate multiple worksheets** létrehozni, és **populate worksheet from list** használni a SmartMarkerProcessor könyvtárral.

A munkalap ismétlése gyakori igény, amikor minden részlegnek, régiónak vagy időszaknak saját füle kell. Az alábbi példa bemutatja a pontos lépéseket, elmagyarázza, miért fontos minden beállítás, és lefedi az olyan széljegyeket, mint az üres listák vagy egyedi elnevezés.

## Előfeltételek

- .NET 6.0 vagy újabb telepítve
- A **GroupDocs.Viewer** (vagy ekvivalens) NuGet csomagra való hivatkozás, amely tartalmazza a `SmartMarkerProcessor`-t
- Egy Excel sablon munkafüzet (`.xlsx`) egy `${repeat:Dept}` jelölővel, amelyet egy ismételni kívánt sorba helyezel
- Alapvető ismeretek C#-ban és LINQ-ban (opcionális, de hasznos)

Nem szükséges további harmadik féltől származó könyvtár.

## 1. lépés: A SmartMarkerProcessor példány létrehozása

A processzor koordinálja a jelölőcsere és a munkalap duplikálás folyamatát. Argumentumok nélkül történő példányosítása az alapértelmezett beállításokat használja.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

A processzor korai létrehozása lehetővé teszi, hogy a globális beállításokat az adatok alkalmazása előtt konfiguráld. Ez a **how to repeat worksheet** helyes végrehajtásának alapja.

## 2. lépés: A munkalap ismétlés engedélyezése

Alapértelmezés szerint a processzor csak az aktuális lapon cseréli a jelölőket. A `RepeatWorksheet` `true` értékre állítása azt mondja a motornak, hogy minden adatgyűjtemény elemhez klónozza az egész munkalapot.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Ennek az opciónak az engedélyezése a **generate multiple worksheets** kulcsa – a processzor minden egyes `Dept` tömb elemhez új fület hoz létre, és megőrzi az eredeti formázást.

## 3. lépés: Az adatforrás előkészítése tömbként vagy listaként

A SmartMarkerProcessor bármely enumerálhatóval működik, de egy tömb használata egyértelművé teszi a szándékot, ha **populate worksheet from list**-et szeretnél. Itt egy anonim objektumot hozunk létre, amely egy `Dept` tulajdonságot tartalmaz, benne egy karakterlánc tömbbel.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Ha már rendelkezel egy `List<string>`-el, azt közvetlenül átadhatod; a processzor ugyanúgy kezeli. A fontos rész, hogy a tulajdonság neve (`Dept`) pontosan egyezzen a sablonban lévő `${repeat:Dept}` jelölővel.

## 4. lépés: A sablon munkalap betöltése

Feltételezve, hogy van egy `ExcelPackage` (EPPlus‑ből) vagy egy `Workbook` objektumod, szerezd meg a ismételni kívánt munkalapot. A `ws` változó ezt a lapot jelöli.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Ha másik könyvtárat részesítesz előnyben (pl. ClosedXML), ugyanaz az elv érvényes: szerezz egy olyan munkalap objektumot, amely implementálja a szükséges interfészt.

## 5. lépés: A munkalap feldolgozása az adatokkal

Most alkalmazd az adatokat a sablonra. A processzor minden részleghez klónozza a munkalapot, a `${repeat:Dept}` jelölőt a tényleges részleg nevével helyettesíti, a lap többi részét érintetlenül hagyja.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

A `Process` befejezése után a `ws` lesz az első a több munkalap közül – egy részlegenként. Az eredeti lap neve megmarad, míg a másolatok növekvő utótagot kapnak (pl. “Sheet1 (1)”, “Sheet1 (2)”). Utólag átnevezheted őket, ha egyedi elnevezési sémára van szükséged.

### Várt kimenet

Amikor megnyitod a létrehozott munkafüzetet, a következőket kell látnod:

- **Sheet1** – az eredeti sablon (gyakran üres vagy mesterként használva)
- **Sheet1 (1)** – kitöltve a “HR” értékkel
- **Sheet1 (2)** – kitöltve az “IT” értékkel
- **Sheet1 (3)** – kitöltve a “Finance” értékkel

Minden lap ugyanazt a elrendezést tartalmazza, de a `${repeat:Dept}` helyén a részleg neve jelenik meg.

## Érintett esetek kezelése

### Üres vagy null tömbök

Ha `Dept` null vagy üres, a processzor nem hoz létre további munkalapokat. A teljesen üres munkafüzet elkerülése érdekében hozzáadhatsz egy védelmi ellenőrzést:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Egyedi munkalap nevek

Az alapértelmezett elnevezési séma nem minden jelentési igényhez illeszkedik. A feldolgozás után egy ciklussal nevezd át a lapokat:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### További oszlopok feltöltése

Ha egyetlen jelölőn túl **populate excel with array** értékeket kell feltölteni, bővítsd a adatobjektumot:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Ezután állítsd be a sablon jelölőket `${repeat:Dept.Name}` és `${repeat:Dept.Headcount}` formára. A processzor minden részleghez ismétli a sort, és mindkét oszlopot kitölti.

## Teljes működő példa

Az alábbi önálló konzolalkalmazás bemutatja a teljes folyamatot a sablon betöltésétől a végleges munkafüzet mentéséig.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explanation of key sections**

- **Processor creation** – létrehozza a motorot, amely értelmezi a jelölőket.
- **RepeatWorksheet option** – aktiválja a fő funkciót, amely megválaszolja a *how to repeat worksheet* kérdést.
- **Data source** – tömböt (`new[]`) használ a **populate excel with array** kielégítésére.
- **Template loading** – bemutat egy gyakori módot a munkalap objektum megszerzésére.
- **Processing** – egy hívásban végrehajtja a duplikálást és az adatok beillesztését.
- **Renaming** – megmutatja, hogyan alakítsuk a generikus “(1)”, “(2)” neveket jelentős címekké, ami tipikus követelmény a **generate multiple worksheets** után.

A program futtatása `Result.xlsx` fájlt hoz létre három részleg‑specifikus lappal, mindegyik a tömbből töltve fel.

## Gyakori buktatók és profi tippek

- **Marker spelling** – a jelölőnek pontosan meg kell egyeznie a tulajdonság nevével (`${repeat:Dept}`). Egy elütés megakadályozza az ismétlést.
- **Worksheet index** – a feldolgozás után az eredeti lap az 0‑ás indexen marad; a generált lapok sorban követik. Rossz indexelés rossz lap átnevezéséhez vezethet.
- **Large data sets** – több száz munkalap generálása jelentősen növelheti a fájlméretet. Fontold meg a jelentések szétbontását vagy egyetlen lap használatát csoportos szakaszokkal, ha a teljesítmény problémát jelent.
- **Thread safety** – a `SmartMarkerProcessor` nem szálbiztos. Hozz létre külön példányt szálanként, ha több munkafüzetet dolgozol fel párhuzamosan.

## Összegzés

Most már tudod, hogyan **how to repeat worksheet** Excelben a SmartMarkerProcessor használatával, hogyan **populate excel with array** adatokat tölts fel, hogyan **generate multiple worksheets** hozol létre, és hogyan **populate worksheet from list** hatékonyan. A teljes példa összekapcsolja az összes koncepciót, az opcionális átnevezési lépés pedig lehetővé teszi tiszta, felhasználóbarát fülnevek előállítását.

A következőket is felfedezheted:

- **populate worksheet from list** használata összetett objektumokkal (beágyazott gyűjtemények)
- Feltételes formázás alkalmazása a munkalap duplikálása után
- A generált munkafüzet exportálása PDF vagy CSV formátumba a további felhasználáshoz

Nyugodtan adaptáld a kódot a saját jelentési szituációidhoz, és élvezd az Excel munkafüzetek automatizálását magabiztosan!

## Mi legyen a következő tanulnivalód?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}