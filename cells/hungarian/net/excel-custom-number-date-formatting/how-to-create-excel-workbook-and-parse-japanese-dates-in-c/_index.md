---
category: general
date: 2026-10-10
description: Excel munkafüzet létrehozása C#-ban, és cellaérték beállítása japán era
  dátummal, majd egyéni formátum alkalmazása és a dátumcellá olvasása az Aspose.Cells
  segítségével.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: hu
lastmod: 2026-10-10
og_description: Excel munkafüzet létrehozása C#-ban és japán korszak dátumok feldolgozása.
  Tanulja meg, hogyan állítsa be a cella értékét, alkalmazzon egyéni formátumot, és
  olvassa be a dátum cellát az Aspose.Cells segítségével.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Excel munkafüzet létrehozása C#-ban – teljes útmutató a dátumok feldolgozásához
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hogyan hozzunk létre Excel munkafüzetet, és dolgozzuk fel a japán dátumokat
  C#‑ban
url: /hu/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan hozhatunk létre Excel munkafüzetet, és elemezzük a japán dátumokat C#-ban

Ha **Excel munkafüzetet** kell létrehoznia a semmiből, ez az útmutató pontosan megmutatja, hogyan. Megtanulja, hogyan **állítsa be a cella értékét** egy japán korszak dátumkarakterlánccal, **alkalmazzon egyedi formátumot**, amely érti a korszakot, és végül **olvassa a dátum cellát**, hogy egy .NET `DateTime`-ot kapjon. A teljes példa a legújabb Aspose.Cells for .NET verzióval működik, így a kódot egyszerűen bemásolhatja bármely C# projektbe.

A japán korszakokat tartalmazó dátumok kezelése nehézkes lehet, mivel az alapértelmezett Excel elemző nem ismeri fel a korszak szimbólumait. Egy egyedi számformátum (`[ja-JP-Era]`) használatával megmondja az Excelnek, hogyan értelmezze a karakterláncot, ezáltal megbízható **excel dátumfeldolgozást** tesz lehetővé. Az alábbi lépések lefedik az egész munkafolyamatot, a munkafüzet létrehozásától a dátum kinyeréséig.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+ alatt is fut)
- Aspose.Cells for .NET (NuGet csomag `Aspose.Cells`)
- Alapvető ismeretek C#-ban és Visual Studio-ban vagy a választott IDE-ben

## 1. lépés: Excel munkafüzet létrehozása és munkalap hozzáadása

Az első művelet a **Excel munkafüzet** memóriában való **létrehozása**. Az Aspose.Cells automatikusan létrehoz egy alapértelmezett munkalapot, de szükség esetén továbbiakat is hozzáadhat.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

A munkafüzet létrehozása lefoglalja a belső struktúrákat, amelyek később a cellákat, stílusokat és képleteket tárolják. Ebben a pontban nem íródik fájl, ami gyors és tesztelhető műveletet biztosít.

## 2. lépés: Celláérték beállítása japán korszak dátumkarakterlánccal

Ezután **állítsa be a cella értékét** a japán korszak ábrázolásra `"R5-04-01"` (Reiwa 5, április 1). A karakterlánc a `EraYear-MM-DD` mintát követi.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

`PutValue` használatával a nyers szöveg kerül tárolásra. Az Excel ezt karakterláncként kezeli, amíg egy számformátum másként nem jelzi. Ez a megközelítés bármilyen egyedi naptárábrázolásra működik, nem csak a japán korszakokra.

## 3. lépés: Egyedi számformátum alkalmazása, amely érti a japán korszakot

Most **alkalmazzon egyedi formátumot**, hogy az Excel a korszak karakterláncot tényleges sorozatszámmá alakítsa. A `[ja-JP-Era]yyyy/MM/dd` formátum azt mondja a motornak, hogy értelmezze az első korszak karaktert (`R` a Reiwa esetén), és számolja ki a gregorián dátumot.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Az egyedi formátum a cella stílusobjektumban tárolódik. Az Aspose.Cells tiszteletben tartja ezt a formátumot mind a megjelenítés, mind az értékkonverzió során, lehetővé téve a megbízható **excel dátumfeldolgozást** a későbbi folyamatban.

## 4. lépés: A cellából kinyert DateTime érték lekérése

Végül **olvassa a dátum cellát**, hogy egy .NET `DateTime`-ot kapjon. A `DateTimeValue` tulajdonság a korábban alkalmazott egyedi formátum alapján visszaadja a konvertált értéket.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

A program futtatásakor a konzol a következőt írja ki:

```
Parsed Gregorian date: 2023-04-01
```

