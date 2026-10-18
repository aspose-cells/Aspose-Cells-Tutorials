---
category: general
date: 2026-01-14
description: Hogyan másolhatunk pivot táblát az Aspose.Cells használatával, és megtanulhatjuk,
  hogyan konvertáljuk az Excelt PPTX‑be, másoljuk a tartományt egy másik munkafüzetbe,
  valamint hogyan tegyük szerkeszthetővé a szövegdobozt PPTX‑ben egyetlen útmutatóban.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: hu
og_description: Hogyan másolhatunk pivot táblát, majd Excel-t PPTX-re konvertálhatunk,
  tartományt másolhatunk egy másik munkafüzetbe, és szerkeszthető szövegdobozt készíthetünk
  PPTX-ben – mindezt az Aspose.Cells segítségével.
og_title: Hogyan másoljunk pivot táblát C#‑ban – Teljes Excel‑ről PPTX‑re útmutató
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Hogyan másoljuk a pivot táblát C#-ban – Excel konvertálása PPTX-be, tartomány
  másolása és szövegdoboz szerkeszthetővé tétele
url: /hu/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan másoljuk a Pivot táblát C#‑ban – Teljes Excel‑ről PPTX‑re útmutató

Az, hogy hogyan másolhatunk pivot táblát egy munkafüzetből a másikba, gyakori kérdés, amikor Excel‑alapú jelentéseket automatizálunk. Ebben az útmutatóban három valós példán keresztül mutatjuk be a **Aspose.Cells for .NET** használatát: pivot‑tábla tartomány másolása, munkalap exportálása PPTX fájlba szerkeszthető szövegdobozzal, és egyetlen cella feltöltése JSON tömbbel a Smart Markers segítségével.  

Látni fogja, hogyan **konvertálhatja az Excelt PPTX‑re**, **másolhat tartományt egy másik munkafüzetbe**, és **készíthet szerkeszthető szövegdobozt PPTX‑ben** anélkül, hogy a formázás megsérülne. A végére egy készen álló kódbázist kap, amelyet bármely .NET projektbe beilleszthet.  

> **Pro tip:** Minden példa az Aspose.Cells 23.12 verzióra épül, de ugyanazok a koncepciók korábbi verziókra is alkalmazhatók kisebb API módosításokkal.

![Diagram, amely bemutatja a pivot tábla másolását, a munkalap PPTX‑re exportálását és a JSON tömb beillesztését – a pivot tábla másolásának munkafolyamata](how-to-copy-pivot-table-diagram.png)

---

## Szükséges eszközök

