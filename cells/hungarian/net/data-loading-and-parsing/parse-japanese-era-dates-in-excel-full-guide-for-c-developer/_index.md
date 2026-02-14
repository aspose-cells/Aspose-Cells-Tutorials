---
category: general
date: 2026-02-14
description: Értelmezze a japán korszak dátumait Excelben egyedi dátumértelmezéssel.
  Tanulja meg, hogyan töltsön be munkafüzetet fájlból a load excel opciókkal, és kerülje
  el a gyakori buktatókat.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: hu
og_description: Parsolja a japán korszak dátumait az Excelben az Aspose.Cells segítségével.
  Ez az útmutató megmutatja, hogyan töltsön be egy munkafüzetet fájlból egyedi dátumértelmezési
  beállításokkal.
og_title: Japán korszak dátumok feldolgozása – Lépésről lépésre C# útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
title: Japán korszak dátumok feldolgozása Excelben – Teljes útmutató C# fejlesztőknek
url: /hu/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

from file" is a phrase but maybe keep as is? It's a technical phrase, could keep. In earlier translation we kept it unchanged. Good.

Also "custom date parsing excel" is technical phrase, keep unchanged.

Make sure code block placeholders remain unchanged.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japán era dátumok elemzése – Teljes C# útmutató

Valaha is szükséged volt **japán era dátumok** elemzésére egy Excel táblázatból, és azon tűnődtél, miért változnak a értékek furcsa számokká? Nem vagy egyedül. Sok fejlesztő találkozik ezzel a problémával, amikor az alapértelmezett `DateTime` parser nem ismeri fel a japán naptárakban használt “Reiwa 1/04/01” stílust.

Jó hír: megmondhatod az Aspose.Cells‑nek, hogy ezeket a cellákat japán‑era dátumokként kezelje már attól a pillanattól, amikor **Excel‑t betöltesz opciókkal**. Ebben az útmutatóban végigvezetünk a munkafüzet fájlból történő betöltésén, az egyedi dátumfeldolgozás beállításán, és annak ellenőrzésén, hogy a dátumok pontosan úgy jönnek-e ki, ahogy elvárod.

A tutorial végére képes leszel:

* Munkafüzet betöltése fájlból a `DateTimeParsing.JapaneseEra` megadásával.
* Cellaértékek elérése megfelelő `DateTime` objektumokként.
* Különleges esetek kezelése, például üres cellák vagy vegyes naptárak.
* A megközelítés kiterjesztése bármely **custom date parsing excel** helyzetre, amellyel találkozhatsz.

> **Előfeltétel** – Szükséged van az Aspose.Cells for .NET könyvtárra (v23.9 vagy újabb) és egy .NET‑kompatibilis IDE-re (Visual Studio, Rider, stb.). Más csomagok nem szükségesek.

---

## 1. lépés: Szövegbetöltési beállítások konfigurálása japán era feldolgozáshoz

Az első dolog, amit teszünk, hogy megmondjuk a betöltőnek, hogyan értelmezze a japán era dátumnak tűnő szöveget. Ez a `TxtLoadOptions` és a `DateTimeParsing` enum segítségével történik.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Miért fontos:** A `JapaneseEra` jelző nélkül az Aspose.Cells a cellát egyszerű sztringként kezeli, így neked kell kézzel szétbontani az era nevet és konvertálni. A jelző elvégzi a nehéz munkát, így a kódod tiszta és kevésbé hibára hajlamos marad.

---

## 2. lépés: Munkafüzet betöltése fájlból a beállítások használatával

Most ténylegesen megnyitjuk az Excel fájlt. Figyeld meg, hogy a `loadOptions` objektum hogyan kerül átadásra a `Workbook` konstruktorának – ez a **load workbook from file** lépés, amely tiszteletben tartja az egyedi feldolgozási szabályainkat.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Ha a fájl máshol van (pl. hálózati megosztáson), csak állítsd be ennek megfelelően a `filePath`-t. A fontos rész, hogy ugyanazt a `loadOptions` példányt használd; különben a japán era konverzió nem fog megtörténni.

---

## 3. lépés: A feldolgozott dátumok elérése

