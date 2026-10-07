---
category: general
date: 2026-03-21
description: Hogyan exportáljunk Excel adatokat oszlopnevekkel, megőrizve a számformátumot,
  és olvassunk be konkrét sorokat az Aspose.Cells C# használatával. Tanulja meg, hogyan
  olvassa be az Excel munkalapot, és exportálja hatékonyan a kiválasztott sorokat.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: hu
og_description: Hogyan exportáljunk Excel adatokat oszlopnevekkel, megőrizve a számformátumot,
  és olvassunk specifikus sorokat az Aspose.Cells segítségével. Teljes, futtatható
  példa C# fejlesztőknek.
og_title: Excel adatok exportálása C#-ban – Teljes programozási útmutató
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel adatok exportálása C#‑ban – Lépésről lépésre útmutató
url: /hu/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan exportáljunk Excel adatokat C#-ban – Teljes programozási útmutató

Gondolkodtál már azon, **hogyan exportálj excel** adatokat anélkül, hogy elveszítenéd az eredeti formázást? Lehet, hogy már próbáltál gyors másolás‑beillesztést, és a dátumok „44728” formában jelentek meg, vagy hiányoznak az oszlopfejlécek. Ez frusztráló, igaz? Ebben az útmutatóban egy tiszta, vég‑től‑végig megoldást mutatunk be, amellyel beolvashatsz egy Excel munkalapot, megőrizheted a számformátumot, exportálhatsz oszlopnevekkel, és még csak a szükséges sorokat is kiválaszthatod.

Az Aspose.Cells könyvtárat fogjuk használni, mert finomhangolt vezérlést biztosít az exportálási beállítások felett. A útmutató végére egy újrahasználható kódrészletet kapsz, amely bármely .NET projektbe beilleszthető, és megérted, miért fontos minden egyes opció. Külső dokumentációra nincs szükség – minden, amire szükséged van, itt található.

---

## Amit megtanulsz

- **Excel munkalap beolvasása** memóriába beolvasása az Aspose.Cells segítségével.
- **Specifikus sorok exportálása** (pl. 0‑49 sorok) az oszlopnevek megtartása mellett.
- **Számformátum megőrzése**, hogy a pénznemek, dátumok és százalékok változatlanok maradjanak.
- Hogyan **exportálj oszlopnevekkel**, és ha szükséges, cellakommentárokat is belefoglalj.
- Teljes, azonnal futtatható C# példa plusz tippek a gyakori buktatókhoz.

### Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.6+ verzióval is működik).
- Aspose.Cells for .NET telepítve NuGet-en keresztül (`Install-Package Aspose.Cells`).
- Egy Excel fájl (`input.xlsx`) egy olyan mappában, amelyre hivatkozhatsz.

> **Pro tipp:** Ha CI pipeline-on dolgozol, fontold meg a NuGet csomag privát tárolóból való lehúzását, hogy elkerüld a licencelési meglepetéseket.

---

## 1. lépés – Aspose.Cells telepítése és névterek hozzáadása

Először győződj meg róla, hogy az Aspose.Cells csomag a projektedben van. Nyisd meg a Package Manager Console-t, és futtasd:

```powershell
Install-Package Aspose.Cells
```

Ezután add hozzá a szükséges `using` direktívákat a C# fájlod tetejéhez:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Ezek az importok hozzáférést biztosítanak a `Workbook`, `Worksheet`, `ExportTableOptions` és `DataTable` osztályokhoz – a **Excel munkalap beolvasása** és az adatok exportálásához szükséges alapdarabokhoz.

---

## 2. lépés – A munkafüzet betöltése (Excel fájl beolvasása)

Most már ténylegesen **beolvassuk az Excel munkalapot**. A `Workbook` konstruktor a fájl elérési útját várja, és az Aspose.Cells kezeli mind a `.xlsx`, mind a régebbi `.xls` formátumokat.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Miért fontos:** A munkafüzet egyszeri betöltése és ugyanannak a `Worksheet` objektumnak a többszöri újrahasználata sokkal hatékonyabb, mint a fájl ismételt megnyitása, különösen nagy táblázatok esetén.

---

## 3. lépés – Exportálási beállítások konfigurálása (Számformátum megőrzése és oszlopnevek)

Itt mondjuk meg az Aspose.Cells‑nek, *hogyan* exportáljon. Az `ExportTableOptions` osztály lehetővé teszi a kimenet finomhangolását. Három jelzőt fogunk engedélyezni:

