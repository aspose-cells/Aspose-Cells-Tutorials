---
category: general
date: 2026-07-13
description: Formázza a dátum oszlopot Excelben, miközben DataTable-t exportál C#-ból.
  Tanulja meg az Excel exportálást DataTable-ból C#-ban, és a DataTable importálását
  Excelbe stílussal percek alatt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: hu
lastmod: 2026-07-13
og_description: Formázza könnyedén a dátum oszlopot Excelben. Ez az útmutató megmutatja,
  hogyan exportálhatja a DataTable-t Excelbe C#-ban, és hogyan importálhatja a DataTable-t
  Excelbe egyedi stílusokkal.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Dátumoszlop formázása Excelben – Lépésről lépésre C# export útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Dátum oszlop formázása Excelben – Teljes C# útmutató a DataTable exportálásához
url: /hu/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dátum oszlop formázása Excelben – Teljes C# útmutató a DataTable exportálásához

Ever needed to **format date column Excel** when pulling data from a database, but the cells kept showing raw timestamps? You're not the only one. In many business apps the default export dumps a `DateTime` value like `2024‑03‑15 00:00:00` and nobody wants that clutter.  

A jó hír, hogy közvetlenül C#-ból szabályozhatja az egyes oszlopok pontos megjelenését. Ebben az útmutatóban egy vég‑től‑végig megoldást mutatunk be, amely **excel export datatable c#**, az első oszlopra dátumstílust, a másodikra pénznemstílust alkalmaz, és végül **import datatable to excel** zökkenőmentes formázással.

A végére egy újrahasználható metódust kap, amelyet bármely .NET projektbe beilleszthet, függetlenül attól, hogy .NET 6, .NET Framework 4.8 vagy egy későbbi verziót használ.

---

## Amire szüksége lesz

- **Aspose.Cells for .NET** (vagy bármely könyvtár, amely biztosítja a `CreateStyle` és `ImportDataTable` funkciókat). A kódrészletek az Aspose-ot használják, mivel API-ja tiszta és széles körben elfogadott.
- Egy **DataTable**, amelyet már feltöltött SQL‑ből, CSV‑ből vagy bármely más forrásból.
- Visual Studio (vagy a kedvenc IDE-je).  
- .NET runtime 5.0+ (a példa a .NET 6‑ra céloz, de a régebbi keretrendszerek is ugyanúgy működnek).

Ha még nincs Aspose.Cells, szerezzen ingyenes próbaverziót a hivatalos oldalról – hitelkártya nélkül.

## 1. lépés: A forrásadatok lekérése DataTable‑ként

Először is szüksége van egy `DataTable`‑ra. Valós körülmények között ez általában a `SqlDataAdapter.Fill`‑ből származik, de a tisztaság kedvéért egy egyszerű táblát fogunk szimulálni:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro tipp:** Amikor közvetlenül tárolt eljárásból húzza az adatokat, győződjön meg róla, hogy az oszloptípusok megfelelnek a kívánt Excel formátumoknak. Egy `datetime` oszlop később a **format date column excel** stílusunk célpontja lesz.

## 2. lépés: Excel munkafüzet létrehozása és oszlopsz styles meghatározása

Most létrehozunk egy új munkafüzetet. A **format date column excel** trükkje egy `Style` objektum létrehozásában rejlik, amelynek a `Number` tulajdonságát a beépített Excel dátumformátumra (kód 14) állítjuk, majd ezt a stílust hozzárendeljük a megfelelő oszlopindexhez.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Miért `Number = 14`? Az Excel a dátumokat sorozatszámként tárolja; a 14-es formátum azt mondja a programnak, hogy a helyi beállítások rövid dátummintáját használja. Ha egy egyedi mintát szeretne (például `dd‑MMM‑yyyy`), akkor beállíthatja a `columnStyles[0].Custom = "dd-MMM-yyyy"` értéket.

## 3. lépés: A DataTable importálása a munkalapba stílusokkal

A stílus tömb elkészülte után az import hívás egyetlen sorból áll. Ez a **excel export datatable c#** magja, és ugyanakkor az a hely, ahol **import datatable to excel**-t végzünk, miközben megőrizük a formázásunkat.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Az `ImportDataTable` túlterhelés elfogadja a stílus tömböt, és minden stílust a megfelelő oszlopra alkalmaz, miközben az adatot írja. Nem szükséges utófeldolgozó ciklus – a dátumoszlop már szép formátumban jelenik meg.

