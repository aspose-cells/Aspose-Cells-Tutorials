---
category: general
date: 2026-04-07
description: Alkalmazzon egyéni számformátumot egy táblázatcellára, és tanulja meg,
  hogyan formázzon számot a táblázatban, miközben C#‑val exportálja a cella értékét.
  Gyors, teljes útmutató.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: hu
og_description: Alkalmazzon egyéni számformátumot egy táblázat cellájára, és exportálja
  formázott karakterláncként. Tanulja meg, hogyan formázhat számot a táblázatban,
  és exportálja a cella értékét.
og_title: Egyéni számformátum alkalmazása – Teljes C# exportálási útmutató
tags:
- C#
- Spreadsheet
- Number Formatting
title: Egyéni számformátum alkalmazása C# táblázat exportálásnál – Lépésről lépésre
  útmutató
url: /hu/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Egyéni számformátum alkalmazása C# táblázat exportálásban – Teljes útmutató

Valaha is szükséged volt **egyéni számformátum alkalmazására** egy cellára, majd a formázott karakterlánc kinyerésére egy táblázatból? Nem vagy egyedül. Sok fejlesztő akad el, amikor azt tapasztalja, hogy a nyers érték jelenik meg ahelyett, hogy a szép, helyi beállításoknak megfelelő karakterlánc lenne. Ebben az útmutatóban pontosan megmutatjuk, hogyan formázzuk a számot a táblázat celláiban, és hogyan exportáljuk a cella értékét formázott karakterláncként egy népszerű C# táblázatkönyvtár segítségével.

Az útmutató végére képes leszel **egyéni számformátum alkalmazására** bármely numerikus cellán, exportálni az eredményt az `ExportTable` segítségével, és látni a pontos kimenetet, amit egy felhasználói felületen vagy jelentésben várnál. Külső dokumentációra nincs szükség – minden itt van.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑on is működik)
- Hivatkozás a táblázatkönyvtárra, amely biztosítja a `Workbook`, `Worksheet` és `ExportTableOptions` osztályokat (pl. **Aspose.Cells** vagy **GemBox.Spreadsheet**; a bemutatott API az Aspose.Cells-nek felel meg)
- Alap C# ismeretek – ha tudsz `Console.WriteLine`-ot írni, már indulhatsz

> **Pro tipp:** Ha másik könyvtárat használsz, a tulajdonságnevek általában hasonlóak (`NumberFormat`, `ExportAsString`). Csak térképezd le őket ennek megfelelően.

## Mit fed le az útmutató

1. Munkafüzet létrehozása és az első munkalap kiválasztása.  
2. Numerikus érték beillesztése egy cellába.  
3. `ExportTableOptions` beállítása **egyéni számformátum alkalmazásához** és karakterlánc visszaadásához.  
4. A cella exportálása és a formázott eredmény kiírása.  
5. Szélsőséges esetek kezelése – mi van, ha a cella képletet vagy null értéket tartalmaz?

