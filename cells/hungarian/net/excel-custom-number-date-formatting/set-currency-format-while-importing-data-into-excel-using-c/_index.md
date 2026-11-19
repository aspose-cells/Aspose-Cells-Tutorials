---
category: general
date: 2026-11-19
description: Állíts be pénznemformátumot Excelben C#-val – tanuld meg, hogyan állíthatod
  be a számformátumot és formázhatod az Excel oszlopokat egy munkalap importálása
  során.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: hu
lastmod: 2026-11-19
og_description: Állíts be pénznemformátumot Excelben C#-val, és fedezd fel, hogyan
  állítható be a számformátum, hogyan rendelhető számformátum, és hogyan formázhatók
  az Excel oszlopok egy Excel munkalap importálása során.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Pénznemformátum beállítása Excelben C#‑val – teljes lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Pénznemformátum beállítása adat importálásakor Excelbe C#-val
url: /hu/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pénznemformátum beállítása Excel-be történő adatimportálás során C#-al

Ha **pénznemformátumot** kell beállítania egy Excel munkalapon, ez az útmutató megmutatja, hogyan **állíthat be számformátumot** és formázhatja az oszlopokat egy **excel munkalap importálása** közben. Egy teljes, futtatható példát fog látni, amely a megfelelő számformátumot rendeli minden `DataTable` oszlophoz, és a kívánt stílussal importálja az adatokat.

Az Excel-lel való munka C#-ból gyakran többet igényel, mint a nyers értékek egyszerű kiírása – szabályoznia kell, hogyan jelennek meg a számok. Legyen szó számlák, pénzügyi jelentések vagy műszerfalak készítéséről, a pénznemek, százalékok vagy dátumok helyes formázása azonnal olvashatóvá teszi a kimenetet.

## Előkövetelmények

* .NET 6.0 (vagy újabb) telepítve.
* Hivatkozás a **Aspose.Cells for .NET**-re (vagy bármely olyan könyvtárra, amely `Style` osztályt biztosít `Number` tulajdonsággal).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Alapvető ismeretek a `DataTable` és a C# gyűjtemények használatáról.
* Fejlesztőkörnyezet, például Visual Studio 2022 vagy VS Code.

## 1. lépés: A munkalapba írandó adatok lekérdezése

Először szerezzen be egy `DataTable`-t, amely a kívánt nyers adatokat tartalmazza. Valós projektekben ez származhat adatbázis-lekérdezésből, API‑hívásból vagy CSV‑elemzőből.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Miért fontos:** Egy teljesen feltöltött `DataTable` importálása lehetővé teszi, hogy az adatlekérdezési logikát elkülönítse az Excel‑generálási logikától, ami javítja a tesztelhetőséget és a karbantarthatóságot.

## 2. lépés: Stílus tömb létrehozása – egy bejegyzés a DataTable minden oszlopához

Az Aspose.Cells egy `Style[]` tömböt vár, amelynek hossza megegyezik a importálni kívánt oszlopok számával. Minden elem egy adott számformátumot tárolhat.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro tipp:** Még ha csak az oszlopok egy részére van szükség formázásra, minden oszlophoz létre kell hozni egy `Style` példányt; ellenkező esetben `NullReferenceException`-t kap importáláskor.

## 3. lépés: Számformátum hozzárendelése a kívánt oszlopokhoz

A beépített stílus számok könyvtáranként eltérnek. Az Aspose.Cells-ben:

* `0` → Általános (egész)  
* `2` → Pénznem (pl. `$#,##0.00`)  
* `3` → Dátum, stb.

Itt **számformátumot** rendelünk két oszlophoz: az első oszlop (Id) egész marad, míg a második oszlop (Amount) pénznemformátumot kap.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Hogyan állítsuk be a számformátumot**: A `Number` tulajdonság használata a leggyorsabb módja egy beépített formátum kiválasztásának. Helyi pénznemek esetén fontolja meg egy egyedi formátumstring használatát, amely tartalmazza a megfelelő pénznemszimbólumot.

## 4. lépés: A DataTable importálása a munkalapba, az oszlopszámok stílusainak alkalmazásával

Miután a stílus tömb készen áll, importálja az adatokat. Az `ImportDataTable` metódus figyelembe veszi a megadott stílusokat.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Várt eredmény

Amikor megnyitja a **FinancialReport.xlsx** fájlt, a következőt fogja látni:

| Azonosító | Összeg      | Leírás           |
|----|------------|------------------|
| 1  | $1,234.56  | Irodai kellékek |
| 2  | $98,765.43 | Tanácsadási díjak |
| 3  | $0.99      | Egyéb            |

*Az **Összeg** oszlop a beállított pénznemformátummal jelenik meg, míg az **Azonosító** egész marad.*

## Hogyan állítsunk be számformátumot további helyzetekben

### Számformátum hozzárendelése dátumoszlopokhoz

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Egyedi számformátumok használata százalékokhoz

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Formázás a számformátumokon túl

Ugyanazon `Style` objektumon belül beállíthat betűtípust, háttérszínt vagy igazítást is:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Miért működik:** A `Style` objektum összegyűjti a cella összes vizuális tulajdonságát. Amikor a tömböt átadja az `ImportDataTable`‑nek, minden cella automatikusan örökli a meghatározott stílust.

## Gyakori buktatók és elkerülésük módja

| Buktató | Tünet | Megoldás |
|---------|-------|----------|
| A `Style` példányosításának elmaradása | `NullReferenceException` importáláskor | Iteráljon végig a tömbön, és a tulajdonságok beállítása előtt hívja a `CreateStyle()`‑t. |
| Rossz beépített számindex használata | Helytelen formátum (pl. a dátumok egész számként jelennek meg) | Tekintse meg a könyvtár dokumentációját a megfelelő `Number` állandókért. |
| A munkafüzet mentésének elmulasztása | Nincs kimeneti fájl vagy üres fájl | Hívja meg a `workbook.Save(...)`‑t az import befejezése után. |
| A pénznem szimbólum helyi beállításának eltérése | `$` jelenik meg még nem US helyi beállításoknál is | Használjon egyedi formátumstringet a megfelelő szimbólummal (pl. "€#,##0.00"). |

## Teljes, futtatható példa



## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeiben.

- [Excel fájl létrehozása C# – cellák formázása és pénznemformátum beállítása](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Hogyan formázzuk az Excel oszlopokat C#-ban – Teljes útmutató](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Excel munkafüzet létrehozása C# – Pénznemformátum alkalmazása és DataTable importálása](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}