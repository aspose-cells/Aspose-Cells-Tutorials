---
category: general
date: 2026-10-20
description: Másolja a pivot táblát egy új munkafüzetbe az Aspose.Cells segítségével,
  és tanulja meg, hogyan exportálhat egy szerkeszthető alakzatot PowerPointba egyetlen
  útmutatóban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: hu
lastmod: 2026-10-20
og_description: Másolja a pivot táblát új munkafüzetbe az Aspose.Cells használatával,
  és exportáljon egy szerkeszthető alakzatot PowerPointba – lépésről‑lépésre kód,
  amelyet már ma futtathat.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Pivot tábla másolása új munkafüzetbe, alakzat exportálása PowerPointba
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Pivot tábla másolása új munkafüzetbe, alakzat exportálása PowerPointba
url: /hu/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tábla másolása új munkafüzetbe, alakzat exportálása PowerPointba

Ha **copy pivot table to new workbook**-t kell végrehajtani a funkcionalitás megőrzése mellett, ez az útmutató pontosan megmutatja, hogyan teheted ezt meg az Aspose.Cells segítségével. Emellett megtekintheted a leggyorsabb módot a **export an editable shape to PowerPoint**-ra, így a szövegdoboz a konverzió után is szerkeszthető marad.

Sok fejlesztő azt feltételezi, hogy egy pivot táblát tartalmazó tartomány másolása elveszíti a pivot logikát, vagy hogy az alakzatok statikus képekké válnak PPTX mentésekor. Ez az útmutató cáfolja ezeket a mítoszokat, és megbízható, termelés‑kész megoldást nyújt.

A következő szakaszokban a következőket fogod megtenni:

* Tölts be egy forrás munkafüzetet, és másolj egy tartományt, amely tartalmaz egy pivot táblát.
* Hozz létre egy cél munkafüzetet, amely ugyanazt a pivot táblát tartalmazza.
* Adj hozzá egy szövegdoboz alakzatot, módosítsd a szövegét, és mentsd a munkafüzetet PowerPoint prezentációként, ahol a szövegdoboz szerkeszthető marad.
* Értsd meg, miért szükséges minden egyes API hívás, és hogyan kerülheted el a gyakori buktatókat.

**Előfeltételek**

* .NET 6.0 vagy újabb (a kód .NET Framework 4.7+‑vel is működik).
* Aspose.Cells for .NET telepítve (`Install-Package Aspose.Cells`).
* Alapvető C# és Visual Studio ismeretek (vagy bármely kedvelt IDE).

---

## Pivot tábla másolása új munkafüzetbe

Ez a lépésről‑lépésre szekció bemutatja, hogyan másolj egy tartományt, amely pivot táblát tartalmaz, és hogyan őrizd meg a pivot definíciót az új fájlban.

### 1. lépés – Töltsd be a forrás munkafüzetet és válaszd ki az első munkalapot

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Miért?*  
`Workbook` az Aspose.Cells-ben minden Excel manipuláció kiindulópontja. A megfelelő munkalap kiválasztása biztosítja, hogy a pontos pivot tábla helyén dolgozzunk.

### 2. lépés – Definiáld a cellaterületet, amely tartalmazza a pivot táblát

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Miért?*  
A pivot tábla egy meghatározott cellablokkban él. Ha egy `CellArea`-t adunk meg, amely teljesen körülveszi a pivotot, az Aspose.Cells tudja, hogy a hozzá tartozó pivot gyorsítótárat is másolja.

### 3. lépés – Hozd létre a cél munkafüzetet és szerezd meg az első munkalapját

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Miért?*  
Egy új munkafüzet garantálja, hogy nincsenek ütköző névvel ellátott tartományok vagy meglévő pivotok, így a másolási művelet tiszta lesz.

### 4. lépés – Másold át a sorokat a forrás területről a cél munkalapra

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Miért?*  
`CopyRows` az **Aspose.Cells copy rows** API része. Másolja a cellaértékeket és a rejtett pivot gyorsítótárat is, így a pivot tábla a mozgatás után is működőképes marad.