A kimenet megerősíti, hogy a japán korszak karakterlánc `"R5-04-01"` helyesen értelmezve lett 2023. április 1‑ként.

## Teljes, futtatható példa

Az egyes részek összeállítása egy önálló programot eredményez, amelyet azonnal lefordíthat és futtathat.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

A program futtatása létrehozza a `JapaneseEraDate.xlsx` fájlt, ahol az A1 cella `2023/04/01`-et jelenít meg, miközben a konzol ugyanazt a gregorián dátumot mutatja. A fájl megnyitható Excelben a formázott érték megtekintéséhez.

## Miért működik ez a megközelítés

- **create excel workbook** – A `Workbook` példányosítása felépíti a teljes Excel fájlstruktúrát memóriában, anélkül, hogy a lemezt érintené.
- **set cell value** – A `PutValue` nyers szöveget tárol, ami szükséges a kultúraspecifikus formátum alkalmazása előtt.
- **apply custom format** – A `[ja-JP-Era]` token áthidalja a korszak jelölés és az Excel belső sorozatszámú dátumrendszere közötti szakadékot.
- **read date cell** – A `DateTimeValue` automatikusan a cella stílusát használja a konverzióhoz, így natív `DateTime`-ot kap.
- **excel date parsing** – A parsing a cella stílusára bízásával elkerülhető a manuális karakterlánc-manipuláció, csökkentve a hibákat és javítva a nyelvi támogatást.

## Szélsőséges esetek és gyakorlati tippek

- **Different eras** – Használja a `S`-t a Showa, `H`-t a Heisei, `R`-t a Reiwa esetén. Ugyanaz a formátum karakterlánc minden korszakra működik.
- **Invalid strings** – Ha a cella hibás korszak dátumot tartalmaz, a `DateTimeValue` `DateTime.MinValue`-t ad vissza. Olvasás előtt ellenőrizze a `dateCell.IsDate` értéket.
- **Multiple cells** – Alkalmazza az egyedi formátumot egy teljes tartományra (`range.ApplyStyle(style)`), ha sok dátumot kell feldolgozni.
- **Performance** – A stílus egyszeri beállítása oszloponként gyorsabb, mint cellánként, nagy táblázatok esetén.
- **Saving options** – Az Aspose.Cells képes XLSX, XLS, CSV vagy PDF formátumba exportálni. Válassza a downstream feldolgozáshoz leginkább illeszkedő formátumot.

## Gyakran ismételt kérdések

**Használhatom a beépített .NET kultúrát egyedi formátum helyett?**  
A .NET `CultureInfo` osztály nem érti a japán korszak szimbólumokat ugyanúgy, mint az Excel. Egyedi számformátum használata a legmegbízhatóbb módszer a korszak karakterláncok **excel date parsing**-jához.

**Mi van, ha vissza kell írnom a dátumot Excelbe korszak formátumban?**  
Állítsa be a cella értékét `DateTime`-ra, és alkalmazza ugyanazt az egyedi formátumot. Az Excel automatikusan megjeleníti a korszakot.

**Működik ez a régebbi Excel verziókon is?**  
A `[ja-JP-Era]` tokenet az Excel 2010 és újabb verziók támogatják. Az Aspose.Cells emulálja a viselkedést, így a munkafüzet helyesen jelenik meg még akkor is, ha régebbi Excel verzióban nyitják meg, amely nem rendelkezik natív korszak támogatással.

## Következtetés

Most már tudja, hogyan **hozzon létre Excel munkafüzetet**, **állítsa be a cella értékét** egy japán korszak karakterlánccal, **alkalmazzon egyedi formátumot**, és **olvassa a dátum cellát**, hogy egy `DateTime`-ot kapjon. Ez a minta megbízható **excel date parsing**-ot biztosít manuális karakterlánc-kezelés nélkül, így a C# automatizálási kódja egyszerű és megbízható lesz.

Ezután fedezze fel a kapcsolódó témákat, mint például a **több dátum oszlop formázása**, **más kulturális naptárakkal való munka**, vagy a **munkafüzet PDF-be exportálása**. Minden kiterjesztés az itt bemutatott elveken alapul, így a megoldást számos lokalizációs forgatókönyvre adaptálhatja. Boldog kódolást!

## Mit érdemes következőként megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Excel munkafüzet létrehozása C#-ban – Egyedi számformátum alkalmazása](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Excel munkafüzet létrehozása egyedi formátummal – C# útmutató](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel automatizálás Aspose.Cells .NET-tel: Munkafüzet létrehozása és külső hivatkozások beállítása](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}