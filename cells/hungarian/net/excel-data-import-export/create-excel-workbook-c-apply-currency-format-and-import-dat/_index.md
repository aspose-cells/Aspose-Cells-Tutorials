---
category: general
date: 2026-03-30
description: Excel munkafüzet létrehozása C#‑ban pénznem formázással. Tanulja meg,
  hogyan importáljon egy DataTable‑t, adjon számformátumot az Excelhez, és pár perc
  alatt alkalmazzon pénznem formátumú oszlopot.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: hu
og_description: Excel munkafüzet létrehozása C#‑ban és a cellák azonnali pénznem formázása.
  Ez a lépésről‑lépésre útmutató bemutatja, hogyan importáljunk egy DataTable‑t Excelbe,
  és hogyan adjunk számformátumot egy oszlopnak Excelben.
og_title: Excel munkafüzet létrehozása C#-ban – Pénznem formázási útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel munkafüzet létrehozása C#‑ban – Pénznem formátum alkalmazása és DataTable
  importálása
url: /hu/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel munkafüzet létrehozása C#‑ban – Pénznem formátum alkalmazása és DataTable importálása

Volt már szükséged **create Excel workbook C#**-ra, ami már úgy néz ki, mint egy kifinomult jelentés? Lehet, hogy egy adatbázisból húzod a sales számokat, és azt szeretnéd, hogy az ár oszlop dollárban jelenjen meg anélkül, hogy manuálisan bajkálnál az Excelben. Ismerős? Nem vagy egyedül – a legtöbb fejlesztő erre a problémára fut bele, amikor először automatizálja az Excel exportokat.

Ebben az útmutatóban végigvezetünk egy teljes, azonnal futtatható megoldáson, amely **creates an Excel workbook C#**, importál egy `DataTable`‑t, és **formats the Price column as currency**. A végén lesz egy `StyledTable.xlsx` nevű fájlod, amelyet megnyithatsz, és szép formázott számokat láthatsz. Nem szükséges extra utófeldolgozás.

> **Mit fogsz megtanulni**
> - Hogyan állítsd be az Aspose.Cells‑t egy .NET projektben  
> - Hogyan **import datatable to excel** egy stílus tömbbel  
> - Hogyan **add number format excel** egy adott oszlophoz  
> - Tippek több oszlop vagy különböző helyi beállítások kezeléséhez  

> **Előfeltételek**  
> - .NET 6+ (vagy .NET Framework 4.6+) telepítve  
> - Aspose.Cells for .NET NuGet csomag (`Install-Package Aspose.Cells`)  
> - Alapvető ismeretek C#‑ban és DataTables‑ban  

---

## Step 1: Prepare the DataTable (import datatable to excel)

Először is szükségünk van néhány mintára. Egy valós alkalmazásban valószínűleg egy DB lekérdezésből töltenéd fel ezt a táblát, de egy hard‑coded példa egyszerűen tartja a dolgokat.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Miért fontos*: A `DataTable` a híd a vállalati adataid és az Excel fájl között. Az Aspose.Cells közvetlenül importálja, megőrizve az oszlopneveket és az adattípusokat.

---

## Step 2: Spin Up a New Workbook (create excel workbook c#)

Most létrehozzuk a tényleges Excel fájl objektumot. Gondolj rá úgy, mint egy üres vászonra, amelyre festeni fogsz.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tipp:** Ha több munkalapra van szükséged, hívd a `workbook.Worksheets.Add()`‑t, és adj mindegyiknek egy értelmes nevet.

---

## Step 3: Define a Currency Style (format cells currency)

Az Aspose.Cells lehetővé teszi, hogy egy `Style` objektumot készíts, amely leírja, hogyan kell kinézzenek a cellák. Pénznemhez a beépített számformátum ID 164‑et (`"$#,##0.00"`) használjuk.

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Miért ne csak a formátum karakterláncot állítanád be?* A beépített ID használata biztosítja a kompatibilitást az Excel verziók között, és elkerüli a helyi beállításokra specifikus furcsaságokat.

---

## Step 4: Build the Style Array (apply currency format column)

DataTable importálásakor átadhatsz egy `Style` objektumok tömbjét – egyet oszloponként. A `null` azt jelenti, hogy „használd az alapértelmezett stílust”. Itt csak a második oszlopra alkalmazzuk a `priceStyle`‑t.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Ha később több oszlopot adsz hozzá, egyszerűen bővítsd a tömböt ennek megfelelően. A `columnStyles` hossza meg kell, hogy egyezzen az importált oszlopok számával, különben az Aspose kivételt dob.

