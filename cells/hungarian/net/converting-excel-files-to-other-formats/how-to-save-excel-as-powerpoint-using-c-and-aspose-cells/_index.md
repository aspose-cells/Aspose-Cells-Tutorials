---
category: general
date: 2026-08-17
description: Excel mentése PowerPointként C#‑val – lépésről‑lépésre útmutató az XLSX
  fájlok konvertálásához, a szövegdobozok szerkeszthetővé tételéhez és PPTX kimenet
  generálásához.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: hu
lastmod: 2026-08-17
og_description: Mentse az Excelt PowerPointként C#-ban egy teljes kódrészlettel. Tanulja
  meg, hogyan konvertáljon XLSX-et, tegyen szerkeszthetővé szövegmezőket, és exportáljon
  PPTX-be.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Excel mentése PowerPointként C#-ban – teljes átalakítási útmutató
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: Hogyan menthetünk Excel fájlt PowerPoint formátumba C# és az Aspose.Cells segítségével
url: /hu/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan mentse el az Excel fájlt PowerPointként C# és Aspose.Cells használatával

Ha egy .NET projektben **Excel fájlt szeretne PowerPointként menteni**, ez az útmutató egy teljes, azonnal futtatható megoldást mutat be. Megmutatjuk, hogyan töltsön be egy XLSX munkafüzetet, hogyan tegye szerkeszthetővé a munkalapon lévő összes szövegdobozt, és hogyan exportálja az eredményt PPTX fájlba – mindezt csak néhány C# sorral.

Az Excel PowerPoint‑re konvertálása gyakori igény jelentéstáblák, diavetítések vagy automatizált prezentációk készítésekor. Ez az oktatóanyag emellett bemutatja, hogyan **szerkeszthetőek a szövegdobozok** programozottan, így a mentés előtt testre szabhatja a dia tartalmát.

## Előfeltételek