1. `ExportAsString = true` – minden cellát karakterlánccá kényszerít, ami garantálja, hogy a számok megőrzik a vizuális megjelenésüket.
2. `IncludeCellComments = true` – másolja a cellákhoz csatolt megjegyzéseket (hasznos dokumentációhoz).
3. `PreserveNumberFormat = true` – megtartja az eredeti számformátumot (pénznem szimbólumok, dátumformátumok stb.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Különleges eset:** Ha `ExportAsString`‑t `false`‑ra állítod, de mégis meg akarod tartani a számformátumokat, nyers numerikus értékekkel (pl. 44728 egy dátum esetén) találkozhatsz. Mindkét jelző bekapcsolása elkerüli ezt a meglepetést.

---

## 4. lépés – Az első munkalap lekérése (Excel munkalap beolvasása)

A legtöbb egyszerű fájlban a szükséges adatok az első lapon vannak, ezért index alapján fogjuk lekérni. Ha másik lapra van szükséged, egyszerűen cseréld le a `0`‑t a megfelelő nulláról induló indexre, vagy használd a `workbook.Worksheets["SheetName"]` szintaxist.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Miért hasznos:** A munkalap objektum közvetlen elérése teljes kontrollt ad a `Cells` gyűjtemény felett, ami elengedhetetlen a későbbi **specifikus sorok exportálásához**.

---

## 5. lépés – Cellatartomány exportálása (Specifikus sorok exportálása)

Most jön a tutorial szíve: a 0‑49 sorok és 0‑4 oszlopok (azaz az első 50 sor és az első öt oszlop) exportálása egy `DataTable`‑be. Emellett kérni fogjuk az Aspose.Cells‑t, hogy a `DataTable` első sorában szerepeljenek az oszlopnevek.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Mit csinál ez

- **`startRow: 0`** – a lap tetejéről indul.
- **`totalRows: 50`** – az első 50 sort veszi (azaz **specifikus sorok exportálása**).
- **`totalColumns: 5`** – az exportot az első öt oszlopra korlátozza.
- **`includeColumnNames: true`** – biztosítja, hogy a `DataTable` oszlopfejlécei megegyezzenek az Excel fejléc sorával, ezzel teljesítve a **oszlopnevekkel exportálás** követelményt.
- **`exportOptions`** – a 3. lépésben beállított opciókat alkalmazza, így a numerikus értékek “$1,234.56” formában maradnak, nem “1234.56”.

---

## 6. lépés – Az export ellenőrzése (Hogyan néz ki az eredmény)

Nyomtassuk ki az első néhány sort a konzolra, hogy lásd, a formázás megmaradt.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Várható kimenet (példa):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Vedd észre, hogy a dátumok `MM/dd/yyyy` formátumban jelennek meg, és a pénznem megtartja a `$` szimbólumot – köszönhetően a **számformátum megőrzésének**.

---

## Gyakori buktatók és hogyan kerüld el őket

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| A dátumok nagy számokká alakulnak | `ExportAsString` `false`‑ra van állítva | `ExportAsString = true` megtartása vagy a cellák kézi konvertálása |
| Hiányzó oszlopfejlécek | `includeColumnNames` `false`‑ra van állítva | `true`‑ra állítás, ha **oszlopnevekkel exportálásra** van szükség |
| A kommentek eltűnnek | `IncludeCellComments` nincs engedélyezve | `IncludeCellComments` bekapcsolása az `ExportTableOptions`‑ban |
| A rossz munkalap exportálása | A `Worksheets[0]` használata több lapos fájlon | Add meg a lap nevét: `workbook.Worksheets["Data"]` |
| Tartományon kívüli kivétel | `totalRows` meghaladja a tényleges sorok számát | `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` használata |

---

## Bónusz: Az egész lap exportálása a formátumok megőrzése mellett

Ha később úgy döntesz, hogy az egész lapra szükséged van, egyszerűen cseréld le a `totalRows` és `totalColumns` értékeket a lap maximális méreteire:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Most már van egy **Excel munkalap beolvasása** rutinod, amely bármilyen méretű lapra működik, miközben továbbra is **a számformátum megőrzése** és **oszlopnevekkel exportálás** biztosított.

---

## Teljes működő példa (másolás‑beillesztés kész)

Az alábbiakban a teljes program található, amelyet beilleszthetsz egy konzolos alkalmazásba. Tartalmazza az összes lépést, importot és egy egyszerű ellenőrző kiírást.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Mentsd el `Program.cs` néven, futtasd a `dotnet run` parancsot, és a terminálodban meg kell jelennie a formázott előnézetnek.

---

## Összegzés

Most végigvettük, **hogyan exportálj excel** adatokat az Aspose.Cells segítségével, lefedve mindent a munkafüzet betöltésétől a számformátum megőrzésig, az oszlopnevekkel történő exportálásig, és a specifikus sorokra való korlátozásig. A kód önálló, teljesen futtatható, és gyakorlati védelmeket tartalmaz a leggyakoribb különleges esetekhez.

Készen állsz a következő kihívásra? Próbáld meg közvetlenül CSV‑be exportálni, miközben megtartod az eredeti számformátumot, vagy küldd a `DataTable`‑t egy Entity Framework Core kontextusba tömeges adatbázis‑beillesztéshez. Mindkét forgatókönyv az itt bemutatott alapokra épül.

Ha hasznosnak találtad ezt az útmutatót

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}