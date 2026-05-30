---
category: general
date: 2026-05-30
description: Tanulja meg, hogyan adhat hozzá váltakozó sorok színeit C# munkalapokon,
  állíthatja be a cella háttérszínét egy egységes kitöltési mintával, és könnyedén
  testreszabhatja a munkalap cellastílusát.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: hu
og_description: A C# munkalapok sorainak váltakozó színezése egyszerűen. Tanulja meg
  a cella háttér beállítását, a szilárd kitöltési mintát, és sajátítsa el a munkalap
  cellastílusát.
og_title: Váltakozó sorok színezése C# munkalapokon – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Váltakozó sorok színei C# munkalapokon – Teljes útmutató
url: /hu/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Váltakozó sor színek C# munkalapokban – Teljes útmutató

Gondolkodtál már azon, hogyan teheted csiszoltá az Excel exportodat a **váltakozó sor színek** használatával? Nem vagy egyedül – a fejlesztők folyamatosan azt kérdezik, hogyan *adjunk háttérszínt* a sorokhoz anélkül, hogy millió sor kódot kellene írni.  

Ebben a tutorialban egy egyszerű módszert mutatunk be arra, hogyan **állítsuk be a cella háttérszínét** minden sorban, alkalmazzunk **szilárd kitöltési mintát**, és irányítsuk a **munkalap cellastílusát**, hogy az eredmény olvasható és vizuálisan vonzó legyen.

## Amit megtanulsz

- Adatok lekérése egy `DataTable`‑ba (vagy bármely táblázatos forrásba).  
- `Style` objektumok tömbjének felépítése, amely két szín között váltogat.  
- A `DataTable` importálása egy munkalapba a stílusok alkalmazásával.  
- Az eredmény ellenőrzése és a színek vagy minták finomhangolása, ha szükséges.  

Nem szükséges külső eszköz, csak egy .NET környezet és egy táblázatkezelő könyvtár (a példákban **Aspose.Cells**-t használunk). A végére egy újrahasználható metódust kapsz, amelyet bármely jelentéscsővezetékbe be lehet illeszteni.

---

## 1. lépés: A forrásadatok lekérése `DataTable`‑ként

Először is – adat nélkül nincs mit formázni. Az alábbi kis segédfüggvény egy `DataTable`‑t hoz létre minta sorokkal. Egy valódi projektben ezt adatbázis‑hívással vagy CSV‑parsolóval kell helyettesíteni.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Miért fontos:** Ha az adat `DataTable`‑ban van, a munkalap motor *importálni* tudja egyetlen hívással, automatikusan megőrizve az oszlopneveket és az adattípusokat.

## 2. lépés: **Váltakozó sor színek** stílusok létrehozása

Most generálunk egy `Style` objektumok tömbjét – egyet soronként – úgy, hogy a páros sorok egy világos sárga árnyalatot, a páratlan sorok pedig egy enyhe cián színt kapjanak. Ez a **váltakozó sor színek** technika magja.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Miért használjunk **szilárd kitöltési mintát**?

A `Pattern` tulajdonság határozza meg, hogyan jelenjen meg a szín. A `Solid` kitöltés garantálja, hogy a teljes cella háttérszíne be legyen festve, ezzel megszüntetve az esetlegesen átszivárgó halvány rácsvonalakat. Ez a leggyakoribb mód a **cell background beállítására**, ha tiszta megjelenést szeretnénk.

## 3. lépés: A `DataTable` importálása az előkészített stílusokkal

A stílustömb készen áll, az import hívás egyetlen soros lesz. Az Aspose.Cells automatikusan a megfelelő stílust alkalmazza minden sorra.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Mi történik a háttérben?**  
> A könyvtár soronként iterál, átmásolja az értékeket a cellákba, majd a `rowStyles`‑ból a megfelelő `Style`‑t alkalmazza. Mivel már definiáltunk egy **szilárd kitöltési mintát**, minden cella egy sorban ugyanazt a háttérszínt örökli, így tökéletes **váltakozó sor színek** jönnek létre.

## 4. lépés: A munkafüzet mentése és az eredmény ellenőrzése

Egy gyors mentés után megnyithatod a fájlt Excelben (vagy bármely kompatibilis nézőben), és láthatod a hatást.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

A fájl megnyitásakor az 1., 3., 5… sorok világos sárga, míg a 2., 4., 6… sorok világos cián színűek lesznek. Az oszlopfejlécek fehérek maradnak, így az adatok kiemelkednek.

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*Image alt text:* **alternating row colors** screenshot of a worksheet where each row’s background alternates between light yellow and light cyan.

## 5. lépés: További testreszabás (opcionális)

### Színek módosítása

Ha a márkád más árnyalatokat használ, egyszerűen cseréld le a `Color.LightYellow` és `Color.LightCyan` értékeket bármely `System.Drawing.Color`‑ra, amelyet kedvelsz. Például:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Más **háttér típus** használata

Bár a `BackgroundType.Solid` a leggyakoribb, kísérletezhetsz a `BackgroundType.Gray125`, `BackgroundType.Horizontal` vagy a könyvtár által támogatott bármely mintával. Ez megváltoztatja a vizuális textúrát, miközben **háttérszínt ad** a celláknak.

### **Worksheet cell style** alkalmazása konkrét oszlopokra

Néha csak az adatoszlopokon szeretnéd a váltakozó hatást, az első oszlopot (pl. ID‑k) érintetlenül hagyva. Hozz létre egy külön stílust ahhoz az oszlophoz, és rendeld hozzá az import után:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Összegzés

Most már van egy komplett, újrahasználható megoldásod a **váltakozó sor színek** alkalmazására C# munkalapokban. Egy `Style` objektumok tömbjének felépítésével, a **cell background** **szilárd kitöltési mintával** történő beállításával, és a `DataTable` egyhívásos importálásával professzionális megjelenésű jelentéseket készíthetsz minimális kóddal.  

Innen tovább:

- **Add background color** a fejlécsorokhoz extra hangsúlyozásként.  
- Kombináld a technikát feltételes formázással dinamikus vizuális jelzésekhez.  
- Fedezd fel a további **worksheet cell style** tulajdonságokat, mint betűtípusok, szegélyek vagy számformátumok.

Próbáld ki a következő exportfolyamatodban – a felhasználóid hálásak lesznek a tisztább, könnyebben olvasható táblázatokért. Boldog kódolást!

## Mit tanulj meg legközelebb?

- [Set Row Height in Worksheet with Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convert Excel Cell Names to Row and Column Indices Using Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Set Worksheet Tab Colors in Excel Using Aspose.Cells .NET - A Comprehensive Guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}