* .NET 6.0 (vagy újabb) SDK telepítve  
* Fejlesztői környezet, például Visual Studio 2022 vagy VS Code  
* Aspose.Cells for .NET licenc (vagy ingyenes értékelő kulcs) – letölthető az [Aspose weboldaláról](https://products.aspose.com/cells/net/)  
* A konvertálni kívánt `input.xlsx` fájl  

> **Pro tipp:** Ha az ingyenes értékelő verziót használja, a kimeneti PPTX vízjelet fog tartalmazni. Egy licencelt verzió eltávolítja azt.

## 1. lépés: Az Aspose.Cells NuGet csomag telepítése

Nyisson egy terminált a projekt mappájában, és futtassa:

```bash
dotnet add package Aspose.Cells
```

Ez hozzáadja az `Aspose.Cells` assembly-t, amely a konverzióhoz szükséges `Workbook`, `Worksheet` és `Shape` osztályokat biztosítja.

## 2. lépés: Konzolos alkalmazás vázának létrehozása

Hozzon létre egy új konzolos projektet (ha még nincs):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Cserélje le a generált `Program.cs` fájlt a következő lépésekben bemutatott kóddal.

## 3. lépés: A munkafüzet betöltése és az első munkalap kiválasztása

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Miért fontos ez:**  
`Workbook` beolvassa az Excel fájlt a memóriába, míg a `Worksheet` hozzáférést biztosít a munkalap celláihoz, diagramjaihoz és alakzataihoz. Az első munkalap gyakran az alapértelmezett jelentés, amelyet prezentálni szeretne.

## 4. lépés: A munkalapon lévő összes szövegdoboz szerkeszthetővé tétele

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Miért van erre szükség:**  
Alapértelmezés szerint az Excel‑ből importált szövegdobozok csak olvashatóak a PowerPointben. Az `IsEditable = true` beállítás lehetővé teszi, hogy Ön (vagy későbbi PowerPoint‑felhasználók) közvetlenül a dián módosítsák a szöveget.

## 5. lépés: A munkafüzet mentése PowerPoint prezentációként

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Mi történik a háttérben:**  
`Workbook.Save` felismeri a `SaveFormat.Pptx` enum értéket, és az Excel munkalap elrendezését – beleértve a sorokat, oszlopokat, diagramokat és a most már szerkeszthető szövegdobozokat – PowerPoint diaobjektumokká alakítja.

## Teljes forráskód (futtatható)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Várható kimenet

A program (`dotnet run`) futtatásakor a következőt kell látnia:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Az `output.pptx` megnyitása a Microsoft PowerPointben egy olyan diát jelenít meg, amely tükrözi az eredeti Excel munkalapot. Az összes szövegdoboz közvetlenül szerkeszthető dupla kattintással.

## Gyakori kérdések és speciális esetek

| Kérdés | Válasz |
|----------|--------|
| **Átkonvertálhatok egy adott munkalapot az első helyett?** | Igen. Cserélje le a `workbook.Worksheets[0]`-t a `workbook.Worksheets["SheetName"]`-re vagy a szükséges indexre. |
| **Mi van, ha a munkafüzet több munkalapot tartalmaz?** | Hívja meg a `workbook.Save`-t minden munkalapra egyszer, minden egyeshez külön PPTX fájlnevet adva, vagy egyesítse őket egyetlen prezentációba az Aspose.Slides `Presentation` objektumok használatával. |
| **Megmaradnak a diagramok?** | Az Aspose.Cells automatikusan átalakítja az Excel diagramokat PowerPoint diagramobjektumokká. Nem szükséges további kód. |
| **Hogyan változtathatom meg a dia méretét?** | A `workbook.Save` után betöltheti a generált PPTX-et az Aspose.Slides segítségével, és módosíthatja a `Presentation.SlideSize` értékét. |
| **Mi van, ha a mentés előtt módosítanom kell a szövegdoboz szövegét?** | A cikluson belül érje el a `shapeItem.TextBox.Text`-et, módosítsa, majd állítsa be az `IsEditable = true` értéket. Példa: `shapeItem.TextBox.Text = "New title";` |

## Hibaelhárítási tippek

* **„ShapeType.TextBox” nem található** – Győződjön meg róla, hogy az Aspose.Cells 25.11 vagy újabb verzióját használja; a korábbi verziók nem tartalmazzák az `IsEditable` tulajdonságot.  
* **Fájl nem található hibák** – Ellenőrizze, hogy a `YOUR_DIRECTORY` abszolút útvonal-e, vagy hogy a relatív útvonal a megfelelő helyre mutat-e.  
* **Licenc nincs alkalmazva** – Hívja meg a `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` kódot a munkafüzet betöltése előtt, hogy eltávolítsa az értékelő vízjeleket.

## Következtetés

Most már tudja, hogyan **mentse el az Excelt PowerPointként** C#‑ban egy XLSX munkafüzet betöltésével, az összes szövegdoboz szerkeszthetővé tételével és PPTX‑be exportálásával. Ez a módszer automatikusan kezeli a diagramokat, képeket és a cellaformázást, így egy azonnal bemutatható diakészletet kap.

Ezután fedezze fel a kapcsolódó témákat, például **Excel konvertálása PowerPointre Aspose.Slides‑szel**, **szövegdobozok programozott szerkesztése a konverzió után**, vagy **több munkafüzet kötegelt feldolgozása**. Mindegyik a itt bemutatott alaplépésekre épül, és tovább automatizálhatja a jelentéskészítési folyamatot.

## Mit érdemes még megtanulni?

Az alábbi oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthassa a további API‑funkciókat, és alternatív megvalósítási megközelítéseket fedezzen fel saját projektjeiben.

- [Hogyan konvertáljuk az Excelt PowerPointre Aspose.Cells for .NET használatával: Teljes útmutató](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Hogyan másoljuk a Pivot táblát C#‑ban – Excel konvertálása PPTX‑re, tartomány másolása és szövegdoboz létrehozása](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Hogyan mentsünk Excel fájlokat több formátumban Aspose.Cells .NET használatával (2023-as útmutató)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}