## 4. lépés: A munkafüzet mentése (vagy közvetlen stream‑elése a böngészőnek)

A szituációtól függően menthet a lemezre, egy memória stream‑be, vagy visszaküldheti a fájlt HTTP válaszként. Íme három gyakori minta:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Figyeljen:** Ha ASP.NET Core‑ban `FileResult`‑ot használ, győződjön meg róla, hogy a fájl dinamikus generálásakor beállítja a `Response.Headers["Cache-Control"] = "no-cache"` értéket. Ez megakadályozza, hogy a böngésző elavult verziót szolgáljon ki.

## 5. lépés: Az eredmény ellenőrzése – Hogyan néz ki az Excel lap

A kód futtatása után nyissa meg az `ExportedReport.xlsx` fájlt. A következőt kell látnia:

| RendelésDátuma (formázott) | Összeg (pénznem) | Vevő |
|----------------------------|------------------|------|
| 03/13/2024                 | $1,245.67        | Acme Corp|
| 03/14/2024                 | $980.00          | Beta Ltd |
| 03/15/2024                 | $1,500.25        | Gamma Inc|

Figyelje meg, hogy a **format date column excel** tiszta rövid dátumot mutat, míg a pénznem oszlop automatikusan a regionális beállításoknak megfelelően igazodik. Kézi cella‑cella formázásra nincs szükség.

![format date column excel example](/images/format-date-column-excel.png)

*Image alt text: format date column excel – egy képernyőképe az Excel lapon, ahol a dátumoszlop megfelelően formázott.*

## Gyakori kérdések és speciális esetek

### Mi van, ha a DataTable-nek több mint három oszlopa van?

Egyszerűen bővítse a `columnStyles` tömböt. Bármely oszlopnál, amelyet nem formáz kifejezetten, hagyja a bejegyzést `null`‑ként; az Excel az alapértelmezett Általános formátumot alkalmazza.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Hogyan alkalmazzon egy egyedi dátumformátumot (pl. „dd‑MMM‑yyyy”)?

Cserélje le a beépített számot egy egyedi karakterláncra:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Használhatom ezt a megközelítést EPPlus-szal vagy ClosedXML-lel?

Igen, a koncepció azonos: hozzon létre egy style objektumot, rendelje hozzá egy oszlophoz, majd töltse be a `DataTable`‑t. Az API eltérő, de a **excel export datatable c#** minta ugyanaz marad.

### Mi a helyzet a nagy adatkészletekkel (100 000+ sor)?

Az `ImportDataTable` a tömeges írásra van optimalizálva, de memóriahatárokba ütközhet. Ebben az esetben fontolja meg a sorok darabonkénti streamelését a `Cells.ImportDataTable`‑vel, vagy használja a `Worksheet.Cells["A1"].PutValue`‑t egy ciklusban, miközben újrahasználja a style objektumokat.

## Teljes működő példa (minden lépés egy metódusban)

Az alábbi önálló metódus beilleszthető bármely konzolos alkalmazásba vagy ASP.NET vezérlőbe. Bemutatja a teljes folyamatot – az adatlekéréstől a stílusos Excel exportig.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Futtassa a programot, nyissa meg a `StyledExport.xlsx` fájlt, és tökéletesen alkalmazva látni fogja a **format date column excel**-t.

## Összefoglalás és következő lépések

Most bemutattuk, hogyan **format date column excel** egy **excel export datatable c#** során, és hogyan **import datatable to excel** per‑oszlopos stílusolással egyetlen hívásban. A főbb tanulságok:

1. Hozzon létre egy `Style` objektumot minden formázni kívánt oszlophoz.  
2. Használja a `Number = 14` értéket dátumokhoz, a `Number = 2` értéket pénznemhez, vagy bármilyen egyedi formátumot, amelyre szüksége van.  
3. Adja át a stílus tömböt az `ImportDataTable`‑nek – a könyvtár elvégzi a nehéz munkát.

Mit szeretne legközelebb felfedezni?

- **Feltételes formázás** a lejárt dátumok kiemeléséhez.  
- **

## Mit érdemes legközelebb megtanulni?

Az alábbi útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljesen működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Hogyan importáljunk DataTable-t Excelbe Aspose.Cells for .NET használatával (lépésről‑lépésre útmutató)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Excel adatok exportálása DataTable-be Aspose.Cells for .NET‑vel: Teljes útmutató](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [HTML karakterláncok exportálása Excelből DataTable-be Aspose.Cells for .NET‑vel: Lépésről‑lépésre útmutató](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}