---

## Step 5: Import the DataTable with Styles (import datatable to excel)

Most megtörténik a varázslat – a `DataTable` a munkalapra kerül, és az ár oszlop azonnal pénznemként jelenik meg.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Mi van, ha több mint két oszlopod van?* Egyszerűen bővítsd a `columnStyles`‑t, hogy minden oszlop a megfelelő stílust kapja (vagy `null` az alapértelmezetthez). Ez a legrendezettebb módja a **add number format excel** szelektív alkalmazásának.

---

## Step 6: Save the Workbook (create excel workbook c#)

Végül a fájlt leírjuk a lemezre. Válassz egy mappát, amelyhez írási jogosultságod van.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Nyisd meg a `StyledTable.xlsx`‑t Excelben, és a következőt kell látnod:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

A **Price** oszlop már pénznemként van formázva – nincs szükség további lépésekre.

---

## Edge Cases & Variations

### More Columns, Different Formats

Ha több oszlopra (pl. Cost, Tax, Total) kell **format cells currency** alkalmazni, hozz létre egy külön `Style`‑t minden egyeshez, és töltsd fel a `columnStyles`‑t ennek megfelelően:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑Specific Currency

Euro vagy brit font esetén használj különböző beépített ID‑kat (pl. 165 a `€#,##0.00`‑hez). Alternatívaként állíts be egy egyedi formátum karakterláncot:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Large Data Sets

Az Aspose.Cells képes millió sor kezelésére, de a memóriahasználat a stílusobjektumokkal nő. Használd újra ugyanazt a `Style` példányt minden pénznem oszlophoz, hogy alacsonyan tartsd a memóriaigényt.

### Missing Styles

Ha a `columnStyles` rövidebb, mint az oszlopok száma, az Aspose az alapértelmezett stílust alkalmazza a maradék oszlopokra. Ez hasznos, ha csak néhány oszlop érdekel.

---

## Full Working Example (All Steps Combined)

Az alábbiakban a teljes program található, amelyet beilleszthetsz egy konzolos alkalmazásba. Tartalmazza az összes korábban tárgyalt részt, valamint néhány hasznos megjegyzést.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Várt eredmény:** A `StyledTable.xlsx` megnyitása a `Price` oszlopot dollárjellel és két tizedesjeggyel mutatja, pontosan úgy, ahogy a `format cells currency` utasítás megkövetelte.

---

## Frequently Asked Questions

**K: Működik ez .NET Core‑dal?**  
V: Teljesen. Az Aspose.Cells .NET‑standard kompatibilis, így célozhatsz .NET 5, .NET 6 vagy későbbi verziót változtatás nélkül.

**K: Mi van, ha a DataTable‑m 10 oszlopot tartalmaz, de csak az 5‑ödik oszlopot szeretném formázni?**  
V: Hozz létre egy `Style[]` tömböt 10 hosszúságúval, töltsd fel a 0‑4 és 6‑9 pozíciókat `null`‑lal, és helyezd a saját stílusodat a 4‑es indexre (nullától számítva). Az Aspose minden bejegyzést figyelembe vesz.

**K: El tudom rejteni a fejléc sort?**  
V: Importálás után állítsd be a `worksheet.Cells.Rows[0].Hidden = true;` értéket, vagy egyszerűen add meg `false`‑t az `includeColumnNames` paraméternek az `ImportDataTable`‑nél.

---

## Conclusion

Most **created an Excel workbook C#**‑t hoztunk létre, importáltunk egy `DataTable`‑t, és **applied a currency format column**‑t használtuk az Aspose.Cells‑szel. Az elsődleges lépések – az adatok előkészítése, egy stílus definiálása, a stílus tömb felépítése, importálás `ImportDataTable`‑vel, és a mentés – lefedik a legtöbb Excel‑automatizálási feladat alapját.

From here you might explore:

- **add number format excel** dátumok vagy százalékok esetén  
- Több munkalap exportálása egyetlen fájlba  
- **format cells currency** használata helyi specifikus szimbólumokkal  
- Diagramok automatikus létrehozása ugyanazon adatok alapján  

Próbáld ki őket, és hamarosan te leszel a csapatod Excel jelentéskészítője. Van egy saját trükköd, amit meg szeretnél osztani? Írj egy megjegyzést alább – jó kódolást!

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}