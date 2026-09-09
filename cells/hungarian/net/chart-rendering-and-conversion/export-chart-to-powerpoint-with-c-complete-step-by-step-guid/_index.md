---
category: general
date: 2026-02-26
description: Exportálja a diagramot PowerPointba Excelből C#-val. Tanulja meg, hogyan
  konvertálja az Excelt PowerPointba, hogyan mentse az Excelt PowerPointként, és hogyan
  tartsa a formákat szerkeszthetőnek.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: hu
og_description: Diagram exportálása PowerPointba Excelből C#-val. Ez az útmutató bemutatja,
  hogyan konvertálhatók az Excel fájlok PowerPointba, hogyan menthető a munkafüzet
  PPTX formátumban, és hogyan maradhatnak a formák szerkeszthetők.
og_title: Diagram exportálása PowerPointba C#-val – Teljes programozási útmutató
tags:
- Aspose.Cells
- C#
- Office Automation
title: Diagram exportálása PowerPointba C#‑val – Teljes lépésről‑lépésre útmutató
url: /hu/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Chart to PowerPoint – Complete Programming Tutorial

Valaha is elgondolkodtál, hogyan **exportálj diagramot PowerPointba** anélkül, hogy elveszítenéd a szerkeszthetőséget? Sok jelentéskészítési helyzetben élő diagramra van szükség egy diavetítésben, de a manuális másolás‑beillesztés fájdalmas. A jó hír, hogy néhány C# sorral programozottan is megoldható.

Ebben az útmutatóban végigvezetünk a teljes folyamaton: egy Excel munkafüzet betöltését, amely diagramot és szövegdobozt tartalmaz, az export beállítását úgy, hogy a szövegdobozok és alakzatok szerkeszthetőek maradjanak, majd a végeredmény mentését **PowerPoint** fájlként. A végére már tudni fogod, hogyan **konvertálj Excel-t PowerPointba**, **mentsd az Excelt PowerPointként**, és még a speciális esetekhez is testre szabhatod a beállításokat.

## What You’ll Need

- **Aspose.Cells for .NET** (23.10 vagy újabb verzió). Ez a könyvtár teszi a konverziót gond nélkül.
- **.NET 6+** runtime – bármely friss SDK megfelelő.
- Egy egyszerű Excel fájl (`ChartWithTextbox.xlsx`), amely legalább egy diagramot és egy szövegdobozt tartalmaz.
- Visual Studio vagy a kedvenc IDE-d.

Nem szükséges további NuGet csomag az Aspose.Cells-en kívül, de a C# szintaxis alapjainak ismerete mindenképp hasznos.

## Export Chart to PowerPoint – Step‑by‑Step

Az alábbiakban a megoldást kisebb, könnyen követhető lépésekre bontjuk. Minden lépéshez a pontos kódot és egy rövid „miért” magyarázatot is mellékelünk.

### Step 1: Load the Excel Workbook That Holds the Chart

Először be kell tölteni a forrásfájlt a memóriába. Az Aspose.Cells `Workbook` osztálya beolvassa az egész táblázatot, beleértve a diagramokat, képeket és beágyazott objektumokat.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Miért fontos:* Ha a munkafüzetet helytelen útvonallal nyitod meg, `FileNotFoundException`-t kapsz. Az egyszerű ellenőrzés megakadályozza, hogy később üres diát exportálj.

### Step 2: Prepare Presentation Options to Keep Shapes Editable

Az Aspose.Cells lehetővé teszi, hogy a szövegdobozok, alakzatok és akár a diagram is **szerkeszthető** maradjon az export után. Az `ExportTextBoxes` és `ExportShapes` `true` értékre állítása megőrzi ezeket az objektumokat natív PowerPoint elemekként, a statikus képként való laposítás helyett.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Miért fontos:* Ha ezeket a jelzőket az alapértelmezett (`false`) értéken hagyod, a kapott dia a diagram bitmap képét tartalmazza, így később nem lehet szerkeszteni a sorozatot vagy a feliratot. Mindkét opció engedélyezése valódi PowerPoint diagramot eredményez, amely úgy viselkedik, mint egy kézzel készített diagram.

### Step 3: Convert Excel to PowerPoint and Save the File

Most meghívjuk a `Save` metódust, megadva a `SaveFormat.Pptx` enumot és a korábban beállított opciókat. A könyvtár gondoskodik arról, hogy az Excel diagram objektumát PowerPoint diagram alakzattá alakítsa.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Miért fontos:* A `Save` hívás végzi el a nehéz munkát – az Excel sorozatok PowerPoint sorozatokra való leképezését, a tengelyformázás megőrzését és a kapcsolódó szövegdobozok átmásolását. Miután ez a sor lefut, egy teljesen **szerkeszthető** `.pptx` fájlod lesz, amely megnyitható a Microsoft PowerPointban.

### Verify the Result

Nyisd meg a `Result.pptx` fájlt PowerPointban. Egy olyan diát kell látnod, amely:

- Az eredeti diagramot tartalmazza, még mindig kapcsolódik az adatforráshoz (dupla‑kattintással szerkesztheted a sorozatot).
- Az Excel‑ben lévő szövegdobozt, most natív PowerPoint szövegdobozként.
- A diák elrendezése automatikusan kiválasztásra kerül (általában egy üres dia).

Ha hiányzó elemeket észlelsz, ellenőrizd, hogy a forrás munkafüzetben valóban látható objektumok voltak-e, és hogy az `ExportTextBoxes` / `ExportShapes` `true`‑ra volt‑e állítva.

### Convert Excel to PowerPoint: Handling Multiple Worksheets

Gyakran egy munkafüzet több lapot tartalmaz, mindegyik saját diagrammal. Alapértelmezés szerint az Aspose.Cells **az összes** diagramot **az összes** munkalapról külön diákra exportálja. Ha csak egy részhalmazra van szükséged, szűrheted őket a mentés előtt:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Pro tipp:* A `chart.IsVisible = false` beállítása olcsóbb, mint a diagram teljes eltávolítása, és lehetővé teszi a diagram felvételének ki‑ és bekapcsolását a forrásfájl módosítása nélkül.

### Save Excel as PowerPoint – Customizing Slide Size

A PowerPoint alapértelmezett mérete 10‑inch × 5.63‑inch dia. Ha a diagram szorultnak tűnik, a `PresentationOptions` objektummal módosíthatod a dia méretét:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Most az exportált diagram több “lélegzetet” kap, és a szövegdobozok megtartják eredeti elrendezésüket.

### How to Convert Excel to PPT: Dealing with Hidden Objects

Rejtett sorok, oszlopok vagy alakzatok néha bekerülnek az exportba. Ezek eltávolításához futtass egy gyors takarítást a mentés előtt:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Ez a lépés nem mindig szükséges, de megakadályozza a váratlan üres helyek megjelenését a végső diakészletben.

### Save Workbook as PPTX – Full Working Example

Mindent összevonva, itt egy kész, futtatható konzolprogram, amely bemutatja a teljes folyamatot:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

A program futtatása létrehozza a `Result.pptx` fájlt egy szerkeszthető diagrammal és szövegdobozzal, pontosan úgy, ahogy egy **workbook‑as‑pptx** mentésnél várnád.

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – szerkeszthető dia")

## Common Questions & Edge Cases

**Mi van, ha az Excel‑fájl egy külső adatforráshoz kapcsolt diagramot tartalmaz?**  
Az Aspose.Cells a *jelenlegi* adatértékeket másolja a PowerPoint diagramba. **Nem** őrzi meg a külső hivatkozást, mivel a PowerPoint nem tud Excel adatkapcsolatot ugyanúgy kezelni. Ha élő frissítésekre van szükség, fontold meg az eredeti Excel‑fájl OLE objektumként való beágyazását a PPTX‑be.

**Exportálhatok-e egy egyedi témát használó diagramot?**  
Igen. A könyvtár megpróbálja az Excel téma színeit a PowerPoint témahelyekre leképezni. Nagyon egyedi paletták esetén előfordulhat, hogy a színeket a PowerPoint saját API‑jával (pl. Aspose.Slides) kell korrigálni.

**Van korlátozás a diagramok számát illetően?**  
Gyakorlatilag nincs – az Aspose.Cells adatfolyamként dolgozik, így még tucatok diagramot tartalmazó munkafüzet is exportálható, bár a végső PPTX mérete lineárisan növekszik.

**Szükségem van licencre az Aspose.Cells‑hez?**  
Az ingyenes értékelő verzió működik, de az első diára vízjelet helyez. Gyártási környezetben szerezz be megfelelő licencet a vízjel eltávolításához és a teljes teljesítmény eléréséhez.

## Recap

Áttekintettük, hogyan **exportálj diagramot PowerPointba** C#‑ben, bemutattuk a pontos kódot az Excel munkafüzet betöltéséhez, a `PresentationOptions` beállításához a szövegdobozok és alakzatok szerkeszthetővé tételéhez, majd a mentést `.pptx`‑ként. Emellett megtanultad, hogyan **konvertálj Excel‑t PowerPointba**, **mentsd az Excelt PowerPointként**, és válaszoltunk a “**hogyan konvertáljunk Excel‑t ppt‑be**” kérdésre egy teljes, futtatható példával.

## What’s Next?

- **Save workbook as PPTX** több diával: iterálj minden munkalapon, és hívd meg a `Save`‑t `PresentationOptions`‑szel minden egyeshez.
- Fedezd fel az **Aspose.Slides**‑t, ha programozottan szeretnéd tovább módosítani a generált PPTX‑et (átmenetek, előadói jegyzetek stb.).
- Próbáld ki a **pivot diagramok** vagy **3‑D diagramok** exportálását – ugyanazok az opciók érvényesek, de esetleg utólagos tengelyformázásra lesz szükség.

Ha bármi gondba ütközöl, írj egy megjegyzést alább, vagy nézd meg az Aspose.Cells hivatalos dokumentációját a legújabb API‑változásokért. Boldog kódolást, és élvezd, ahogy néhány C# sorral Excel diagramjaidat elegáns PowerPoint‑prezentációkká varázsolod!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}