![egyéni számformátum alkalmazása példa](https://example.com/image.png "egyéni számformátum alkalmazása")

## 1. lépés – Munkafüzet létrehozása és az első munkalap lekérése

Az első dolog, amire szükséged van, egy munkafüzet objektum. Gondolj rá úgy, mint az Excel fájlra, amelyet az Office alkalmazásban nyitsz meg. Miután megvan, vedd az első lapot – a legtöbb útmutató itt kezd, mert így a példa tömör marad.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Miért fontos:** Egy új munkafüzet tiszta kiindulópontot biztosít, garantálva, hogy semmilyen rejtett formázás ne zavarja meg a későbbi egyéni számformátumunkat.

## 2. lépés – Numerikus érték beillesztése a B2 cellába (a cella, amelyet exportálni fogunk)

Most szükségünk van valami formázandóra. A **B2** cella kényelmes hely – könnyen hivatkozható, és elég messze van az alapértelmezett A1 sarkától, hogy elkerüljük a véletlen felülírásokat.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Mi van, ha az érték képlet?**  
Ha később a nyers értéket képletre cseréled (pl. `=SUM(A1:A10)`), az exportálási rutin továbbra is figyelembe veszi a következő lépésben alkalmazott számformátumot, mivel a formázás a cellához, nem az értéktípushoz van rendelve.

## 3. lépés – Exportálási beállítások konfigurálása a formázott karakterlánc visszakapásához

Itt van az útmutató szíve: megmondjuk a könyvtárnak, hogy **egyéni számformátumot alkalmazzon** az exportálás során. A `NumberFormat` karakterlánc ugyanazt a mintát követi, mint az Excel „Egyéni” kategóriájában.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` biztosítja, hogy a metódus `string`‑et adjon vissza nyers double helyett.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` az Excel mintáját tükrözi: vessző ezresek elválasztásához, két tizedesjegy, és zárójelek a negatív számokhoz.

> **Miért használjunk egyéni formátumot?** Biztosítja a konzisztenciát a különböző kultúrák között (pl. USA vs. európai számelválasztók), és lehetővé teszi üzleti specifikus stílusok, például a könyvelési zárójelek beágyazását.

## 4. lépés – A cella exportálása a konfigurált beállításokkal

Most ténylegesen kinyerjük az értéket a munkalapról, hagyva, hogy a könyvtár végezze a nehéz munkát a definiált formátum alkalmazásával.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Szélsőséges eset – üres cella:** Ha a `B2` üres lenne, a `formattedResult` `null` lesz. Egyszerű null‑ellenőrzéssel megvédheted magad a kiírás előtt.

## 5. lépés – A formázott karakterlánc megjelenítése

Végül kiírjuk az eredményt a konzolra. Egy valódi alkalmazásban ezt a karakterláncot PDF‑be, e‑mailbe vagy UI címkébe is beillesztheted.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Várt kimenet**

```
1,234.56
```

Ha a nyers értéket `-9876.54`‑re változtatod, ugyanaz a formátum `(9,876.54)`‑t ad – pontosan azt, amit sok könyvelési jelentés megkövetel.

## Teljes, futtatható példa

Az alábbiakban a teljes programot találod, amelyet beilleszthetsz egy új konzolos projektbe. Fordítható és futtatható úgy, ahogy van, feltéve, hogy hozzáadtad a megfelelő NuGet csomagot a táblázatkönyvtárhoz.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Gyors ellenőrzés

- **Fordul-e le?** Igen – csak győződj meg róla, hogy a `Aspose.Cells` (vagy ekvivalens) DLL-re hivatkozol.
- **Működik-e más kultúrákkal?** A formátum karakterlánc kultúra‑független; a könyvtár tiszteletben tartja a megadott mintát. Ha helyi specifikus elválasztókra van szükséged, az exportálás előtt hozzáadhatsz `CultureInfo` kezelést.

## Gyakori kérdések és változatok

### Hogyan **formázzuk a számot a táblázatban** egy másik mintával?

A `NumberFormat` karakterlánc cseréjével. Például, ha egy százalékot egy tizedesjeggyel szeretnél megjeleníteni:

```csharp
NumberFormat = "0.0%";
```

### Mi van, ha **cell érték exportálása** HTML‑ként a sima szöveg helyett?

A legtöbb könyvtárnak van egy túlterhelése, amely export típust fogad. Beállítanád a `ExportAsString = true`‑t, és hozzáadnád az `ExportHtml = true`‑t (vagy hasonlót). Az elv ugyanaz: definiáld a formátumot, majd válaszd ki a kimeneti reprezentációt.

### Alkalmazhatom a formátumot egy teljes tartományra, nem csak egy cellára?

Természetesen. A `NumberFormat`‑ot hozzárendelheted egy `Style` objektumhoz, majd ezt a stílust alkalmazhatod egy `Range`‑re. Az export hívás változatlan marad; automatikusan felveszi a stílust.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Mi történik, ha a cella képletet tartalmaz?

Az exportálási rutin először kiértékeli a képletet, majd formázza a kapott numerikus értéket. Nem szükséges extra kód – csak győződj meg róla, hogy a `Calculate` meghívásra került, ha letiltottad az automatikus számítást.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Összegzés

Most már tudod, hogyan **alkalmazz egyéni számformátumot** egy táblázat cellájára, **formázd a számot a táblázatban** és **exportáld a cella értékét** egy megjeleníthető karakterláncként. A fenti tömör kódminta minden lépést lefed – a munkafüzet létrehozásától a végső kimenetig –, így közvetlenül beillesztheted egy éles projektbe.

Készen állsz a következő kihívásra? Próbáld meg kombinálni ezt a technikát a **numerikus cellák formázásával** dátumok, pénznemjelek vagy feltételes formázás esetén. Vagy fedezd fel, hogyan exportálj több cellát CSV‑ként, miközben megőrzöd minden cella egyéni formátumát. A lehetőségek végtelenek, és ezekkel az alapokkal szilárd alapot építettél.

Boldog kódolást, és ne feledd a kísérletezést – néha a legjobb megoldások akkor jönnek elő, amikor egy kicsit módosítod a formátum karakterláncot!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}