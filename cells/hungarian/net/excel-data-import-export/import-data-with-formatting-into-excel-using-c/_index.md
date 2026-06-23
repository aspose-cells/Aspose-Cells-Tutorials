---
category: general
date: 2026-03-01
description: Importáljon adatokat formázással Excelbe C#-ban. Tanulja meg, hogyan
  importálhat DataTable-t Excelbe, és hogyan adhat háttérszínt a celláknak néhány
  egyszerű lépésben.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: hu
og_description: Adatok importálása formázással Excelbe C#-al. Lépésről lépésre útmutató,
  amely bemutatja, hogyan importáljunk egy DataTable-t, és hogyan adjunk háttérszínt
  a celláknak.
og_title: Adatok importálása formázással az Excelbe – C# útmutató
tags:
- C#
- Excel
- DataTable
- Formatting
title: Adatok importálása formázással Excelbe C#‑val
url: /hu/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adatok importálása formázással Excel-be C#-al

Valaha is szükséged volt **adatok importálására formázással** egy Excel munkafüzetbe, de csak egy egyszerű, unalmas lapot kaptál? Nem vagy egyedül. A legtöbb fejlesztő erre a problémára fut, amikor rájön, hogy az alapértelmezett import eltávolítja az összes színt és stílust, amelyet gondosan beállítottak a forrásadatokban.

Ebben a bemutatóban egy teljes, azonnal futtatható megoldáson keresztül vezetünk végig, amely **importál egy DataTable-t Excel-be** és **háttérszínt ad az Excel cellákhoz** egyszerre. Nem szükséges extra utófeldolgozás – a táblázat pontosan úgy néz ki, ahogy szeretnéd, közvetlenül a dobozból.

## Amit megtanulsz

- Hogyan lehet adatokat lekérni egy `DataTable`-be.  
- Hogyan definiáljunk egy `Style` objektumok tömbjét, amely háttérszíneket tartalmaz.  
- Hogyan hívjuk meg az `ImportDataTable`-t ezekkel a stílusokkal, hogy az importálás megőrizze a formázást.  
- Egy teljes, futtatható példát, amelyet beilleszthetsz egy konzolalkalmazásba, és azonnal láthatod az eredményt.  
- Tippek, buktatók és variációk valós projektekhez.  

### Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.6+‑vel is működik).  
- A **GemBox.Spreadsheet** könyvtár (az ingyenes verzió elegendő a demóhoz).  
- Alapvető ismeretek C#-ban és Excel koncepciókban.  

Ha azon gondolkodsz, *miért a GemBox?*, az azért, mert egy egyetlen soros `ImportDataTable` metódust kínál, amely stílus tömböket fogad – pontosan amire szükségünk van a **adatok importálására formázással** anélkül, hogy ciklust írnánk.

---

## 1. lépés: A projekt beállítása és a GemBox.Spreadsheet hozzáadása

A kezdéshez hozz létre egy új konzolalkalmazást:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** Az ingyenes verzió 150 k cellára korlátozza a munkalapokat, ami bőven elegendő demókhoz. Ha elérnéd a határt, frissíts vagy válts EPPlus-ra, de az API kissé más lesz.

## 2. lépés: A forrásadatok lekérése `DataTable`-ként

Az első dolog, amire szükségünk van, egy `DataTable`, amely utánozza a normál adatbázisból lekért adatokat. Íme egy apró segédfüggvény, amely memóriában hoz létre egyet:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Miért fontos:** Az adatlekérést külön metódusba szervezve bármilyen forrást – SQL, CSV, webszolgáltatás – be tudsz cserélni anélkül, hogy az importálási logikát módosítanád. Ez tisztán tartja a kódot, és a **hogyan importáljunk datatable-t Excel-be** tutorial újrahasználhatóvá válik.

## 3. lépés: A kívánt stílusok definiálása