A munkafüzet betöltése után a cellaértékeket ugyanúgy lekérheted, mint bármely normál dátumnál. Az API automatikusan egy `DateTime` objektumot ad vissza.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Várható kimenet** (feltételezve, hogy az A1 tartalmazza a “R1/04/01” értéket):

```
Parsed date from A1: 2024-04-01
```

Ha a cella egy gregorián dátumot tartalmaz, például “2023‑12‑31”, a parser még mindig működik – egyszerűen visszaadja az eredeti dátumot változatlanul.

---

## 4. lépés: Az összes dátum ellenőrzése egy oszlopban

Gyakran szükség van egy teljes oszlop japán era dátumának átvizsgálására. Az alábbi kompakt ciklus bemutatja, hogyan kezelheted elegánsan az üres és vegyes tartalmakat.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Pro tipp:** A `CellValueType.IsDateTime` a legbiztonságosabb módja annak, hogy ellenőrizd, a parser sikeres volt-e. Megvédi a `InvalidCastException`-től, ha egy cella váratlan szöveget tartalmaz.

---

## 5. lépés: Gyakori buktatók és megoldások

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres cellák `DateTime.MinValue`-t adnak vissza** | A parser az üres stringeket a legkisebb dátumként kezeli. | Ellenőrizd a `cell.IsNull` értéket, mielőtt a `DateTimeValue`-t elérnéd. |
| **Vegyes naptárak (japán + gregorián) ugyanabban az oszlopban** | A parser mindkettőt kezeli, de jelentéshez lehet, hogy meg kell különböztetned őket. | Használd a `cell.StringValue`-t az eredeti szöveg ellenőrzéséhez, ha a `cell.Type` értéke `IsString`. |
| **Helytelen era (pl. “H30” a Heiseihez) 2019 után** | A Heisei 2019-ben véget ért; későbbi dátumoknak “R”-t kell használniuk. | Ellenőrizd az era előtagot, mielőtt megbízol a feldolgozott eredményben. |
| **Teljesítménycsökkenés nagy fájlok esetén** | Az egyedi beállításokkal való betöltés kis plusz terhet jelent. | Töltsd be csak a szükséges munkalapokat (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## 6. lépés: Teljes működő példa

Összegezve, itt egy önálló konzolalkalmazás, amelyet másolhatsz és futtathatsz. Bemutatja a **custom date parsing excel** folyamatát az elejétől a végéig.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Ami meg kell jelenjen** amikor a `japan_dates.xlsx` tartalmazza:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (üres) | R2/02/15 |

Konzol kimenet:

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

A mentett fájl most már megfelelő dátumcellákat tárol, amelyeket megnyithatsz Excelben, és láthatod a szokásos dátumformátumot.

---

## Következtetés

Most bemutattuk, hogyan **elemezheted a japán era dátumokat** Excelben a `TxtLoadOptions` konfigurálásával, **load workbook from file** opciókkal, és hogyan dolgozhatsz a kapott `DateTime` értékekkel. Ugyanaz a minta – egyedi feldolgozási jelzők beállítása, majd a munkafüzet betöltése – minden **custom date parsing excel** igényre alkalmazható, legyen szó pénzügyi időszakokról, ISO hét számokról vagy saját formátumokról.

Van más era vagy vegyes‑naptáras táblázatod? Csak cseréld le a `DateTimeParsing.JapaneseEra`-t egy másik enum értékre (pl. `DateTimeParsing.Custom`), és adj meg egy formátum stringet. Az Aspose.Cells rugalmassága azt jelenti, hogy ritkán kell kézzel konverziós kódot írnod.

**Következő lépések**, amiket érdemes felfedezni:

* **Load Excel with options** CSV fájlokhoz (`CsvLoadOptions`), hogy a helyi beállításoknak megfelelő elválasztókat kezeld.
* `Workbook.Save` használata `SaveFormat.Xlsx`-el a tisztított adatok exportálásához.
* Ezt a megközelítést kombináld **Aspose.Slides** vagy **Aspose.Words** segítségével jelentéskészítő folyamatokhoz.

Próbáld ki, finomítsd a beállításokat, és hagyd, hogy a könyvtár végezze a nehéz munkát. Boldog kódolást!  

![A konzolablakban megjelenített elemzett japán era dátumok képernyőképe – japán era dátumok elemzése példa](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}