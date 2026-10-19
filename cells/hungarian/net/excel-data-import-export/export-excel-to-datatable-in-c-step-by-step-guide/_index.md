---
category: general
date: 2026-03-25
description: Tanulja meg, hogyan exportálhatja az Excelt DataTable-be C#-ban gyorsan.
  Ez az útmutató lefedi az Excel exportálását oszlopnevekkel, valamint az Excel adatainak
  stringként történő exportálását a megbízható adatkezelés érdekében.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: hu
og_description: Exportálja az Excelt DataTable-be C#‑ban oszlopnevekkel és karakterlánc‑konvertálással.
  Kövesse ezt a tömör útmutatót egy azonnal futtatható megoldáshoz.
og_title: Excel exportálása DataTable-be C#-ban – Teljes útmutató
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Excel exportálása DataTable-be C#-ban – Lépésről lépésre útmutató
url: /hu/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel exportálása DataTable-be C#‑ban – Lépésről‑lépésre útmutató

Valaha is szükséged volt **export Excel to DataTable**-re, de nem tudtad, melyik beállítást kell módosítani? Nem vagy egyedül – sok fejlesztő ugyanabba a helyzetbe ütközik, amikor először próbálja a táblázat adatokat egy `DataTable`‑be betölteni.  

A jó hír? Néhány kódsorral **export Excel with column names** és akár **export Excel data as string** is elvégezhető, így elkerülheted a típus‑eltérés okozta fejfájást. Az alábbiakban egy teljes, futtatható példát találsz, valamint a beállítások „miértjét”, hogy bármely projekthez könnyedén alkalmazhasd.

## Mit fed le ez az útmutató

* Hogyan hozzunk létre egy munkafüzetet memóriában (fizikai fájl nélkül).  
* Néhány mintasor feltöltése, hogy azonnal lásd az eredményt.  
* Az `ExportTableOptions` konfigurálása úgy, hogy minden cellát stringként kezeljen.  
* Egy téglalap alakú tartomány exportálása `DataTable`‑be, miközben az első sor oszlopfejlécként marad.  
* A kimenet ellenőrzése és az első sor kiírása a konzolra.  

Nem szükséges külső dokumentációs hivatkozás – minden, amire szükséged van, itt van. Ha már van egy Excel fájlod a lemezen, egyszerűen cseréld le a munkafüzet‑létrehozó sort `new Workbook("path/to/file.xlsx")`‑re, és már használhatod.

---

## 1. lépés: A projekt beállítása és az Aspose.Cells NuGet csomag hozzáadása

Before we write any code, make sure your project references **Aspose.Cells for .NET** (the library that powers the `Workbook` class). You can add it via the NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Használd a legújabb stabil verziót (2026. március állapotában ez a 22.12), hogy megkapd a legújabb hibajavításokat és teljesítményjavításokat.

---

## 2. lépés: Munkafüzet létrehozása és mintadatok feltöltése

We’ll start with a brand‑new `Workbook` and write a couple of rows so you can see the export in action. This step also demonstrates **how to export excel to datatable** when the source data lives only in memory.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Miért fontos:* Az első sor (fejléc) beillesztésével (`A1` & `B1`) később megmondhatjuk az exportálónak, hogy az első sort oszlopnevekként kezelje – pontosan ez a **export excel with column names** jelentése.

---

## 3. lépés: Az Aspose.Cells beállítása, hogy minden cellát stringként kezeljen

When you export numeric or date cells, Aspose tries to infer the .NET type. That can cause subtle bugs if your downstream code expects strings. The `ExportTableOptions.ExportAsString` flag forces a uniform string conversion.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Miért használjuk?* Képzelj el egy olyan oszlopot, amely néha számokat, néha szöveget tartalmaz (pl. „00123” vs. „ABC”). Ha mindent stringként exportálsz, elkerülöd a vezető nullák elvesztését vagy a típuskonverziós kivételeket.

---

## 4. lépés: A kívánt tartomány exportálása DataTable‑be

Now we actually **export excel to datatable**. The `ExportDataTable` method takes the start row/column, the number of rows/columns, a flag for column‑name extraction, and the options we just built.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Mi történik a háttérben?*  
- `startRow: 0` az első Excel sorra (a fejléc sorra) mutat.  
- `exportColumnNames: true` azt mondja az Aspose‑nek, hogy a “Name” és “Age” értékeket a `DataTable` oszlopsorozatába vegye fel.  
- `totalRows`/`totalColumns` nagyobb lehet a tényleges adatoknál; a felesleges cellák üres stringgé válnak az `ExportAsString` miatt.

---

## 5. lépés: Az eredmény ellenőrzése – Az első sor kiírása

A quick console dump proves that the conversion succeeded and that column names are intact.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Várható kimenet**

```
First row: Alice, 30
```

Ha módosítod a mintadatot, a konzol automatikusan tükrözi a változásokat – nincs szükség extra kódra.

---

## Gyakran Ismételt Kérdések és Szélsőséges Esetek

| Question | Answer |
|----------|--------|
| **Exportálhatok egy már létező munkalapot a lemezen?** | Igen – cseréld le a `new Workbook()`-t `new Workbook("myFile.xlsx")`-re. A többi lépés változatlan marad. |
| **Mi van, ha az Excel fájlomban egyesített cellák vannak?** | Az egyesített cellák feloldásra kerülnek; a bal‑felső cella értéke lesz az egész egyesített tartomány értéke. |
| **Aggódom-e a kultúraspecifikus számformátumok miatt?** | Nem, ha `ExportAsString = true`; minden a Excelben látható nyers stringként érkezik. |
| **Hány sort exportálhatok egyszerre?** | Az Aspose.Cells több millió sort is kezel, de a memóriaigény a `DataTable` méretével nő. Ha korlátba ütközöl, fontold a lapozást. |
| **Mi van a rejtett oszlopokkal?** | A rejtett oszlopok exportálásra kerülnek, hacsak nem állítod `ExportHiddenColumns = false`-ra az `ExportTableOptions`‑ban. |

---

## Bónusz: Exportálás CSV‑be a DataTable helyett

Sometimes you might prefer a flat file. The same `ExportTableOptions` can be reused with `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

That one‑liner gives you a ready‑to‑import CSV while still **export Excel data as string**.

---

## Teljes működő példa (másolás‑beillesztés kész)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Run the program (`dotnet run`) and you’ll see the **export excel to datatable** result printed to the console. Swap out the sample data, change `totalRows`/`totalColumns`, or point the workbook at a real file—everything scales.

---

## Következtetés

You now have a **complete, self‑contained solution for exporting Excel to DataTable** in C#. By configuring `ExportTableOptions.ExportAsString` you guarantee that **export excel data as string**, and by setting `exportColumnNames: true` you get the familiar column headers you expect when you **export excel with column names**.  

* A `DataTable`‑t betáplálhatod az Entity Framework vagy Dapper segítségével tömeges beszúrásokhoz.  
* Átadhatod egy jelentéskészítő motorba, mint a **FastReport** vagy **RDLC**.  
* Átalakíthatod JSON‑ná egy API válaszhoz (`JsonConvert.SerializeObject(table)`).  

Feel free to experiment—maybe try exporting a larger sheet, or combine this with **how to export excel to datatable** from a network share. The pattern stays the same, and the code is ready for production.

![Diagram of Excel → DataTable conversion flow – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}