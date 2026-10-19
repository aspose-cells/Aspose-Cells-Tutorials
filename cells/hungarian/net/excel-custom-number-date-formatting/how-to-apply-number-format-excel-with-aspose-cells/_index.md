---
category: general
date: 2026-10-10
description: Alkalmazzon számformátumot az Excelben gyorsan egy DataTable importálásával,
  a dátum- és pénznemformátumok beállításával, valamint a fejlécsor megőrzésével egyetlen
  lépésben.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: hu
lastmod: 2026-10-10
og_description: Alkalmazza a számformátumot Excelben C#-ban az Aspose.Cells használatával.
  Tanulja meg a dátumformátum beállítását Excelben, a pénznemformátum beállítását
  Excelben, és a fejlécsor megőrzését Excelben egy DataTable importálásakor.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Számformátum alkalmazása Excelben C#-ban – lépésről‑lépésre útmutató
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Hogyan alkalmazz számformátumot Excelben az Aspose.Cells segítségével
url: /hu/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan alkalmazzunk számformátumot Excelben az Aspose.Cells segítségével

Ha **számformátumot kell alkalmazni Excelben** adatbetöltés közben egy `DataTable`‑ból, ez az útmutató pontosan megmutatja, hogyan. Emellett megtanulod, hogyan **állíts be dátumformátumot Excelben**, **állíts be pénznemformátumot Excelben**, és hogyan **őrizd meg a fejlécsort Excelben** az importálás során, így a kész munkalap professzionális megjelenést kap extra utófeldolgozás nélkül.

Mindent lefedünk a könyvtár telepítésétől egy teljes, futtatható kódrészlet írásáig. A végére képes leszel bármely `DataTable`‑t Excel munkafüzetbe importálni, automatikusan formázni a numerikus oszlopokat, és a fejlécsort érintetlenül hagyni – mindezt csak néhány C# sorral.

## Előfeltételek

Mielőtt elkezdenéd, győződj meg róla, hogy rendelkezel:

* .NET 6.0 vagy újabb verzióval (a kód .NET Framework 4.6+‑tal is működik)
* Visual Studio 2022‑vel (vagy bármely kedvelt C# IDE‑vel)
* **Aspose.Cells for .NET** – telepítsd a NuGet‑en keresztül:

```bash
dotnet add package Aspose.Cells
```

* `DataTable` forrás – a példában egy segédfüggvény `GetTable()`‑t használunk, amely mintaadatokat ad vissza.

> **Pro tipp:** Az Aspose.Cells egy kereskedelmi könyvtár, de ingyenes értékelő módot kínál, amely legfeljebb 30 napig letiltja a vízjelet.

## 1. lépés: Munkafüzet létrehozása és az első munkalap elérése

A `Workbook` objektum a belépési pont minden Excel művelethez. Egy új munkafüzet létrehozása egy alapértelmezett munkalapot ad index 0‑nál.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Miért ez a lépés?*  
A `Workbook` kezeli a fájlformátumot, a számítási motorot és a stílusraktárat. A `Worksheet` korai elérése lehetővé teszi, hogy később a cél munkalapot átadjuk az importálási metódusnak.

## 2. lépés: A forrásadatok lekérése DataTable‑ként

Valós projektekben az adatok gyakran adatbázis‑lekérdezésből, CSV‑parserből vagy API‑válaszból származnak. Illusztrációként egy egyszerű `DataTable`‑t generálunk három oszloppal: **Product**, **Price**, és **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Miért ez a lépés?*  
A `DataTable` egy táblázatos, memóriában tárolt reprezentációt biztosít, amelyet az Aspose.Cells közvetlenül importál, megőrizve az oszlopsorrendet és az adattípusokat.

## 3. lépés: `Style` tömb előkészítése – egy stílus oszloponként

Az Aspose.Cells lehetővé teszi, hogy az importálás során minden oszlopra külön stílust alkalmazzunk egy `Style` objektumokból álló tömb átadásával. A tömb hossza meg kell, hogy egyezzen a forrástábla oszlopainak számával.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Miért ez a lépés?*  
Ha kihagyod a kifejezett létrehozást (`CreateStyle()`), a `Number` beállítása `NullReferenceException`‑t eredményez. Minden `Style` inicializálása biztosítja, hogy a későbbi hozzárendelések sikeresek legyenek.

## 4. lépés: Számformátumok hozzárendelése – pénznem és dátum

Az Excel a beépített számformátumokat azonosítóval (ID) ismeri.  
* **14** – Pénznem (pl. `$1,234.00`)  
* **22** – Rövid dátum (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Megjegyzés:** Ha egyedi formátumra van szükséged (pl. `"¥#,##0.00"`), használd a `Style.Custom = "¥#,##0.00"`‑t a beépített ID helyett.

*Miért ez a lépés?*  
A megfelelő **számformátum** importáláskor történő alkalmazása kiküszöböli a második átfutást, amely a cellák formázását módosítaná. Emellett garantálja, hogy a **format excel cells date** és a **set currency format excel** minden sorban konzisztens legyen.

## 5. lépés: DataTable importálása a fejlécsor megőrzésével

Az `ImportDataTable` metódus képes az adatokat másolni, megtartani az első sort fejlécnek, és alkalmazni a korábban előkészített oszlopszinteket.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Várható kimenet** – Nyisd meg a `FormattedReport.xlsx` fájlt, és a következőt fogod látni:

| Termék | Ár (pénznem) | Megjelenési dátum |
|--------|--------------|-------------------|
| Widget A| $12.99       | 05/01/2023        |
| Widget B| $23.50       | 06/15/2023        |
| Widget C| $7.75        | 07/30/2023        |

A fejlécsor érintetlen, a **Price** oszlop a pénznem szimbólumát jeleníti meg, a **ReleaseDate** oszlop pedig rövid dátumformátumot – mindezt további stíluskód nélkül.

### Gyakori edge case‑ek kezelése

| Helyzet                                 | Megoldás |
|----------------------------------------|----------|
| **Több oszlop, mint stílus**            | Győződj meg róla, hogy a `columnStyles.Length` megegyezik a `sourceTable.Columns.Count`‑tal. A hiányzó bejegyzések az alapértelmezett munkafüzet‑stílust használják. |
| **Null értékek numerikus oszlopokban** | Az Excel a `null`‑t üres cellaként kezeli; a számformátum továbbra is érvényes, ha később érték kerül be. |
| **Egyedi, helyi specifikus pénznem**   | Használd a `columnStyles[i].Custom = "\"€\"#,##0.00"`‑t, és állítsd `columnStyles[i].Number = -1`‑re a beépített ID letiltásához. |
| **Nagy táblák (> 100 000 sor)**        | Fontold meg az `ImportDataTable` túlterhelést `ImportTableOptions`‑szel, hogy adatfolyamként importálj és csökkentsd a memóriaigényt. |
| **Ugyanaz a stílus több oszlopra**     | Használd ugyanazt a `Style` példányt a tömbben (pl. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bónusz: Egyedi formátumkarakterlánc használata

Ha a beépített azonosítók nem felelnek meg az igényeidnek, definiálhatsz egy egyedi számformátumot:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Ez a megközelítés teljes irányítást ad a **format excel cells date** és a **set currency format excel** felett, a predefined ID‑kön túl.

## Összegzés

Most már tudod, hogyan **alkalmazz számformátumot Excelben** hatékonyan egy `DataTable` importálásakor az Aspose.Cells‑szel. Oszloponkénti `Style` tömb létrehozásával, beépített vagy egyedi szám‑ID‑k hozzárendelésével, valamint a **preserve header row excel** opcióval rendelkező `ImportDataTable` túlterhelés használatával egyetlen lépésben készíthetsz publikálásra kész munkalapokat.

### Mi a következő?

* Fedezd fel a **set date format excel**‑t egyedi mintákkal, például `"dddd, mmmm dd, yyyy"`.
* Kombináld ezt a technikát **conditional formatting**‑kel, hogy kiemeld a tartományon kívüli értékeket.
* Használd a **format excel cells date**‑t pivot táblákban vagy diagramokban a dinamikus jelentéskészítéshez.

Nyugodtan kísérletezz különböző szám‑ID‑kkel vagy egyedi karakterláncokkal, hogy megfeleljenek a szervezeted stílusirányelveinek. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy segítsenek további API‑funkciók elsajátításában és alternatív megvalósítási módok felfedezésében saját projektjeidben.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}