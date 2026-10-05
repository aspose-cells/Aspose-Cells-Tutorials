---
category: general
date: 2026-04-07
description: Adj háttérszínt az Excel sorokhoz C#-ban. Tanuld meg, hogyan alkalmazz
  váltakozó sorok színeit, állíts be egyszínű háttérstílusokat, és importáld a DataTable-t
  Excelbe egyetlen munkafolyamatban.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: hu
og_description: Adj háttérszínt az Excel soroknak C#-al. Ez az útmutató bemutatja,
  hogyan alkalmazz váltakozó sorok színeit, állíts be egyszínű háttérszínt, és importáld
  hatékonyan a DataTable-t Excelbe.
og_title: Háttérszín hozzáadása Excelben – Váltakozó sorstílusok C#-ban
tags:
- C#
- Excel
- DataTable
- Styling
title: Háttérszín hozzáadása Excelben – Váltakozó sorstílusok C#‑ban
url: /hu/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel háttérszín hozzáadása – Váltakozó sorstílusok C#-ban

Valaha szükséged volt **add background color excel** sorok hozzáadására, de nem tudtad, hogyan csináld ezer soros bonyolult kód nélkül? Nem vagy egyedül – a legtöbb fejlesztő ugyanebbe a falba ütközik, amikor először megpróbálja, hogy a táblázatai több legyen, mint egy nyers adathalom.  

A jó hír? Néhány perc alatt **apply alternating row colors**, beállíthatsz **solid background**, és még **import datatable to excel**-t is használhatsz egy tiszta, újrahasználható mintával C#-ban.  

Ebben az útmutatóban végigvezetünk a teljes folyamaton, a `DataTable`-be történő adatlekéréstől a sorok stílusozásáig egy világos‑sárga‑fehér csíkos mintával. Nem szükséges külső könyvtárak, csak egy megbízható Excel‑kezelő csomag (például **ClosedXML** vagy **GemBox.Spreadsheet**) elegendő, és meg fogod érteni, miért teljesítményes és könnyen karbantartható ez a megközelítés.

## Mit fogsz megtanulni

- Hogyan lehet adatot lekérni és betölteni egy Excel munkalapra.
- Hogyan **style excel rows** váltakozó háttérszínekkel.
- A **set solid background** működése a `Style` objektum használatával.
- Hogyan **import datatable to excel** miközben megőrzöd a sorstílusokat.
- Tippek a szélhelyzetek kezelésére, például üres táblák vagy egyedi színsémák esetén.

> **Pro tip:** Ha már egy munkafüzet objektum (`wb`) használsz egy olyan könyvtárból, amely támogatja a stílus létrehozását, újra felhasználhatod ugyanazokat a `Style` példányokat több munkalapon – memória megtakarítva és a kódod rendezett marad.

---

## 1. lépés: Az adatok lekérése – DataTable előkészítése

Mielőtt bármilyen stílus alkalmazható lenne, szükségünk van egy sorforrásra. A legtöbb valós helyzetben ez egy adatbázisból, egy API‑ból vagy egy CSV‑fájlból származik. Bemutatásként egyszerűen egy memóriában lévő `DataTable`-t hozunk létre.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** A `DataTable` használata egy táblázatos, séma‑tudatos tárolót biztosít, amelyet az Excel könyvtár közvetlenül importálhat, így elkerülve a cellánkénti ciklusok írását.

## 2. lépés: Sorstílusok létrehozása – **Apply alternating row colors**

Most egy `Style` objektumok tömbjét építjük fel – soronként egyet –, hogy minden sor saját háttérszínt kapjon. A használt minta egy klasszikus világos‑sárga a páros sorokhoz és fehér a páratlan sorokhoz.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` egy tiszta stílusobjektumot ad, amelyet módosíthatsz anélkül, hogy másokra hatna.  
- A ternáris operátor `(i % 2 == 0)` határozza meg, hogy a sor páros (világos sárga) vagy páratlan (fehér).  
- A `Pattern = BackgroundType.Solid` beállítása a kulcsfontosságú lépés, amely **set solid background**; enélkül a szín figyelmen kívül maradna.

## 3. lépés: Cél munkalap lekérése

A legtöbb könyvtár munkalap-gyűjteményt biztosít. Az elsővel fogunk dolgozni, de tetszőleges indexet vagy nevet is megcélozhatsz.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Ha a munkafüzet újszerű, a könyvtár általában létrehoz egy alapértelmezett lapot. Ellenkező esetben explicit módon is hozzáadhatsz egyet:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

## 4. lépés: DataTable importálása sorstílusokkal – **Import datatable to excel**

A stílusok elkészültek, az utolsó lépés a `DataTable` betöltése a munkalapra, miközben a megfelelő stílust minden sorra alkalmazzuk.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` azt jelzi a metódusnak, hogy az oszlopfejléceket az első sorba írja.  
- `0, 0` a bal‑felső sarkot (A1) jelöli beillesztési pontként.  
- `rowStyles` minden `Style`-t a megfelelő adat sorhoz illeszt, így megkapjuk a korábban előkészített váltakozó színeket.

## 5. lépés: Munkafüzet mentése

A puzzle utolsó darabja a munkafüzet fájlba mentése, hogy megnyithasd Excelben és lásd az eredményt.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Nyisd meg a fájlt, és egy rendezett táblázatot kell látnod:

- Fejléc sor félkövérrel (alapértelmezett könyvtári stílus).  
- 1., 3., 5.… sor tiszta fehér háttérrel.  
- 2., 4., 6.… sor finom világos‑sárga kitöltéssel, ami könnyűvé teszi a áttekintést.

### Várható kimenet pillanatképe

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

A 2., 4., 6., … sorok világos‑sárga háttérrel jelennek meg – pontosan a **apply alternating row colors** hatást elérve.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Az alt szöveg tartalmazza az elsődleges kulcsszót a SEO-hoz.)*

## Szélhelyzetek és változatok kezelése

### Üres DataTable

Ha a `dataTable.Rows.Count` nulla, a `rowStyles` tömb üres lesz, és az `ImportDataTable` továbbra is írni fogja a fejléc sort (ha az `includeHeaders` `true`). Kivétel nem keletkezik, de érdemes lehet védekezni egy szinte üres fájl generálása ellen:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Egyedi színsémák

Szeretnél kék/szürke csíkot a sárga/fehér helyett? Csak cseréld le a `Color` értékeket:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Nyugodtan húzd a színeket egy konfigurációs fájlból, hogy a nem fejlesztők is módosíthassák a palettát kód érintése nélkül.

### Stílusok újrahasználata több munkalapon

Ha több táblát exportálsz ugyanabba a munkafüzetbe, egyszer generálhatod a stílus tömböt és újra felhasználhatod:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Csak ügyelj arra, hogy mindkét tábla ugyanannyi sort tartalmazzon, vagy generálj új tömböt minden laphoz.

## Teljes működő példa

Összeállítva mindent, itt egy önálló program, amelyet beilleszthetsz egy konzolos alkalmazásba.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Futtasd a programot, nyisd meg a `Report.xlsx`-t, és a leírt módon fogod látni a váltakozó háttérszínt.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}