Most jön a szórakoztató rész: létrehozunk egy `Style` objektumok tömbjét, mindegyik egyedi `ForegroundColor`-ral. A GemBox lehetővé teszi a `BackgroundPatternColor` (a cella kitöltése) és a `ForegroundColor` (a szöveg színe) beállítását. A demóhoz az első két oszlopot különböző színekkel színezzük.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Magyarázat:**  
- `Style` objektumok könnyű tárolók; nem kell újat létrehozni minden cellához.  
- Az array sorrendjének a oszlopsorrenddel való egyeztetésével a GemBox automatikusan alkalmazza a megfelelő stílust importáláskor.  
- Ez a kulcsa a **adatok importálásának formázással** — a formázás az adatokkal együtt utazik, nem utólag.

## 4. lépés: A `DataTable` importálása a munkalapba stílusokkal

Az adatok és a stílusok készen állnak, most létrehozhatunk egy munkafüzetet, kiválaszthatjuk az első munkalapot, és meghívhatjuk az `ImportDataTable`-t. A metódus aláírása így néz ki:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Így használjuk:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Mi történik a háttérben?**  
- `true` azt jelzi a GemBox-nak, hogy az oszlopneveket az első sorba írja.  
- `0, 0` az importálást az A1 cellára helyezi.  
- `importStyles` minden oszlopot összekapcsol a korábban definiált színekkel.  

Amikor megnyitod a *Report.xlsx*-t, láthatod, hogy az **ID** oszlop világoskék, a **Name** oszlop világoszöld háttérrel van színezve, a **Score** oszlop pedig érintetlen marad. Ez a **adatok importálása formázással** egyetlen hívásban.

## 5. lépés: Az eredmény ellenőrzése (várt kimenet)

Nyisd meg a generált `Report.xlsx` fájlt. Valami ilyesmit kell látnod:

| ID (világoskék) | Név (világoszöld) | Pont |
|-----------------|-------------------|------|
| 1               | Alice             | 93.5 |
| 2               | Bob               | 78.0 |
| 3               | Charlie           | 85.2 |
| 4               | Diana             | 91.3 |
| 5               | Ethan             | 67.8 |

- Az **ID** oszlop cellái világoskék háttérrel rendelkeznek.  
- A **Név** oszlop cellái világoszöld háttérrel rendelkeznek.  
- A **Pont** oszlop az alapértelmezett fehér háttérrel marad.

![Excel táblázat, amely bemutatja az adat importálását formázással – ID oszlop világoskék, Név oszlop világoszöld](excel-screenshot.png "adat importálás formázással példa")

*Az alt szöveg tartalmazza a fő kulcsszót a SEO érdekében.*

## Gyakori kérdések és szélhelyzetek

### Alkalmazhatok-e több mint csak háttérszíneket?

Természetesen. A `Style` lehetővé teszi betűtípusok, szegélyek, számformátumok és még feltételes formázás beállítását is. Például, hogy a 90 fölötti pontszámok félkövér és piros legyenek:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Mi van, ha a DataTable-nek több oszlopa van, mint a stílusok?

A GemBox csak azokra az oszlopokra alkalmaz stílusokat, amelyekhez van megfelelő bejegyzés a tömbben. A többlet oszlopok az alapértelmezett stílusra visszaesnek – hiba nem keletkezik.

### Működik ez nagy adathalmazokkal is?

Igen, de figyelj a ingyenes verzió cellalimitére (150 k cella). Nagy jelentésekhez érdemes a fizetett licencet választani, vagy soronként streamelni az adatot a `worksheet.Cells[row, col].Value = …` módszerrel – bár ekkor elveszik az egy soros kényelmes megoldás előnye.

### Hogyan importálhatok adatot formázással egy meglévő Excel sablonból?

Először betölthetsz egy sablon munkafüzetet:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Ez lehetővé teszi a fejléc logók, láblécek és bármely előre definiált stílus megőrzését, miközben a dinamikus részhez **adat importálás formázással** történik.

## Teljes működő példa (másolás-beillesztés kész)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Futtasd a programot (`dotnet run`), majd nyisd meg a generált *Report.xlsx*-t, hogy azonnal lásd a színek alkalmazását.

## Összegzés

Most már egy szilárd, befejezést rendelkezel, amely lehetővé teszi az adatok importálását formázással Excel-be C#-al. 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}