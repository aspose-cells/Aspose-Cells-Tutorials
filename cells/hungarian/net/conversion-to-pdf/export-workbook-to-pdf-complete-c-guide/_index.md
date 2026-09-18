---
category: general
date: 2026-02-26
description: Exportálja a munkafüzetet PDF-be beágyazott betűtípusokkal, és exportálja
  a diagramokat PowerPointba C#-ban. Tanulja meg, hogyan másolja a pivot tábla munkalapját,
  és mentse a munkafüzetet PPTX formátumban.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: hu
og_description: Exportálja a munkafüzetet PDF-be beágyazott betűtípusokkal, és exportálja
  a diagramokat PowerPointba C#-ban. Kövesse a lépésről‑lépésre útmutatót a pivot
  táblák másolásához és PPTX formátumban való mentéshez.
og_title: Munkafüzet exportálása PDF‑be – Teljes C# útmutató
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Munkafüzet exportálása PDF-be – Teljes C# útmutató
url: /hu/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Munkafüzet exportálása PDF-be – Teljes C# útmutató

A munkafüzet PDF-be exportálása gyakori igény, amikor jelentéseket kell megosztani az érintettekkel, akiknek esetleg nincs telepítve az Excel. Ebben az útmutatóban megmutatjuk, hogyan **exportálhat diagramokat PowerPointba**, hogyan **másolhat egy pivot tábla munkalapot**, és hogyan ágyazhat be betűtípusokat, hogy a PDF pontosan úgy nézzen ki, mint a képernyőn megjelenő tervezés.

Gondolkodtál már azon, miért veszítenek egyes PDF‑ek az eredeti elrendezésükben, vagy miért hiányoznak alakzatok a PowerPoint diákból? A válasz általában a hiányzó exportálási beállításokban rejlik. A útmutató végére egyetlen, újrahasználható C# metódust kapsz, amely megoldja ezeket a problémákat – többé nem kell kézzel másolgatni vagy az export beállításait állgatni.

> **Pro tipp:** Ha már használod az Aspose‑t a projektedben, egyszerűen beillesztheted a kódrészleteket változtatás nélkül; egyébként először add hozzá a NuGet csomagokat `Aspose.Cells` és `Aspose.Slides`.

## Mit fogsz megtanulni

- Hogyan hozz létre egy munkafüzetet, adj hozzá Smart Marker kifejezéseket, és dolgozd fel őket.  
- Hogyan **másolj egy pivot tábla munkalapot** anélkül, hogy megsértenéd az adatforrást.  
- Hogyan **exportálj diagramokat, alakzatokat és szövegdobozokat** egy PowerPoint prezentációba, miközben szerkeszthetőek maradnak.  
- Hogyan **ágyazz be szabványos betűtípusokat** a PDF exportálás során, hogy minden gépen egységesen jelenjen meg.  
- Hogyan **mentsd el a munkafüzetet PPTX formátumban** a `save workbook as pptx` megközelítéssel.  

Mindez a legújabb Aspose.Cells és Aspose.Slides .NET könyvtárakkal működik (a cikk írásakor a 23.11-es verzió). Nincs szükség külső eszközökre, utófeldolgozó szkriptekre – csak tiszta C#.

## Előfeltételek

- .NET 6.0 vagy újabb (a kód .NET Framework 4.7.2‑n is fut).  
- Visual Studio 2022 (vagy bármely kedvelt IDE).  
- Aspose.Cells .NET és Aspose.Slides .NET telepítve NuGet‑en keresztül.  
- Alapvető ismeretek a C#‑ról és az Excel koncepciókról, mint a Smart Markers és a PivotTables.  

![Munkafüzet exportálása PDF-be diagram](export-workbook-to-pdf.png "Munkafüzet exportálása PDF-be munkafolyamat, amely PDF és PPTX kimeneteket mutat")

## Munkafüzet exportálása PDF-be – Lépésről‑lépésre megvalósítás

Az alábbiakban a teljes, azonnal futtatható példát láthatod. A kód létrehoz egy munkafüzetet, beilleszti a Smart Marker kifejezéseket, feldolgozza őket, másolja a pivot tábla tartományt, majd végül elmenti mind a PDF, mind a PowerPoint fájlt.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Miért működik ez

1. **Smart Marker feldolgozás** lehetővé teszi, hogy a munkafüzetet bármilyen adatforrásból (JSON, DataTables stb.) töltsd fel anélkül, hogy ciklusokat írnál.  
2. **DetailSheetNewName** külön lapot hoz létre minden részlegnek, így tiszta, részlegenkénti fület kapsz.  
3. **A tartomány másolása** (`sourceRange.Copy`) megkettőzi a pivot táblát *beleértve* a gyorsítótárát, így a másolt lap pontosan úgy viselkedik, mint az eredeti.  
4. **PresentationOptions** a `ExportCharts`, `ExportShapes` és `ExportTextBoxes` beállításokkal azt mondja az Aspose‑nak, hogy ezeket az objektumokat natív PowerPoint elemekként renderelje, megőrizve a szerkeszthetőséget.  
5. **PdfSaveOptions.EmbedStandardFonts** biztosítja, hogy a PDF azonosuljon a gépeken, ahol az eredeti betűtípusok nincsenek telepítve.  