- Visual Studio 2022 (vagy bármely C# IDE)
- .NET 6.0 vagy újabb futtatókörnyezet
- Aspose.Cells for .NET NuGet csomag  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Két minta Excel fájl (`source.xlsx`, `chartWithTextbox.xlsx`) egy általad irányított mappában (cseréld le a `YOUR_DIRECTORY`‑t a saját elérési útvonaladra).

Nem szükséges további könyvtár; ugyanaz az `Aspose.Cells` összeállítás kezeli az Excelt, a PPTX‑t és a Smart Markers‑t.

---

## Hogyan másoljuk a Pivot táblát és őrizzük meg az adatait

Amikor egy olyan tartományt másolsz, amely pivot táblát tartalmaz, az alapértelmezett viselkedés csak a **értékek** beillesztése. A pivot definíció érintetlenül tartásához engedélyezned kell a `CopyPivotTable` jelzőt.

### Lépés‑ről‑lépésre

1. **Töltsd be a forrás munkafüzetet**, amely a pivot táblát tartalmazza.  
2. **Hozz létre egy üres cél munkafüzetet** – ez fogja fogadni a másolt tartományt.  
3. **Használd a `CopyRange`‑t `CopyPivotTable = true` beállítással**, hogy a pivot definíció az adatokkal együtt kerüljön át.  
4. **Mentsd el a cél fájlt** a kívánt helyre.

#### Teljes kódpélda

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Miért működik ez:**  
`CopyOptions.CopyPivotTable` azt mondja az Aspose.Cells‑nek, hogy klónozza a háttérben lévő `PivotTable` objektumot, nem csak a megjelenített értékeket. A cél munkafüzet most már egy teljesen működő pivot táblát tartalmaz, amelyet programozottan frissíthetsz vagy módosíthatsz.

**Különleges eset:** Ha a forrás munkafüzet külső adatforrásokat használ, előfordulhat, hogy be kell ágyaznod az adatokat vagy módosítanod kell a kapcsolati karakterláncokat a másolás után, különben a pivot “#REF!” hibát fog mutatni.

---

## Excel konvertálása PPTX‑re és a szövegdoboz szerkeszthetővé tétele

A munkalap PowerPoint‑ba exportálása hasznos a diavetítések közvetlen adatból történő létrehozásához. Alapértelmezés szerint az exportált szövegdoboz statikus alakzat lesz, de az `IsTextBoxEditable` beállítása megfordítja ezt a viselkedést.

### Lépés‑ről‑lépésre

1. **Nyisd meg a munkafüzetet**, amely a kívánt diagramot és szövegdobozt tartalmazza az exportáláshoz.  
2. **Állítsd be a `ImageOrPrintOptions`‑t** `SaveFormat = SaveFormat.Pptx` értékkel.  
3. **Határozd meg a nyomtatási területet**, amely tartalmazza a szövegdobozt.  
4. **Engedélyezd az `IsTextBoxEditable`‑t**, hogy a szöveget a PPTX megnyitása után szerkeszthesd.  
5. **Mentsd el a PPTX fájlt**.

#### Teljes kódpélda

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Eredmény:** Nyisd meg a `result.pptx` fájlt PowerPointban – a Excel‑ben elhelyezett szövegdoboz most már egy normál szövegdoboz lesz, amelybe beírhatsz szöveget. Nem kell manuálisan újra létrehozni.

**Gyakori hibaforrás:** Ha a munkalap összevont cellákat tartalmaz, amelyek átfedik a nyomtatási területet, a kész dia eltolódhat. Állítsd be a nyomtatási területet, vagy bontsd fel a cellákat az exportálás előtt.

---

## Tartomány másolása egy másik munkafüzetbe Smart Markerekkel (JSON → egyetlen cella)

Néha szükség van egy JSON tömb beágyazására egyetlen Excel cellába, például amikor olyan downstream rendszereknek kell adatot átadni, amelyek JSON karakterláncot várnak. Az Aspose.Cells Smart Markerei képesek egy tömböt egy cellába sorosítani, ha `ArrayAsSingle = true` értéket állítasz be.

### Lépés‑ről‑lépésre

1. **Tölts be egy sablon munkafüzetet**, amely Smart Marker helyőrzőt tartalmaz (pl. `&=Items.Name`).  
2. **Készítsd elő az adatobjektumot** – egy anonim típust egy `Items` tömbbel.  
3. **Hozz létre egy `SmartMarkerProcessor`‑t** és alkalmazd az adatot `ArrayAsSingle` beállítással.  
4. **Mentsd el a feltöltött munkafüzetet**.

#### Teljes kódpélda

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Magyarázat:**  
Ha `ArrayAsSingle` igaz, az Aspose.Cells összefűzi az `Items.Name` minden elemét egy JSON‑szerű karakterláncba (`[\"A\",\"B\"]`) és beírja azt abba a cellába, amely a smart markert tartalmazta. Ez megakadályozza, hogy minden tömb elemhez külön sor jöjjön létre.

**Mikor érdemes használni:** Ideális konfigurációs táblák, API payloadok exportálásához, vagy bármilyen esetben, ahol a fogyasztó egy kompakt JSON karakterláncot vár a táblázatos elrendezés helyett.

---

## További tippek és különleges esetek kezelése

| Forgatókönyv | Mire figyeljünk | Javasolt megoldás |
|--------------|-------------------|-------------------|
| **Nagy pivot táblák** | A memóriahasználat megugrik, amikor hatalmas pivot gyorsítótárakat másolsz. | Használd a `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` beállítást a betöltés előtt. |
| **Exportálás PPTX‑be képekkel** | A képek alacsony DPI-n rasterizálódhatnak. | Állítsd be a `pptxOptions.ImageResolution = 300` értéket a tisztább diákért. |
| **Smart Marker JSON formázás** | A speciális karakterek (`\"` , `\\`) hibát okoznak a JSON-ban. | Escapeld őket manuálisan vagy használd a `JsonSerializer`‑t az előzetes sorosításhoz a Smart Markerekhez való átadás előtt. |
| **Tartomány másolása különböző Excel verziók között** | A régebbi `.xls` fájlok elveszíthetik a formázást. | Mentsd a célt `.xlsx` formátumban a modern funkciók megőrzéséhez. |

---

## Összefoglalás – Hogyan másoljuk a Pivot táblát és sok más dolgot

Kezdetben megválaszoltuk, hogyan **másoljuk a pivot táblát** miközben megőrzük a funkcionalitását, majd bemutattuk, hogyan **konvertáljuk az Excelt PPTX‑re**, **készítsünk szerkeszthető szövegdobozt PPTX‑ben**, és végül hogyan **másoljuk a tartományt egy másik munkafüzetbe** a Smart Markerek segítségével, egy JSON tömböt egyetlen cellába ágyazva.  

Mindhárom kódrészlet önálló; beillesztheted őket egy új konzolalkalmazásba, módosíthatod a fájl útvonalakat, és már ma futtathatod őket.

---

## Mi a következő?

- **Fedezd fel a többi export formátumot** – az Aspose.Cells támogatja a PDF, XPS és HTML formátumokat is.  
- **Frissítsd a pivot táblákat programozottan** a `PivotTable.RefreshData()` használatával a másolás után.  
- **Kombináld a Smart Markereket diagramokkal**, hogy dinamikus műszerfalakat hozz létre, amelyek automatikusan frissülnek.  

Ha érdekel a **munkafüzet PPTX‑ként mentése** egyedi diatervekkel, nézd meg az Aspose.Cells dokumentációt a `SlideOptions`‑ról.  

Nyugodtan kísérletezz—cseréld ki a nyomtatási területet, próbálj ki különböző `CopyOptions`‑t, vagy adj egy összetettebb JSON payload‑ot. Az API elég rugalmas a legtöbb jelentéskészítő csővezetékhez.

### Gyakran Ismételt Kérdések

**K: A `CopyPivotTable` másolja a szeletelőket is?**  
V: Nem közvetlenül. A szeletelők különálló objektumok; másolás után újra kell őket létrehozni, vagy a `Worksheet.Shapes` gyűjteményen keresztül másolni.

**K: Exportálhatok több munkalapot egyetlen PPTX prezentációba?**  
V: Igen. Iterálj végig minden munkalapon, hívd meg a `Save`‑et ugyanazzal az `ImageOrPrintOptions`‑szel, és állítsd be a `pptxOptions.StartSlideNumber`‑t a számozás folytatásához.

**K: Mi van, ha a JSON tömböm beágyazott objektumokat tartalmaz?**  
V: Állítsd `ArrayAsSingle = false`‑ra, és használj egy egyedi sablont, amely iterál…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}