### 5. lépés – Mentsd el az új munkafüzetet

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Eredmény*  
Nyisd meg a `CopyWithPivot.xlsx` fájlt Excelben. A pivot tábla pontosan úgy jelenik meg, ahogy a forrásfájlban volt, és normálisan frissíthető vagy módosítható.

---

## Szerkeszthető alakzat exportálása PowerPointba

Most hozzáadunk egy szövegdoboz alakzatot, megváltoztatjuk a tartalmát, és a munkafüzetet PPTX fájlként mentjük. Az alakzat teljesen szerkeszthető marad, amikor PowerPointban nyitod meg.

### 1. lépés – Hozz létre egy új munkafüzetet és férj hozzá az első munkalaphoz

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### 2. lépés – Adj egy szövegdoboz alakzatot a munkalaphoz

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Miért?*  
`AddTextBox` egy **editable textbox in PowerPoint**‑kompatibilis alakzatot hoz létre. A koordináták pontokban vannak megadva; állítsd be őket a layoutodhoz.

### 3. lépés – Szerezd meg az alakzatot és módosítsd a szövegét

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Miért?*  
A `Shape` objektum közvetlen elérése lehetővé teszi, hogy megváltoztasd a `Text`, `Font` vagy `Fill` tulajdonságokat. Ez a lépés bemutatja, hogyan állítható be programozottan a kezdeti tartalom.

### 4. lépés – Mentsd el a munkafüzetet PowerPoint prezentációként

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Eredmény*  
Nyisd meg a `Presentation.pptx` fájlt a Microsoft PowerPointban. A szövegdoboz megjelenik az első dián, és dupla‑kattintással szerkesztheted a szöveget, akárcsak bármely natív PowerPoint alakzat.

---

## Várt kimenet

| Fájl | Mit fogsz látni |
|------|-----------------|
| `CopyWithPivot.xlsx` | Egy munkalap, amely az eredeti pivot táblát tartalmazza, teljesen működőképes (a frissítés működik). |
| `Presentation.pptx` | Egyetlen dia egy szerkeszthető szövegdobozzal, amely a „Change me in PowerPoint” szöveget tartalmazza. |

---

## Gyakori buktatók és legjobb gyakorlatok

* **Pivot cache loss** – Ha csak a cellaértékeket másolod (például `CopyRows` használatával, ahol a `PasteOptions` flag `PasteValues`‑ra van állítva), a pivot gyorsítótár kimarad, és a tábla statikussá válik. Mindig használd a bemutatott alapértelmezett `CopyRows` overload‑t.
* **Shape positioning** – A `AddTextBox` pont egységeket használ, nem Excel cella indexeket. Teszteld a koordinátákat egy mintafájlban, hogy elkerüld a dián kívüli elhelyezést.
* **File format mismatch** – A munkafüzet PPTX‑ként történő mentése `SaveFormat.Pptx`‑el automatikusan konvertálja az összes támogatott alakzatot. Ha `Pdf`‑ként próbálod menteni, a forma raszterképpé alakul, így nem lesz szerkeszthető.

---

## Következtetés

Most már tudod, hogyan **copy pivot table to new workbook** és hogyan **export an editable shape to PowerPoint** az Aspose.Cells for .NET segítségével. A teljes, futtatható kódpéldák lefedik minden szükséges API hívást, elmagyarázzák, miért fontos minden lépés, és bemutatják a várt eredményeket.

Next, you might explore:

* **Working with charts** – diagramok másolása pivot táblákkal együtt (`Aspose.Cells copy rows between worksheets`).
* **

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Új munkafüzet létrehozása – Hogyan másolj egy munkalapot pivot táblával](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Pivot tábla másolása és Excel exportálása PPTX-be az Aspose.Cells segítségével](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Új munkafüzet létrehozása C#‑ban – Pivot tábla másolása](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}