Az eredmény két fájl – `FinalReport.pdf` és `FinalPresentation.pptx` – amelyeket e‑mailben küldhetsz, archiválhatsz vagy bármely megjelenítőben megnyithatsz anélkül, hogy a minőség romlana.

## Diagramok exportálása PowerPointba (Munkafüzet mentése PPTX‑ként)

Ha a jelentésed diagramokat tartalmaz, valószínűleg szerkeszthető formában szeretnéd őket PowerPointban. A `PresentationOptions` osztály a kulcs. Íme egy fókuszált kódrészlet, amely csak a diagram‑exportálási részt mutatja:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Mi történik a háttérben?** Az Aspose minden egyes Excel diagramot natív PowerPoint diagrammá alakít, megőrizve a sorozatokat, tengelycímeket és a formázást. Ez sokkal jobb, mint a diagram statikus képként való exportálása, mert a közönség később módosíthatja az adatpontokat.

## Pivot tábla munkalap másolása adatvesztés nélkül

A pivot táblák gyakran a legnehezebb részei az exportálásnak, mivel egy rejtett gyorsítótárra támaszkodnak. Az egyszerű `Copy` metódus működik, mert az Aspose mind a látható tartományt **és** a mögöttes gyorsítótár objektumot másolja.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Megjegyzés:** Ha csak a pivot táblára van szükséged egy új lapon ugyanabban a munkafüzetben, az előző `sourceRange.Copy` megközelítés könnyebb, és elkerüli egy teljesen új munkafüzet létrehozását.

## Betűtípusok beágyazása PDF exportáláshoz – Miért fontos

Amikor egy PDF‑et nyitsz meg egy olyan gépen, amelyen nincsenek az eredeti betűtípusok, a szöveg eltolódhat, a sortörések megváltozhatnak, vagy karakterek tűnhetnek el. A `EmbedStandardFonts = true` beállítás azt mondja az Aspose‑nak, hogy ágyazza be a leggyakoribb betűtípusokat (Arial, Times New Roman stb.) közvetlenül a PDF‑folyamba.

Ha egyedi betűtípusokat használsz, állítsd át `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`‑ra. Íme egy példa:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Most minden címzett pontosan ugyanazt a kialakítást látja, amit terveztél – nincs meglepetés.

## Teljes működő példa összefoglalása

Mindent összevetve, a teljes program (korábban bemutatva) a következőket végzi:

1. **Létrehozza** a munkafüzetet Smart Marker helyőrzőkkel.  
2. **Feldolgozza** a helyőrzőket, részlethalapot generálva a részleg nevével.  
3. **Másolja** a pivot táblát tartalmazó tartományt egy új munkalapra, megőrizve annak funkcióját.  
4. **Exportálja** a munkafüzetet PowerPointba, a diagramokat, alakzatokat és szövegdobozokat szerkeszthető állapotban tartva.  
5. **Exportálja** ugyanazt a munkafüzetet PDF‑be, miközben szabványos betűtípusokat ágyaz be a megbízható megjelenítéshez.  

Futtasd a programot, nyisd meg a generált fájlokat, és a következőket fogod látni:

- **PDF**: Éles táblázatok, beágyazott betűtípusok, és ugyanaz a vizuális stílus, mint az Excel forrás.  
- **PowerPoint**: Szerkeszthető diagramok, amelyeket jobb‑kattintással → *Edit Data* (Adatok szerkesztése) módon módosíthatsz PowerPointban, valamint alakzatok, amelyek teljesen manipulálhatók maradnak.

## Gyakran Ismételt Kérdések (GYIK)

**Q: Működik ez .NET Core‑ral?**  
Igen – az Aspose.Cells és az Aspose.Slides platformfüggetlenek. Csak célozd meg a .NET 6‑ot vagy újabbat, és ugyanaz a kód fut Windows, Linux vagy macOS rendszeren.

**Q: Mi van, ha csak a munkafüzet egy részét szeretném exportálni?**  
Használd a `Workbook.Save`‑t `SaveOptions`‑szel, amely lehetővé teszi a `SheetNames` megadását. Példa: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Titkosíthatom a PDF‑et?**  
Természetesen. A `PdfSaveOptions.EncryptionDetails`‑t állítsd be egy jelszóval a `Save` hívása előtt.

**Q: A pivot táblám külső adatforrást használ – a másolás megtöri a kapcsolatot?**  
A másolási művelet a gyorsítótárat, nem pedig a külső kapcsolatot másolja. A pivot offline is működni fog, de nem frissül az eredeti forrásból. Ha élő frissítésre van szükség, exportáld a forrásadatokat együtt a munkafüzettel.

## Következő lépések és kapcsolódó témák

- **Dinamikus adatforrások** – Ismerd meg, hogyan lehet JSON‑t vagy DataTable‑t betáplálni a Smart Markerekbe valós idejű jelentéskészítéshez.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}