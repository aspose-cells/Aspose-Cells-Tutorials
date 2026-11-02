---
category: general
date: 2026-09-11
description: Másolja a pivot táblát, és exportálja az Excelt PPTX-be az Aspose.Cells
  segítségével. Tanulja meg, hogyan generáljon szerkeszthető PPTX-et, és mentse a
  munkafüzetet PPTX formátumban C#-ban.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: hu
lastmod: 2026-09-11
og_description: Másolja a kimutatást és exportálja az Excelt PPTX-be C#-ban az Aspose.Cells
  használatával. Generáljon szerkeszthető PPTX-et, és mentse a munkafüzetet PPTX-ként
  néhány sor kóddal.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Pivot tábla másolása és Excel exportálása PPTX-be – teljes C# útmutató
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Pivot tábla másolása és Excel exportálása PPTX-be az Aspose.Cells használatával
url: /hu/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tábla másolása és Excel exportálása PPTX-be az Aspose.Cells segítségével

Ha egy pivot táblát kell átmásolni egy munkalapról egy másikra, majd az Excel fájlt PowerPoint prezentációba exportálni, ez az útmutató megmutatja, hogyan teheted. Az Aspose.Cells segítségével néhány C# sorral generálhatsz szerkeszthető PPTX-et, és mentheted a munkafüzetet PPTX formátumban.

Az útmutató minden szükséges lépést bemutat a pivot tábla áthelyezéséhez, annak funkcionalitásának megőrzéséhez, és egy PPTX fájl előállításához, ahol a diagram és az alakzatok szerkeszthetőek maradnak. Külső eszközökre nincs szükség – csak az Aspose.Cells könyvtárra és egy .NET fejlesztői környezetre.

## Mit fogsz elérni

* **Copy pivot table** egy forrás munkalapról egy cél munkalapra, miközben az összes adatkapcsolat érintetlen marad.  
* **Export Excel to PPTX** így a kapott dia szerkeszthető a PowerPointban.  
* **Generate editable PPTX** ahol a diagramok, táblázatok és alakzatok nem lapulnak le képekké.  
* **Save workbook as PPTX** ugyanazzal az Aspose.Cells API hívással.  

### Előfeltételek

* .NET 6.0 vagy újabb (a kód .NET Framework 4.6+ esetén is működik).  
* Aspose.Cells for .NET (NuGet csomag `Aspose.Cells`).  
* Alapvető ismeretek a C# konzolalkalmazásokról.  

> **Pro tipp:** Telepítsd a NuGet csomagot a CLI-n keresztül, hogy biztosan a legújabb verzió legyen:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Pivot tábla másolása munkalapok között

Az első művelet a pivot tábla áthelyezése a definíció megőrzésével. Az Aspose.Cells egy `CopyRange` metódust biztosít egy `CopyOptions` objektummal, amely tartalmazza a `CopyPivotTable` jelzőt.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Miért működik:**  
`CopyRange` másolja a cellák adatait, formázását, és ha a `CopyPivotTable` igaz, akkor a pivot tábla gyorsítótárát és metaadatait is. A cél tartomány a `A1` cellánál kezdődik (sor 0, oszlop 0), de az eltolásokat módosíthatod, hogy a pivot táblát máshová helyezd.

**Gyakori szélhelyzet:** Ha a cél munkalap már tartalmaz egy azonos nevű pivot táblát, az Aspose.Cells automatikusan átnevezi a bejövőt, elkerülve a névütközést.

## Excel exportálása PPTX-be és szerkeszthető PPTX generálása

Miután a pivot tábla a helyén van, exportálhatod az egész munkafüzetet egy PPTX fájlba. Az `ImageOrPrintOptions` osztály lehetővé teszi, hogy beállítsd az `ExportImageFormat = ImageFormat.Pptx` értéket, ami azt mondja az Aspose.Cells-nek, hogy a kimenetet PowerPoint prezentációként kezelje, nem pedig raszteres képként.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Miért működik:**  
Amikor az `ExportImageFormat` `Pptx`-re van állítva, az Aspose.Cells minden munkalapot egy diára konvertál. Az alakzatok, diagramok és pivot táblák natív PowerPoint objektumként kerülnek beírásra, így PowerPointban duplán kattintva szerkesztheted az alatta lévő adatokat.

**Tipus nagy munkafüzetekhez:** Ha csak a munkalapok egy részére van szükséged, a `Save` hívás előtt állítsd be a `workbook.Worksheets.RemoveAt(index)`-et a nem exportálandó lapokra. Ez csökkenti a PPTX fájl méretét.

## Teljes, futtatható példa

Az alábbiakban a teljes program látható, amely összekapcsolja a korábbi lépéseket. Cseréld le a `YOUR_DIRECTORY`-t a géped tényleges útvonalára.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Várt kimenet

A program futtatása a következőt írja ki:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Amikor megnyitod a `output.pptx`-t a Microsoft PowerPointban, egy olyan diát látsz, amely a másolt pivot táblát szerkeszthető diagramként tartalmazza. A diagramra duplán kattintva megnyílik a PowerPoint diagram szerkesztő, amely lehetővé teszi a sorozatok, tengelyek és adatcímkék módosítását anélkül, hogy vissza kellene térned az Excelhez.

## Tipikus buktatók kezelése

| Probléma | Ok | Megoldás |
|----------|----|----------|
| A pivot tábla statikus képként jelenik meg | `CopyPivotTable` jelző hiányzik vagy az `ExportImageFormat` `Png`-re van állítva | Győződj meg róla, hogy `CopyPivotTable = true` és `ExportImageFormat = ImageFormat.Pptx`. |
| A cél munkalap üres cellákat mutat | A forrás tartomány nem fedi le a pivot tábla teljes területét | Bővítsd a tartományt (pl. `"A1:H30"`), hogy tartalmazza az összes pivot mezőt. |
| Az exportált PPTX hatalmas | Felesleges munkalapok is benne vannak | Távolítsd el a nem kívánt lapokat a `Save` hívása előtt. |
| A PowerPoint nem tudja szerkeszteni a diagramot | Régebbi Aspose.Cells verzió használata, amely nem támogatja a PPTX-et | Frissíts a legújabb Aspose.Cells verzióra (ellenőrizd a kiadási megjegyzéseket). |

## Következő lépések és kapcsolódó témák

* **Export Excel sheet to PPTX with custom slide layouts** – fedezd fel a `WorksheetToPdfConverter`-t a diák megjelenésének finomabb vezérléséhez.  
* **Export Excel to PDF** – cseréld le az `ImageFormat.Pptx`-t `ImageFormat.Pdf`-re, hogy PDF-et generálj.  
* **Programmatically modify PPTX after export** – használd az `Aspose.Slides` könyvtárat animációk vagy előadói jegyzetek hozzáadásához.  

A **copy pivot table**, **export excel to pptx**, és **generate editable pptx** elsajátításával teljes jelentéskészítő csővezetékeket építhetsz, amelyek az adatokat a táblázatokból közvetlenül a prezentációs diákba viszik, anélkül, hogy elveszítenék a szerkeszthetőséget.

---

## Mit érdemes még megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészletet tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan másolj pivot táblát C#-ban – Excel konvertálása PPTX-be, tartomány másolása és szövegdoboz készítése](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Új Excel munkafüzet létrehozása – Pivot tábla másolása és duplikálása](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Pivot tábla létrehozása Excelben az Aspose.Cells for .NET használatával](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}