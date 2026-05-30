---
category: general
date: 2026-05-30
description: Módosítsa a szövegdoboz betűméretét Excelben C#-val. Tanulja meg, hogyan
  változtassa gyorsan az Excel szövegdoboz betűtípusát lépésről‑lépésre kóddal.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: hu
og_description: Módosítsa a szövegdoboz betűméretét Excelben C#-al. Ez az útmutató
  bemutatja, hogyan lehet biztonságosan és hatékonyan módosítani az Excel szövegdoboz
  betűtípusát.
og_title: Szövegdoboz betűméretének módosítása Excelben C#‑val – Teljes útmutató
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: A szövegdoboz betűméretének módosítása Excelben C#‑val – Teljes útmutató
url: /hu/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Szövegdoboz betűméretének módosítása Excelben C#‑vel – Teljes útmutató

Szükséged van **a szövegdoboz betűméretének módosítására** egy Excel munkalapon C#‑ból? Jó helyen jársz. Akár jelentéseket generálsz, irányítópultot építesz, vagy csak egy sablont finomítasz, a szövegdoboz megjelenésének beállítása sokkal professzionálisabbá teheti a táblázatodat.

Ebben az útmutatóban a **excel szövegdoboz betűtípusának módosítását** is bemutatjuk a méret mellett – gondolj betűcsaládra, félkövérre, és akár több alakzat kezelésére is. A végére egy azonnal futtatható kódrészletet kapsz, amely a folyamat minden szakaszát érinti, a munkafüzet megnyitásától a COM objektumok tisztításáig. Felesleges szócska nélkül, csak gyakorlati kód, amelyet ma beilleszthetsz a projektedbe.

## Előfeltételek — Amire szükséged lesz

Mielőtt belemerülnénk, győződj meg róla, hogy a következők telepítve vannak a gépeden:

| Követelmény | Miért fontos |
|-------------|----------------|
| **.NET 6+** (vagy .NET Framework 4.7.2+) | Biztosítja a C# fordítót és futtatókörnyezetet. |
| **Microsoft.Office.Interop.Excel** NuGet package | Megadja a COM interop típusokat, amelyek szükségesek az Excelhez való kommunikációhoz. |
| **Excel installed** (any recent version) | Az Interop réteg csak akkor működik, ha az Office alkalmazás telepítve van. |
| **Basic C# knowledge** | Könnyen követni tudod, de minden sort elmagyarázunk. |

Ha bármelyik hiányzik, állj meg most és telepítsd; a további útmutató feltételezi, hogy mind megvan.

## 1. lépés: A projekt beállítása és a névterek importálása

Először is—hozz létre egy új konzolos alkalmazást (vagy integráld egy meglévőbe), és importáld az interop névteret.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro tipp:** Ha .NET 6+ célplatformot használsz, add hozzá a `Microsoft.Office.Interop.Excel` csomagot a `dotnet add package Microsoft.Office.Interop.Excel` paranccsal. Ez biztosítja, hogy az `Excel` alias helyesen feloldódjon.

## 2. lépés: A munkafüzet megnyitása és a cél munkalap lekérése

Most el kell indítanunk az Excelt, meg kell nyitnunk a fájlt, és rá kell mutatnunk arra a munkalapra, amely a szövegdobozt tartalmazza. Ennek `try/finally` blokkba helyezése garantálja, hogy a COM objektumok felszabadulnak, még ha valami hiba is történik.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Miért fontos

A munkafüzet COM‑on keresztüli megnyitása élő objektummodellt biztosít – minden változtatás azonnal megjelenik a fájlban. A `Visible = false` beállítás felgyorsítja a folyamatot és megakadályozza, hogy automatikus futtatás közben megjelenjenek a Windowsok.

## 3. lépés: A szövegdoboz alakzatának lekérése

Az Excel a szövegdobozokat `Shape` objektumokként kezeli a `Shapes` gyűjteményben, nem pedig külön `TextBox` gyűjteményként. Ezért a lenti kód kissé eltér attól a részlettől, amelyet esetleg online láttál.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Figyelem:** A `Shapes` gyűjtemény 1‑es indexelésű, ezért a megadott null‑alapú `textboxIndex` értékhez `+1`‑et adunk. Ennek elhagyása “index out of range” hibákat eredményez, amelyek hibakeresése frusztráló lehet.

## 4. lépés: A szövegdoboz betűméretének (és nevének) módosítása

Itt végre **megváltoztatjuk a szövegdoboz betűméretét**. A `TextFrame2` tulajdonság hozzáférést biztosít a gazdag szövegformázási lehetőségekhez, beleértve a `Font.Name` és `Font.Size` értékeket.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Miért használjuk a `TextFrame2`‑t

A `TextFrame2` az Office 2007‑tel bevezetett újabb objektummodell. Támogatja a fejlett tipográfiai funkciókat, és általában megbízhatóbb, mint a régebbi `TextFrame`. Ennek használata biztosítja, hogy a **szövegdoboz betűméretének módosítása** művelet modern Excel verziókban is működjön.

## 5. lépés: Mentés, takarítás és ellenőrzés

A betűkészlet módosítása után el kell menteni a változtatásokat, és felszabadítani minden COM hivatkozást. A takarítás kihagyása elárvult Excel folyamatok maradásához vezethet a háttérben.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro tipp:** Ha sok munkalapon kell **módosítani az excel szövegdoboz betűtípusát**, tedd a belső logikát egy ciklusba, amely a `Workbook.Worksheets` elemein iterál. Ne felejtsd el minden lapnál visszaállítani a `textboxIndex`‑et.

## Szélsőséges esetek kezelése — Több szövegdoboz és hiányzó alakzatok

A valós életben használt táblázatok ritkán tartalmaznak csak egy szövegdobozt. Az alábbiakban két gyors stratégiát mutatunk, amelyeket a teljes metódus újraírása nélkül alkalmazhatsz.

### 1. Az *összes* szövegdoboz módosítása egy lapon

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Szövegdoboz azonosítása **név** alapján, index helyett

Ha a szövegdoboznak jelentős nevet adtál (pl. „TitleBox”), közvetlenül lekérheted:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Mindkét megközelítés lehetővé teszi, hogy **módosítsd az excel szövegdoboz betűtípusát** precízen, függetlenül a munkafüzet felépítésétől.

## Vizuális áttekintés (opcionális)

Ha egy gyors vizuális támpontot kedvelsz, képzeld el a következő diagramot:

![Képernyőkép, amely Excel munkalapot mutat kiemelt szövegdobozzal – bemutatja a szövegdoboz betűméretének módosítását](change-textbox-font-size.png)

*Alt szöveg:* *szövegdoboz betűméretének módosítása Excelben – kiemelt szövegdoboz készen áll a betűtípus módosítására.*

## Teljes működő példa

Mindent egybe rakva, itt egy egyetlen fájl, amelyet beilleszthetsz egy konzolos projektbe és azonnal futtathatsz (csak frissítsd a fájl útvonalát és a lap nevét).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## Mit tanulj meg legközelebb?

- [Betűméret módosítása Excelben](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Hogyan testre szabjuk a betűméretet Excel cellákban Aspose.Cells .NET használatával | Teljes útmutató](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Hogyan állítsuk be a betűstílusokat Excelben Aspose.Cells for .NET használatával (Lépésről‑lépésre útmutató)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}